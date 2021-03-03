# BIMプロジェクトの共有環境構築

## BIMcloud とは

BIMプロジェクトの共通管理方法としては以下の2パターンがある。

- BIMcloud BASIC 環境を構築して利用する
- BIMcloud のライセンスを購入して利用する（クラウド環境）

上記の詳細な違いについては[こちら](https://ssilab.co.jp/blog/tech-blog/tech-blog-child/bimcloud-basic-vs-bimcloud)を参照。

<br>

## 料金比較
BIMcloud BASIC
- 基本無料

BIMcloud
- BIMcloud User License(BUL) = 24,000円/年間/ユーザ

<br>

## BIMcloud BASIC の構築

本項では、BIMcloud BASIC を AWS 上へ構築する手順を記載する。  
BIMcloud BASIC の動作要件については[こちら](https://graphisoft.com/jp/resources-and-support/system-requirements)を参照のこと。

<br>

### インスタンス条件

|項目|内容|
|--|--|
|ami|Microsoft Windows Server 2019 Base (x86_64)|
|type|m5.xlarge (vCPU x 4, MEM x 16GB)|
|storage|SSD 100GB|
<br>

構築手順

1. [WinSrvの日本語化](https://www.dell.com/support/kbdoc/ja-jp/000111205/windows-server-2019%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%8C%96%E6%89%8B%E9%A0%86?gacd=10058743-13022-6164316-275449057-0&dgc=ST&ds_rl=1287091&ds_rl=1288324&gclid=Cj0KCQiA962BBhCzARIsAIpWEL0BJlWTlOy1ZcX4_6Vc2lpgSvJ3GHv9vA782yvNUZZXMBboJ2QS9uMaAorQEALw_wcB&gclsrc=aw.ds)
2. タスクマネージャーを通知領域へ常駐化
3. IEだとChromeをなぜかダウンロード出来ないので、Firefox→Chromeの順にインストール
4. BIMcloud を[ダウンロード](https://graphisoft.com/jp/downloads/bimcloud)
5. BIMcloud Serverをインストール
    | 項目 | 内容 |
    | -- | -- |
    | インストール先 | C:\Program Files\GRAPHISOFT\BIMcloud |

6. BIMcloud Serverの設定
    | 項目 | 内容 |
    | -- | -- |
    | 通信ポート | 22001 |
    | データフォルダ(TeamWorkProject) | C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-03-03\Projects |
    | データフォルダ(Library) | C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-03-03\Attachments |
    | データフォルダ(Cache) | C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-03-03\BlobCache |
    | データフォルダ(FileStorage) | C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-03-03\Files |
    | バックアップ/スナップショット | ※BIMcloud BASICでは利用出来ません |

7. BIMcloud Managerをインストール
    | 項目 | 内容 |
    | -- | -- |
    | インストール先 | C:\Program Files\GRAPHISOFT\BIMcloud |

8. BIMcloud Managerの設定
    | 項目 | 内容 |
    | -- | -- |
    | 表示名 | BIMCLOUD |
    | 通信ポート | 22000 |
    | 管理アカウント | masteradmin/password |
    | バックアップ | ※BIMcloud BASICでは利用出来ません |

初期設定

1. BIMcloud Managerへ管理アカウントで[ログイン](http:/localhost:2200/install.html?lang=ja)
2. 初期ユーザの作成
    | 必要項目 |
    | -- |
    | フルネーム |
    | ログイン名 |
    | パスワード |
    | メールアドレス |

3. 製品プランの選択
    | 項目 | 内容 |
    | -- | -- |
    | 製品プラン | BIMcloud BASIC (旧 BIM Server) |
    | ARCHICADバージョン | 24 |

4. サーバアドレスの設定  
    ARCHICADからこのサーバへの接続に使用可能なアドレスを設定（http://XXXXX.XXX:22000）

5. メールサーバの設定

<br>

## 参考サイト
- [ダウンロードサイト](https://graphisoft.com/jp/downloads/bimcloud)
- [BIMcloud BASIC と BIMcloud の違い](https://ssilab.co.jp/blog/tech-blog/tech-blog-child/bimcloud-basic-vs-bimcloud)
- [BIMcloud BASIC インストール手順](https://support.graphisoft.co.jp/hc/ja/articles/360009104253-BIMcloud-Basic%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%96%B9%E6%B3%95)
