#  60 分で学ぶ Amazon Athena、AWS Glue 総復習

日付: 2021/07/06 11:00-12:00

<br>

## キーワード
- カーディナル
- OLAP/OLTP
- プリミティブ

<br>

## Amazon Athena

S3上のデータにSQLを実行できる
- 課金はスキャンしたデータに対しての従量課金（データ量）
- JDBC/ODBC/API経由でBIツールやシステムと連携
- S3をデータソースとして利用できる

使い所
- 高速なDWHへ入れる前のお試しorデータ選定目的
- OLTP向けでは無く、OLAP向け。トランザクションは未サポート
- ELTでは無く、分析向け
- いかにして読み込むデータ量を抑えるかがキモ

実態
- Presto（0.172）：高速な分散クエリエンジン
- データは全てインメモリで処理
- デフォルトではGlueのデータカタログをメタデータ管理に使用
- メタデータは、DB/Table/View/Partitionなどの情報を指す
- データかとログはApacheHiveMetastore互換

Athenaを利用するうえで非常に重要なのはパーティション
- データを探索範囲を絞る
- 速度、コストに影響が発生する

扱える型
- プリミティブ型
- 配列型
- map型
- struct型

扱えるデータ形式
- CSV
- TSV
- JSON
- Apache Avro
- ORC
- Parquet形式
- Apacheログ
- などなど

データ圧縮形式
- SNAPPY(Parquetの場合)
- ZLIB
- GZIP
- LZO

Athena Workgroups
- ワークグループ単位で扱えるデータを分けられる
- ワークグループ単位でIAMで認可することができる

