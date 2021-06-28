# AWS SAMについて

> 本ドキュメントは2021/06/27時点の ```SAM CLI, version 1.23.0``` を利用して記載されたものです。

<br>

AWS SAMは、コンピュートリソースとしてのLambdaを中心に、関連するマネージドサービスを統合的に構築可能なフレームワークである。  
AWS SAMを以下の3点に分解して理解する。

- AWS SAMリソース
- AWS SAMテンプレート
- AWS SAM CLI

<br>

## 1. 前提

本ドキュメントでは、Lambda関数のRuntimeとして ```Python3.8``` を選択することを前提とする。

<br>

## 2. AWS SAMリソース

AWS SAMのリソースとして用意しなければいけないものは以下2点である。

- Lambda関数のコード
- AWS SAMテンプレート

また、開発環境を準備するために AWS SAM CLIをローカルへインストールしておく必要がある。  
インストールに関する詳細な手順は以下を参照のこと。

- [【公式】AWS SAM CLIのインストール](https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)

AWS SAM CLIをインストール出来たら開発環境を準備する。  
これには2通りの方法が存在する。

1.  ```sam init``` コマンドでAWSのテンプレートから環境を準備する
2.  自分でプロジェクトディレクトリを掘る

本ドキュメントでは(2)を前提として記載する。

<br>

### 2.1. ディレクトリ構造

最低限必要なプロジェクトのディレクトリ構造は以下の通り。

```sh
.
├── lambda_function.py  # Lambdaへデプロイするコード
├── requirements.txt    # Lambdaが要求するライブラリ情報
├── samconfig.toml      # sam deploy時に勝手に生成される
└── template.yaml       # CloudFormationライクなテンプレートファイル
```

Lambda関数が複数存在したり、eventファイルを保存しておきたいなら以下のようになる。  

```
.
├── README.md
├── event/
│   └── event.json
├── functions/
│   ├── functionA/
│   │   ├── lib/
│   │   ├── requirements.txt
│   │   └── lambda_function.py
│   └── functionB/
│       ├── lib/
│       ├── requirements.txt
│       └── lambda_function.py
├── samconfig.toml
└── template.yaml
```

Lambda関数が複数になる場合の注意点
- functionA/functionBがLambdaへのデプロイ単位になる為、それぞれに ```requirements.txt``` が必要となる。
- 各関数共通のLibrariyが存在していても、それぞれのディレクトリへ配置しておく必要がある（シンボリックリンクとかいけるのかな？）

<br>

### 2.2. 環境変数について

Lambda関数へ設定したい環境変数や、既存のAWSリソース名などは ```template.yaml``` へ直接記載するべきではない。  
この場合、```sam local``` や ```sam deploy``` では外部から環境変数やパラメータとして渡すことになるが、それぞれで変数の渡し方が異なる。

詳細についてはAWS SAM CLIへ記載する。

<br>

## 3. AWS SAMテンプレート

AWS SAMテンプレートは、Lambda関数およびその周辺のマネージドサービスを構築するためのCloudFormationライクなテンプレートファイルである。
記法はJSONとYAMLから選択でき、CloudFormationの記法でリソースを記述することも可能。

