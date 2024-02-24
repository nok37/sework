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
  - [2.2. 関数](#22-関数)
    - [2.2.1. 【dir】オブジェクトの属性をリストで取得](#221-dirオブジェクトの属性をリストで取得)
    - [2.2.2. 【print】文字列出力](#222-print文字列出力)
  - [2.3. 代入とコピー](#23-代入とコピー)
  - [2.4. 文字操作](#24-文字操作)
  - [2.5. 数値](#25-数値)
  - [2.6. 配列](#26-配列)
    - [2.6.1. tuple ()](#261-tuple-)
    - [2.6.2. list \[\]](#262-list-)
    - [2.6.3. dict](#263-dict)
    - [2.6.4. set {}](#264-set-)
- [3. 制御構文](#3-制御構文)
  - [3.1. if](#31-if)
  - [3.2. for](#32-for)
  - [3.3. while/break/continue](#33-whilebreakcontinue)
  - [3.4. with xxx as](#34-with-xxx-as)
  - [3.5. リスト内方式](#35-リスト内方式)
- [4. 関数](#4-関数)
  - [4.1. 関数の作成](#41-関数の作成)
  - [4.2. 無名関数](#42-無名関数)
  - [4.3. 特殊メソッド(__str__、\_\_repr\_\_など)](#43-特殊メソッドstr__repr__など)
  - [4.4. オリジナル関数](#44-オリジナル関数)
    - [4.4.1. ログ出力](#441-ログ出力)
- [5. サンプル集](#5-サンプル集)
  - [5.1. スクリプトパスの取得](#51-スクリプトパスの取得)
- [6. クラス](#6-クラス)
  - [6.1. クラス生成](#61-クラス生成)
  - [6.2. pythonにおけるカプセル化](#62-pythonにおけるカプセル化)
- [7. ライブラリ](#7-ライブラリ)
  - [7.1. 【csv】csvファイルの読み込み](#71-csvcsvファイルの読み込み)
  - [7.2. 【openpyxl】エクセル操作（基本）](#72-openpyxlエクセル操作基本)
  - [7.3. 【xlwings】エクセル操作（開いて図形追加）](#73-xlwingsエクセル操作開いて図形追加)
- [8. フレームワーク](#8-フレームワーク)
  - [8.1. Flask](#81-flask)
    - [8.1.1. 爆速でFlaskスタブサーバを作成／起動する](#811-爆速でflaskスタブサーバを作成起動する)
- [9. その他](#9-その他)
  - [9.1. モジュール](#91-モジュール)
  - [9.2. pythonにおけるMixin](#92-pythonにおけるmixin)
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
       > wget 'https://bootstrap.pypa.io/get-pip.py' -O 'get-pip.py'
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


### 2.2. 関数

#### 2.2.1. 【dir】オブジェクトの属性をリストで取得
```python
>>> import os
>>> dir(os)
['mkdir', 'rename'...など]
```

#### 2.2.2. 【print】文字列出力

```python
# シングルクォート ('...') とダブルクォート ('...') に違いはない
>>> print('hello!')
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

>>> # 代入(assignment)　⇒オリジナル更新を反映
>>> l_assign = l_org
>>> l_org[1] = 100
>>> l_org[2][0] = 200
>>> print(l_assign)
[0, 100, [200, 3]]

>>> # 浅いコピー(shallow copy)　⇒オリジナル更新は一部反映
>>> l_copy = l_org.copy()
>>> l_org[1] = 100
>>> l_org[2][0] = 200
>>> print(l_copy)
[0, 1, [200, 3]]

>>> # 深いコピー(deep copy)　⇒オリジナル更新は反映されない
>>> l_deepcopy = copy.deepcopy(l_org)
>>> l_org[1] = 100
>>> l_org[2][0] = 200
>>> print(l_deepcopy)
[0, 1, [2, 3]]
```

```python
# 複数同時の代入(multiple assignment)
>>> a,b = 0,1
>>> print(a)
0
>>> print(b)
1
```

### 2.4. 文字操作
```python
>>> print(word)
Python

# 文字列の長さを取得
>>> len(word)
6

# 最初の文字のインデックスは0
>>> word[0]
'P'

# 最初の文字～インデックス2まで（終端は含まない）
>>> word[:2]
'Py'

# インデックス2～最後の文字
>>> word[2:]
'thon'

# 最初の文字～インデックスから2番目
>>> word[:-2]
'Pyth'
```
### 2.5. 数値

### 2.6. 配列
#### 2.6.1. tuple ()
```python
>>> tuple_num = (1, 2, 3)

# 要素のアクセス
>>> print(tuple_num[0])
1
>>> print(tuple_num[:2])
(1, 2)
```

```python
# tupleはイミュータブル（更新不可）
>>> tuple_num[0] = 100
TypeError: 'tuple' object does not support item assignment

>>> tuple_num.append(100)
AttributeError: 'tuple' object has no attribute 'append'

# 連結して新しいオブジェクト作成は可能
>>> tuple_num + tuple_num
(1, 2, 3, 1, 2, 3)
```

```python
# tips
# listと比較してメモリ使用量が少ない
>>> from sys import getsizeof
>>> getsizeof([1, 4, 9, 16, 25])
104
>>> getsizeof((1, 4, 9, 16, 25))
80
```

#### 2.6.2. list []
```python
>>> list_num = [1, 4, 9, 16, 25]

# 要素のアクセス
>>> list_num[2]
9

# 要素のインデックスも取得できる
>>> for idx,num in enumerate(list_num):
...     print(idx,num)
...
0 1
1 4
2 9
3 16
4 25
```

```python
# 要素の追加
>>> list_num.append(2)
>>> list_num
[1, 4, 9, 16, 25, 2]
```

#### 2.6.3. dict
```python
>>> dict_profile  = {'name': 'nok37', 'age': 28, 'city': 'Gunma'}

# 要素のアクセス（キーを使用）
>>> dict_profile['name']
'nok37'
```

```python
# キーの取得
>>> dict_profile.keys()
dict_keys(['name', 'age', 'city'])

# 値の取得
>>> dict_profile.values()
dict_values(['nok37', 28, 'Gunma'])
```

#### 2.6.4. set {}
```python
# setでは重複値は無視され、生成時の順序は保持されない
>>> set_num = {1, 9, 9, 4, 6, 3}
>>> set_num
{1, 3, 4, 6, 9}
```

```python
# 要素の追加
>>> set_num.add(3)
>>> set_num.add(7)
>>> set_num
{1, 3, 4, 6, 7, 9}
```

```python
>>> s1 = {1, 9, 9, 4, 6, 3}
>>> s2 = {1, 9, 9, 5, 1, 2, 1, 4}

# 和集合
>>> s1 | s2
{1, 2, 3, 4, 5, 6, 9}
>>> s1.union(s2)
{1, 2, 3, 4, 5, 6, 9}


# 積集合
>>> s1 & s2
{1, 4, 9}
>>> s1.intersection(s2)
{1, 4, 9}

# 差集合
>>> s1 - s2
{3, 6}
>>> s1.difference(s2)
{3, 6}

# 対称差集合
>>> s1 ^ s2
{2, 3, 5, 6}
>>> s1.symmetric_difference(s2)
{2, 3, 5, 6}
```

<br>

## 3. 制御構文

### 3.1. if
```python
# 基本
>>> x = int(input('数値を入力してください：'))
数値を入力してください：32

>>> if x < 0:
...     print('less')
... elif x == 0:
...     print('zero')
... else:
...     print('more')
...
more
```

### 3.2. for
```python
# 配列でループ
>>> words = ['m21', 'c4', 'tel sea i']
>>> for w in words:
...     print(w, len(w))
...
m21 3
c4 2
tel sea i 10
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
>>> for j in range(3, 30,5):
...     print(j)
...
3
8
13
18
23
28
```

### 3.3. while/break/continue
### 3.4. with xxx as
### 3.5. リスト内方式

<br>

## 4. 関数

### 4.1. 関数の作成

### 4.2. 無名関数

### 4.3. 特殊メソッド(__str__、__repr__など)

### 4.4. オリジナル関数

#### 4.4.1. ログ出力
通常のprintだと即時反映されないため。

```python
def log_print(text):
  print(text, flush=True)
```

<br>

## 5. サンプル集

### 5.1. スクリプトパスの取得
```python
import os
print(os.path.dirname(Cookies))
```


<br>

## 6. クラス
### 6.1. クラス生成
### 6.2. pythonにおけるカプセル化


<br>

## 7. ライブラリ
### 7.1. 【csv】csvファイルの読み込み
```python
import csv

# ファイルオープン
csv_file = open('./my.csv', 'r', encoding='ms932')

# ファイルクローズ
csv_file.close()
```

```python
# リスト形式で読み込み
>>> f = csv.reader(
...     csv_file,
...     delimiter=',',
...     doublequote=True,
...     lineterminator='\r\n',
...     quotechar="'",
...     skipinitialspace=True
...     )

# 値の取得
>>> next(f)
['nok37', 'takahana']
>>> next(f)
['m21', 'matsuis']
>>> next(f)
StopIteration # ここで終わり

# 値を取得してリスト作成
>>> list = []
>>> for row in f:
...     list.append(row)
...
>>> list
[['nok37', 'takahana'], ['m21', 'matsuis']]
```

```python
# 辞書形式で読み込み
>>> f = csv.DictReader(
...     csv_file,
...     delimiter=',',
...     doublequote=True,
...     lineterminator='\r\n',
...     quotechar="'",
...     skipinitialspace=True
...     )

# 値を辞書形式で取得
>>> for row in f:
...     print(row)
...
{'name': 'nok37', 'adomain': 'takahana'}
{'name': 'm21', 'adomain': 'matsuis'}
```

### 7.2. 【openpyxl】エクセル操作（基本）
  ```python
  import openpyxl
  ```

* ファイル操作
  ```python
  # 新規作成
  wb = openpyxl.Workbook()

  # 既存ファイル読み込み
  wb = openpyxl.load_workbook('myfile.xlsx')

  # 保存
  wb.save('myfile.xlsx')
  ```

* シート操作
  ```python
  # 新規シート作成（左に追加）
  ws = wb.create_sheet(0)
  # 新規シート作成（右に追加）
  ws = wb.create_sheet()
  # 新規シート作成（シート名指定で追加）
  ws = wb.create_sheet(title='mysheet')

  # シート名から選択
  ws = wb.get_sheet_by_name('mysheet')

  # アクティブシート選択
  ws = wb.active

  # シート名変更
  ws.title = 'newsheet'
  ```

* セル操作
  ```python
  # セル書き込み（セル名指定）
  ws['A1'].value = 'nok37'
  # セル書き込み（行列指定）
  ws.cell(row=2, column=1).value = 'takahana'
  # セル書き込み（行列指定　※省略版）
  ws.cell(3, 1, 'm21')
  ```

* セルの書式設定（表示形式）
  ```python
  ```

* セルの書式設定（配置）
  ```python
  from openpyxl.styles import Alignment
  ws['A1'].alignment = Alignment(
      # 横位置
      horizontal='center',
      # 縦位置
      vertical='bottom',
      # 方向
      text_rotation=0,
      # 折り返して全体を表示
      wrap_text=False,
      # 縮小して全体表示
      shrink_to_fit=False,
      # インデント
      indent=0
  )
  ```

  | 位置指定 | 内容 |
  | --- | --- |
  | general　| 標準 |
  | bottom   | 下詰め |
  | center   | 中央揃え |

* セルの書式設定（フォント）
  ```python
  from openpyxl.styles import Font
  ws['A1'].font = Font(
      name='Meiryo UI',
      bold=True,
      italic=False,
      size=12,
      #下線
      #文字飾り
      color='FF000000'
  )
  ```

* セルの書式設定（罫線）
  ```python
  ```

* セルの書式設定（塗りつぶし）
  ```python
  ```

### 7.3. 【xlwings】エクセル操作（開いて図形追加）

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
    * Serving Flask app '__main__' (lazy loading)
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

<br>
