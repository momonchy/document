# SSMを利用したEC2へのログインアカウント管理
SSMサービスを利用することで、IAMユーザをベースにEC2へのログインアカウントを管理することができる。

これにより、SecurityGroupでメンテナンスアクセス用のルート（22ポート）を開放する必要は無くなり、グローバルIPが未アサインなEC2、およびプライベートなセグメントへ所属するEC2に対してもアクセス可能となる。

<br>

# 前提条件
AMI / OS：Amazon Linux 2

<br>

# EC2上での手順
EC2で 2.3.672.0 以上のSSMエージェントがインストールされている必要がある。  
公式の手順は[こちら](https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/sysman-manual-agent-install.html)を参照。

尚、現在（2021/02/15時点）では Amazon Linux へ既にSSMエージェントがインストールされているので、yum update するだけで良い。

1. バージョン確認
	```Shell
	$ rpm -qi amazon-ssm-agent
	```

2. アップデート
	```Shell
	$ sudo yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm
	```

3. SSMエージェントをリスタート
	```Shell
	$ sudo systemctl restart amazon-ssm-agent
	```

<br>

# IAMの設定
IAMユーザへ以下のポリシーをアサインする。  
尚、IAMユーザへ AdministratorAccess 権限が付与されている場合には以下ポリシーをアサインする必要は無い。

- AmazonSSMFullAccess

EC2へ以下のポリシーが含まれるRoleをアサインする。

- AmazonSSMManagedInstanceCore

<br>

# 接続クライアントの設定 (for Mac)
v1.16.12以上のAWSCLIと、v1.1.23.0以上のSession Managerプラグインが必要です。
公式の手順は[こちら](https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)を参照。

1. AWSCLIのバージョンアップ
	```Shell
	$ sudo pip install --upgrade awscli
	```

2. プラグインのインストール＆アップデート
	```Shell
	$ curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/mac/sessionmanager-bundle.zip" -o "sessionmanager-bundle.zip"
	$ unzip sessionmanager-bundle.zip
	$ sudo ./sessionmanager-bundle/install -i /usr/local/sessionmanagerplugin -b /usr/local/bin/session-manager-plugin
	```

3. バージョン確認
	```Shell
	$ session-manager-plugin --version
	1.1.31.0
	```

4. ssh configの作成
	``` ApacheConf
	$ vim ~/.ssh/config
	---------
	# SSH over Session Manager
	host i-* mi-*
		ProxyCommand sh -c "aws ssm start-session --target %h --document-name AWS-StartSSHSession --parameters 'portNumber=%p'"
	---------

	複数ノードやプロファイルを管理してる場合はこんな感じ
	---------
	Host <uniq name>
		HostName <instance id>
		User ec2-user
		Port 22
		ProxyCommand sh -c "aws --profile <profile name> ssm start-session --target %h --document-name AWS-StartSSHSession --parameters 'portNumber=%p'"
		IdentityFile <pem file path>
		TCPKeepAlive yes
		IdentitiesOnly yes
	---------
	```

<br>

# 接続
秘密鍵とEC2のIDを指定して、SSHまたはSCPを行う。

```Shell
$ ssh -i <秘密鍵> ec2-user@<EC2のID>
or
$ ssh <uniq name>

$ scp -i <秘密鍵> <ローカルファイル> ec2-user@<EC2のID>:＜転送先DIR>
```

<br>

# 参考サイト
- [Qiita](https://qiita.com/comefigo/items/b705325d082018ab2348)
- [DeveloperIO](https://dev.classmethod.jp/cloud/aws/session-manager-launches-tunneling-support-for-ssh-and-scp/)
- [DeveloperIO ](https://dev.classmethod.jp/cloud/ssm-session-manager-from-mac-to-linux-ec2/)