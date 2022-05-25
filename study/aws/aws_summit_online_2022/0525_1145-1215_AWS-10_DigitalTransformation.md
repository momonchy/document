# DX を推進するお客さまの取り組みと AWS のサービス(AWS-10)

日時：2022/05/25　11:45 〜 12:15
資料：[AWS-10_DigitalTransformation_KMD25-KMD26.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202205_AWS_SUMMIT_JAPAN_2022/AWS-10_DigitalTransformation_KMD25-KMD26.pdf)

<br>

## キーワード

- デジタルツイン
- Working Backwards

<br>

## memo

開発の進め方
- ユーザー体験をイメージして素早くサービスを立ち上げる
- 顧客の声を聞いて継続的に改善を行う

ビルディングブロック
- AWSが提供するクラウドサービスをブロックのように組み合わせる

肝はデータの利活用
- DataLakes（S3）を中心に組み上げる
- データ投入（Kinesis, API Gateway+Lambda）
- 分析（QuickSight, Redshift）
- AI/ML（SageMaker）

データドリブンの現実
- 99%：データドリブンの意思決定のための積極的な投資を行っている企業の数
- 24%：データドリブンを実行できていると考えている企業の数

課題は必ずしもテクノロジーではない
- 企業はニューエコノミーで競争するために「人」と「カルチャー」を優先する必要がある

<br>

## 事例

ニチガス
- デジタルツインシステムを他工場に横展開し全国のガス会社へMDDMを展開
- ガスボンベの状態をIoTで集めてアプリで可視化、自動で製造ラインと連携
- 完全Serverlessアーキテクチャで実現