# 第17回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2022/04/28
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## 今月のお勧め5分間アップデート

- Aurora Serverless v2 がGA
    - MySQL8.0, PostgreSQL13のエンジンへ対応
    - Primaryへプロビジョンタイプ、ReaderへServerlessのような構成をとることが可能★
- Athenaのデータリソース先が増えた
- Lambda関数URLのリリース
    - HTTPSエンドポイントをLambdaが持てるようになった（Gatewayがいらなくなった）
- PrivateLink, Transit GatewayのAZ間のデータ転送料金が無料になった

<br>

## Security Hub

発見的統制とは？
- ゲートキーパー式 vs ガードレール式
- ゲートキーパー式
    - デフォルトDeny、必要なツールなどは許可制
    - 開発の必要性に応じて徐々にIAM Roleへ権限を追加していく
- ガードレール式
    - 特定の範囲内（最低限の範囲）で自由にさせる（許可範囲内においてもルールは作る）
    - 最低限のアクションだけDenyして残りはAllowにする（脅威を発見する仕組みを入れておく）

Security Hubとは？ 
- AWS環境内におけるセキュリティとコンプライアンス状態を一元表示
- GuardDuty, Inspector, Configなどのアラートを集約
- ダッシュボードみたいなもの

参考ブログ
    - [Enabling AWS Security Hub integration with AWS Chatbot](https://aws.amazon.com/jp/blogs/security/enabling-aws-security-hub-integration-with-aws-chatbot/)

<br>

## AWS Control Tower

Control Towerとは
- マルチアカウントアーキテクチャーの実現
- 統制を効率よくカスタマイズして保守する
    - システム全体の可視性を高める
    - トラブルシューティングや新市電との全容解明
    - ガードレールの構築（SCP、Config Rules）
- Organizations, Config, CloudTrail, などの既存サービスの推奨設定がパッケージされたもの？


<br>

## Amazon GuardDuty

Amazon GuardDutyとは
- すべてのAWSサービスで有効化することが推奨されている
- 異常、脅威を検知するサービス
    - AWSアカウント、S3バケットの侵害なども検出
- データソースから脅威を検出
    - VPC flow logs
    - DNS Query Logs
    - CloudTrail Events
    - S3 Data Plane Events
    - EKS control plane logs
- S3プロテクション
    - ポリシー
    - 不正アクセス
    - 異常な振る舞い
- k8sプロテクション
    - ポリシー
    - 不正アクセス
    - 疑わしい振る舞い

有効化する前に知っておきたいこと
- 料金について
    - 分析した対象のデータ量、イベント量に対して課金
    - 僅かな料金（月間料金の1％くらい）
- パフォーマンス影響について
    - 影響無し
    - サービス提供リソースに対して分析するわけじゃないから
- 分析対象となるデータソースへ事前に何かする必要はあるか（ログ出力など）
    - 必要無し
    - GuardDutyをONにするだけ 
- GuardDutyのイベントログ保存期間は？
    - デフォルトでは90日保存
    - それ以上の場合には保存先としてS3を設定する必要がある