# 第12回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2021/11/25
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## キーワード

- 


<br>

## 5分間アップデート

- Amazon Aurora で MySQL8.0 をサポート
- RDS for MySQL/PostgreSQLでMulti-AZ DB Clusterをリリース
- AWS CloudTrailがErrorRate Insightsをサポート（エラー発生率に基づいて異常を検知）
- ECS Fargate で Graviton2 が選択できるようになった
- Control Towerがネストされた組織単位をサポート（OUの中にOU）
- OpenSearch Serviceでブルー/グリーンデプロイをサポート

<br>

## Amazon Comprehend と Amazon Kendra を使った文書の検索と解析についてのご紹介

- Comprehend = 自然言語処理/テキストの解析
    - エンティティ、キーフレーズ、感情、言語種別を検出
- Kendra = 高精度な文章検索
    - 自然言語によるクエリ、キーワードクエリ
    - S3/GoogleDriveをコネクタとしてサポートしている
- Comprehendで文章を分析して、KendraでIndexを張る
- Kendraをサーチエンジンとして利用できる
    - RDSも対象にできるのでどのように活用できるのか気になる

<br>

## 200 以上の AWS サービスと連携できるようになった AWS Step Functions のご紹介

- プロセス = Lambdaとして、プロセス間の連携をStep Functionで繋げ実現させる
- Workflow Studioでステートマシンをdrawio的に構築できる
- SDKをサポートするAWSサービスをStepFunctionsから直接呼べる（AWS SDKサービス統合）
    - ASLからSDKを直接呼び出す（S3のcopyObjectとか）
    - Lambdaを経由する必要が無い
    - 注意: AWS SDKサービス統合のIAMポリシーは手動で追加する必要がある（自動では追加されない）
- ASLの組み込み関数を使い込むことでLambdaで処理する必要が無い
    - 文字列変換
    - 文字列をJSONへ変換（その逆も）
    - 配列の確認など

<br>

## 連携機能で SaaS をより便利に。 Amazon EventBridge のご紹介

- EventBridge = イベントバス
    - リクエスト再送処理などをイベントバスが勝手に判断してくれる
    - 受付機能がバックエンドのステートを意識する必要がない
- Lambda関数、StepFunctionsステートマシンなどもキックできる
- クロスアカウントイベントに対応
- 外部SaaSなどの定期ウォッチやWebhook連携は、SaaS連携パートナーであればEventBrigeから容易に連携できる
    - Lambdaでの定期ウォッチや、API Gatewayの構築によるWebhook連携をする必要が無い
- SaaS連携パートナーから飛んでくるリソースのフォーマット次第で、EventBridgeでのフィルタリング、その先のAWSリソースでINPUTデータが変わる
- SaaS連携パートナーのメリット
    - AWSアカウント間での認証作業が簡素化する
    - 連携自体は無料
    - 連携手順が標準化される
- AWS Partner Networkへ加入するとEventBridgeのSaaS連携パートナーになれる