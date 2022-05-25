# ガバメントクラウドで考える技術的統制と効率性〜AWSでの実現策〜(CUS-50)

日時：2022/05/25　14:00 〜 14:30
資料：[CUS-50_AWS-Summit-2022_Digital.pdf](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202205_AWS_SUMMIT_JAPAN_2022/CUS-50_AWS-Summit-2022_Digital.pdf)

<br>

## ガバメントクラウド

日本はめちゃくちゃITが遅れている世界で評価されている

- IaCテンプレートの必要性
- 予防的統制・発見的統制（ガードレール）
- 成長するチーム

<br>

## IaCテンプレートの必要性

- 省庁、地方自治体のシステムは非常に多い
- 統制の効いたアーキテクチャの素早い横展開が必要
- アーキテクチャにはOSの無い環境を設計する

<br>

## ガバメントクラウドの設計

マルチアカウントの管理方法
- AWSをマルチアカウントで利用
- AWS ControlTower と AWS Organizations と AWS SSOを利用

アカウントの払い出し方法
- ガバメントクラウド管理者はControlTowerでAWSアカウントを発行し、ユーザはSSOで発行する
- システム利用者は上記環境上で開発
- 全てのアカウントをSSOで発行はしない
    - システムが多すぎて集中管理は無理