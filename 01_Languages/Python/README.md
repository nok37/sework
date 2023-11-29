# Python

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. バージョン](#11-バージョン)
  - [1.2. 環境構築](#12-環境構築)
  - [1.3. プロキシ](#13-プロキシ)
- [2. 言語構文](#2-言語構文)
  - [2.1. tuple](#21-tuple)
  - [2.2. list](#22-list)
  - [2.3. dict](#23-dict)
  - [2.4. set](#24-set)
  - [2.5. その他データ型](#25-その他データ型)
- [3. 制御構文](#3-制御構文)
  - [3.1. if/for/while/break/continue](#31-ifforwhilebreakcontinue)
  - [3.2. with xxx as](#32-with-xxx-as)
  - [3.3. リスト内方式](#33-リスト内方式)
- [4. 関数](#4-関数)
  - [4.1. 関数の作成](#41-関数の作成)
  - [4.2. 無名関数](#42-無名関数)
  - [4.3. 特殊メソッド(__str__、\_\_repr\_\_など)](#43-特殊メソッドstr__repr__など)
  - [4.4. オリジナル関数](#44-オリジナル関数)
    - [4.4.1. ログ出力](#441-ログ出力)
- [5. クラス](#5-クラス)
  - [5.1. クラス生成](#51-クラス生成)
  - [5.2. pythonにおけるカプセル化](#52-pythonにおけるカプセル化)
- [6. フレームワーク](#6-フレームワーク)
  - [6.1. Flask](#61-flask)
    - [6.1.1. 爆速でFlaskスタブサーバを作成／起動する](#611-爆速でflaskスタブサーバを作成起動する)
- [7. その他](#7-その他)
  - [7.1. モジュール](#71-モジュール)
  - [7.2. pythonにおけるMixin](#72-pythonにおけるmixin)
  - [7.3. pythonにおける文字列操作](#73-pythonにおける文字列操作)
  - [7.4. flaskを使ったbackend開発](#74-flaskを使ったbackend開発)
  - [7.5. djangoを使ったbackend開発](#75-djangoを使ったbackend開発)
---
<br>
<!-- /TOC -->

## 1. 設定

###  1.1. バージョン
python2.X系とpython3.X系

###  1.2. 環境構築
apt/yum/dnf
pip
virtualenv/virtualenvwrapper

###  1.3. プロキシ
set HTTP_PROXY=http://host:port
set HTTP_PROXY=http://user:pass@host:port
set HTTPS_PROXY=https://user:pass@host:port

<br>

## 2. 言語構文

###  2.1. tuple
###  2.2. list
###  2.3. dict
###  2.4. set
###  2.5. その他データ型

<br>

## 3. 制御構文

###  3.1. if/for/while/break/continue
###  3.2. with xxx as
###  3.3. リスト内方式

<br>

## 4. 関数

###  4.1. 関数の作成

###  4.2. 無名関数

###  4.3. 特殊メソッド(__str__、__repr__など)

### 4.4. オリジナル関数

#### 4.4.1. ログ出力
通常のprintだと即時反映されないため。

```python
def log_print(text):
  print(text, flush=True)
```

<br>

## 5. クラス

###  5.1. クラス生成
###  5.2. pythonにおけるカプセル化


<br>

## 6. フレームワーク

### 6.1. Flask

#### 6.1.1. 爆速でFlaskスタブサーバを作成／起動する

1. Swagger EditorでAPIを定義する　⇒例
2. コード自動生成で「Flask」を選択する
3. httpsの場合以下のように編集する  
    python-flask-server\swagger_server\__main__.py

    ```python
    #!/usr/bin/env python3

    import connexion
    import ssl
    from swagger_server import encoder


    def main():
        app = connexion.App(__name__, specification_dir='./swagger/')
        app.app.json_encoder = encoder.JSONEncoder
        app.add_api('swagger.yaml', arguments={'title': 'Swagger alpha-kinpo'})
        context = ssl.SSLContext(ssl.PROTOCOL_TLSv1_2)
        context.load_cert_chain('server.crt', 'server.key')
        app.run(host='localhost', port=8080, ssl_context=context)


    if __name__ == '__main__':
        main()    
    ```

4. 必要モジュールの設定  
    python-flask-server\requirements.txt
    ```python
    attrs==21.2.0
    certifi==2021.10.8
    cffi==1.15.0
    charset-normalizer==2.0.7
    click==8.0.3
    clickclick==20.10.2
    colorama==0.4.4
    connexion==1.1.15
    cryptography==36.0.0
    Flask==1.1.2
    Flask-Cors==3.0.10
    idna==3.3
    importlib-metadata==4.8.1
    importlib-resources==5.4.0
    inflection==0.5.1
    isodate==0.6.0
    itsdangerous==2.0.1
    Jinja2==3.0.2
    jsonschema==3.0.1
    MarkupSafe==2.0.1
    openapi-schema-validator==0.1.5
    openapi-spec-validator==0.3.1
    pycparser==2.21
    pyOpenSSL==21.0.0
    pyrsistent==0.18.0
    python-dateutil==2.6.0
    PyYAML==6.0
    requests==2.26.0
    six==1.16.0
    swagger-spec-validator==2.7.4
    swagger-ui-bundle==0.0.9
    typing-extensions==3.10.0.2
    urllib3==1.25.11
    Werkzeug==0.16.1
    zipp==3.6.0
    ```

5. モジュールのインストール
    ```bash
    $ pip install -r requirements.txt
    ```

6. 起動する。

    ```bash
    $ python -m swagger_server
    * Serving Flask app "__main__" (lazy loading)
    * Environment: production
    WARNING: This is a development server. Do not use it in a production deployment.
    Use a production WSGI server instead.
    * Debug mode: off
    * Running on https://localhost:8080/ (Press CTRL+C to quit)
    ```

<br>

## 7. その他

###  7.1. モジュール
###  7.2. pythonにおけるMixin
###  7.3. pythonにおける文字列操作
###  7.4. flaskを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス
blueprintとルーティング
template(jinja2)
APIサーバとしてJSONレスポンスを返す。
スタティックファイルの扱い
pytestをつかったunitテスト
デプロイ
###  7.5. djangoを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス(django.model)
ルーティング
template
APIサーバとしてJSONレスポンスを返す。(JsonResponse)
ユニットテスト
デプロイ

<br>
