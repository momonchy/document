# AWS Amplify と AWS AppSync を使ったフルスタックアプリケーションの開発(AWS-26)

日時：2021/05/12　12:30 〜 13:00

<br>

## 認証認可機能
Cognitoと連携
Amplify CLIでAuthカテゴリを追加
Amplify UI Componentsを使ってSign-Up画面を簡単に作成

<br>

## GraphQL API
Amplify CLIでAPI認証方法などのカテゴリを追加
schema.graphqlでスキーマを定義
→ connectionディレクティブでDynamoDBでもリレーションできる

クライアント側のGraphQLのクエリも自動生成する
この時点でモックを作成してローカルのGraphQL APIで検証できる

<br>

## チャット機能
GraphQLのSubscriptionディレクティブを使ってWebSocketによる双方向通信を実現する

<br>

## ビデオ通話機能
Amazon Chime SDKを利用
AmplifyからAmazon Chime APIを呼び出す必要がある
