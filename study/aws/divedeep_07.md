# 第7回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2021/06/24
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## 資料

今後、[connpass](https://awsj-saas.connpass.com/event/215850/)の方へアップロードされる予定

<br>

## 5分間アップデート

- 週間AWSでブログ形式でもアップデート情報が提供されている
- ECS Anyware（オンプレ環境へライブラリを入れるとAWSのECSコントロールと接続する）
    - ラズパイの事例がブログにのってる
- Amazon Locationが日本の地図に対応
- CloudWatch Resource Health
    - ヒートマップでEC2の状況を可視化できる

<br>

## ノンコーディングでデータ前処理（Glue DataBrew）

AWS Glue DataBrew
- データのクリーンアップ、正規化をノンコーディングで実施できる（前処理）
- 250種類以上の組み込みの変換処理から選択

デモを見る感じ、[Tableau Prep](https://www.tableau.com/ja-jp/products/prep) みたいな感じ？
これいい！

<br>

## Amazon Athena の基礎的な使い方、最近のアップデート

Amazon Athena
- スキャンしたデータに対する従量課金制
- Prestoと同様、標準ANSI SQLに準拠したクエリに対応
- 地理空間関数に対応
- SageMagerと連携してAthenaからMLを使った推論を実行可能

PyAthenaってのがある
pandasで直接S3からCSVを読み込めるらしい