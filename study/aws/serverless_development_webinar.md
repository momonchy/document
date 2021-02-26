# イチから理解するサーバレスアプリ開発 2021

日付：2021/02/25

## 用語集
- ラウンドトリップ
- セマンティック
- アーティファクト
- at least once
- ファンアウトパターン
- ストラングラーパターン
- モノリシック

<br>

## ドキュメント
- [サーバレスのおさらい](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210225_1_Serverless.pdf)
- [サーバレスアプリケーション開発・設計の始め方](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210225_2_Serverless_Development.pdf)
- [サーバレスユースケースパターン](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210225_3_usecase_patterns.pdf)
- [【チラシ】サーバレスの始め方](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/202101_LearningSteps.pdf)

<br>

## サーバレスのおさらい

コロナによる影響でサーバレスへの関心・期待が高まっている

サーバレスとは？
- サーバがない ×
- サーバの存在を意識しない ◯

サーバを意識した設計
- 規模の見積り
- 可用性の設計
- データ保全の検討

サーバを意識しない設計
- HTTP REST(API Gateway)
- 処理ロジック(Lambda)
- データ管理(DynamoDB)
※サービス側自動でリソースがスケールする
- 自動スケール
- 設計済みのリトライ
- データの信頼性

これらの負荷からエンジニアリソースを解放する
- コンピュートリソース
- ネットワーク
- OS保守、パッチ
- アプリ実行基盤
- 冗長化、可用性
- 暗号化
- サーバ間通信

それ以外の利点
- アイドル時のリソース確保が不要（コスト最適化）

従来型の開発に比べてモダンな開発が可能
- サイジング、キャパシティプランニングの必要がない
- 利用されて無いとコストが発生しないのでスタートし易い

<br>

### 主要コンポーネントと機能概要

Function as a Service: AWS Lambda
- 処理ロジック部分で利用
- MVCモデルでの　Model に該当
- View/ControlはS3などでSPAにて提供
- Step Functionと連動することで複数のLambdaの処理フローをグループで管理できる

負荷が高まった場合の対応
- 入り口でスロットリングする
- DB接続を制御する
    - RDS Proxyによってコネクションプーリング可能
- DBを分散させる
    - DynamoDBがおすすめ
- ストラングラーパターン

<br>

## 開発・設計の始め方

### サーバレスのサービスを知る

#### API Gateway
特徴
- API管理（設定やデプロイの制御）
- 認証と認可（アクセス制御）
- 流量制御と保護（スロットリング）

設定可能なプロトコル
- REST（ステートレス）  
    バックエンドへ投げるまでに様々な制御ができる
- HTTP API（ステートレス）  
    バックエンドへ投げるまでかなりシンプル   
    VPCリンクでALBとかと連動可能
- WebSocket（ステートフル）




ファンアウトパターン
```
event -> sns -> sqs(複数) -> lambda(複数)
```
