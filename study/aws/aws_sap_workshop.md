# AWS認定試験ワークショップ - Solution Architect Professional

## 要確認/気付いた点

- CloudFrontの署名付きURLとは？
- Amazon Inspectorの正しいサービス理解
- CloudTrailはログファイル出力時にファイル自体のハッシュ値を署名し整合性を担保できる
- ネットワークACLはステートレスであるためアウトバウンド/インバウンドの両設定が必要

<br>

## 組織の複雑性に対応する設計

[資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20211029_ERW_SAP_Session1-1.pdf)

主題領域
- クロスアカウント認証とアクセス戦略
- ネットワーク（ハイブリット構成）
- マルチアカウントのAWS環境

ユーザーフェデレーション
- 外部のユーザアイデンティティにAWSリソースを仕様する権限を付与（SAML2.0, OpenID）
- 長期のセキュリティ情報を配布しないためセキュリティが向上する
    - AWS Managed Microsoft AD
    - AD Connector（オンプレのADと繋げるためのProxy的サービス）
    - Simple AD

一時的なアクセスの委任
- 複数AWSアカウント間で簡易に権限を委譲する（クロスアカウントアクセス）
    - Switch Role
    - Security Token Service(STS)

リソースと請求の分離
- １つのAWSアカウントで複数VPC環境を管理
- 複数のAWSアカウントで環境を管理

複数アカウントの請求戦略
- グループエイリアスに通知を送信（ML）
- アカウント全体でAWSタグ付け標準を仕様
- AWS APIおよびスクリプトで会社のベースラインの設定を自動化

AWS Organizations
- 複数のAWSアカウントをポリシーベースで一元管理（SCP）
    - 上位組織（OU）へアタッチしたポリシーを下位組織が継承する
- APIを仕様して新しいアカウントの作成を自動化
- 一括請求（コンソリデーティッドビリング）

<br>

## 新しいソリューションの設計

[資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20211029_ERW_SAP_Session2-1.pdf)

よく出てくる構成
- CloudFront + ALB + EC2
- Route53 + EC2
- CloudFront + S3 & EC2 + EBS
    - 署名付きURL（期限付きURLでアクセスを制限しててもアクセスできる）
    - オリジンアクセスアイデンティティ（OAI）

<br>

## 既存のソリューションの継続的な改善

[資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20211029_ERW_SAP_Session3-1.pdf)

AWSでのトラブルシューティング
- S3
    - バケットアクセスの問題やデータ
    - リクエストのトラブルシューティング
- ELB
    - トラフィックのパターン分析
    - ネットワーク問題のトラブルシューティング
- CloudTrail
    - 誰が、何を、いつ、どこから行ったのかを監査及び特定
- VPCフローログ
    - L3ログのチェック
- CloudWatch Logs
    - モニタリング及びトラブルシューティング
- AWS Config
    - リソースの設定変更イベントの検知
    - 機能停止、セキュリティ攻撃分析の実行

<br>

## コスト管理

[資料](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20211029_ERW_SAP_Session4-1.pdf)

コストの最適化
- 「必要と推測した分の支払い」に「実際に必要な分の支払い」へ近づいていく

計画を立てる
- 何を測定するか
- 誰/何が測定できるか？
- 誰/何が測定を参照できるか？

リソースのプロビジョニングを制限する
- IAM, Policy, Roleで不要なリソースを作らせないようにする

監査可能な状況
- タグを適切に運用する
- 何に使われていて必要かどうかを判断