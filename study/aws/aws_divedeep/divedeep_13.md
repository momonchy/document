# 第13回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2021/12/16
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## キーワード

- 

<br>

## Amazon S3 アップデート情報

- Glacier Instant Retrival というストレージクラスが発表
    - ミリ秒以内でデータアクセス可能になった
    - 旧Glacierでは「復元」を行なわないとデータアクセスできなかった
    - スタンダードクラスとの違いは？
- 通常の Glacier が Glacier Flexible Retrieval に名前が変わった
    - 色々と料金が安くなった
- S3 のコンソールにポリシーチェック機能が統合された
    - IAM Access Analyzer が S3 コンソールへ統合された

<br>

## AWS Amplify Studio 紹介＆デモ

- 最小限のコーディングでUI開発を亜ｋ速させるGUI開発環境
- Figmaで作成したコンポーネントをGUIでバックエンドに接続、CLIdeコードに変換することが可能
- なにこれスゲ〜
- react.jsと連携すれば簡単にデザインと画面ができる

<br>

## Amazon Inspector (V2)　アップデート情報

- 何もしなくても使えるようになった？ｗ
- ソフトウェアの脆弱性や意図しないネットワーク露出領域を継続的なスキャンで検知する脆弱性管理サービス
    - リアルタイムな脆弱性監視、パッチ管理の迅速化、脆弱性対応の自動化
- （V1）今までは EC2 などにエージェントをインストールする必要があった
- （V2）Systems Manager Agentへ統合された（Amazon Linuxにはすでに入ってる）
    - IAM RoleでAmazon Inspectorからのアクセスを許可してあげる必要がある
- ★これVK案件で使える！
- EC2 と ECS で使える
- どのCVE番号に該当するかリスト化される
- 注意：ソースインストールしたものは Inspector は対象外（RPMとかで導入されたものが対象）

<br>

## AWS Chatbot のアップデート情報

- Slack連携で、Slack上でAWS CLIを打つことができるｗ
- Channelガードレールで制限かけられる
- まだプレビュー版の機能

<br>

## Amazon SageMaker Canvas の紹介＆デモ

- ノーコードで機械学習可能なツール
- まだ東京リージョンでサポートしてない
- モデルの学習
    - 2値分類、多値分類、数値分類、時系列予測などデータによってサジェストされる

<br>

## リージョンからインターネット/CloudFrontのデータ転送量無料枠拡大

- 1ヶ月あたり最大100GBまで無料
- EC2, S3, ELBなどが対象
- CloudFrontからインターネットへのデータ転送は
- 1ヶ月あたり最大1TBまで無料

<br>

## Amazon VPC IP Address Manager が発表

- VPC側で自動的にVPCへプライベートアドレスがアサインされる
    - 自動的にコンフリクトしないようになる
- 事前にでかいプレフィックスでプールを作っておく
    - 10.0.0.0/12とか
    - 既存のVPCも検出してくれる

<br>

## Amazon Kendra のアップデート集

- 検索インデックスを作成
    - 全文検索が可能となるマネージドサービス（ElasticSearchの代わりになる？）
    - S3とかをデータソースにできる
- Custom Document Enrichment
    - ドキュメントの前処理にLambdaを呼び出すことができるようになった
    - 検索バーも一緒に作ってくれる

- Search Analytics Dashboard
    - クリックレートとか
    - トップレートとか
