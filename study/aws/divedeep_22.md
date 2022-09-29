# 第22回「アップデート紹介とちょっぴりDiveDeepするAWSの時間」

日付：2022/09/29
Twitter ハッシュタグ: #ちょっぴりDD

<br>

## キーワード

- オプトイン：ユーザーに宣伝広告を配信する際、事前に許可を求めること。

<br>

## 今月のお勧め5分間アップデート

- AWS Fargateでコンピューティングとメモリのリソース構成が4倍に増加
- Amazon Cognitoが、ホストされたUIにおける時間ベースのワンタイムパスワード（TOTP）のセルフ登録に対応
  - 事前に準備されたUI（Hosted UI）でMFAができるようにになった

<br>

## Amazon GuardDuty で Malware Protection

- GuardDutyとは
  - マネージド型の脅威検出サービス
  - とりあえず有効化しておいて問題無いサービス
  - 検出するだけ（通知方法との連携はユーザが行う）
  - IDS/IPSなどで検出が難しいAWSのアカウントやS3バケットの侵害も検出
- Malware Protectionの仕組み
  - GuardDutyがマルウェアっぽい挙動を検出したらEBSスナップショットを自動で実施してスキャン（サービスパフォーマンスへ影響しない設計）
  - エージェントレスだよ
  - マルウェアのダウンロードをリアルタイムで遮断するわけでは無い
- AWS Organizationsを採用している場合にはrootアカウントで実行するだけでよい？

<br>

## セキュリティーリスクを見える化して脅威に強い環境を構築するための 1st ステップをご紹介

- AWS Configとは
  - 構成情報の記録、評価を行うマネージドサービス
  - 構成情報のスナップショットを記録する
  - AWSリソースの構成変更（EC2リソース追加、SGの変更）を検知
  - AWS Config Rules
    - 変更のあった構成情報を評価ができる
    - 問題があった場合にSNS連携等で通知
    - AWS Config Rulesによりポリシー準拠評価のしくみ
      - 例：EC2インスタンスにNameタグが設定されているか
      - 例：EBSが暗号されているか
  - AWS Config適合パック
    - 複数のConfig Ruleをまとめてパッケージ化
    - AWS Organizationsで組織全体に一括適用可能
- AWS Security Hubとは
  - 組織内のセキュリティデータを集約して一元的な可視化を行うマネージドサービス
  - AWS Config、GuardDutyなどのセキュリティインシデントを集約
  - Security Hubセキュリティ基準
  - AWS Organizaitons配下へ統合的に適応可能

<br>

## AWS Lambda にも来ました。属性ベースのアクセス制御 (ABAC) サポート

- RBAC
  - Role-based access control
  - ロールベースでアクセスをコントロール
  - よく利用するやつ
  - デメリットとしてロールが増えすぎて辛い
- ABAC
  - Attribute-base access control
  - 属性によって権限を分けられる
  - ここでいう属性とは？
    - タグを利用する
  - プリンシパルタグ（リクエスト元）とリソースタグ（Lambda等に付けたタグ）のValueが一致した場合のみアクセス許可するなど

<br>

## 今日から始められる AWS Network Firewall の Managed Threat Signature のご紹介

- AWS Network Firewallの場合、L3〜L7まで制御可能（ステートフルもいけるよ）
- VPCの中にも設置可能