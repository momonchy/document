# Amazon SageMaker JumpStart ワークショップ（機械学習基盤を簡単に構築する）

日付：2021/03/09

## ハンズオンシナリオ
[GitHubリポジトリ](https://github.com/harunobukameda/Amazon-SageMaker-JumpStart)

<br>

## 機械学習運用のワークフロー

1. データ取得
2. データ前処理
3. モデルの開発
4. モデルの学習
5. モデルの評価
6. 本番環境へのデプロイ
7. 監視・評価データ収集

<br>

## SageMakerの構成
コンテナで起動する

- Jupyter notebook
- 学習インスタンス → 学習データはS3から取得
- 推論インスタンス → 学習が終わった環境はECRへ保存される

Managed Spot Trainingを利用することで学習コストを最大で90%削減

<br>

## ハイパーパラメーター最適化（HPO）

汎用的に最適化されたパラメーターを利用してくれる

<br>

## Amazon SageMaker Studio

- Jupyter Notebookを拡張して作られた統合開発環境
- サーバレスノートブックで共同開発が容易

<br>

## SageMaker Jump Start

- 15＋のシーン150＋のモデルを提供（自動運転、リスク予測、需要予測。。。）
- 転移学習でモデルを追加学習可能

