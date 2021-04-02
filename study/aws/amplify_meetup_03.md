# Amplify Meetup #03
事例を中心としたLightning Talks

質問(Twitter)：#AWSAmplifyJP
アンケート：https://bit.ly/3dm3zMI
コンパス：Amplify Meetup

<br>

## 学習ツール

- [Amplify SNS Workshop](https://amplify-sns.workshop.aws/ja/)

<br>

## AWS Amplify とは

Twitter（こやきむ）：@kimyan_udon2

- Amplify ライブラリ
    バックエンドと直感的なインターフェースで接続できる
- Amplify CLI
    数コマンドでバックエンドを構築
- Amplify Console
- Amplify Admin UI
    バックエンドコンテンツを管理するGUIツール
    IAMが無くてもアクセスできる（Admin UI）

Amplify Japan User Group というコミュニティがある
AWS Amplify Japan Comunity Slack がある

<br>

## 株式会社スカラーパートナーズ　木村

タイトル：バックエンドエンジニアがAmplifyで中規模案件に挑戦した話

「[エールラボえひめ](https://yell-lab.ehime.jp/)」という愛媛県が提供するサービスをAmplifyで構築した。

開発後の運用ジレンマ
- 作った分だけ運用が必要
- インフラ運用を楽にしたい
その他
- スピード感を出したい

学習方法
- ★Amplify SNS Workshopを利用（初学者の教科書）
- Amplify Framework Documentation（英語）
- AWSサポートの利用

ぶつかる課題
- データ設計
    - DynamoDBの設計＆学習
    - 「DynamoDBではテーブルを1つだけにすることが推奨」
    - 検索機能要件を充実するならElasticSearchが必須
        - ES中心にデータ設計するのが良い
- バリデーションの観点
    - バックエンドでちゃんとやった方がよい

<br>

## O株式会社　青木

タイトル：ExpoとAmplifyを使った開発

EXPOとは、Webとネイティブアプリ（React Native）を同時に作ってくれるプラットフォーム

```
VScode → Github → Amplify → App Build
```

[Amazon Pinpointとは？](https://aws.amazon.com/jp/pinpoint/)

<br>

## 株式会社ビータス　谷

タイトル：toC をAmplifyを使ってリリースした

- Amplify Libraries：React Nativeから簡単にAWSリソースへ認証/アクセスできるライブラリ群
- Amplify CLI：Cognito連携が楽。認証画面も簡単にできる
- Amplify Console：CI/CDを一瞬でできる

Amazon Pinpointでデータ蓄積？分析？

<br>

## 株式会社マーケットエンタープライズ　南島

タイトル：レガシーなWebシステムにAmplifyを生してみた

良さ
- branch毎に環境を作れる
- cognitoを簡単に使える

SSOの導入
- RDSとCognitoのユーザ情報はRDSのtriggerで同期をとるようにした（Lambdaをキック）

距離検索
- Elastic Searchへgeo_distanceでクエリーを投げる

<br>

## スタートアップテクノロジー 松井

タイトル：Amplifyで作る配信サイト/ビデオチャットWebアプリ

Vuetify

<br>

## Amplify Update

- flutter
- kotlin

