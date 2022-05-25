# AWS の Observability（可観測性）の全体像〜 Amazon CloudWatch とオープンソースの活用〜(AWS-21)

日時：2022/05/25　13:15 〜 13:45
資料：[AWS-21_Observe_and_detect_for_application_availability_and_performance_KMD05-KMD13.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202205_AWS_SUMMIT_JAPAN_2022/AWS-21_Observe_and_detect_for_application_availability_and_performance_KMD05-KMD13.pdf)

<br>

## Observability（可観測性）

Observability（可観測性）とは？
- システムの動作状況を把握できている状態
- システム運用において判断に必要な情報がきちんと取得できている状態

データに基づく意思決定
- ログ
- メトリクス
- トレース

<br>

## AWSでのObservability

- CloudWatch metrics
- CloudWatch Logs
- X-Ray
- Amazon Managed Grafana

<br>

## Amazon CloudWatch

ビルディングブロックを実現
- さまざまなCloudWatchサービスの中からチョイスする
- Metrics, Logs, Alarms, DashBoard, ServiceLens, Logs Insights...
