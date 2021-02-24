# Assume Role のススメ

Assume Role は、わざわざ Credencial を発行する事なく一時的に AWS リソースへのアクセス権限を得る事が可能な仕組みです。

EC2 などに IAM Role をアサインした際、内部で一時的なアクセス権限を取得しているアレです。

<br>

## プログラム上で利用

Switch Role が導入されたローカル開発環境などで AWS リソースへのアクセス権限を得る際には2つのやり方があります。(もっとあると思う)

- sts:AssumeRole を使って一時的な Credencial を取得する
- 予め Profile 化しておいてそれを参照する

<br>

## sts:AssumeRole を利用する

以下は sts:AssumeRole を利用しているパターンです。  

```python
import boto3

class STS():
    def get(self, **kwargs) -> dict:
        __session_name = kwargs.get('session_name')
        __role_arn = kwargs.get('role_arn')

        __sts_client = boto3.client('sts')
        __credentials = __sts_client.assume_role(
            RoleArn=__role_arn,
            RoleSessionName=__session_name
        )

        return __credentials
```

Switch Role が導入されていることを前提としているため、Role ARN を引数として渡しています。  
セッション名はなんでも良いです。

<br>

## Profile を利用する

AWS CLI で利用できるように、以下のような設定を入れておくことが前提です。

```Apache
$ cat ~/.aws/config

[default]
region = ap-northeast-1
output = json

[profile myaccount-dev]
role_arn = arn:aws:iam::{ACCOUNTID}:role/{ROLENAME}
source_profile = default
region = ap-northeast-1
output = json

--snip
```
```python
import boto3
from boto3.session import Session

class EC2:
    def __new__(self) -> obj:
        __profile = 'myaccount-dev'

        __session = Session(profile_name=__profile)
        __ec2_client = __session.client('ec2', __region)

        return __ec2_client
```

上記も Switch Role が導入されていることを前提として Profile を読み込んでます。
