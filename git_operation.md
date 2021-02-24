# ブランチの操作

ブランチの一覧を表示
```
$ git branch -a
```

ブランチを切り替える
```
$ git checkout <ブランチ名>
```

ブランチを作成
```
$ git checkout -b <ブランチ名>
```

ブランチをリモートへ登録する
```
$ git push origin develop
```

ブランチをマージする
```
マージ先へ移動
$ git branch -a 
$ git checkout master

ブランチを指定してマージ
$ git merge <マージしたいブランチ名>
```