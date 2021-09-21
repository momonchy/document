# 模擬試験メモ

受験日：2021/07/26

<br>

### 01問

>あるソリューションアーキテクトが、気象予測アプリケーションを設計しています。毎時間、アプリケーションは測候所から一連の生データを受信します。アプリケーションはこのデータを分析して、ユーザーがダウンロードできる現地気象予測を生成します。
この分析は2000 vCPU のクラスターで実行すると通常 50 分ほどかかります。この分析は次のデータセットが入ってくるまでに完了する必要があります。
各現地気象予測のサイズは通常 10 GB です。予測データにアクセスが集中するのは利用可能になってから最初の 1 時間であり、その後より新しい気象予測データが使用可能になるにつれて急速に使用量が減少します。

次のステップの組み合わせのうち、最もコスト効率が優れたアーキテクチャはどれですか? (2 つ選択)

1. 複数の AWS リージョンで 1 時間のスポットブロックを使用し、Amazon EC2 ベースのクラスターで分析を実施する。
2. 単一の AWS リージョンでリザーブドインスタンスを使用し、Amazon EC2 ベースのクラスターで分析を実施する。
3. Amazon S3 Standard に気象予測データを保管する。30 日経過後に Amazon S3 Standard-Infrequent Access (S3 Standard-IA) に移行するようライフサイクルポリシーを構成する。
4. Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA) に気象予測データを保管する。90 日経過後にデータを Amazon Glacier に移行するようライフサイクルポリシーを構成する。
5. Amazon S3 Standard-Infrequent Access (S3 Standard-IA) に気象予報データを保管する。90 日経過後に データをAmazon Glacier に移行するようライフサイクルポリシーを構成する。

<br>

### 02問

>ある会社が AWS にデータベースサーバークラスタの展開を計画しています。データベースクラスタにはノード間のニアリアルタイムのレプリケーションが必要です。ビルトインクラスタテクノロジーには次の要素が必要となります。
> - ノード間の最小ネットワークレイテンシー
> - 最大のネットワークスループット

次のうち、データベースクラスタのパフォーマンス要件を満たすものはどれですか?

1. Elastic Network Adapter (ENA) を使って拡張ネットワーキングを有効にした Amazon EC2 インスタンスを起動する。すべてのインスタンスをスプレッドプレイスメントグループで起動する。
2. ジャンボフレームを有効にしたネットワーク最適化 Amazon EC2 インスタンスを起動する。同じアベイラビリティゾーンでインスタンスを起動する。
3. Elastic Network Adapter (ENA) を使って拡張ネットワーキングを有効にした Amazon EC2 インスタンスを起動する。すべてのインスタンスをクラスタプレイスメントグループで起動し、ジャンボフレームサポートを有効にする。
4. ネットワークインターフェイスが複数ある Amazon EC2 インスタンスを起動する。すべてのインスタンスをクラスタプレイスメントグループで起動し、ジャンボフレームサポートを有効にする。

<br>

### 03問

>ある動画共有モバイルアプリケーションは Amazon S3 バケットに 10 GB を超えるファイルをアップロードします。しかし、S3 バケットリージョンから遠い場所でアプリケーションを使うとアップロードに長時間かかり、完了しない場合もあります。

次の方法の組み合わせのうち、アプリケーションへのアップロードパフォーマンスを改善するものはどれですか?（2つ選択）

1. 各リージョンで S3 バケットを構成してアップロードを受信し、クロスリージョンレプリケーションを使ってファイルを配信用バケットにコピーする。
2. アップロード前にファイルにランダムなプレフィックスを付けるようアプリケーションを変更する。
3. レイテンシーベースルーティングで Amazon Route 53 をセットアップし、アップロードを一番近い S3 バケットリージョンに対して行う。
4. S3 バケットで S3 Transfer Acceleration を有効にして、アップロードに Transfer Acceleration エンドポイントを使用するようにアプリケーションを構成する。
5. アプリケーションで動画ファイルを小さい単位に分割して、マルチパートアップロードを使ってファイルを Amazon S3 に転送するよう構成する。

