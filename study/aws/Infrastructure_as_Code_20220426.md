# Infrastructure as Code 談議 2022 ~ AWS Develover Live Show

## なぜ IaC なのか？

IaCの邦訳版がオライリーから出版されてる
- https://www.oreilly.co.jp/books/9784873117966/

ダイナミックインフラストラクチャが台頭
- インフラストラクチャの変更管理を容易にするため

IaC の原則
- 簡単に再現可能
- 使い捨てにできる
- 絶えず変化するデザイン
- 統一的にできる
- 反復できる

<br>

## 何故 IaC を行うのか？

[デジタル庁 ガバメントクラウド](https://digital-gov.note.jp/m/m8adae0df5516)

<br>

## IaC で解決しきれないこと

- DBの中身をいじるとかができない
- ロールバックが出来ないケースがある（Python2 → Python3へ上げたけどロールバックに失敗）
    - あくまでもパッケージ（コンテナ）の外側に対してイミュータブルである
    - 厳密には破棄→作成