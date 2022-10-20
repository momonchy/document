# より便利で使いやすくなった AWS Lambda と AWS Step Functions のアップデート情報 (T3-2)

日時：2022/10/20　11:40 〜 12:10
資料：[登壇資料_T3-2_より便利で使いやすくなった_AWS_Lambda_と_AWS_Step_Functions_のアップデート情報](https://contents-s3-bucket.s3.ap-northeast-1.amazonaws.com/documents/aws/202210_MODERN_APPLICATIONS_EDITION/%E7%99%BB%E5%A3%87%E8%B3%87%E6%96%99_T3-2_%E3%82%88%E3%82%8A%E4%BE%BF%E5%88%A9%E3%81%A6%E3%82%99%E4%BD%BF%E3%81%84%E3%82%84%E3%81%99%E3%81%8F%E3%81%AA%E3%81%A3%E3%81%9F_AWS_Lambda_%E3%81%A8_AWS_Step_Functions_%E3%81%AE%E3%82%A2%E3%83%83%E3%83%95%E3%82%9A%E3%83%86%E3%82%99%E3%83%BC%E3%83%88%E6%83%85%E5%A0%B1.pdf)
キーワード: 

<br>

## AWS Lambda アップデート

Function URLs のリリース
- 任意の関数にHTTPSエンドポイントを追加可能
    - Function URLをエイリアスへ紐づけることを推奨
- IAM認証をサポート
    - IAMユーザ、IAM Role
        - InvokeFunction Actionを許可
    - SigV4署名付きリクエスト
        - AWS SDKから呼び出せば実装する必要無い
- API Gatewayとの比較

    || Lambda | API Gateway |
    | -- | -- | -- |
    | HTTP | No | No |
    | HTTPS | Yes | Yes |
    | 認証認可 | IAM認証 | IAM,Cognito |
    | ペイロード | 6MB | 6MB |
    | タイムアウト | 最大15分 | 最大29秒 |
    | SDK | No | Yes |
    | WAF | No | Yes |

ABAC のリリース
- 接続元(Principal) の属性情報で認証可能
- 主に IAM ユーザへセットしたタグベースで実施
- { "project": "AA" }: "Allow" など
