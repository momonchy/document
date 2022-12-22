# 第25回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」
AWS re: Invent 2022 Live デモ祭り

日付：2022/12/22
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## CodeCatalyst (Preview)

- 統合ソフトウェア開発サービス
- プロジェクトセットアップを加速
  - Blueprintで何パターンかが用意されている
  - スピーディーにプロジェクトを立ち上げられる
- 日々のワークフローを自動化
  - CDをビジュアル化
  - 簡単にPipelineを構築可能
- 自動化された開発環境
  - ブラウザ上で VSCode などが使える
- CodeCatalystは別アカウント（QuickSight系）
  - デプロイ先はAWS
- チームメイトをメールでインバイト
  - Issueの追跡など
  - GitHubみたいなもの
- GitHub 上に Online IDE が追加された感じ
- git push すると自動で CD が走る
- Slack へ通知する設定も簡単に行える

<br>

## Application Composer (Preview)

- GUI でサーバレスアプリケーションを構築して IaC コードを生成する
- 新規作成だけでなく既存の CFn と SAM テンプレートも編集可能
- ビジュアルアーキテクチャーをそのまま CFn でデプロイ可能
- Connected を選択するとローカルのテンプレートコードがリアルタイムで更新される
  - VS Code の拡張プラグイン AWS Toolkit で連携する
  - Lambda等のコードは事前に良いしておいて template.yml は Composer で作るって流れ

<br>

## AWS Verified Access (Preview)

- AWS ゼロトラストの基本原則に基づいて構築
- VPN を使わない安全なアクセスを実現
- 外部向けの Endpoint を作ってくれる
- OIDC/IAM, Policy で認証

<br>

## Quick Sight API

- Assets as Code
- API の操作範囲が拡張
  - Asset の削除が可能
  - ユーザの追加/削除が可能
- ビジュアル定義を Json で出力可能
  - API でインポートすればダッシュボードの複製が簡単

<br>

## RDS　Blue/Green Deployments

- 現行のDBからレプリケートされたステージング環境をClone
- ステージング環境で作業（レプリケーションが継続されている）
- エンドポイントを変更せずに切り替え（スイッチオーバーガードレール）
- MySQL系のみ対応
- ゼロタイムダウンというのは無理
  - わざと更新のロックとセッションのクリアを行なっている

<br>

## EventBridge Pipes

- イベントドリブンアーキテクチャ
  - プロデューサー（クライアントリクエストを受けるやつ）とコンシューマー（裏側で処理するやつ）
  - コンシューマーが増えると破綻する（密結合状態）
  - イベントドリブンアーキテクチャでは、プロデューサーとコンシューマーの間にイベントバスを投入する（疎結合）
- EventBridge Pipes とは
  - イベントバス不要でソースとターゲットをシームレスに接続する
  - フィルタリング、変換機能も備える
  - DynamoDB、MSK、Kinesis もプロデューサーとして使える
- マネコン上でグラフィカルにパイプラインを構築できるので分かり易くてイイ！