<br>

### 04問

>ある会社は e コマースウェブアプリケーションを運営しています。アプリケーションは ELB Application Load Balancer の背後にある Amazon EC2 インスタンスで実行されています。インスタンスは複数のアベイラビリティゾーンにわたる EC2 Auto Scaling グループで実行されています。ユーザーは、この会社のさまざまな部門からの品目を１つのリストに入れて注文することができます。それぞれの品目について、ウェブアプリケーションが関連部門に対する内部注文サービスを呼び出します。注文サービスのアーキテクチャパターンは e コマースウェブアプリケーションと同じです。注文サービスのバグにより、これらのサービスへのリクエストに定期的に障害が発生しています。これらの障害は注文全体に及ぶため、ユーザーエクスペリエンスを低下させています。

次のアーキテクチャ変更のうち、購入プロセスをより確実にするものはどれですか?

1. ウェブアプリケーションの Elastic Load Balancer の前面にある Amazon API Gateway API を作成する。スロットルリクエストがウェブアプリケーションに行くように API を構成する。サービスへの呼び出しをキャッシュするよう各注文サービスの Amazon ElastiCache をセットアップする。注文サービスを呼び出す前にキャッシュをチェックするようウェブアプリケーションを変更する。
2. ウェブアプリケーションの Auto Scaling グループの最大容量を増やす。ウェブアプリケーションの Auto Scaling グループ起動構成のインスタンスタイプのサイズを増加させる。注文サービスのロードバランサーを Network Load Balancers に切り替える。
3. 各注文サービスに Amazon SQS キューを (注文キューとして) 作成する。ウェブアプリケーションを変更して、購入の全データを適切な注文キューを送信するよう変更する。サービスを AWS Lambda 関数として書き換える。注文キューを Lambda 関数のイベントソースとして構成する。
4. Auto Scaling グループの最大容量を増やす。バースト可能パフォーマンスを持つ EC2 インスタンスに切り替えて、Auto Scaling グループ起動構成のインスタンスタイプのサイズを増加させる。注文サービスのロードバランサーを Network Load Balancers に切り替える。

<br>

### 05問

>ある会社の開発チームはそれぞれ、AWS Organizationsに独自の非プロダクション用 AWS アカウントを持っています。これらの各アカウントで、開発者はユーザーに管理およびコスト権限を付与する IAM ユーザーを開発者用 IAM グループ内に持っています。各開発チームには月間予算がありますが、超過することは日常茶飯事です。財務部門から、開発チームの予算超過問題に対処するため制約を設けるよう要請がありました。IT 部門は、新たな制約が開発者の革新する能力と試みを制約するものではあってはならないと考えています。

財務部門と IT 部門の両方の要請を満たすシナリオは次のうちどれですか?

1. マスターアカウントで、リンクされた各開発アカウントに対して AWS Budgets を使用して予算を作成する。予測された予算が月間予算の 100% に到達したら、SNS トピックにパブリッシュする。新規インフラストラクチャのローンチを拒否するポリシーを開発者 IAM グループに追加するトピックにAWS Lambda 関数をサブスクライブする。
2. マスターアカウントで、リンクされた各開発アカウントに対して AWS Budgets を使用して予算を作成する。予測された予算が月間予算の 100% に到達したら、SNS トピックにパブリッシュする。新規インフラストラクチャのローンチを拒否する新しい SCP をアカウントに作成するトピックにAWS Lambda 関数をサブスクライブする。
3. 各開発アカウントで、AWS Budgets を使用して予算を作成する。予測された予算が月間予算の 100% に到達したら、SNS トピックにパブリッシュする。新規インフラストラクチャのローンチを拒否するポリシーを開発者 IAM グループに追加するトピックにAWS Lambda 関数をサブスクライブする。
4. 各開発アカウントで、AWS Budgets を使用して予算を作成する。予測された予算が月間予算の 100% に到達したら、SNS トピックにパブリッシュする。新規インフラストラクチャのローンチを拒否する新しい SCP をアカウントに作成するトピックにAWS Lambda 関数をサブスクライブする。

