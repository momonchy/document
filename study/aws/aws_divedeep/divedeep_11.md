# 第11回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2021/10/28
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## キーワード

- オーケストレーション、オーケストレーター

<br>

## 5分間アップデート

- ECS AnywhereがGPUベースのワークロードをサポート
- QuickSightでSPICEの増分更新ができるようになった（これまでは常にデータをフルロードしてた）
- QuickSightのSPICE容量が5億行へ上限が上がった
- ★ AWS BatchでStepFunctionsが実行できるようになった
    - ワークフローオーケストレーションからStepFunctionの設定ができる
- ★ AWS GlueのクローラーがAmazon S3イベント通知を受け取れるようになった
    - イベントのあったフォルダだけを自動クローリング可能

<br>

## AWS 環境における Infrastructure as Code

- 考え方
    - 100%の管理を目指さない
    - 巨大化させない（適切なサイズ・範囲に分割）
- レイヤとライフサイクルでテンプレートの巨大化を防ぐ（スタックを整理する）
- ベストプラクティス
    - クロススタック参照（テンプレート間でリソースID等をエクスポート）
    - ドリフトの是正（ドリフト上手く動かなくね？ローカルのテンプレートとの差分をどうやってするの？）
    - 機密情報をSSMから動的に参照

<br>

## AWS Copilot で始める ECS on Fargate

- Copilot CLI
    - OSSのCLIツール
    - ECSでコンテナアプリケーションの構築、リリース、運用を用意にする
    - ECSクラスターやCI/CDパイプラインをインタラクティブに作成
- 実践
    - app initでSystem Manager Parameter Storeで枠が作成される（CloudFormationが動く）
    - env initで環境を指定。ローカルに保存されているprofileを選択
        - 既存のネットワーク(VPC群)を使うか新規で作成するか聞かれる
    - svc initでサービスを作成（App Runner/Fargate等を選択）
        - Dockerfileを指定するとECRリポジトリが作成される
        - Manifestファイルが作成される（詳細なスペック情報など。Taskが作成される）
    - svc deployでデプロイ
        - Dockerイメージを作成しECRへプッシュ
        - Taskを作成してECSクラスターへデプロイ

<br>

## Amazon CloudWatch Synthetics Canaries で始める Synthetic Monitoring

- 外形監視を実現
    - URL監視、ステータスコードチェック、応答時間の測定、サービス内でのワークフローの動作監視
    - AWS内だけでなく外部サービスも監視可能
- BluePrintによりすぐに利用可能（テンプレート）
    - ハートビート（URLを登録）
    - API Canary（API Gatewayなら登録簡単）
    - リンク切れチェッカー
    - Canary Recorder（Chromeプラグインを利用してブラウザ上での振舞い/ドリルダウンを自動でスクリプト化可能）
    - GUIワークフロービルダー（DOM指定＆クリックなどのより複雑な操作ステップを管理コンソールのUIで組み立てられる）
    - Visual Monitoring
- カナリヤ（実体はHeadless Chromeブラウザ）を定義してサービスを利用
    - カナリヤ用Lambda関数が作成される
    - これを変更することでなんでもできる（Node.js/Python）
- 「CloudWatch Alarms/Event Bridge」とカナリヤを連携させることで通知、動的リカバリー処理なのどのActionが可能
