# AWS Builders Online

日付：2022/01/20

<br>

## オープニングセッション （亀田 治伸）

- AWS IoT RoboRunner
    - 異なるベンダーのロボットをクラウド上で統合管理する
- AWS Local Zones（米国のみ）
    - 通信環境の悪い地域にスポットでおいてく
- IoT TwinMaker
    - デジタルツイン（シュミレート環境をデジタル的に作成する）
- IoT FeetWise
    - 物理領域のデータ量は多い（1時間の走行で2TBの情報量）
        - いらないデータは予めすてる（通信環境が弱いため）
- AWS Well-architected Sustainability Pillar
    - サステナビリティ観点の柱が追加された
        - よりワットパフォーマンスの高いCPUをチョイスしているか
        - 無駄なサーバが起動していないか

<br>

## Amazon SageMaker JumpStart を用いた IT エンジニアによる機械学習 PoC のすゝめ （呉 和仁）

画像からキノコの山とタケノコの里を検出するモデルを学習してみた

- Amazon SageMaker Ground Truthを使うとラベリング処理が楽
- 画像認識は畳み込みニューラルネットを使う
    - 普通に学習すると1時間ほど掛かってしまう
    - SageMaker JumpStartで既存の学習済みモデルからFine-Tuneをする（楽をする）
- [How to Start Github](https://github.com/kazuhitogo/builders-online-202201-demo)

資料: [20220120_BuildersOnline_SageMaker.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20220120_BuildersOnline_SageMaker.pdf)

<br>

## 今日からはじめるサーバーレス - AWS Lambda と AWS Step Functions で小さな課題を解決するところから

- レベル感が微妙

資料: [20220120_BuildersOnline_Lambda+StepFunctions.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20220120_BuildersOnline_Lambda%2BStepFunctions.pdf)

<br>

## Amazon DynamoDB サーバーレスデータベースサービスを知る最初の一歩

- ただのサービスの紹介

資料: [20220120_BuildersOnline_DynamoDB.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20220120_BuildersOnline_DynamoDB.pdf)

<br>

## (私のように)セキュリティを何から始めれば良いか分からない開発者の方へ

- これは有益な情報なので資料読み返し推奨

資料: [20220120_BuildersOnline_Security.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20220120_BuildersOnline_Security.pdf)

<br>

## Amazon Redshift Serverless & Amazon QuickSight によるサーバーレス分析

- QuickSight上でアップロードされたデータファイルの結合などtableau prepのような編集作業ができる
- RedshiftServerlessでも簡易的な可視化が可能で、クエリーエディタで色々データをいじれる

資料: [20220120_BuildersOnline_QuickSight+RedshiftServerless.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/20220120_BuildersOnline_QuickSight%2BRedshiftServerless.pdf)

<br>