<br>

### 06問

>ある会社は、機密性の高いデータをオンプレミス環境から Amazon S3 バケットに定期的に転送する必要があります。会社のセキュリティポリシーに準拠するため、データは転送中と保管中は暗号化され、パブリックのインターネットを絶対に通過しない必要があります。S3 バケットとそのコンテンツには、会社のオンプレミスネットワークと、会社の Amazon VPC からのみアクセスできる必要があります。
会社には、会社の Virtual Private Cloud (VPC) に対してプライベート仮想インターフェイスを持った AWS Direct Connect 接続があります。S3 バケットではデフォルト暗号化が有効化されています。

これらの要件を満たすために必要な追加ステップはどれですか?

1. パブリック仮想インターフェイスを追加する。S3 バケットポリシーに、セキュアな転送を使わないすべてのリクエストを拒否するステートメントを追加する。S3 バケットポリシーに、会社の IP アドレス範囲からのみトラフィックを許可するステートメントを追加する。
2. Direct Connect 接続上に VPN 接続を確立する。S3 VPC エンドポイントを作成する。非 VPC トラフィックへのアクセスを拒否し、セキュアな転送を義務付けるよう S3 バケットポリシーを構成する。負荷分散された Amazon EC2 インスタンスを使って、トラフィックをオンプレミスから S3 VPC エンドポイントにプロキシする。
3. S3 VPC エンドポイントを作成する。非 VPC トラフィックへのアクセスを拒否し、セキュアな転送を義務付けるよう S3 バケットポリシーを構成する。負荷分散された Amazon EC2 インスタンスを使って、トラフィックをオンプレミスから S3 VPC エンドポイントにプロキシする。
4. パブリック仮想インターフェイスを追加する。Direct Connect 接続上に VPN 接続を確立する。S3 VPC エンドポイントを作成する。非 VPC トラフィックへのアクセスを拒否し、セキュアな転送を義務付けるよう S3 バケットポリシーを構成する。

<br>

### 07問

>ウェブアプリケーションがELB Application Load Balancer の背後にある Amazon EC2 インスタンスで実行されます。インスタンスは 2 つのアベイラビリティゾーンにまたがる Amazon EC2 Auto Scaling グループで実行されます。ロードバランサーはパブリックサブネットにあり、EC2 インスタンスはプライベートサブネットにあります。ロードバランサーと EC2 インスタンスに関連付けられているセキュリティグループは異なります。アプリケーションはプライベート仮想インターフェイスを使って 1 Gbps  AWS Direct Connect 接続上で企業のデータセンターにあるオンプレミスデータベースからデータを読み出します。同じデータセンターにある複数のアプリケーションもオンプレミスデータベースを参照します。
 
次のうち、アーキテクチャを改善する変更はどれですか?

1. プライベート仮想インターフェイスをパブリック仮想インターフェイスに置き換える。
2. アプリケーションが同期的に、オンプレミスデータベースにアクセスするための新しい AWS Lambda 関数を呼び出すようにする。
3. データセンターと VPC の仮想プライベートゲートウェイ間に VPN 接続を追加する。
4. オンプレミスデータベースを VPC の EC2 インスタンスに移行する。

<br>

### 08問

>ある会社では VPC 内の Amazon EC2 インスタンスで機密性の高いアプリケーションを実行しています。この会社は脅威を検出するため、ネットワークトラフィックをモニタおよび分析したいと考えています。ソリューションは次のようなものである必要があります。
> - 開発および管理業務を最小限に抑える。
> - 大規模なネットワークトラフィックに対応するためスケールできる。
> - データのクエリと可視化が可能である。

これらの要件を満たすソリューションはどれですか?

