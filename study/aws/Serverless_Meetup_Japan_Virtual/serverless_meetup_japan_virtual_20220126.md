# Serverless Meetup Japan Virtual #20

日付：2022/01/26
Connpass: https://serverless.connpass.com/event/234895/

<br>

## キーワード

- [AWS Black Belt Online Seminar 資料集](https://aws.amazon.com/jp/aws-jp-introduction/aws-jp-webinar-service-cut/)

<br>

## Lambda アップデート

- Amazon EFSと/tmpストレージが連携可能（どういうこと？）
- コンテナ方式によるデプロイ
    - ストレージを必要とするケースで利用（機械学習とか）
    - 普段コンテナで開発してるケース（実行環境としてLambdaを使うことでオンデマンドな料金体系を利用可能）
- これ便利
<img src="./img/serverless_meetup_japan_virtual_20_lambda_001.png" >
- Event source mappingとは？（SAM上で触る？）
    - Lambdaの実行条件を書けるらしい（Filter定義: Price <= 500）

<br>

## Serverless App Experience（SAM）

- Lambdaの実行CPUを指定できる（x86_64 or arm64）
- AWS SAM Pipelines
    - SAMがパイプラインを生成
        - sam pipeline bootstrap
        - sam pipeline init
    - Github Actionsで実行可能（sam build 〜 sam deployまで）
        - OIDC連携が可能になった
        - Github上でクレデンシャルを登録する必要がなくなった
- AWS SAM Accelerate（プレビュー版）
    - 開発をスピードアップするための機能
    - sam syncコマンドの提供
        - ソースコードの更新のみが可能（CloudFormationのスタック更新をスキップ）
        - sam sync --watch でソースコード編集＆保存するだけで勝手にデプロイしてくれる
    - ログのトレース機能（集約されたフィードバック機能）
        - sam logs --stack-name sam-app --tail --include-traces
        - sam traces --tail
- CDK with SAM でローカルテストが可能