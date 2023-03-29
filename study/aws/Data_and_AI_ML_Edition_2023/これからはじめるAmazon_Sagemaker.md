# これからはじめる Amazon SageMaker - フェーズ別、役割別の機能紹介

日付：2023/02/22
資料：[登壇資料_T2-1_これからはじめる_Amazon_SageMaker_〜フェーズ別、役割別の機能紹介〜.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/Data_and_AI_ML_Edition_2023/%E7%99%BB%E5%A3%87%E8%B3%87%E6%96%99_T2-1_%E3%81%93%E3%82%8C%E3%81%8B%E3%82%89%E3%81%AF%E3%81%97%E3%82%99%E3%82%81%E3%82%8B_Amazon_SageMaker_%E3%80%9C%E3%83%95%E3%82%A7%E3%83%BC%E3%82%B9%E3%82%99%E5%88%A5%E3%80%81%E5%BD%B9%E5%89%B2%E5%88%A5%E3%81%AE%E6%A9%9F%E8%83%BD%E7%B4%B9%E4%BB%8B%E3%80%9C.pdf)

<br>

## SageMaker のどの機能を使えばよいか？

- SageMaker は様々な機能がある（公式ドキュメント3000ページ分）

<br>

## 機械学習プロジェクトのフェーズと役割

- 企画フェーズ
  - ビジネス担当者、IT/DX担当者
- 研究開発フェーズ（PoC）
  - データエンジニア、データサイエンティスト、システムエンジニア
- 運用フェーズ
  - MLエンジニア、システムエンジニア

<br>

## 研究開発フェーズについて

データ収集 → 前処理 → 特徴量エンジニアリング → 学習・チューニング・評価
- SageMaker Studio 統合開発環境が使いやすい
- Jupyter Notebook が利用可能
  - Notebook Job を使えばそのままバッチ実行できる
- SageMaker Training Job
  - 学習データ、実行環境、ソースコードを読み込んで学習する
  - CodeBuildみたいな感じ
- SageMaker Processing Job
  - データの前処理を行う
  - Training Job と同じ考え方
- SageMaker Experiments
  - 複数の機械学習を統合管理
- Processing（前処理）→ Training（学習）→ Processing（評価）といった連携

<br>

## 運用フェーズ

デプロイ
- SageMaker Endpoint
  - モデルのエンドポイントを提供

モニタリング
- SageMaker Model Monitor
  - 入力データやモデルの推論結果の異常を検知してアラートを上げる

<br>

## MLOps

色々な自動化を目指す
- SageMaker Pipeline
- SageMaker ??
