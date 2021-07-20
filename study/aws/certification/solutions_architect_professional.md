# AWS Solutions Architect Professional

## 参考図書

- [AWS認定ソリューションアーキテクト-プロフェッショナル ~試験特性から導き出した演習問題と詳細解説](https://www.amazon.co.jp/AWS%E8%AA%8D%E5%AE%9A%E3%82%BD%E3%83%AA%E3%83%A5%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%A2%E3%83%BC%E3%82%AD%E3%83%86%E3%82%AF%E3%83%88-%E3%83%97%E3%83%AD%E3%83%95%E3%82%A7%E3%83%83%E3%82%B7%E3%83%A7%E3%83%8A%E3%83%AB-%E8%A9%A6%E9%A8%93%E7%89%B9%E6%80%A7%E3%81%8B%E3%82%89%E5%B0%8E%E3%81%8D%E5%87%BA%E3%81%97%E3%81%9F%E6%BC%94%E7%BF%92%E5%95%8F%E9%A1%8C%E3%81%A8%E8%A9%B3%E7%B4%B0%E8%A7%A3%E8%AA%AC-%E5%B9%B3%E5%B1%B1-%E6%AF%85/dp/4865942483/ref=pd_lpo_14_img_0/358-3609452-5128715?_encoding=UTF8&pd_rd_i=4865942483&pd_rd_r=4c19afd8-df72-47d4-a610-63dab33ecc6b&pd_rd_w=ZqhEB&pd_rd_wg=SWw4E&pf_rd_p=cc043046-48af-4a56-a049-b4a889070edc&pf_rd_r=72JGPHYW2AA2QC13PM75&psc=1&refRID=72JGPHYW2AA2QC13PM75)

<br>

## IAM

P.84 IAMロールの信頼ポリシーで設定する外部ID（sts:ExternalId）
- 他カウントへAssumeRoleを許可する為のIAMロールの信頼関係へ条件を追加する
- 外部IDは文字列マッチで評価する
- [参考URL](https://dev.classmethod.jp/articles/iam-role-externalid/)

P.186 特定IAMユーザへBilling and Cost Management画面の閲覧を許可するIAMポリシー
- ```"Action": "aws-portal: ViewBilling"``` Billing and Cost Managementコンソール画面の表示を許可/拒否
- ```"Action": "aws-portal: ViewUsage"``` 使用状況レポート画面の表示を許可/拒否
- その他にも沢山ある：[参考URL](https://docs.aws.amazon.com/ja_jp/awsaccountbilling/latest/aboutv2/billing-permissions-ref.html)

P.226 タグベースのIAM制限ポリシー
- タグベースでIAMポリシーを発動できる
- ```PrincipalTag```: IAMユーザに付与したタグベースで制限
- ```ResourceTag```: 特定タグが付与されたリソースのみ操作可能な制限
- ```RequestTag```: 特定リソースへの特定タグの付与を強制
- ```TagKeys```: よくわからん
- [参考URL](https://aws.amazon.com/jp/premiumsupport/knowledge-center/iam-tag-based-restriction-policies/)

<br>

## リソースベースポリシー

P.92 リソースポリシーで他アカウントからのアクセスを制御する
- IAMベースとリソースベースは異なる（[参考](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)）
- S3、SNS、SQS、KMSなどがサポートしてる
- 他アカウントのIAMユーザへアサインされたIAMロール/ポリシーを気にする必要がない
- [参考URL](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/access-policy-language-overview.html)

<br>

## VPC

P.95 インターリージョンVPCピアリング
- 異なるリージョン間でのVPCピアリングが可能（バージニア↔オレゴン↔東京）
- VPCピアリングは単一リージョン間のみサポート（東京↔東京）
- [参考URL: ちょっと古い（現在、東京リージョンはサポート済み）](https://dev.classmethod.jp/articles/inter-regrion-vpc-peering/)

P.206 VGWルートプロパゲーション
- VPC内の経路情報を外部のルートテーブルへ伝播させる
- ネット上の情報ではTGWとの連携ばかりだがP2P間での接続でも必要？オンプレ側のルータへ手動で入れるかプロパゲーションで取得するかってこと？
- [参考URL](https://dev.classmethod.jp/articles/transit-gateway-vpc/#toc-9)

<br>

## AWS Config

P.102 AWS Configで出来ること
- AWSリソースの構成情報を評価、監査するサービス
- 設定変更の記録（SGの追加/変更）やSNSでの通知が出来る
- CloudTrailとの住み分け
    - AWS Configはリソースの設定や変更に対する履歴を取得
    - AWS CloudTrailはAWSユーザ/呼出元IPの操作記録にフォーカスした監査サービス
- [参考URL](https://dev.classmethod.jp/articles/aws-config-start/)

<br>

## AWS Shield

P. 115 AWS Shieldとは？
- DDoS攻撃から保護するサービス
- スタンダードは標準で有効: L3/L4を標的とするDDoS攻撃から保護（無料）
- アドバンストはオプション: L7まで検出対象で24/365の専門サポート有（有料）
- [参考URL](https://www.wafcharm.com/blog/aws-shield-for-beginners/)

<br>

## Rotue53

P. 119 Evaluate Target Healthとは？
- 様々なルーティングポリシーとセットで利用
- ALBのようなヘルスチェックを別途定義してルーティングポリシーへアサインする
- ヘルスチェックはあくまでもオプション

P. 232 レイテンシーベースルーティング
- ユーザとレコードに紐づいているリージョンとのレイテンシーを過去の統計情報から計算
- 最もレイテンシーが低いリージョンのエンドポイントに名前解決する

<br>

## Disaster Recovery

P.123 4つのDR戦略
| 構成 | コスト | RTO (目標復旧時間) | RPO (目標復旧時点) | 詳細 |
| -- | :--: | :--: | -- | -- |
| バックアップ＆リストア | 低 | 長 | 最終バックアップタイミング | バックアップをS3へ保存しDRサイトへレプリケーション<br>DR時はS3のバックアップから復旧 |
| パイロットライト | ↑ | ↑ | 最終データ同期タイミング | 低スペックのDBをDRサイトでスタンバイ起動し常時レプリケーション<br>DR時はAPを起動しDBをスケールアップ |
| ウォームスタンバイ | ↓ | ↓ | 最終データ同期タイミング | 低スペックのAP/DBをDRサイトで常時起動<br>DR時はAP/DBをスケールアップしDNS参照先を変更 |
| ホットスタンバイ<br>マルチサイト | 高 | 短 | 最終データタイミング | 同スペックのAP/DBをDRサイトで常時起動<br>DR時はDNS参照先を変更 |

<br>

## Storage Gateway

P.125 Storage Gatewayとは？
- オンプレ側に「VM/Hyper-V/KVM」or「[HWアプライアンス](https://aws.amazon.com/jp/storagegateway/hardware-appliance/)」を用意して裏側でAWSストレージサービスを利用

    ![image](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2020/05/04/Figure-2-High-level-architecture-of-storage-gateway.png)

- 大きく3つ、詳細には4つの種別がある

    | 種別 | 接続 | 内容 |
    | -- | :--: | -- |
    | ファイルゲートウェイ | NFS/SMB | S3へデータを保存 |
    | ボリュームゲートウェイ<br>GatewayStored Volumes | iSCSI | オンプレ側へデータを保存し非同期でS3へデータをバックアップ<br>S3→Backup→EBS→EC2マウント何てことも可能 |
    | ボリュームゲートウェイ<br>GatewayCached Volumes | iSCSI | オンプレ側にはキャッシュのみ保存<br>データ全体はS3へ保存 |
    | テープゲートウェイ | VTL | S3へデータを保存（Glacier/Clacie rDeep Archiveと連動） |

<br>

