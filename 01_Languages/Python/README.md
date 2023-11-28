# Python

<!-- TOC -->

- [１．設定](#１．設定)
    - [バージョン](#バージョン)
    - [環境構築](#環境構築)
    - [プロキシ](#プロキシ)
- [２．言語構文](#２．言語構文)
    - [tuple](#tuple)
    - [list](#list)
    - [dict](#dict)
    - [set](#set)
    - [その他データ型](#その他データ型)
- [３．制御構文](#３．制御構文)
    - [if/for/while/break/continue](#ifforwhilebreakcontinue)
    - [with xxx as](#with-xxx-as)
    - [リスト内方式](#リスト内方式)
- [４．関数](#４．関数)
    - [関数の作成](#関数の作成)
    - [無名関数](#無名関数)
    - [特殊メソッド(__str__、__repr__など)](#特殊メソッド__str____repr__など)
    - [オリジナル関数](#オリジナル関数)
        - [ログ出力](#ログ出力)
- [５．クラス](#５．クラス)
    - [クラス生成](#クラス生成)
    - [pythonにおけるカプセル化](#pythonにおけるカプセル化)
- [６．フレームワーク](#６．フレームワーク)
    - [Flask](#flask)
        - [爆速でFlaskスタブサーバを作成／起動する](#爆速でflaskスタブサーバを作成／起動する)
- [７．その他](#７．その他)
    - [モジュール](#モジュール)
    - [pythonにおけるMixin](#pythonにおけるmixin)
    - [pythonにおける文字列操作](#pythonにおける文字列操作)
    - [flaskを使ったbackend開発](#flaskを使ったbackend開発)
    - [djangoを使ったbackend開発](#djangoを使ったbackend開発)

<!-- /TOC -->
---
<br>

## １．設定

###  バージョン
python2.X系とpython3.X系

###  環境構築
apt/yum/dnf
pip
virtualenv/virtualenvwrapper

###  プロキシ
set HTTP_PROXY=http://host:port
set HTTP_PROXY=http://user:pass@host:port
set HTTPS_PROXY=https://user:pass@host:port

<br>

## ２．言語構文

###  tuple
###  list
###  dict
###  set
###  その他データ型

<br>

## ３．制御構文

###  if/for/while/break/continue
###  with xxx as
###  リスト内方式

<br>

## ４．関数

###  関数の作成

###  無名関数

###  特殊メソッド(__str__、__repr__など)

### オリジナル関数

#### ログ出力
通常のprintだと即時反映されないため。

```python
def log_print(text):
  print(text, flush=True)
```

<br>

## ５．クラス

###  クラス生成
###  pythonにおけるカプセル化


<br>

## ６．フレームワーク

### Flask

#### 爆速でFlaskスタブサーバを作成／起動する

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

## ７．その他

###  モジュール
###  pythonにおけるMixin
###  pythonにおける文字列操作
###  flaskを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス
blueprintとルーティング
template(jinja2)
APIサーバとしてJSONレスポンスを返す。
スタティックファイルの扱い
pytestをつかったunitテスト
デプロイ
###  djangoを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス(django.model)
ルーティング
template
APIサーバとしてJSONレスポンスを返す。(JsonResponse)
ユニットテスト
デプロイ

<br>
