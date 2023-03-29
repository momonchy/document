# AWS Organizations 管理外な AWS アカウントを AWS SSO へ登録する

通常、AWS SSO でマルチアカウント認証/認可を実現する場合、まずは AWS Organizations で組織を作成し、その組織内へ AWS アカウントを登録し、組織の管理下へ置く必要があります。

AWS アカウントを AWS Organizations へ登録しなくても AWS SSO を利用してマルチアカウント認証/認可を実現する方法について手順を解説します。

<br>

## 利用する機能

AWS SSO Application Assignments の「External AWS Account」というアプリケーションを利用します。

<br>

## 作業の流れ

本手順では、AWS SSO が有効化されている AWS アカウントを「**from SSO**」、SSO される側の AWS アカウントを「**to SSO**」と表現します。

from SSO

1. AWS SSO 上で External AWS Account を追加
2. SAML metadata ファイルをダウンロード

to SSO

3. IAM 上で Identity providers を登録（SAML metadata ファイルアップロード）
4. Assume させる IAM Role を作成
5. 作成した IAM Role へ許可したい適切な IAM Policy をアサイン

from SSO

6. External AWS Account へ Attribute mapping を追加
7. External AWS Account へ SSO ユーザ（or グループ）を登録

<br>

## 手順

#### from SSO

1. AWS SSO からアプリケーション「External AWS Account」を追加<br>
![1](images/unmanaged_account_register_to_sso_1.drawio.svg)
![2](images/unmanaged_account_register_to_sso_2.drawio.svg)

2. SAML metadata ファイルをダウンロードし、アプリケーションを追加<br>
![3](images/unmanaged_account_register_to_sso_3.drawio.svg)

<br>

#### to SSO

<br>

#### from SSO

