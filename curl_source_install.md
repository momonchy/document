# 目的
HTTP2を利用するためcURLバージョンを7.43.0以上へアップデートしたいが、  
rpmパッケージが見つからないのでソースから最新版をインストール。

<br>

# オフィシャルサイト
ダウンロード: https://curl.se/download/  
インストールドキュメント: https://curl.se/docs/install.html

<br>

# 導入手順
情報確認
```sh
$ cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.5 (Maipo)

$ curl -V
curl 7.29.0 (x86_64-redhat-linux-gnu) libcurl/7.29.0 NSS/3.44 zlib/1.2.7 libidn/1.28 libssh2/1.8.0
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp scp sftp smtp smtps telnet tftp
Features: AsynchDNS GSS-Negotiate IDN IPv6 Largefile NTLM NTLM_WB SSL libz unix-sockets

$ which curl
/usr/bin/curl

$ rpm -qf /usr/bin/curl
curl-7.29.0-57.el7_8.1.x86_64
```

libnghttp2-develがインストールされてるか確認
```sh
$ rpm -qa | grep libnghttp2-devel

無かったらインストール
$ sudo yum -y install libnghttp2-devel
```

コンパイル環境の準備（2020/11/19時点最新バージョン：v7.73.0）
```sh
$ cd /usr/local/src/
$ sudo wget https://curl.se/download/curl-7.73.0.tar.gz
$ sudo tar xvfz curl-7.73.0.tar.gz
$ sudo chown -R <ログインユーザ>:<ログイングループ> curl-7.73.0/
$ cd curl-7.73.0/
```

configureオプションの確認
```sh
$ ./configure --help
```

makeファイルの作成
```sh
$ ./configure --prefix=/usr/local --with-nghttp2
----------------------
--snip
  curl version:     7.73.0
  SSL:              enabled (OpenSSL)
  SSH:              no      (--with-{libssh,libssh2})
  zlib:             enabled
  brotli:           no      (--with-brotli)
  zstd:             no      (--with-zstd)
  GSS-API:          no      (--with-gssapi)
  TLS-SRP:          no      (--enable-tls-srp)
  resolver:         POSIX threaded
  IPv6:             enabled
  Unix sockets:     enabled
  IDN:              no      (--with-{libidn2,winidn})
  Build libcurl:    Shared=yes, Static=yes
  Built-in manual:  enabled
  --libcurl option: enabled (--disable-libcurl-option)
  Verbose errors:   enabled (--disable-verbose)
  Code coverage:    disabled
  SSPI:             no      (--enable-sspi)
  ca cert bundle:   /etc/pki/tls/certs/ca-bundle.crt
  ca cert path:     no
  ca fallback:      no
  LDAP:             enabled (OpenLDAP)
  LDAPS:            enabled
  RTSP:             enabled
  RTMP:             no      (--with-librtmp)
  Metalink:         no      (--with-libmetalink)
  PSL:              no      (libpsl not found)
  Alt-svc:          no      (--enable-alt-svc)
  HTTP2:            enabled (nghttp2)　　　　　　← 有効になっていることを確認
  HTTP3:            no      (--with-ngtcp2, --with-quiche)
  ECH:              no      (--enable-ech)
  Protocols:        DICT FILE FTP FTPS GOPHER HTTP HTTPS IMAP IMAPS LDAP LDAPS MQTT POP3 POP3S RTSP SMB SMBS SMTP SMTPS TELNET TFTP
  Features:         AsynchDNS HTTP2 HTTPS-proxy IPv6 NTLM NTLM_WB SSL UnixSockets libz
----------------------
```

コンパイル
```sh
$ make
```

コンパイルに問題がなければインストール
```sh
$ sudo make install
```

<br>

# 確認

バージョン確認
```sh
$ /usr/local/bin/curl -V
curl 7.73.0 (x86_64-pc-linux-gnu) libcurl/7.73.0 OpenSSL/1.0.2k-fips zlib/1.2.7 nghttp2/1.33.0
Release-Date: 2020-10-14
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps mqtt pop3 pop3s rtsp smb smbs smtp smtps telnet tftp
Features: AsynchDNS HTTP2 HTTPS-proxy IPv6 Largefile libz NTLM NTLM_WB SSL UnixSockets
```

動作確認
```sh
$ /usr/local/bin/curl -I --http2 https://www.google.co.jp
HTTP/2 200　　← HTTP2になっていることを確認
content-type: text/html; charset=Shift_JIS
p3p: CP="This is not a P3P policy! See g.co/p3phelp for more info."
date: Thu, 19 Nov 2020 05:08:35 GMT
server: gws
x-xss-protection: 0
x-frame-options: SAMEORIGIN
expires: Thu, 19 Nov 2020 05:08:35 GMT
cache-control: private
set-cookie: 1P_JAR=2020-11-19-05; expires=Sat, 19-Dec-2020 05:08:35 GMT; path=/; domain=.google.co.jp; Secure
set-cookie: NID=204=C9taETFkTW4o8H6EMfum-baleukGl3qijs2D9894nV8qIO-mrdT2hovN6mjRAXJQQ0eexachxDQM3GBF_GEBiZUubz5FIBKBPQ6748BJ7ldRLQsnDTj01wTBEwubSlVvVBeuhvXuO1tIs-ER9sPV3P2-A1D6kLGyZjTXXalZQTI; expires=Fri, 21-May-2021 05:08:35 GMT; path=/; domain=.google.co.jp; HttpOnly
alt-svc: h3-Q050=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-T051=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
```

インストール状況
```sh
$ tree -P *curl* -I "share|src" /usr/local/

/usr/local/
├── bin
│   ├── curl
│   └── curl-config
├── etc
├── games
├── include
│   └── curl
│       ├── curl.h
│       └── curlver.h
├── lib
│   ├── libcurl.a
│   ├── libcurl.la
│   ├── libcurl.so.4.7.0
│   └── pkgconfig
│       └── libcurl.pc
├── lib64
├── libexec
└── sbin
```