1. VPC のフローログを作成して、Amazon DynamoDB テーブルにパブリッシュする。AWS Lambda 関数を使って、DynamoDB ストリームからのデータを読み取り、ログデータをAmazon Aurora にあるテーブルに書き込む。Amazon QuickSight からデータベースを接続してデータを可視化する。
2. VPC のフローログを作成して、Amazon S3 バケットにパブリッシュする。Amazon Athena に外部テーブルを作成してログファイルをクエリし、Amazon QuickSight から Amazon Athena を接続してデータを可視化する。
3. Amazon Kinesis Data Streams を使って Amazon CloudWatch からログファイルをキャプチャーする。Amazon Kinesis Data Firehose を使ってログファイルを Amazon S3 にプッシュする。Amazon Athena に外部テーブルを作成してログファイルをクエリし、Amazon QuickSight から Amazon Athena に接続してデータを可視化する。
4. VPC のフローログを作成して、Amazon EMR クラスターで実行されているインメモリの Spark アプリケーションにパブリッシュする。Amazon QuickSight からクラスターに接続し、Spark SQLを使用してデータを可視化する。

<br>

### 09問

>あるウェブアプリケーションは、ELB Application Load Balancer の背後にある Amazon EC2 インスタンスで実行されています。このインスタンスは、複数のアベイラビリティゾーンにわたり EC2 Auto Scaling グループ内で実行されています。データは Amazon DynamoDB テーブルに保管されています。アプリケーションは、各オペレーションが DynamoDB テーブルで何回呼び出されたかを記録し、各オペレーションに呼び出される項目として、オペレーション ID と呼び出し回数が含まれています。すべてのアプリケーションログは、統合されたCloudWatch エージェントを使用してAmazon CloudWatch Logs にストリーミングされます。最近の監査で、ELB アクセスログに記録された GET リクエスト件数が、DynamoDB テーブルでのGET 呼び出しの件数よりはるかに多いことがわかりました。この問題を調査中に、ソリューションアーキテクトがアプリケーションのデバッグログを有効化したところ、アプリケーションログに次のようなステートメントが見つかりました。

```
2018-11-03 11:20:20.23 DEBUG "Retrieved GET count: 23"
2018-11-03 11:20:20.26 DEBUG "Saved incremented GET count: 24"
2018-11-03 11:20:23.45 DEBUG "Retrieved GET count: 24"
2018-11-03 11:20:23.48 DEBUG "Saved incremented GET count: 25"
2018-11-03 11:20:27.56 DEBUG "Retrieved GET count: 25"
2018-11-03 11:20:27.57 DEBUG "Retrieved GET count: 25"
2018-11-03 11:20:27.59 DEBUG "Saved incremented GET count: 26"
2018-11-03 11:20:27.60 DEBUG "Saved incremented GET count: 26"
2018-11-03 11:20:30.43 DEBUG "Retrieved GET count: 26"
2018-11-03 11:20:30.46 DEBUG "Saved incremented GET count: 27"
```

ソリューションアーキテクトはどうすればアプリケーションを修正できるでしょうか?

1. GetItem 呼び出しが現行数を取得したら、整合性のある読み込みを使う。
2. DynamoDB テーブルの RCUを増やす。
3. DynamoDB テーブルの WCUを増やす。
4. UpdateItem 呼び出しが増加後の呼び出し件数を保存したら、条件付き書き込みを使う。

<br>

### 10問

>ある会社にはハードウェアベースのロードバランサーを含むオンプレミスのアプリケーションがあります。2 つの Apache ホストが SSL を終了し、Java/Tomcat アプリケーションサーバーを実行する 4 台のサーバーの 1 つからダイナミックコンテンツを取得しています。データは、月末のレポート専用のリードレプリカがある My SQL サーバーに保管されます。
ソリューションアーキテクトはアプリケーションを AWS に移行する必要があります。ソリューションでは、アプリケーションコード、コスト、およびプラットフォーム管理に対する変更を最小限に抑える必要があります。

次のアクションの組み合わせのうち、ソリューションアーキテクトがアプリケーションを移行するために実行すべきなのはどれですか。(2 つ選択)

