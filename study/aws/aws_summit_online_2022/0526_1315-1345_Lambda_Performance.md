# AWS Lambda Performance Tuning Deep Dive〜本当に知りたいのは”ここ”だった 〜(AWS-46)

日時：2022/05/26  13:15 〜 13:45
資料：[AWS-46_AWS_Lambda_Performance_Tuning_Deep_Dive.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202205_AWS_SUMMIT_JAPAN_2022/AWS-46_AWS_Lambda_Performance_Tuning_Deep_Dive.pdf)

<br>

## サブタイトル

同時実行数（Concurrency）を意識する
- リクエストレート（rps）増加
- 実行時間（duration）増加
- Little's Law（リトルの法則）
    - Concurrency = rps x duration

Tuningの観測、Throttlingへの対処
- 関数単位でConcurrencyを設定する
    - リザーブドであり最大値
- 外部リソースへのリトライを実装していると同時実行数が増えていく

<br>

## Lmabda実装プラクティス

効率的な関数コード
- FAT/monolithicな関数実装を避ける

揮発性を意識
- イベント処理終了まで次のイベントを受け付けない
- Lambdaのグローバルスコープを利活用