# S3バケットのデータを異なるAWSアカウントのS3バケットへ再帰的にコピーする

## やりたい事

タイトルの通りです。  
これを実現する為におこなう設定は以下の通り。

- コピー元のAWSアカウント上の実行IAMユーザへカスタムポリシーをアサインする
- コピー先のS3バケットポリシーへポリシーを追加する

<br>

## 前提

- コピー元のS3バケットに対する操作権限を十分に有する

<br>

## 参考サイト
- [【AWS FAQ】別の AWS アカウントから S3 オブジェクトをコピーするにはどうすればよいですか?](https://aws.amazon.com/jp/premiumsupport/knowledge-center/copy-s3-objects-account/)
- [【AWS FAQ】ある Amazon S3 バケットから別のバケットにすべてのオブジェクトをコピーするにはどうすればよいですか?](https://aws.amazon.com/jp/premiumsupport/knowledge-center/move-objects-s3-bucket/)

<br>

## 手順

1. コピー元でカスタムポリシーを作成し、実行IAMユーザへアサインする。

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "s3:*",
                "Resource": [
                    "arn:aws:s3:::SOURCE-S3-BUCKET-NAME",
                    "arn:aws:s3:::SOURCE-S3-BUCKET-NAME/*"
                ]
            },
            {
                "Effect": "Allow",
                "Action": "s3:*",
                "Resource": [
                    "arn:aws:s3:::DESTINATION-S3-BUCKET-NAME",
                    "arn:aws:s3:::DESTINATION-S3-BUCKET-NAME/*"
                ]
            }
        ]
    }
    ```

2. コピー先S3バケットのバケットポリシーへ、以下のポリシーを適応する。

    ```json
    {
        "Version": "2008-10-17",
        "Id": "OtherBucketCopyPolicy",
        "Statement": [
            {
            "Sid": "SampleStmt",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::NNNNNNNNNNNN:user/IAM-USER-NAME"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::DESTINATION-S3-BUCKET-NAME",
                "arn:aws:s3:::DESTINATION-S3-BUCKET-NAME/*"
            ],
            "Condition": {
                "StringEquals": {
                "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
            }
        ]
    }
    ```

3. コピー先S3バケットの「オブジェクト所有者」を「希望するバケット所有者」へ変更する。  
これによりコピーされたオブジェクトの所有者がバケット所有者になる。

4. AWS CLIからコピーする。  
尚、実行端末上でコピー元AWSアカウントの Credentials が既に登録されていることが前提。

    ```
    $ aws s3 cp --recursive s3://SOURCE-S3-BUCKET-NAME/hoge/ s3://DESTINATION-S3-BUCKET-NAME/fuga/ --acl bucket-owner-full-control
    ```

<br>

## 注意

本手順では copy は出来ても sync をおこなう事が出来ません。  
これは、コピー先S3バケットへ登録したバケットポリシー内の「Condition」に起因し、ListeObjectV2 APIの実行権限を得られないタメです。

> fatal error: An error occurred (AccessDenied) when calling the ListObjectsV2 operation: Access Denied

その為、```sync``` では無く ```cp --recursive``` で代用しています。

詳細は以下のリンクで確認して下さい。

- [Cannot match Condition statement with actions and resources in s3 bucket policy](https://stackoverflow.com/questions/44847726/cannot-match-condition-statement-with-actions-and-resources-in-s3-bucket-policy)
- [AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/amazon-s3-policy-keys.html)