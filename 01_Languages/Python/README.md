# Python

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. バージョン](#11-バージョン)
  - [1.2. 環境構築](#12-環境構築)
  - [1.3. プロキシ](#13-プロキシ)
- [2. 基本](#2-基本)
  - [2.1. コーディング](#21-コーディング)
  - [2.2. 基本関数](#22-基本関数)
    - [2.2.1. 【print】文字表示](#221-print文字表示)
  - [2.3. 文字操作関数](#23-文字操作関数)
- [3. 言語構文](#3-言語構文)
  - [3.1. tuple](#31-tuple)
  - [3.2. list](#32-list)
  - [3.3. dict](#33-dict)
  - [3.4. set](#34-set)
  - [3.5. その他データ型](#35-その他データ型)
- [4. 制御構文](#4-制御構文)
  - [4.1. if/for/while/break/continue](#41-ifforwhilebreakcontinue)
  - [4.2. with xxx as](#42-with-xxx-as)
  - [4.3. リスト内方式](#43-リスト内方式)
- [5. 関数](#5-関数)
  - [5.1. 関数の作成](#51-関数の作成)
  - [5.2. 無名関数](#52-無名関数)
  - [5.3. 特殊メソッド(__str__、\_\_repr\_\_など)](#53-特殊メソッドstr__repr__など)
  - [5.4. オリジナル関数](#54-オリジナル関数)
    - [5.4.1. ログ出力](#541-ログ出力)
- [6. サンプル集](#6-サンプル集)
  - [6.1. スクリプトパスの取得](#61-スクリプトパスの取得)
- [7. クラス](#7-クラス)
  - [7.1. クラス生成](#71-クラス生成)
  - [7.2. pythonにおけるカプセル化](#72-pythonにおけるカプセル化)
- [8. フレームワーク](#8-フレームワーク)
  - [8.1. Flask](#81-flask)
    - [8.1.1. 爆速でFlaskスタブサーバを作成／起動する](#811-爆速でflaskスタブサーバを作成起動する)
- [9. その他](#9-その他)
  - [9.1. モジュール](#91-モジュール)
  - [9.2. pythonにおけるMixin](#92-pythonにおけるmixin)
  - [9.3. pythonにおける文字列操作](#93-pythonにおける文字列操作)
  - [9.4. flaskを使ったbackend開発](#94-flaskを使ったbackend開発)
  - [9.5. djangoを使ったbackend開発](#95-djangoを使ったbackend開発)
---
<br>
<!-- /TOC -->

## 1. 設定

###  1.1. バージョン
* python2.X系<br>

* python3.X系<br>
  ※unix系ではpython2.X系と衝突しないためにpythonという名前ではインストールされない。

###  1.2. 環境構築
* apt/yum/dnf
* pip
* virtualenv/virtualenvwrapper

###  1.3. プロキシ
set HTTP_PROXY=http://host:port
set HTTP_PROXY=http://user:pass@host:port
set HTTPS_PROXY=https://user:pass@host:port

<br>

## 2. 基本

### 2.1. コーディング
デフォルトでは、UTF-8でエンコードされる。
デフォルトエンコーディング以外のエンコーディングを使用する場合は先頭行で明記する。（シェバンがある場合はその次の行）

```python
#!/usr/bin/env python3
# -*- coding: cp1252 -*-
```

### 2.2. 基本関数

#### 2.2.1. 【print】文字表示

```python
# シングルクォート ('...') とダブルクォート ("...") に違いはない
>>> print("hello!")
hello!
>>> print('hello!')
hello!
```

### 2.3. 文字操作関数

```python
>>> print(word)
Python
>>> len(word)
6
# 最初から2番目まで+2番目から最後まで
>>> word[:2] + word[2:]
'Python'
# 最初から後ろから2番目まで
>>> word[:-2]
'Pyth'
```

<br>

## 3. 言語構文

###  3.1. tuple

###  3.2. list
```python
squares = [1, 4, 9, 16, 25]
```

###  3.3. dict
###  3.4. set
###  3.5. その他データ型

<br>

## 4. 制御構文

###  4.1. if/for/while/break/continue
###  4.2. with xxx as
###  4.3. リスト内方式

<br>

## 5. 関数

###  5.1. 関数の作成

###  5.2. 無名関数

###  5.3. 特殊メソッド(__str__、__repr__など)

### 5.4. オリジナル関数

#### 5.4.1. ログ出力
通常のprintだと即時反映されないため。

```python
def log_print(text):
  print(text, flush=True)
```

<br>

## 6. サンプル集

### 6.1. スクリプトパスの取得
```python
import os
print(os.path.dirname(Cookies))
```


<br>

## 7. クラス

###  7.1. クラス生成
###  7.2. pythonにおけるカプセル化


<br>

## 8. フレームワーク

### 8.1. Flask

#### 8.1.1. 爆速でFlaskスタブサーバを作成／起動する

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

## 9. その他

###  9.1. モジュール
###  9.2. pythonにおけるMixin
###  9.3. pythonにおける文字列操作
###  9.4. flaskを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス
blueprintとルーティング
template(jinja2)
APIサーバとしてJSONレスポンスを返す。
スタティックファイルの扱い
pytestをつかったunitテスト
デプロイ
###  9.5. djangoを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス(django.model)
ルーティング
template
APIサーバとしてJSONレスポンスを返す。(JsonResponse)
ユニットテスト
デプロイ

<br>
