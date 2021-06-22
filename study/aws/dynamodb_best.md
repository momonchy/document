# Level Up Amazon DynamoDB - オンラインで学ぶAmazon DynamoDBのベストプラクティス

日付: 6/3(木) 09:30〜

<br>

## 資料
- [20210603_DynamoDB-History-and-How-it-Works-DDB_JP.pdf](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210603_DynamoDB-History-and-How-it-Works-DDB_JP.pdf)
- [20210603_DynamoDB-Operations.pdf](https://contents-s3-bucket.s3-ap-northeast-1.amazonaws.com/documents/aws/20210603_DynamoDB-Operations.pdf)

<br>

## キーワード
結果整合性
ACID特製
カーディナリティ
OLTP/OLAP
パーパスビルド

<br>

## イントロダクション
7兆のアクセスに耐えられるｗ
4000万PV/秒に耐えられる

<br>

## 歴史とアーキテクチャ
なぜ開発したのか？: Amazonのサービスが止まったのが原因
負荷が高くなるほどレイテンシーが低くなる
OLTPユースケース向けに設計されたDynamoDB
- SQLはOLAPに適してる

大規模な水平スケーリング
- 一番の特徴と考えられる
- Casandraだとノード足し引き、データのリバランスがめんどい

SQL→スケールアップ、DynamoDB→スケールアウト
パーティションキーが同じだと同じパーティション（ストレージ）にitemが保存されている
ソートキーの部分で前方一致などの詳細なフィルタを設定できる

ローカルセカンダリインデックス（LSI）の方がグローバルセカンダリインデックス（GSI）よりローンチが古い
- LSIにはテーブル作成後に追加できないなどの制約がある
- 古い（歴史ある）仕様なのでAWS的にはGSIの方を選択して欲しい

<br>

### レプリケーション
3つのAZに書き込まれてる（Aゾーン〜Cゾーン）
特定のリーダーに書き込まれた後に他のゾーンにリーダーがコピーする（Solrっぽい？）
- いずれかのノードにコピーできれば 200 OK を返す

<br>

### キャパシティ
オートキャパシティユニット：自動的にキャパシティをスケールしてくれるので結果としてコストを安く抑えられる
アダプディブキャパシティ：特定itemの負荷が高い時に自動的に別パーティションへ分離してくれる

<br>

## ベストプラクティス
プロヴィジョンキャパシティよりはオンデマンド（オートキャパシティ）の方がクラウドネイティブなコスト発想

<br>

### 大きなアイテムを保存する必要があるか？
S3へ保存する（DBへバイナリを入れるのはお勧めしない）
行の長さ（Attributeの数）を工夫するとWCUのコスト感が変わってくる

<br>

### Attribute名を短くすると効果的
Jsonっぽくデータを保存しているので、item数が多くなってくるとストレージ量を圧迫する
WCUのコスト感が変わってくる 

<br>

### 様々なバックアップ
オンデマンドバックアップ（自動でバックアップ）
ポイントインタイムリカバリ（PITR）

<br>

### セキュリティ
FGAC: Cognitoと連携して自分のitemのみアクセスできるようにパーミッション管理できる

<br>

### 

<br>

### 

<br>
