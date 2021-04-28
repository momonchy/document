# 新機能 Amazon Athena Federated Query を Amazon QuickSight で体験

日付：2021/04/27

<br>

## ドキュメント
- [講義資料](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210427_Athena-DDB-QuickSight.pdf)
- [ハンズオン資料](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210427_Athena-DDB-QuickSight-Handson.zip)

<br>

## ハンズオンの全体像
1. AthenaのFederated QueryでDynamoDBのデータをクエリする
2. S3上のCSVデータをDynamoDBのデータをジョインする
3. クエリ結果をSPICEに格納し、QuickSightで可視化する

<br>

## Athena
S3上のデータに対して標準SQLによるインタラクティブなクエリを投げられる
- サーバレス
- 大規模データに対して高速なクエリ（Prestoベース）
- スキャンしたデータに対しての従量課金
    - 1TB = $5
    - MB以下は切り捨て
- JDBC / ODBC / API経由でBIツールとシステム連携

Athena Federated Queryとは
- S3以外のデータへアクセス可能（HBase, ElasticCache, DynamoDB, RDS, CloudWatch, DocumentDB）
- 背後でLambdaが動いている（自動でスケール）

フェデレーションとは？
- データを事前コピーせず、都度アクセスする手法
- メリット：リアルタイム性
- デメリット：可用性と性能がレプリケーションに劣る

<br>

## QuickSight
特徴
- サーバレスなBIツール
- 安く使える
- ブラウザだけで利用可能
- SPICEというインメモリデータベースを備えている

料金
- Author: $18/user/month
    - ダッシュボード作成
- Reader: 従量課金（最大 $5/user/month）
    - ダッシュボード閲覧

