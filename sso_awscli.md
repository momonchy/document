# AWS SSO 環境下における AWS CLI の運用

AWS Control Tower にて管理された AWS アカウントにおいては AWS SSO が有効になっており、AWSCLI を利用する場合、通常とは異なり Credential での認証は行わない（出来はするが推奨されない）
本ドキュメントでは、ローカル開発環境において AWS SSO に最適化された Profile 運用する為の設定手順を紹介する。

<br>

## 1. AWSCLI の導入（未導入の場合）

こちら [公式の手順](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html) に沿って作業を行う。

<br>

## 2. Profile の作成

こちら [公式の手順](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-configure-sso.html) に沿って作業を行う。尚、事前に以下情報をメモしておくこと。

- AWS SSO にて Switch Role が許可された AWS アカウント ID（数字12桁）
- AWS SSO にて Switch Role が許可された AWS アカウントのロール名（AWSPowerUserAccess とか）
- AWS SSO ログイン後の URL情報（↓のようなやつ）
    ```
    https://d-XXXXXXXXXX.awsapps.com/start
    ```
- 許可されたリージョン（大体は ap-northeast-1 で問題無い）
- プロファイル名

作業が終わると ```~/.aws/config``` へ以下のような設定情報が登録される。尚、今後管理する AWS アカウントが増える場合には該当ファイルを直編集しても問題無い。

```
[profile my-dev-profile]
sso_start_url = https://my-sso-portal.awsapps.com/start
sso_region = us-east-1
sso_account_id = 123456789011
sso_role_name = readOnly
region = us-west-2
output = json
```

<br>

## 3. 利用方法

AWSCLI、AWS SAM、AWS CDK 等を利用する場合に事前に AssumeRole を行って STS を取得しておく必要がある。その際、Web ブラウザにて ID/Password 認証が発生する。

```
例）
$ aws sso login --profile {プロファイル名}
```

STS の有効期限は AWS SSO の設定（許可セット）にて定義されている（デフォルトは1時間）
上記ログインが完了後は通常通り ```--profile {プロファイル名}``` オプションを指定してコマンドを実行する。

```
例）
$ aws --profile my-dev-profile  s3 ls
$ sam deploy --profile my-dev-profile
$ cdk bootstrap --profile my-dev-profile
```

