# AWS Solutions Architect Professional

## 参考図書

- [AWS認定ソリューションアーキテクト-プロフェッショナル ~試験特性から導き出した演習問題と詳細解説](https://www.amazon.co.jp/AWS%E8%AA%8D%E5%AE%9A%E3%82%BD%E3%83%AA%E3%83%A5%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%A2%E3%83%BC%E3%82%AD%E3%83%86%E3%82%AF%E3%83%88-%E3%83%97%E3%83%AD%E3%83%95%E3%82%A7%E3%83%83%E3%82%B7%E3%83%A7%E3%83%8A%E3%83%AB-%E8%A9%A6%E9%A8%93%E7%89%B9%E6%80%A7%E3%81%8B%E3%82%89%E5%B0%8E%E3%81%8D%E5%87%BA%E3%81%97%E3%81%9F%E6%BC%94%E7%BF%92%E5%95%8F%E9%A1%8C%E3%81%A8%E8%A9%B3%E7%B4%B0%E8%A7%A3%E8%AA%AC-%E5%B9%B3%E5%B1%B1-%E6%AF%85/dp/4865942483/ref=pd_lpo_14_img_0/358-3609452-5128715?_encoding=UTF8&pd_rd_i=4865942483&pd_rd_r=4c19afd8-df72-47d4-a610-63dab33ecc6b&pd_rd_w=ZqhEB&pd_rd_wg=SWw4E&pf_rd_p=cc043046-48af-4a56-a049-b4a889070edc&pf_rd_r=72JGPHYW2AA2QC13PM75&psc=1&refRID=72JGPHYW2AA2QC13PM75)

<br>

## AWS Budgets

P.188 請求アラート
- 全体 or 特定AWSリソースに対するバジェットを設定し閾値＆アラーム通知を設けることができる
- アカウント設定から「請求アラートを受け取る」を有効化し、CloudWatchでアラームを設定可能

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

## Cloud Front

P.213 オリジンフェイルオーバーの動作仕様
- Primary Originのレスポンスによって透過的にSecondary Originへリルーティングする
- [参考URL](https://dev.classmethod.jp/articles/cloudfront-origin-failover/)

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

## DynamoDB

P.128 クライアントアプリから直接DynamoDBを更新する？
- あまり実例が無さそう
- AmplifyなどでAppSync経由で書込むデザインパターンはあるっぽい

    ![image2](https://d1.awsstatic.com/Developer%20Marketing/jp/magazine/2021/img_amplify-lib-existing-appsync_01.fdeb4589a59e3c0599ff254b9f5a38a39cc19307.png)

<br>

## Elastic Beanstalk

P.148 Elastic Beanstalkとは？
- VPC/EC2/ALBなどのベタなインフラ構成はEBが勝手に作る
- Runtime環境を選ぶと環境毎の実行パスへアップロードしたZipファイルを展開（PHPならApacheドキュメントルート）
- php.iniなどの設定ファイルは何かしらの方法を使って設定できるっぽい
- SSHも可能らしい
- [一連の作業の参考URL](https://dev.classmethod.jp/articles/cm-advent-calendar-2015-aws-re-entering-elasticbeanstalk/)

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

## OpsWorks

P.163 OpsWorksとは？
- 予め用意したChef/Puppetのレシピ（GitHubなどのリポジトリ上）を使ってEC2上でレシピを実行してくれる
- EC2の作成/構成管理などはOpsWorks上で実施することで、IAMユーザと連動してSSH/sudo実行管理が可能
- NW/マネージドサービス領域はCloudFormation、EC2/ELB/RDSはOpsWorksって分け方か？
- [参考①](https://techblog.zozo.com/entry/cloudformation-and-opsworks)、[参考②](https://dev.classmethod.jp/articles/use-rds-layer-on-opsworks/)

    ![image4](https://cdn-ak.f.st-hatena.com/images/fotolife/v/vasilyjp/20170831/20170831223939.png)

P.236 Stack/Layer/Recipeの関係性
- Stack: OpsWorksを管理する一番大きな論理的グループ
- Layer: 役割単位で管理する論理的グループでChef/Puppetのデプロイ単位
- Recipe: デプロイのトリガーとなるイベントで5つの中から選択できる

    | イベント | 実行タイミング |
    | -- | -- |
    | Setup | インスタンス初回起動時 |
    | Configure | スタックの状態が変化したタイミング |
    | Deploy | アプリケーションがデプロイされるタイミング |
    | Undeploy | アプリケーションが削除されたタイミング |
    | Shutdown | インスタンスが停止する45秒前 |

- イメージ
    ![image5](https://cdn-ak.f.st-hatena.com/images/fotolife/v/vasilyjp/20170831/20170831224115.png)

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

## Redshift

P.127 RedshiftのDRについて
- RedshiftはAZを超えてクラスタ構成が組める
- リージョンを跨いでDR構成としたい場合はマルチリージョンなS3へ増分スナップショットを作成可能
- 増分スナップショットは「8時間 or 5GB」毎に自動的に作成
- [参考①](https://aws.amazon.com/jp/about-aws/whats-new/2019/10/amazon-redshift-improves-performance-of-inter-region-snapshot-transfers/)、[参考②](https://d1.awsstatic.com/webinars/jp/pdf/services/20210127_AWS_BlackBelt_RedshiftOperation.pdf)

<br>

## RDS

P.153 オンプレ環境からAurora MySQLへのレプリケーションについて
- Aurora MySQLバージョン 5.6以降から可能
- SSL通信が行えるよう各種証明書の準備が必要
- バイナリログの転送設定などは通常のMySQLと同じ
- 同期方向は異なるがこんなイメージか

    ![image3](https://cdn-ak.f.st-hatena.com/images/fotolife/t/tommy_39/20190805/20190805131146.jpg)

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

## System Manager

P.209 Patch Manager
- System Manager内のノード管理からパッチマネージャーを利用可能
- SSMログインが可能となったインスタンス（マネージドインスタンス）を対象とする
- パッチマネージャ上のベースラインで定義したルールに従ってRPM(ex Linux)をリモートからアップデート可能
- パッチ適応はスケジューリング可能
- パッチリリースからN日以内の適応が指定可能
- 定義可能なルール
    - 重要度: Critical, Important, Medium, Low
    - 分類: Security, Bugfix, Enhancement, Recommended, Newpackage

P.230 Parameter Store
- パスワードのような定数を保存しておく
- KMSを使って暗号化も出来る
- こんな感じで取得できる
    ```python
    import boto3

    ssm = boto3.client('ssm')

    def get_notify_url() -> str:
        # {NotifyTrainDelayToSlack-WebhookURL} は登録したパラメータ名
        response = ssm.get_parameter(
            Name='NotifyTrainDelayToSlack-WebhookURL',
            WithDecryption=True
        )
        return response['Parameter']['Value']
    ```
- [参考URL](https://dev.classmethod.jp/articles/secure-string-with-lambda-using-parameter-store/)

<br>

## VPC

P.95 インターリージョンVPCピアリング
- 異なるリージョン間でのVPCピアリングが可能（バージニア ↔ オレゴン ↔ 東京）
- VPCピアリングは単一リージョン間のみサポート（東京 ↔ 東京）
- [参考URL: ちょっと古い（現在、東京リージョンはサポート済み）](https://dev.classmethod.jp/articles/inter-regrion-vpc-peering/)

P.206 VGWルートプロパゲーション
- VPC内の経路情報を外部のルートテーブルへ伝播させる
- ネット上の情報ではTGWとの連携ばかりだがP2P間での接続でも必要？オンプレ側のルータへ手動で入れるかプロパゲーションで取得するかってこと？
- [参考URL](https://dev.classmethod.jp/articles/transit-gateway-vpc/#toc-9)

<br>

## リソースベースポリシー

P.92 リソースポリシーで他アカウントからのアクセスを制御する
- IAMベースとリソースベースは異なる（[参考](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)）
- S3、SNS、SQS、KMSなどがサポートしてる
- 他アカウントのIAMユーザへアサインされたIAMロール/ポリシーを気にする必要がない
- [参考URL](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/access-policy-language-overview.html)

<br>

## 移行戦略

P.169 「6つのR」とは？
- 全体イメージ
    ![image6](https://cdn-ssl-devio-img.classmethod.jp/wp-content/uploads/2019/08/six-rs-whiteboard.174ea49a238eaa705fc4fb563ec0eafcaf1a7d76.png)
- AWSへの移行を検討する上での戦略ツール
    | 戦略 | 英名 | 内容 |
    | -- | -- | -- |
    | リホスト | Rehost | サーバごとまるっと移行する。VM形式の仮想イメージで移す感じだと楽 |
    | リプラットフォーム | Replatform | クラウド環境に合わせてプラットフォームを最適化しつつ移行<br>アプリケーションのコアアーキテクチャは変更しないものの、クラウドのメリットを享受するため一部のシステムをマネージドサービスへ移行 |
    | 再購入 | Repurchase | 別製品、サービス、SaaSへ置き換える |
    | リファクタリング | Refactor | プログラム及び全体のアーキテクチャを改善 |
    | 保持 | Retain | 現状維持 |
    | 廃止 | Retire | 稼働中のシステムを停止もしくは廃止する |

<br>

## ★SQS

P.216 ベント再生用パイプライン

<br>

## ★S3

P.177 S3のストレージクラス
- マトリックス
    | クラス | 可用性 | 耐久性 | AZ | コスト | 内容 |
    | -- | -- | -- | -- | -- | -- |
    | Standard | 99.99% | 99.999999999% | 3AZ以上 |  | デフォルトのストレージクラス |
    | Standard-IA | 99.9% | 99.999999999% | 3AZ以上 |  | データの読み出し容量に対して課金される |
    | Intelligent-Tiering | 99.9% | 99.999999999% | 3AZ以上 |  | 長時間アクセスの無いオブジェクトをStandard-IAへ退避する |
    | One Zone-IA | 99.5% | 99.999999999% | 1AZ |  |  |
    | Glacier | 99.99% | 99.999999999% | 3AZ以上 |  |  |
    | Glacier Deep Archive | 99.99% | 99.999999999% | 3AZ以上 |  |  |
    | 低冗長化ストレージ(RRS) |  | 99.99% |  |  |  |

P.193 S3マルチパートアップロードAPI