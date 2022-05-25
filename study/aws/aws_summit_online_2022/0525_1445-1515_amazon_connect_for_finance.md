# 金融サービス業界での Amazon Connect 活用の広がり(AWS-14)

日時：2022/05/25　14:45 〜 15:15
資料：[AWS-14_ExpandingAmazonConnect_FSI.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202205_AWS_SUMMIT_JAPAN_2022/AWS-14_ExpandingAmazonConnect_FSI.pdf)

<br>

## 事例

コンタクトセンターの黙ナイぜーションが進んでる

auじぶん銀行
- ソフトフォンのカスタマイズ
- 完全マネージドサービス
- CloudFront, S3, API Gateway, Lambda, DynamoDB
- ソフトフォン着信時にさまざまな情報を画面へ表示（待ち時間、発信元電話番号、IVRメニューで選択した内容）
- コールセンターがAmazon Connectへ接続する際にはAWS SSOを利用して認証している

クレディセゾン
- ほぼマネージドサービス
- Polly, Kinesis Data Streams, EventBridge, Lambda, DynamoDB
- 架電ジョブリストをS3へ保存してジョブをLambda経由でSQS、DynamoDBへ保存
- SQSを読み取ったLambdaがAmazonConnectへ接続してDynamoDBから読み取った督促先へ架電しPollyで読み上げ

Affirm
- 海外のECサイト
- Voice IDによる声紋判定
- Amazon TranscribeでASR
- Amazon Comprehendで感情分析