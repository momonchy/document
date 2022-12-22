# 第四回「アップデート紹介とちょっぴりDiveDeepするAWSの時間

日付：2021/04/28  
Twitter ハッシュタグ: #ちょっぴりDiveDeep

<br>

## 資料

- [お勧め三分間アップデート](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210428_divedeep_04_update_tips.pdf)
- [ECS Execの紹介](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210428_ecs_exec.pdf)
- [Amplifyの紹介](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210428_about_amplify.pdf)
- [Amplifyを使ったチーム開発](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210428_amplify_for_team_development.pdf)

<br>

## EC2

- シリアルコンソールが使えるようになった
    - パスワード無しでもシェルにログインできるようになる
    - EC2の「接続」から選択できる

<br>

## IAM

- IAMロールのアサイン状況をIAM側から検索できるようになった
    - IAMの利用状況も確認できる？

<br>

## Amazon Lex

- 日本語に対応した

<br>

## Network Firewall

- 東京リージョンでも利用できるようになった
- どんなサービス？

<br>

## ECS Exec

- 今までは、ステートレス且つイミュータブルな環境を維持する為に起動中のコンテナへはアクセスできないようなポリシーとしていた
- CLIで接続する感じ
- コマンドの実行ログをCloudWatch Logsへ出力できる
- CloudTrailで接続情報（APIコール）の監査ログが取れる

<br>

## Amplify

- Admin UIはAWSのWebコンソールとは異なるUIを提供可能
- envコマンドでAWS環境を簡単に複製できる（checkoutで移動）
- mockコマンドでローカル環境にAPI/Lambda等のモックを作れる
    - モックの起動/停止で環境変数を自動で書き換える
    - 接続先URLなどがローカルに勝手に変わる
- Web previews機能でPull Request毎にバックエンドが作成できる
    - 現在サポートされているのはGithubだけ
    - Github上でPull Requestを削除するとAmplify上のプレビュー環境も削除される

<br>

## 以降のスケジュール

| 日付 | 開催 | 内容 |
| :--: | :--: | -- |
| 5/14 | 第五回 | セキュリティ |
| 5/27 | 第六回 | Graviton2、マルチAZベストプラクティス、ちょっとLex |
| 6/24 | 第七回 | アナリティクス(Redshift, Athena) |
| 7/29 | 第八回 | RDS (Aurora) |
| 8/26 | 第九回 | コンテナ、ちょっとML |
| 9/30 | 第十回 | セキュリティ |
| 10/28 | 第十一回 | 運用、ちょっとComprehend |
| 11/25 | 第十二回 | サーバレス |
| 12月 | 第十三回 | re:Invent 2021アップデートでライブデモ祭り (8連発) |
