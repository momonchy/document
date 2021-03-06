# AWSアカウント管理のベストプラクティス

## AWSアカウントを分割するメリット

- PCIDSSへの準拠（[セグメンテーション](https://dev.classmethod.jp/articles/pci-dss-compliance-on-aws/)）
- Webコンソールの分離
- AWSアカウント間においてセキュリティ対策を分離
- 課金管理などからサービスプロバイダー型のサービス提供がし易い

<br>

## デメリットへの対策

- IAMのクロスアカウントアクセス（Switch Role）
- 一括請求（Consolidated Billing）

<br>

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
- 一括請求（Consolidated Billing）でアカウント毎の請求をまとめられる
- CloudTrail、AWS Configなどのセキュリティログを集中管理（Organizationsの機能なの？）

<br>

## 考察

- 一括請求用のAWSアカウントをOrganizationsのrootアカウントとする
- Switch Role用のAWSアカウントを決める（IAMユーザの集中管理）
    - スイッチ先に適切なロールを作成（EC2のみ利用可など）
    - スイッチ元にスイッチ先AWSアカウント数分のAssume Role許可ポリシーを作成
        - 適宜IAMユーザへアサイン

<br>

## 参考
- [AWSにおけるマルチアカウント管理の手法とベストプラクティス](https://d0.awsstatic.com/events/jp/2017/summit/slide/D4T2-2.pdf)