# Python

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. バージョン](#11-バージョン)
  - [1.2. 環境構築](#12-環境構築)
  - [1.3. プロキシ](#13-プロキシ)
  - [1.4. 構築](#14-構築)
    - [1.4.1. Windows embeddable package](#141-windows-embeddable-package)
- [2. 基本](#2-基本)
  - [2.1. コーディング](#21-コーディング)
  - [2.2. 基本関数](#22-基本関数)
    - [2.2.1. 【print】文字表示](#221-print文字表示)
  - [2.3. 代入とコピー](#23-代入とコピー)
  - [2.4. 文字操作関数](#24-文字操作関数)
- [3. 言語構文](#3-言語構文)
  - [3.1. tuple](#31-tuple)
  - [3.2. list](#32-list)
  - [3.3. dict](#33-dict)
  - [3.4. set](#34-set)
  - [3.5. その他データ型](#35-その他データ型)
- [4. 制御構文](#4-制御構文)
  - [4.1. if](#41-if)
  - [4.2. for](#42-for)
  - [4.3. while/break/continue](#43-whilebreakcontinue)
  - [4.4. range](#44-range)
  - [4.5. with xxx as](#45-with-xxx-as)
  - [4.6. リスト内方式](#46-リスト内方式)
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
- [8. ライブラリ](#8-ライブラリ)
  - [8.1. openpyxl：エクセル操作](#81-openpyxlエクセル操作)
    - [8.1.1. ファイル操作](#811-ファイル操作)
    - [8.1.2. シート操作](#812-シート操作)
    - [8.1.3. セル操作](#813-セル操作)
    - [8.1.4. セルの書式設定（表示形式）](#814-セルの書式設定表示形式)
    - [8.1.5. セルの書式設定（配置）](#815-セルの書式設定配置)
    - [8.1.6. セルの書式設定（フォント）](#816-セルの書式設定フォント)
    - [8.1.7. セルの書式設定（罫線）](#817-セルの書式設定罫線)
    - [8.1.8. セルの書式設定（塗りつぶし）](#818-セルの書式設定塗りつぶし)
  - [8.2. xlwings：エクセル操作](#82-xlwingsエクセル操作)
- [9. フレームワーク](#9-フレームワーク)
  - [9.1. Flask](#91-flask)
    - [9.1.1. 爆速でFlaskスタブサーバを作成／起動する](#911-爆速でflaskスタブサーバを作成起動する)
- [10. その他](#10-その他)
  - [10.1. モジュール](#101-モジュール)
  - [10.2. pythonにおけるMixin](#102-pythonにおけるmixin)
  - [10.3. pythonにおける文字列操作](#103-pythonにおける文字列操作)
  - [10.4. flaskを使ったbackend開発](#104-flaskを使ったbackend開発)
  - [10.5. djangoを使ったbackend開発](#105-djangoを使ったbackend開発)
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

### 1.4. 構築

#### 1.4.1. Windows embeddable package
組み込み用のため、インストール不要で使えるので便利。

1. 公式サイトからzipファイルを入手し、任意の場所で展開する。
2. pipを使えるようにする。
     * pthファイルの修正
       ```
       python312._pth(修正前)
       #import site

       python312._pth(修正後)
       import site
       ```

     * get-pipの入手（PowerShell）
       ```powershell
       # 一時的にTLS1.2を有効化
       > [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12;
       # Wget
       > wget "https://bootstrap.pypa.io/get-pip.py" -O "get-pip.py"
       ```
     * pipインストール
       ```cmd
       > python get-pip.py
       ```

3. ライブラリをインストールする。
    ```cmd
    > python -m pip install wxpython

    > python -m pip freeze
    pillow==10.2.0
    setuptools==69.1.0
    six==1.16.0
    wheel==0.42.0
    wxPython==4.2.1 ★new!
    ```

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

# 要素の間に空白が挿入される
>>> print(1,2)
1 2

# 引数endで末尾を変更できる
>>> print(1,end=',')
1,>>>
```

### 2.3. 代入とコピー

```python
>>> import copy
>>> l_org = [0, 1, [2, 3]]
>>> l_assign = l_org
>>> l_copy = l_org.copy()
>>> l_deepcopy = copy.deepcopy(l_org)
>>> l_org[1] = 100
>>> l_org[2][0] = 200

>>> print(l_org)
[0, 100, [200, 3]]

>>> # assignment(代入)
>>> print(l_assign)
[0, 100, [200, 3]]

>>> # shallow copy(浅いコピー)
>>> print(l_copy)
[0, 1, [200, 3]]

>>> # deep copy(深いコピー)
>>> print(l_deepcopy)
[0, 1, [2, 3]]
```

```python
# multiple assignment(複数同時の代入)
>>> a,b = 0,1
>>> print(a)
0
>>> print(b)
1
```

### 2.4. 文字操作関数
```python
>>> print(word)
Python
>>> len(word)
6
# 最初の文字のインデックスは0
>>> word[0]
'P'
# 最初の文字～2番目まで　※注意　終了値は含まない！
>>> word[:2]
'Py'
# 2番目の文字～最後まで
>>> word[2:]
'thon'
# 最初の文字～後ろから2番目まで
>>> word[:-2]
'Pyth'
```

<br>

## 3. 言語構文

### 3.1. tuple

### 3.2. list
```python
>>> squares
[1, 4, 9, 16, 25]
>>> squares.append(2)
>>> squares
[1, 4, 9, 16, 25, 2]
```

### 3.3. dict
### 3.4. set
### 3.5. その他データ型

<br>

## 4. 制御構文

### 4.1. if
```python
# 基本
>>> x = int(input("数値を入力してください："))
数値を入力してください：32

>>> if x < 0:
...     print("less")
... elif x == 0:
...     print("zero")
... else:
...     print("more")
...
more
```

### 4.2. for
```python
# 基本
>>> words = ['m21', 'c4', 'tell sea i']
>>> for w in words:
...     print(w, len(w))
...
m21 3
c4 2
tell sea i 10
```

```python
# 反復処理の場合はrange関数が便利
>>> for i in range(3):
...     print(i)
...
0
1
2

# 開始値、終了値、増加量も指定できる
>>> for j in range(3,30,5):
...     print(j)
...
3
8
13
18
23
28
```

### 4.3. while/break/continue
### 4.4. range
### 4.5. with xxx as
### 4.6. リスト内方式

<br>

## 5. 関数

### 5.1. 関数の作成

### 5.2. 無名関数

### 5.3. 特殊メソッド(__str__、__repr__など)

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
### 7.1. クラス生成
### 7.2. pythonにおけるカプセル化


<br>

## 8. ライブラリ
### 8.1. openpyxl：エクセル操作
```python
import openpyxl
```

#### 8.1.1. ファイル操作
```python
# 新規作成
wb = openpyxl.Workbook()

# 既存ファイル読み込み
wb = openpyxl.load_workbook('FILEPATH')

# 保存
wb.save('FILEPATH')
```

#### 8.1.2. シート操作
```python
# 新規シート作成（左に追加）
ws = wb.create_sheet(0)
# 新規シート作成（右に追加）
ws = wb.create_sheet()
# 新規シート作成（シート名指定で追加）
ws = wb.create_sheet(title='SHEETNAME')

# シート名から選択
ws = wb.get_sheet_by_name('SHEETNAME')

# アクティブシート選択
ws = wb.active

# シート名変更
ws.title = 'New Title'
```

#### 8.1.3. セル操作
```python
# セル書き込み（セル名指定）
ws['A1'].value = 'nok37'
# セル書き込み（行列指定）
ws.cell(row=2, column=1).value = 'takahana'
# セル書き込み（行列指定　※省略版）
ws.cell(3, 1, 'm21')
```

#### 8.1.4. セルの書式設定（表示形式）
```python
```

#### 8.1.5. セルの書式設定（配置）
```python
from openpyxl.styles import Alignment
ws['A1'].alignment = Alignment(
    wrap_text=False,  # 折り返し改行
    horizontal='general',  # 水平位置
    vertical='bottom'  # 上下位置
)
# vertical  : 縦位置[*1]
# horizontal: 横位置[*1]
# wrap_text : 折り返し改行[True/False]
# *1 
#  general : 標準
#  bottom  :
```

#### 8.1.6. セルの書式設定（フォント）
```python
from openpyxl.styles import Font
ws['A1'].font = Font(
    name='Meiryo UI',
    size=12,
    bold=True,
    italic=False,
    color='FF000000'
)
```

#### 8.1.7. セルの書式設定（罫線）
```python
```

#### 8.1.8. セルの書式設定（塗りつぶし）
```python
```

### 8.2. xlwings：エクセル操作

<br>

## 9. フレームワーク
### 9.1. Flask
#### 9.1.1. 爆速でFlaskスタブサーバを作成／起動する

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

## 10. その他

###  10.1. モジュール
###  10.2. pythonにおけるMixin
###  10.3. pythonにおける文字列操作
###  10.4. flaskを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス
blueprintとルーティング
template(jinja2)
APIサーバとしてJSONレスポンスを返す。
スタティックファイルの扱い
pytestをつかったunitテスト
デプロイ
###  10.5. djangoを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス(django.model)
ルーティング
template
APIサーバとしてJSONレスポンスを返す。(JsonResponse)
ユニットテスト
デプロイ

<br>