- [【公式】SAM Template Reference](https://github.com/aws/serverless-application-model/blob/master/versions/2016-10-31.md)

<br>

### 3.1. 記述方法

基本的にはドキュメントの通りだが大きく4つのパートに別れる。これはCloudFormationと一緒。

| セクション | 内容 |
| -- | -- |
| Parameters | 外部から得るパラメータを定義 |
| Globals | Resources部で共通する設定をこちらで一括定義 |
| Resources | AWS上へ作成したいリソースを定義<br>AWS SAM記法であることを宣言する場合は ```Type``` へ ```AWS::Serverless::XXXX``` と記述 |
| Outputs | ```sam deploy``` 後に出力したい内容を記載（APIのエンドポイントURLとか） |

<br>

また、よく使う組み込み関数についても以下へ記載する。  
実際にどのような値が返却されるのかはリソース毎にドキュメントへ記載されているので [そちら](https://github.com/aws/serverless-application-model/blob/master/versions/2016-10-31.md) を確認すること。

| 関数名 | 内容 |
| -- | -- |
| !Ref | Prameters/Resourcesセクションで指定した値を参照する<br>```Bucket: !Ref S3Bucket``` |
| !GetAtt | Resourcesの属性（ARNなど）を取得する<br>```Endpoint: !GetAtt HelloWorldFunc.Arn``` |

<br>

以下へいくつか記述例を記載し、その中で注意点についても触れる。

<br>

#### 3.1.1. リソースタイプ

[AWS::Serverless::Function](https://github.com/aws/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction) リソースについての一般的な例。

```yaml
Resources:
HalloWorldFunc:                         # 論理名（色んなところからこの値で呼び出される）
    Type: AWS::Serverless::Function     # AWS SAM形式での記法を宣言
    Properties:
    FunctionName: hellow-world-func     # デプロイされた時のLambdaの関数名
    CodeUri: functions/hello/           # 複数のLambda関数が存在する場合に記載
    Handler: app.lambda_handler
    Environment:
        Variables:
        API_TOKEN: !Ref ApiToken        # 環境変数。Globalsで共通的に指定してもOK
        ROOM_ID: !Ref RoomId
    Events:                             # トリガー。APIなどはここへ記載するだけで作ってくれる
        SubSnsTopic:
        Type: SNS
        Properties:
            Topic: !Ref SnsTopic
```

```Event``` はLambda関数のトリガーを指定する箇所で、ここに記載したリソースも一緒に作成してくれる。  
但しあまり詳細な情報を記述できないので、より細やかな設定を定義したい場合は個別にリソースを定義する。

[AWS::Serverless::SimpleTable](https://github.com/aws/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlesssimpletable) リソース。  
こちらは ```sort key``` が指定できないなどの制約がある為、CloudFormation記法でリソース定義することをお勧めする。

```yaml
# ↓ではパーティションキーしか指定できない

UserTable:
    Type: AWS::Serverless::SimpleTable
    Properties:
        TableName: myTable
        PrimaryKey:
            Name: id
            Type: String

# ↓の方がより詳細に定義できる

UserTable:
    Type: AWS::DynamoDB::Table
    Properties:
        TableName: myTable
        AttributeDefinitions:
        - AttributeName: id
            AttributeType: S
        - AttributeName: username
            AttributeType: S
        KeySchema:
        - AttributeName: subStatus
            KeyType: HASH
        - AttributeName: mailAddress
            KeyType: RANGE
        BillingMode: PAY_PER_REQUEST
```

<br>

#### 3.1.2. Globalsセクション

共通の設定を記述できる。Lambda関数が複数ある時なんかは便利。

```yaml
Globals:
  Function:
    Runtime: python3.8
    Timeout: 900
    ReservedConcurrentExecutions: 2
    EventInvokeConfig:
      MaximumEventAgeInSeconds: 21600
      MaximumRetryAttempts: 0
      DestinationConfig:
        OnSuccess:
          Type: SNS
          Destination: arn:aws:sns:ap-northeast-1:xxxx:mytopic
        OnFailure:
          Type: SNS
          Destination: arn:aws:sns:ap-northeast-1:xxxx:mytopic
```

Globalsセクションで指定できるパラメータは [【公式】Globals Section](https://github.com/aws/serverless-application-model/blob/master/docs/globals.rst) を参照のこと

<br>

#### 3.1.3. Parametersセクション

テンプレートの外部からパラメータを受け取りたい時に定義する。  
注意点として、パラメータ名に ```「 _ 」などの記号は使えない``` ことを認識しておく。

```yaml
Parameters:
  SnsTopic:
    Type: String
・・・
Resources:
  SnsSubscribe:
    Type: AWS::SNS::Subscription
    Properties:
      TopicArn: !Ref SnsTopic
      ・・・
```

<br>

## 4. AWS SAM CLI

SAMテンプレートの作成や、ビルド、デプロイなどを実行するためのコマンド。詳細については以下のドキュメントを参照のこと。

- [【公式】AWS SAM CLI command reference](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-command-reference.html)

ここでは、開発環境の準備〜デプロイまでの手順をザッと紹介する。

<br>

### 4.1. 開発環境の準備

```sam init``` コマンドを実行し、インタラクティブに開発環境を作ることができる。

<br>

### 4.2. ビルド

Lambda関数、SAMテンプレートの準備が完了したらビルドを実施する。

```sh
$ sam build
```

これによりプロジェクトのトップディレクトリ配下へ ```.aws-sam/``` というディレクトリが生成され、Lambda関数が要求するライブラリのダウンロードなどが行われる。
このコマンドはテンプレートファイルが配置されているプロジェクトのトップディレクトリで実行すること。

また、テンプレートファイルの修正、Lambda関数のコード修正を実施するたびにビルドし直す必要がある。

<br>

### 4.3. テスト

ローカル環境でLambda関数を実行し、動作テストを行う。

まずはトリガーとなるイベントを生成する。以下ではSNSイベントドリブンなLambda関数を想定した手順となる。

```sh
$ sam local generate-event sns notification --subject "ALARM" --message "{\"NewStateReason\": \"Threshold Crossed\"}" > event/event.json
```

出来上がったevent.jsonの中身。  

```json
$ cat event/event.json
{
  "Records": [
    {
      "EventSource": "aws:sns",
      "EventVersion": "1.0",
      "EventSubscriptionArn": "arn:aws:sns:us-east-1::ExampleTopic",
      "Sns": {
        "Type": "Notification",
        "MessageId": "95df01b4-ee98-5cb9-9903-4c221d41eb5e",
        "TopicArn": "arn:aws:sns:us-east-1:123456789012:ExampleTopic",
        "Subject": "ALARM",
        "Message": "{\"NewStateReason\": \"Threshold Crossed\"}",
        "Timestamp": "1970-01-01T00:00:00.000Z",
        "SignatureVersion": "1",
        "Signature": "EXAMPLE",
        "SigningCertUrl": "EXAMPLE",
        "UnsubscribeUrl": "EXAMPLE",
        "MessageAttributes": {
          "Test": {
            "Type": "String",
            "Value": "TestString"
          },
          "TestBinary": {
            "Type": "Binary",
            "Value": "TestBinary"
          }
        }
      }
    }
  ]
}
```

ここで注意したいのは「SNSのメッセージ内容によって処理を分岐」のようなLambda関数を作成した場合、重要となるのはSNS全体のフォーマットではなく ```[Sns][Subject]``` と ```[Sns][Message]``` の内容であり、これは実際にSNSからメッセージを受信してみないと内容が分からない。そういった場合には実際にSNSからメッセージを受信して ```event.json``` を作成すべきである。

S3イベントなどは ```generate-event``` で生成できるもので十分。

次に、環境変数の定義ファイルを作成する。テンプレートファイル内で外部参照の記述が無い場合には本手順は必要無い。


```json
$ cat env.json
{
    "Parameters": {
        "API_TOKEN": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "ROOM_ID": "xxxxxxxx"
    }
}
```

複数のLambda関数で参照する環境変数が異なる場合には以下のように記述可能。

```json
$ cat env.json
{
    "functionA": {
        "API_TOKEN": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "ROOM_ID": "xxxxxxxx"
    },
    "functionB": {
        "S3_BUCKET": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
        "S3_PREFIX": "xxxxxxxx"
    }
}
```

ここでの注意点は、上記で定義した変数は ```環境変数``` として読み込まれる点である。CloudFormation風にいうところの ```パラメータ``` でないことに注意（Environment→Variablesへ直接代入される）

パラメータを引き渡したい場合にはコマンド引数に ```--parameter-overrides``` を指定する。

実際に以下のコマンドでLambda関数をローカル環境で呼び出してみる。

```sh
$ sam local invoke -e event/event.json -n env.json HalloWorldFunc
```

上記コマンドを実行すると、ローカルのDocker内へLambdaのエミュレート版コンテナが生成され、Lambda関数をローカル環境で実行してくれる。

<br>

### 4.4. デプロイ

デプロイには以下のコマンドを実行する。初回は ```--guided``` をつけることで、インタラクティブに必要情報を入力できる。

```sh
$ sam deploy --guided
```

テンプレートファイルが外部からパラメータの読み込みを必要とする場合には以下のように ```--parameter-overrides``` を指定する。

```sh
$ sam deploy --guided --parameter-overrides ApiToken=${API_TOKEN} RoomId=${ROOM_ID}
```

初回のデプロイが完了すると、名称を変更していなければ ```samconfig.toml``` というファイルが生成され、以降のデプロイ時には ```--guided``` や ```--parameter-overrides``` を引数に指定する必要は無い。

ここで注意したいのは、```--parameter-overrides``` で指定したのは ```パラメータ``` であって ```環境変数``` では無いことである。  
その為、事前にテンプレートファイル内のParametersセクションで明示的にパラメータを定義しておく必要がある。その際は以下についても注意する。
> 注意点として、パラメータ名に ```「 _ 」などの記号は使えない``` ことを認識しておく。

<br>

### 4.5. 動作確認

デプロイされたLambda関数のログ（CloudWatch Logs）を以下のコマンドで確認可能。

```sh
$ sam logs -t -n HelloWorldFunc
```

```-t``` オプションを付けることでログを ```tail``` できる。