1. データベースを Amazon RDS MySQL Multi-AZ DB インスタンスに移行する。
2. データベースを Amazon Aurora MySQL に移行させる。Amazon CloudWatch Events を使って、月末レポートにリードレプリカを追加し、その後削除する AWS Lambda 関数をスケジュールする。
3. Java/Tomcat サーバーを AWS Elastic Beanstalk に移行する。
4. Java/Tomcat サーバーを ELB Application Load Balancer の背後にある Amazon EC2 インスタンスに移行させる。インスタンスの EC2 Auto Scaling グループを構成する。
5. リードレプリカの Auto Scaling を使ってデータベースを Amazon RDS for MySQL に移行させる。

<br>

### 11問

>ある会社はオンプレミスアプリケーションと MySQL データベースを移行するためにソリューションアーキテクトを採用しました。アプリケーションは何百人というユーザーに活発に使用されており、新しいデータが常に生成されてデータベースに保存されます。アプリケーションはミッションクリティカルであるため、ダウンタイムを最小に抑える必要があります。ユーザーが常に最新のデータを利用できる状態であることが必須です。

データベースを AWS に移行するためにソリューションアーキテクトが実施すべき移行戦略は次のうちどれですか?

1. 新しい Amazon RDS MySQL DB インスタンスと AWS DMS レプリケーションインスタンスを作成する。AWS DMS タスクを構成し、フルロード移行戦略を採用しオンプレミスから RDS インスタンスにデータをコピーする。
2. mysqldump ユーティリティを使用してデータをローカルストレージにエクスポートする。データを Amazon S3 バケットにコピーする。新しい Amazon RDS MySQL DB インスタンスを作成する。データを新しい RDS インスタンスにインポートする。
3. AWS Storage Gateway を使用してデータベースのデータを Amazon S3 バケットにコピーする。AWS Management Consoleを使って新しい Amazon RDS インスタンスを作成し、Amazon S3 からデータをインポートする。
4. Amazon RDS MySQL DB インスタンスと AWS DMS レプリケーションインスタンスを作成する。フルロードと変更データキャプチャ (CDC) 戦略を採用しオンプレミスデータベースから RDS インスタンスにデータをコピーする AWS DMS タスクを構成する。

<br>

### 12問

>ある会社は、アプリケーションをデータセンターから AWS に移行しているところです。アプリケーションは現在、サードパーティサービスへのアクセスに使用する API キーをローカルファイルに保管しています。AWS にデプロイすると、アプリケーションは Amazon EC2 インスタンスで実行されます。移行の一貫として、アプリケーションは API キーをより厳重にセキュリティ保護する必要があります。特に、次の点が重要です。
> - 各環境 (開発、テスト、およびプロダクションなど) には独自の API キーが必要です。
> - 監査目的のため、すべての API キーアクセスリクエストを記録する必要があります。
> - API キーはカスタマーマネージドキーを使って保存時に暗号化される必要があります。
> - アクセス権限の粒度はきめ細かなもの (開発環境はプロダクション API キーにアクセスできないなど) である必要があります。

これらの要件を満たす最もセキュアな方法は次のどれですか?

1. 各 API キーについて AWS System Manager Parameter StoreでSecure Stringを作成する。カスタマーマネージド AWS KMS カスタマーマスターキー (CMK) を使ってSecure Stringを暗号化する。CMK については kms:decrypt アクションに対する権限を持ち、API キーについては ssm:getparameter アクションに対する権限を持つ IAM ユーザーを環境に作成する。そのユーザーのアクセスキーを各 Amazon EC2 インスタンスの資格情報ストアに保管する。
2. 各 API キーについて AWS System Manager Parameter StoreでSecure Stringを作成する。カスタマーマネージド AWS KMS カスタマーマスターキー (CMK) を使ってSecure Stringを暗号化する。両方の環境に、CMK については kms:decrypt アクションに対する権限を持ち、適切な API キーについては ssm:getparameter アクションに対する権限を持つ IAM ユーザーを作成する。適切な IAM ロールで、各 Amazon EC2 インスタンスを起動する。
3. AWS KMS カスタマーマスターキー (CMK) を使って暗号化された Amazon DynamoDB テーブルを作成する。テーブルの異なるアイテムに各 API キーを保管する。各環境に、CMK についてはkms:decrypt アクションに対する権限を持ち、対応するアイテムへのdynamodb:getitem アクションに対する権限を持つ IAM ユーザーを作成する。適切な IAM ロールで、各 Amazon EC2 インスタンスを起動する。
4. ユーザーデータを利用して 各 Amazon EC2 インスタンスに適切な API キーを渡す。カスタマーマネージド AWS KMS カスタマーマスターキー (CMK) について、各 EC2 インスタンスに kms:encrypt と  kms:decrypt アクションに対する権限を持つ IAM ロールを割り当てる。ユーザーデータスクリプトでは、CMK を使って API キーを暗号化する。各 EC2 インスタンスに暗号化された API キーを保管する。

