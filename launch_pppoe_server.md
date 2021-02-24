# PPPoEサーバの構築

## はじめに
ネットワーク機器の検証等（特にルーターなど）で、一時的にインターネット回線を利用したいケースが多々あります。  
そんな時、PPPoEサーバを用意しておくと仮想的なISPを社内ネットワーク内へ作れるので非常に便利です。

<br>

## 参考サイト
NetworkManager辺りが微妙: https://www.hori-tec.net/works/2017/0804_161428.html  
設定ファイル辺りは正確: https://masasoft.jp/redhat-linux/pppoe-server-HOWTO.txt

<br>

## 環境
* Linuxサーバになれるマシン（以下、マシン）
* 2つ以上のネットワークへ接続可能なインターフェース（LANポートx2、LANポート＋WiFiなど）
* CentOS7

<br>

## 今回のネットワーク構成
構成
```
[社内LAN]② ---(WiFi)--- ①[マシン]② ---(LANケーブル)--- ①[WiFiルーター]② ---(WiFi)--- ①[MacBook Pro]
```

IPアドレス
* 社内LAN②： 10.7.14.254
* マシン①(wlp2s0): 10.7.14.102
* マシン②(enp3s0): 172.16.0.254
* WiFiルーター①: 172.16.0.1
* WiFiルーター②: 192.168.1.254
* MacBook Pro①: 192.168.1.1

<br>

## 手順
### Linux関連の設定
1. SELinuxをOFFにする

2. 関連パッケーッジをインストールする
    ```
    # yum -y install ppp rp-pppoe
    ```

3. ルーティングを有効にする
    ```
    # vim /etc/sysctl.d/10-ipv4.conf
    net.ipv4.ip_forward=1
    ```

4. NetworkManagerを停止する（こいつがいると邪魔臭い）
    ```
    # systemctl stop NetworkManager
    # systemctl disable NetworkManager
    ```

5. ネットワークを整える  
NetworkManagerを停止すると自動生成されていたネットワークまわりの設定が使い物にならなくなる。  
その為、自力でネットワークが取得できる環境を整える必要がる。  
    > - 有線関連は[こちら](https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/6/html/deployment_guide/s1-networkscripts-interfaces)を参照  
    > - WiFi関連は[こちら](https://qiita.com/naoi/items/ab5d8c9f9d31dae937e7)を参照

<br>

### PPPoE関連設定
6. PPPoEの設定
    ```diff
    # cd /etc/ppp/
    # diff -u pppoe-server-options.org pppoe-server-options
    --- pppoe-server-options.org	2020-09-07 17:10:23.453743412 +0900
    +++ pppoe-server-options	2020-09-09 11:59:56.946763318 +0900
    @@ -1,6 +1,13 @@
    # PPP options for the PPPoE server
    # LIC: GPL
    require-pap
    -login
    +# login
    lcp-echo-interval 10
    lcp-echo-failure 2
    +ms-dns {{社内ネットワークで利用されているDNSのIPアドレス}}
    +ms-dns {{社内ネットワークで利用されているDNSのIPアドレス}}
    +proxyarp
    ```

7. pap認証の追加
    ```diff
    # diff -u pap-secrets.org pap-secrets
    --- pap-secrets.org	2020-09-08 15:59:46.287289404 +0900
    +++ pap-secrets	2020-09-09 11:32:01.670997109 +0900
    @@ -1,2 +1,3 @@
    # Secrets for authentication using PAP
    # client	server	secret			IP addresses
    +{{アカウント}} * {{パスワード}} 172.16.0.1
    ```

8. ルーティング自動設定スクリプトの作成
    ```
    # vim ip-up.local
    -----
    #!/bin/bash

    if [ `echo $5 | awk -F. '{print $4}'` = "0"]; then
        /sbin/route add -net $5 netmask 255.255.255.0 dev $1
    fi

    exit 0
    -----
    # chmod 755 ip-up.local
    ```

9. 有線インターフェース（enp3s0）の初期化
    ```
    # ifdown enp3s0
    # ifconfig enp3s0 0.0.0.0 up
    ```

10. PPPoEサーバの起動
    ```
    # pppoe-server -I enp3s0 -L 172.16.0.254
    ```

11. iptableの追加
    ```
    # iptables -t nat -A POSTROUTING -s 172.16.0.0/16 -j MASQUERADE

    一応セーブしておく
    # iptables-save > /etc/sysconfig/iptables

    読み込む時はこちら
    # iptables-restore < /etc/sysconfig/iptables
    ```

11. WiFiルーター側で(7)の手順で設定した認証情報を使ってPPPoE認証をしてみる