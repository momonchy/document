# 第26回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」
AWS re: Invent 2022 Live デモ祭り 第二弾

日付：2023/01/26
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## AWS Step Functions Distributed Map ([資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/DD/20230126_DD_26th_ISV_DiveDeepSeminar_sfn_dmap.pdf))

Distributed Map とは
- 10,000並列まで同時実行できるようになった
- S3からの大規模データ読み込み、書き戻しをサポート

クレームチェックパターン（MapReduceみたいなもの）
- 効率的な大容量データの受け渡し手法
- 今まではこれを自前で実装しなければならなかった

結論
- Map関数の関数部分 = Lambda（同時10,000超える）
- Map関数の配列部分 = S3へ保存されたCSV/JSON等で区切られたファイル
  
<br>

## Amazone Verified Permissions ([資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/DD/20230126_DD_26th_ISV_DiveDeepSeminar_verified_permissions.pdf))

Verified Permissionsとは？
- Cognito等のIdPと共に利用するサービス
- きめ細やかなアクセス許可管理（認可）を行えるサービス
- **アプリケーション内でやっていた認可機能をオフロード出来る**
  - これまでAWSリソースに関する認可は Cognito, IAM で出来てた

ポリシーの保存
- [Cedar](https://www.cedarpolicy.com/) という独自言語で記述する
- 簡易版 IAM Policy のような感じ

ポリシーの評価
- SDKで必要な情報を投げるとAllow or Denyを返してくれる

<br>

## AWS Glue Custom Visual Transforms

AWS Glue Studio の新機能
- 事前に用意した Python スクリプトを S3 へ配置しておいて、Glue Studio 側から呼び出すことができる？

<br>

## AWS Glue on Ray

Ray とは
- ETLジョブの処理エンジンとして、Apache Spark, Python に次いで Ray がサポートされた
- Python = シングル処理
- Apache Spark = 分散処理
- Ray = Pythonを分散処理可能とするフレームワーク
- Pandasの代替として利用可能（書き方が類似してる）

<br>

## Amazon ECS Service Connect ([資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/DD/20230126_DD_26th_ISV_DiveDeepSeminar_ECS_Service_Connect.pdf))

Service Connectとは？
- Containerを利用したサービス間通信を実現する新たな方法
- ECSのタスクにService Connectエージェントが追加される
- Service ConnectエージェントがAWS Cloud Mapで名前解決して他のECSタスクへデータを転送する
- ★サービスメッシュとは？？

手順
- Cloud Mapで名前空間を作成する
- タスク定義を作る
- サービスを作る際に
  - Service Connectオプションをオンにする
  - 名前空間を指定する
  - コンテナマップポートを登録
- バックエンド転送時のバランシングロジックは？
  - [Envoy](https://thinkit.co.jp/article/13471) を利用してる