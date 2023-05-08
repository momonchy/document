# Route53 で登録・購入したドメインを他の AWS アカウントへ移管する方法

表題の通りです。  
AWS アカウントの統合・解約など、ドメイン管理用の AWS アカウントを変更したい場合に有用な手順となります。

本手順は、実際に Route53 上でドメインを新規取得した 30 分後に別の AWS アカウントへ移行（取得先アカウントを間違えた）した際の手順となります。

その他、注意事項等については公式のドキュメントを確認して下さい。

<br>

## 参考サイト

- [公式ドキュメント](https://docs.aws.amazon.com/ja_jp/Route53/latest/DeveloperGuide/domain-transfer-from-route-53.html)
- [DeveloperIO](https://dev.classmethod.jp/articles/how-to-transfer-route-53-domain-to-another-aws-account/)

<br>

## 手順

本手順は全て AWS CLI で実施します。  
事前に以下の情報を収集しておいて下さい。

- 移管対象ドメイン名
- 移管先の AWS アカウント ID（12桁）

<br>

### 1. 移管元アカウントに対するドメイン移管の申請

```sh
$ aws --profile ${移管元プロファイル名} route53domains transfer-domain-to-another-aws-account --domain-name ${対象ドメイン名} --account-id ${移行先AWSアカウントID} --region us-east-1
```

以下のようなレスポンスが返ってくるので、Password 情報をメモっておいて下さい。

```json
{
    "OperationId": "xxxxxxxxxx",
    "Password": "xxxxx"
}
```

<br>

### 2. 移管先アカウントでドメイン移管を承認

```sh
$ aws --profile ${移管先プロファイル名} route53domains accept-domain-transfer-from-another-aws-account --domain-name ${対象ドメイン名} --password ${上記手順で取得したパスワード} --region us-east-1
```

<br>

### 3. ホステッドゾーンの移行

新規ドメインの場合は、普通に移管先アカウント上でホステッドゾーンを作って下さい。  
既に運用中のドメインの場合は、[公式ドキュメント](https://docs.aws.amazon.com/ja_jp/Route53/latest/DeveloperGuide/hosted-zones-migrating.html)に沿って移行作業を行なって下さい。

<br>

### 補足. ドメイン移行申請のキャンセル

```sh
$ aws --profile ${移管元プロファイル名} route53domains cancel-domain-transfer-to-another-aws-account --domain-name ${対象ドメイン名} --region us-east-1
```