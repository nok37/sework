# Python

## 目次
<!-- TOC -->

- [１．設定](#１．設定)
    - [◆ バージョン](#◆-バージョン)
    - [◆ 環境構築](#◆-環境構築)
    - [◆ プロキシ](#◆-プロキシ)
- [２．言語構文](#２．言語構文)
    - [◆ tuple](#◆-tuple)
    - [◆ list](#◆-list)
    - [◆ dict](#◆-dict)
    - [◆ set](#◆-set)
    - [◆ その他データ型](#◆-その他データ型)
- [３．制御構文](#３．制御構文)
    - [◆ if/for/while/break/continue](#◆-ifforwhilebreakcontinue)
    - [◆ with xxx as](#◆-with-xxx-as)
    - [◆ リスト内方式](#◆-リスト内方式)
- [４．関数](#４．関数)
    - [◆ 関数の作成](#◆-関数の作成)
    - [◆ 無名関数](#◆-無名関数)
    - [◆ 特殊メソッド(__str__、__repr__など)](#◆-特殊メソッド__str____repr__など)
- [５．クラス](#５．クラス)
    - [◆ クラス生成](#◆-クラス生成)
    - [◆ pythonにおけるカプセル化](#◆-pythonにおけるカプセル化)
- [６．その他](#６．その他)
    - [◆ モジュール](#◆-モジュール)
    - [◆ pythonにおけるMixin](#◆-pythonにおけるmixin)
    - [◆ pythonにおける文字列操作](#◆-pythonにおける文字列操作)
    - [◆ flaskを使ったbackend開発](#◆-flaskを使ったbackend開発)
    - [◆ djangoを使ったbackend開発](#◆-djangoを使ったbackend開発)

<!-- /TOC -->
<br>


<a id="markdown-１．設定" name="１．設定"></a>
### １．設定
---
<a id="markdown-◆-バージョン" name="◆-バージョン"></a>
#### ◆ バージョン
python2.X系とpython3.X系

<a id="markdown-◆-環境構築" name="◆-環境構築"></a>
#### ◆ 環境構築
apt/yum/dnf
pip
virtualenv/virtualenvwrapper

<a id="markdown-◆-プロキシ" name="◆-プロキシ"></a>
#### ◆ プロキシ
set HTTP_PROXY=http://host:port
set HTTP_PROXY=http://user:pass@host:port
set HTTPS_PROXY=https://user:pass@host:port

<br>

<a id="markdown-２．言語構文" name="２．言語構文"></a>
### ２．言語構文
---
<a id="markdown-◆-tuple" name="◆-tuple"></a>
#### ◆ tuple
<a id="markdown-◆-list" name="◆-list"></a>
#### ◆ list
<a id="markdown-◆-dict" name="◆-dict"></a>
#### ◆ dict
<a id="markdown-◆-set" name="◆-set"></a>
#### ◆ set
<a id="markdown-◆-その他データ型" name="◆-その他データ型"></a>
#### ◆ その他データ型

<br>

<a id="markdown-３．制御構文" name="３．制御構文"></a>
### ３．制御構文
---
<a id="markdown-◆-ifforwhilebreakcontinue" name="◆-ifforwhilebreakcontinue"></a>
#### ◆ if/for/while/break/continue
<a id="markdown-◆-with-xxx-as" name="◆-with-xxx-as"></a>
#### ◆ with xxx as
<a id="markdown-◆-リスト内方式" name="◆-リスト内方式"></a>
#### ◆ リスト内方式

<br>

<a id="markdown-４．関数" name="４．関数"></a>
### ４．関数
---
<a id="markdown-◆-関数の作成" name="◆-関数の作成"></a>
#### ◆ 関数の作成
<a id="markdown-◆-無名関数" name="◆-無名関数"></a>
#### ◆ 無名関数
<a id="markdown-◆-特殊メソッド__str____repr__など" name="◆-特殊メソッド__str____repr__など"></a>
#### ◆ 特殊メソッド(__str__、__repr__など)

<br>

<a id="markdown-５．クラス" name="５．クラス"></a>
### ５．クラス
---
<a id="markdown-◆-クラス生成" name="◆-クラス生成"></a>
#### ◆ クラス生成
<a id="markdown-◆-pythonにおけるカプセル化" name="◆-pythonにおけるカプセル化"></a>
#### ◆ pythonにおけるカプセル化

<br>

<a id="markdown-６．その他" name="６．その他"></a>
### ６．その他
---
<a id="markdown-◆-モジュール" name="◆-モジュール"></a>
#### ◆ モジュール
<a id="markdown-◆-pythonにおけるmixin" name="◆-pythonにおけるmixin"></a>
#### ◆ pythonにおけるMixin
<a id="markdown-◆-pythonにおける文字列操作" name="◆-pythonにおける文字列操作"></a>
#### ◆ pythonにおける文字列操作
<a id="markdown-◆-flaskを使ったbackend開発" name="◆-flaskを使ったbackend開発"></a>
#### ◆ flaskを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス
blueprintとルーティング
template(jinja2)
APIサーバとしてJSONレスポンスを返す。
スタティックファイルの扱い
pytestをつかったunitテスト
デプロイ
<a id="markdown-◆-djangoを使ったbackend開発" name="◆-djangoを使ったbackend開発"></a>
#### ◆ djangoを使ったbackend開発
概要説明
install/ひな型作成
実処理作成/データベースアクセス(django.model)
ルーティング
template
APIサーバとしてJSONレスポンスを返す。(JsonResponse)
ユニットテスト
デプロイ