<br>

### 13問

>ある会社は、ELB Application Load Balancer の背後にある Amazon EC2 インスタンスでウェブアプリケーションを実行しています。これまでに何度もトラフィックの急増加が原因でアプリケーションの反応を遅くなり、障害が発生しました。ログによると、増加分のトラフィックには、複数のソースからの不正なリクエストが含まれていることが明らかになりました。

サイトが今後このタイプの攻撃を最速でブロックできる方法は次のうちどれですか?

1. Amazon CloudFront ディストリビューションを作成し、Elastic Load Balancer をオリジンに設定する。被害を軽減するために、AWS Shield Standard を有効にする。
2. ロードバランサーに 文字列一致条件を指定したAWS WAF ルールを追加して、不正なリクエストをブロックする。
3. AWS Lambda 関数を作成して、Elastic Load Balancer アクセスログから不正なリクエストを特定し、悪意のあるトラフィックのソース IP アドレスをブロックするよう Load Balancer に関する AWS WAF ルールを更新する。
4. Amazon CloudFront ディストリビューションを作成し、Elastic Load Balancer をオリジンに設定する。AWS Lambda 関数を作成して、CloudFront ログから不正なリクエストを特定し、悪意のあるトラフィックのソース IP アドレスをブロックするよう CloudFront に関する AWS WAF ルールを更新する。

<br>

### 14問

>ある会社は us-west-2 でウェブアプリケーションを実行しています。アプリケーションは ELB Network Load Balancer の背後にある Amazon EC2 インスタンスで実行されています。インスタンスは複数のアベイラビリティゾーンにわたる EC2 Auto Scaling グループで実行されています。静的コンテンツは Amazon S3 から配信され、トランザクションデータは Amazon RDS MySQL DB インスタンスに保管されます。DNS には Amazon Route 53 が使用されています。S3 バケット名やデータベース接続文字列などの構成情報は、AWS Systems Manager Parameter Store に保管されます。安定した状態では、Auto Scaling Group に 4 つの EC2 インスタンスがあります。アプリケーションは、AWS CloudFormation テンプレートでデプロイされます。
ソリューションアーキテクトは、アプリケーションについて自動化された災害復旧計画を策定する必要があります。計画は、30 分の RTO と 15 分の RPO でアプリケーションが 2 番目のリージョンへとフェイルオーバーできるものでなければなりません。ソリューションアーキテクトはアプリケーションソースコードを変更する能力がありません。

> ソリューションアーキテクトは次のステップを既に実装しました。
> - 2 番目のリージョンに静的コンテンツをレプリケートするよう S3 クロスリージョンレプリケーションを構成した
> - すべての既存静的コンテンツを 1 番目のリージョンの S3 バケットから 2 番目のリージョンの S3 バケットにコピーした
> - 2 番目のリージョンに RDS MySQL DB インスタンスのリードレプリカを作成した
> - 2 番目のリージョンの AWS Systems Manager Parameter Store に S3 バケットとデータベース接続文字列を追加した
> - CloudFormation のマッピングセクションを、適切な AMI とリージョンのマッピングを行い更新した
> - 2 番目のリージョンにおけるアプリケーションスタックを起動のためにCloudFormation テンプレートを使用した
> - 2 番目のリージョンの Auto Scaling グループの最小および希望する容量を 1 に更新した
> - Amazon Route 53 ホストゾーンでフェールオーバールーティングポリシーを更新した
> - 2 番目のリージョンに Network Load Balancer をポイントする Route 53 ホストゾーンにセカンダリレコードセットを追加した
> - 1 番目のリージョンでアプリケーションに障害が発生したときに SNS 通知をパブリッシュするヘルスチェックアラームを構成した

