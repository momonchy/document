# RE:GROWTH - AWS re:Ivent ふりかえり勉強会

日時: 2022.12.6 19:00 - 21:00
場所: Youtube Live

<br>

## Amazon Verified Permissions

- 「YouTube SEC335」で検索すればヒットする
- アプリケーションへの権限管理機能を提供する（IAMとはあまり関係ない）
- RBAC: ロールベース
- ABAC: 属性ベース（タグ、プリンシパル）
- PBAC: Policy based access control
    - Cedarという独自言語でポリシーを定義
    - Lambda等でVerified Permissionsへアクセス
    - アプリケーション経由でユーザができること、できないことを制御可能
    - Webアプリ上で実装するロール設定みないなもの？？

<br>

## DeveloperIO BASECAMPのアップデート

- Amazon S3 Access Points のクロスリージョン化
- OpenSearch のサーバレス化
    - AWS PrivateLink との連携も可能

<br>

## Analyticsアップデートまとめ

- Amazon DataZone
    - マネコンからデータカタログにメタデータを追加
    - 3rd party系との連携も可能
    - [類似OSS](https://dev.classmethod.jp/articles/introduction-of-open-metadata/)