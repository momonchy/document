# ECS ExecでECSコンテナへ接続する

ここで紹介するのは、ECS上で稼働するコンテナへSSM経由でコンソール接続する為の手順です。  
必要な手順はざっくり以下の流れとなります。

- AWSCLIを準備する
- 専用のIAMポリシーをタスク定義でアサインする
- ECS Cluster上でECS Execを有効化する（その後タスク/コンテナを作り直す）

<br>

## 本ドキュメントの前提条件

- ローカルPCにAWSCLIをインストールしている
- ECSプラットフォームへFargateを利用している
- ECS Cluster & Service が既に存在している

<br>

## 手順
### AWSCLIの準備

1. ローカルPCのAWSCLIが「--enable-execute-command」オプションを利用できることを確認
    ```sh
    $ aws ecs update-service help

    --snip

    SYNOPSIS
            update-service
          [--cluster <value>]
          --service <value>
          [--desired-count <value>]
          [--task-definition <value>]
          [--capacity-provider-strategy <value>]
          [--deployment-configuration <value>]
          [--network-configuration <value>]
          [--placement-constraints <value>]
          [--placement-strategy <value>]
          [--platform-version <value>]
          [--force-new-deployment | --no-force-new-deployment]
          [--health-check-grace-period-seconds <value>]
          [--enable-execute-command | --disable-execute-command]  ← このオプションが使えることを確認
          [--cli-input-json | --cli-input-yaml]
          [--generate-cli-skeleton <value>]
    ```
    オプションが利用できない場合は、以下の公式ドキュメントを参照しAWSCLIをアップデート
    - [AWS CLI バージョン 1 のインストール、更新、アンインストール](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-cliv1.html)
    - [AWS CLI バージョン 2 のインストール、更新、アンインストール](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/install-cliv2.html)
    <br>

2. Session　Managerプラグインがインストールされていることを確認
    ```sh
    $ session-manager-plugin --version
    ```
    Session　Managerプラグインがインストールされていない場合は、以下の公式ドキュメントを参照しインストール
    - [AWS CLI 用の Session Manager プラグインをインストールする](https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html)
    <br>

### IAM権限の追加

- ECS Serviceへ登録しているタスク定義の「タスクロール」へ以下のIAM権限をAllowで追加

    - ssmmessages:CreateControlChannel
    - ssmmessages:CreateDataChannel
    - ssmmessages:OpenControlChannel
    - ssmmessages:OpenDataChannel
    <br>

- 出来合いのIAMポリシー「AmazonSSMManagedInstanceCore」をアサインする方が簡単

<br>

### ECSの準備

1. 対象のECS Serviceで「ExecuteCommand」が無効になっていることを確認
    ```sh
    $ aws ecs describe-services --cluster {クラスタ名} --service {サービス名} | jq .'services'[0].'enableExecuteCommand'
    null
    ```

2. 「ExecuteCommand」を有効化
    ```sh
    $ aws ecs update-service --cluster {クラスタ名} --service {サービス名} --enable-execute-command
    ```
    確認
    ```sh
    $ aws ecs describe-services --cluster {クラスタ名} --service {サービス名} | jq .'services'[0].'enableExecuteCommand'
    true
    ```

3. 既存タスクを停止するなどして、ECS Service内のタスクを作り直す

<br>

### コンテナへ接続

- タスクIDの確認（返却値はタスクARNなのでクラスタ名以降のタスクIDを参照）
    ```sh
    $ aws ecs list-tasks --cluster {クラスタ名} --service-name {サービス名}
    ```

- コマンドを実行したい時
    ```sh
    $ aws ecs execute-command --cluster {クラスタ名} --task {タスクID} --interactive --command "ls"
    ```

- コンテナへログインしたい時
    ```sh
    $ aws ecs execute-command --cluster {クラスタ名} --task {タスクID} --interactive --command "/bin/sh"
    ```