計画を実施するために必要な追加ステップの組み合わせはどれですか? (2 つ選択)

1. CloudFormation テンプレートにパラメータを追加してデプロイ先リージョンを指定する。
2. 必要な AMI を 1 番目のリージョンから 2 番目のリージョンにコピーする。
3. 2 番目のリージョンに、Auto Scaling グループの希望する容量を 4 に増やす AWS Lambda 関数を書く。関数をヘルスチェックアラーム SNS トピックにサブスクライブする。
4. 2 番目のリージョンに、リードレプリカ RDS DB インスタンスをスタンドアロン DB インスタンスにプロモートする AWS Lambda 関数を書く。関数をヘルスチェックアラーム SNS トピックにサブスクライブする。
5. 1 番目のリージョンで必要な AMI に関する権限を 2 番目のリージョンからアクセスできるように変更する。

<br>

### 15問

>ある会社はログストリームを生成する動画アプリケーションを開発しています。ストリームの各レコードには最大 400 KB のデータが含まれます。動画ストリーミング体験を改善するために複雑な SQL クエリを用いて、一定期間のトレンドについて分析し、ストリームから指標のサブセットを収集する必要があります。
ソリューションアーキテクトは、顧客の介入がなくてもアプリケーションをスケールできるソリューションを作成するつもりです。

次のうち、これらの要件を満たすためソリューションアーキテクトが実装すべきソリューションはどれですか?

1. ログデータを Amazon Kinesis Data Firehose 配信ストリームに送信する。AWS Lambda 関数を使用してデータを変換する。データを Amazon Redshift に配信する。Amazon Redshift でデータをクエリする。
2. ログデータを Amazon SQS スタンダードキューに送信する。そのキューを、データを変換して Amazon Redshift に保管する AWS Lambda 関数のイベントソースにする。Amazon Redshift でデータをクエリする。
3. ログデータを Amazon CloudWatch Logs ロググループに送信する。そのロググループを、データを変換して Amazon S3 バケットに保管する AWS Lambda 関数のイベントソースにする。Amazon Athena でデータをクエリする。
4. ログデータを Amazon Kinesis データストリームに送信する。データを変換して 2 番目のデータストリームに送信する AWS Lambda 関数をストリームにサブスクライブする。Amazon Kinesis Data Analytics を使って、2 番目のストリームでデータをクエリする。

<br>

### 16問

>ある会社は AWS でウェブアプリケーションをホストしています。アプリケーションは Auto Scaling グループ内の Amazon EC2 インスタンスで実行されています。データベースレイヤーは、5 テビバイト (TiB) の Amazon EBS 汎用 SSD (gp2) ストレージが搭載された PostgreSQL インスタンスの db.m5.4xlarge Amazon RDS で実行されています。
使用ピーク期間中、ウェブアプリケーションへのユーザーリクエストの一部がタイムアウトします。ソリューションアーキテクトは、ピーク使用期間中、RDS インスタンスの Amazon CloudWatch DiskQueueDepth 指標が急上昇することを検出しました。

ピーク期間中にアプリケーションの可用性を改善するためにソリューションアーキテクトが行うべきなのは次のどれですか?

1. RDS インスタンスの gp2 ボリュームのサイズを 16 TiB に増やす。
2. RDS インスタンスのストレージタイプを Provisioned IOPS SSD (io1) に変更し、最大の IOPSをプロビジョンする。
3. DB インスタンスが Multi-AZ配置されるよう変更する。
4. DB インスタンスで Amazon EBS 最適化を有効にする。

<br>

### 17問

>ある会社はオンプレミスデータセンターから AWS へシステムの完全移行を実施しています。会社はオンプレミスに保管された全データを 4 週間以内にAmazon S3 へ移行する必要があります。現在、オンプレミスストレージが保管するデータは 900 TB で、100 Mbps のリンクでインターネットに接続されています。リンクのスループットの最大 20% が既存システムによってリアルタイムで使用されています。

