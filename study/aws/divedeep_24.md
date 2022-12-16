# 第24回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2022/11/24
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## キーワード

- 

<br>

## 今月のお勧め5分間アップデート

- SESがVirtual Deliverability Managerでメール逢信成功率向上をレポートするようになった
  - Dashboardが充実した
- SNSのメッセージデータ保護
  - リアルタイムで特定データをチェックしてマスキングできる
  - コンプライアンス向け機能
- EventBridgeで新たなスケジューラを提供
  - EventBridge Scheduler

<br>

## AWS サーバーレスアプリケーションモデルを使って、TypeScript で Lambda を作成しよう

- AWS SAM で Package & Deploy
  - Package は S3 へあげるだけ
- AWS SAM CLI esbuild を一般提供
  - esbuild によって Typescript で書いたコードを Build できるようになった
  - top-level await
- Metadata: ってパラメータが追加された
  - BuildMethod: で esbuild を指定
- TypeScript で Lambda コードを書くと、esbuild によって JavaScritp へ変換した上でデプロイするよって話

<br>

## Amazon DevOps Guru を使って機械学習によるサーバーレスアプリケーションの改善しよう

- Amazon DevOps Guru
  - アプリケーションを監視して問題点をMLモデル使って検知
  - マネージドサービス
- タグ、CFnスタック、AWSアカウント全体などを指定
  - 選択されたリソースを DevOps Guru が分析＆レポート
  - SNS、EventBridge と連携
  - AWS Trusted Advisor みたいなもの？
- 細かく CloudWatch を確認するよりは、DevOps Guru で問題点と分析をまとめて表示させると便利かも
  - スロットリングした情報も表示してくれる
  - 管理DXソリューションの監視に利用すると便利かも

<br>

## コードとデモで理解する！ AWS Lambda の実装を加速する AWS Lambda Powertools のご紹介

- 利用方法
  - Lamda Layer で外部 ECR の ARN を指定して利用する
  - ```pip install aws-lambda-posertools``` でインスコ
