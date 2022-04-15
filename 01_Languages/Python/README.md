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
<!-- NEXT INDENT -->

<a id="markdown-１．設定" name="１．設定"></a>
## １．設定

<a id="markdown-バージョン" name="バージョン"></a>
###  バージョン
python2.X系とpython3.X系

<a id="markdown-環境構築" name="環境構築"></a>
###  環境構築
apt/yum/dnf
pip
virtualenv/virtualenvwrapper

<a id="markdown-プロキシ" name="プロキシ"></a>
###  プロキシ
set HTTP_PROXY=http://host:port
set HTTP_PROXY=http://user:pass@host:port
set HTTPS_PROXY=https://user:pass@host:port

<br>
<!-- NEXT INDENT -->

<a id="markdown-２．言語構文" name="２．言語構文"></a>
## ２．言語構文

<a id="markdown-tuple" name="tuple"></a>
###  tuple
<a id="markdown-list" name="list"></a>
###  list
<a id="markdown-dict" name="dict"></a>
###  dict
<a id="markdown-set" name="set"></a>
###  set
<a id="markdown-その他データ型" name="その他データ型"></a>
###  その他データ型

<br>
<!-- NEXT INDENT -->

<a id="markdown-３．制御構文" name="３．制御構文"></a>
## ３．制御構文

<a id="markdown-ifforwhilebreakcontinue" name="ifforwhilebreakcontinue"></a>
###  if/for/while/break/continue
<a id="markdown-with-xxx-as" name="with-xxx-as"></a>
###  with xxx as
<a id="markdown-リスト内方式" name="リスト内方式"></a>
###  リスト内方式

<br>
<!-- NEXT INDENT -->

<a id="markdown-４．関数" name="４．関数"></a>
## ４．関数

<a id="markdown-関数の作成" name="関数の作成"></a>
###  関数の作成

<a id="markdown-無名関数" name="無名関数"></a>
###  無名関数

<a id="markdown-特殊メソッド__str____repr__など" name="特殊メソッド__str____repr__など"></a>
###  特殊メソッド(__str__、__repr__など)

<a id="markdown-オリジナル関数" name="オリジナル関数"></a>
### オリジナル関数

<a id="markdown-ログ出力" name="ログ出力"></a>
#### ログ出力
通常のprintだと即時反映されないため。

```python
def log_print(text):
  print(text, flush=True)
```

<br>
<!-- NEXT INDENT -->

<a id="markdown-５．クラス" name="５．クラス"></a>
## ５．クラス

<a id="markdown-クラス生成" name="クラス生成"></a>
###  クラス生成
<a id="markdown-pythonにおけるカプセル化" name="pythonにおけるカプセル化"></a>
###  pythonにおけるカプセル化


<br>
<!-- NEXT INDENT -->

<a id="markdown-６．フレームワーク" name="６．フレームワーク"></a>
## ６．フレームワーク

<a id="markdown-flask" name="flask"></a>
### Flask

<a id="markdown-爆速でflaskスタブサーバを作成／起動する" name="爆速でflaskスタブサーバを作成／起動する"></a>
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
<!-- NEXT INDENT -->

<a id="markdown-７．その他" name="７．その他"></a>
## ７．その他

<a id="markdown-モジュール" name="モジュール"></a>
###  モジュール
<a id="markdown-pythonにおけるmixin" name="pythonにおけるmixin"></a>
###  pythonにおけるMixin
<a id="markdown-pythonにおける文字列操作" name="pythonにおける文字列操作"></a>
###  pythonにおける文字列操作
<a id="markdown-flaskを使ったbackend開発" name="flaskを使ったbackend開発"></a>
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
<a id="markdown-djangoを使ったbackend開発" name="djangoを使ったbackend開発"></a>
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
<!-- NEXT INDENT -->