所定の期間内にデータ移行を行うのに最もコスト効率に優れた方法はどれですか?

1. 複数の AWS Snowball デバイスを注文してデータを配送する。
2. マルチパートアップロードを使って、既存リンク上でデータを転送する。
3. AWS Direct Connect リンクをセットアップして、データをアップロードする。
4. AWS 環境に VPN トンネルを構成してデータをアップロードする。

<br>

### 18問

>ソリューションアーキテクトがゲノム研究会社向けのアプリケーションを設計しています。アプリケーションは、毎晩複数の複雑な数学的計算を実行します。各計算は独立しており、それぞれ完了に数時間かかる場合があります。
アプリケーションの設計はコストと相互依存関係を最小限に抑えるものであり、計算は平行して実行される必要があります。

これらの要件を満たすのはどれですか？

1. AWS Batch にジョブとして計算を登録する。ジョブを Amazon ECS 内のコンテナで別々に実行する。
2. それぞれの計算を Amazon API Gateway に送信する。AWS Lambda 関数を使って計算を実行する。
3. 各計算をマスター Amazon EC2 インスタンスに送信する。このEC2 インスタンスを構成して、計算を適切な EC2 作業者ノードに転送する。
4. ELB Application Load Balancer に送信する。パスベースのルーティングを使ってリクエストを適切な Amazon EC2 作業者ノードに転送するよう ELB を構成する。

<br>

### 19問

>アカウント件数が増える中、会社はプロダクション AWS アカウントでの承認されていないサービスの利用を禁止し、管理オーバーヘッドを最小限に抑えたいと考えています。

これらの要件を満たすアプローチは次のうちどれですか?


1. 一括請求機能を有効にした新組織を作成する。プロダクションアカウントと非プロダクションアカウントの 2 つの新規組織単位 (OU) を作成する。新組織で、プロダクションの各サブアカウントに適用し、未承認のサービスへのアクセスを拒否する IAM ロールを作成する。
2. すべての機能を有効にした新組織を作成する。プロダクションアカウントと非プロダクションアカウントの 2 つの新規組織単位 (OU) を作成する。新組織で、プロダクションの各サブアカウントに適用し、未承認のサービスへのアクセスを拒否する IAM ロールを作成する。
3. すべての機能を有効にした新組織を作成する。プロダクションアカウントと非プロダクションアカウントの 2 つの新規組織単位 (OU) を作成する。新組織で、未承認のサービスへのアクセスを拒否する SCP を作成し、その SCP をプロダクション OU に適用する。
4. 一括請求機能を有効にした新組織を作成する。プロダクションアカウントと非プロダクションアカウントの 2 つの新規組織単位 (OU) を作成する。新組織で、未承認のサービスへのアクセスを拒否する SCP を作成し、その SCP をプロダクション OU に適用する。

<br>

### 20問

>ある会社ではオンプレミスの MySQL データベースから AWS への移行準備を行なっています。最近、クライアントアプリケーション数の増加が原因でデータベースのパフォーマンスが低下しています。データベースサイズは現在 20 TB ですが、毎年 4 TB ずつ増加することが予測されます。データベースのメンテナンスと継続的オペレーションには大規模なチームが必要ですが、これは会社にとって管理面での負担となります。
会社は迅速に実装でき、管理業務が最小限で済み、現在そして将来も高パフォーマンスを提供する費用効率の高いソリューションを求めています。データベースは可用性が高く保ち、移行中も稼働していなければなりません。

次のソリューションの組み合わせのうち、これらの要件を満たすものはどれですか? (2 つ選択)

1. ストレージと高 I/O 向けに最適化された Amazon EC2 インスタンスで 稼働しているMySQL を使用する。
2. Amazon Aurora MySQL Multi-AZ インスタンスを使用する。
3. Amazon RDS Oracle Multi-AZ DB インスタンスを使用する。
4. AWS DMS を使用してデータを移行する。
5. mysqldump ユーティリティを使用してデータを移行する。