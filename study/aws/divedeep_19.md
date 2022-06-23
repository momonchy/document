# 第19回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2022/06/23
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## 今月のお勧め5分間アップデート

- Aurora PostgreSQL がダウンタイムなしのパッチ適用に対応
- AWS Security Hub が AWS Confing のマネージド/カスタムルールの評価結果を受け取れるようになった
  - Security Hub で一元的にインシデントを閲覧可能
- Route53 が DNS クエリの IP ベースのルーティングに対応（★要確認）
- Amazon Personalize へ 6言語追加
- Amazon EMR Serverless が一般公開へ

<br>

## イチから覚える AWS Schema Conversion Tool 

Schema Conversion Toolとは？
- オンプレDB→フルマネDBへマイグレーションする為のAWSツール
  - 評価レポートの作成
    - 移行可能割合をレポート
  - スキーマの移行
  - アプリケーションソースコードの評価/移行
    - アプリケーションのソースに埋まっているSQLも変換可能
- 対応OS
  - Fedora Linux, MS Windows, Ubuntu
  - 無料でダウンロードして利用可能

基本的な使い方
- 専用ビューがある
- 移行元と移行先のテーブル情報を見ながら
- エクスポートされた評価レポートから、CSVで変換エラーの一覧が閲覧可能

Tips
- マルチサーバ評価
  - N → 1
  - 1 → N（複数のフルマネDBから選択）
- 移行工数を算出可能

<br>

## Purpose-built Database つかってみませんか？

Purpose-built Database とは何か？
- ワークロードに応じて適材適所なDBを選択する
- Amazon.comは元々Oracleを使ってた
  - 特定のワークロードに最適化するために様々なAWSサービスDBへ移行
