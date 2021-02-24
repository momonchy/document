## 手順
- [WinSrvの日本語化](https://www.dell.com/support/kbdoc/ja-jp/000111205/windows-server-2019%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%8C%96%E6%89%8B%E9%A0%86?gacd=10058743-13022-6164316-275449057-0&dgc=ST&ds_rl=1287091&ds_rl=1288324&gclid=Cj0KCQiA962BBhCzARIsAIpWEL0BJlWTlOy1ZcX4_6Vc2lpgSvJ3GHv9vA782yvNUZZXMBboJ2QS9uMaAorQEALw_wcB&gclsrc=aw.ds)
- IEだとChromeをなぜかダウンロード出来ないので、Firefox→Chromeの順にインストール
- TシリーズのインスタンスだとWinSrvはもたないのでc5.large以上がお勧め（クレジットをすぐ消費してしまう）
- BIMcloud Serverのインストールサイズは1.5GB
- BIMcloud Managerのインストールサイズは1.6GB
- バックアップやスナップショット機能はライセンスの関係で利用出来ない
- BIMcloud basic を選択した場合はARCHICADのバージョンが１つしか対応できない

<br>

# 設定パラメータ

BIMcloud Server
```
ARCHICADバージョン：24
ポート：22001
データフォルタ：
    チームワークプロジェクト：C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-02-17\Projects
    ライブラリ：C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-02-17\Attachments
    キャッシュ：C:\Program Files\GRAPHISOFT\BIMcloud\Server-2021-02-17\BlobCache
    ファイルストレージ：C:\PROGRA~1\GRAPHI~1\BIMcloud\SERVER~1\Files
```

BIMcloud Manager
```
表示名：BIMCLOUD-TEST
ポート：22000
ユーザ：masteradmin
パスワード：password
データフォルダ：C:\Program Files\GRAPHISOFT\BIMcloud\Manager-2021-02-17\Data
```

<br>

## 料金比較
BIMcloud BASIC
- 基本無料

BIMcloud
- BIMcloud User License(BUL) = 24,000円/年間/ユーザ

<br>

## 参考サイト
- [ダウンロードサイト](https://graphisoft.com/jp/downloads/bimcloud)
- [BIMcloud BASIC と BIMcloud の違い](https://ssilab.co.jp/blog/tech-blog/tech-blog-child/bimcloud-basic-vs-bimcloud)
- [BIMcloud BASIC インストール手順](https://support.graphisoft.co.jp/hc/ja/articles/360009104253-BIMcloud-Basic%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%96%B9%E6%B3%95)


