# docker image の操作

ダウンロード済みイメージの一覧表示。
```sh
$ docker images
```

イメージのダウンロード。
```sh
$ docker pull ${image name}
```

イメージの削除。
```sh
$ docker rmi ${image id/name}
```

<br>

# docker build の操作

イメージの作成。dockerファイルがcurrentにある場合は「.」でOK。
```sh
$ docker build -t ${image name}:${tag} ${docker file path/.}
```

dockerファイル内で「ARG ${key}」を使って引数を取っている場合、コマンド引数から${value}を指定可能。
```sh
$ docker build -t ${image name}:${tag} ${docker file path/.} --build-arg ${key}=${value}
```

<br>

# docker image へのタグ操作

イメージへタグを付与。
```sh
$ docker tag ${image name}:${current tag} ${image name}:${new tag}
```

code buildを使ったパターン。日付タグとは別にlatestタグを最新イメージへ付け回す書き方。
```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      docker: 18
    commands:
      - echo install step...
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - $(aws ecr get-login --no-include-email --region ${AWS_DEFAULT_REGION})
  build:
    commands:
      - echo Build started on $(date)
      - DATETIME=$(date +%Y%m%d.%H%m%S)
      - echo Building the Docker image...
      - echo docker build -t ${IMAGE_REPO_NAME}:${DATETIME} . --build-arg APP_ENV=${APP_ENV}
      - docker build -t ${IMAGE_REPO_NAME}:${DATETIME} . --build-arg APP_ENV=${APP_ENV}
      - echo docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}
      - docker tag ${IMAGE_REPO_NAME}:${DATETIME} ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${DATETIME}
      - docker tag ${IMAGE_REPO_NAME}:${DATETIME} ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:latest 
  post_build:
    commands:
      - echo Build completed on $(date)
      - echo Pushing the Docker image...
      - docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${DATETIME}
      - docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:latest
      - printf '[{"name":"'${SERVICE_NAME}'","imageUri":"%s"}]' ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:latest > artifacts.json

artifacts:
  files: artifacts.json
```

<br>

# docker container の作成

コンテナ登録＆起動（コンテナ名を付与）
```sh
$ docker run --name ${container name} ${image id/name}
```

コンテナ登録＆起動＆バックグランド実行（コンテナ名を付与）
```sh
$ docker run -d --name ${container name} ${image id/name}
```

コンテナ登録＆起動＆バックグランド実行＆ポートフォワード（コンテナ名を付与）
```sh
$ docker run -d --name ${container name} -p ${host port}:${container port} ${image id/name}
```

<br>

# docker container の操作

コンテナの一覧表示。
```sh
$ docker ps -a
```

コンテナの起動。
```sh
$ docker start ${container id/name}
```

コンテナの停止。
```sh
$ docker stop ${container id/name}
```

コンテナの削除。
```sh
$ docker rm ${container id/name}
```

コンテナへログイン。
```sh
$ docker exec -it ${container id/name} /bin/bash
```