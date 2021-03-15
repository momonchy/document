# AWSアカウント管理のベストプラクティス

## AWSアカウントを分割するメリット

- PCIDSSへの準拠（[セグメンテーション](https://dev.classmethod.jp/articles/pci-dss-compliance-on-aws/)）
- Webコンソールの分離
- AWSアカウント間においてセキュリティ対策を分離
- 課金管理などからサービスプロバイダー型のサービス提供がし易い

## デメリットへの対策

- IAMのクロスアカウントアクセス（Switch Role）
- 一括請求（Consolidated Billing）

## AWS Organizations とは

- AD/LDAPでAWSアカウントを管理するイメージ
    ```mermaid
    graph TD
        A[root] --> B[OU]
        A --> C[OU]
        B --> D[OU]
        B --> BB([AWS Account])
        D --> DD([AWS Account])
        D --> DDD([AWS Account])
        C --> CC([AWS Account])
    ```
- root、OU、AWS Account それぞれにポリシー（SCP）を割り当てられる
    - OU間、アカウント間でAWSAPIリソースへのアクセス制御（ホワイトリスト、ブラックリスト）
    - 明示的なAllowよりも明示的なDENYが優先される
    - SCPとIAMポリシー両方で許可されたAWSAPIが最終的に利用可能

## AWS推奨構成

- 支払アカウント
- 基盤管理アカウント
- 各種LOBアカウント

## 参考
- [AWSにおけるマルチアカウント管理の
手法とベストプラクティス](https://d0.awsstatic.com/events/jp/2017/summit/slide/D4T2-2.pdf)