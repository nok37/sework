# PostgreSQL

<!-- TOC -->

- [１．設定／全般](#１．設定／全般)
    - [接続](#接続)
    - [情報表示オプション(d)](#情報表示オプションd)
        - [スキーマの確認](#スキーマの確認)
        - [拡張機能の確認](#拡張機能の確認)
    - [バックアップ](#バックアップ)
    - [その他](#その他)
        - [文字コード](#文字コード)
- [２．関数](#２．関数)
    - [日付／時刻](#日付／時刻)
    - [文字列関数と演算子](#文字列関数と演算子)
        - [CHR（文字コードからASCIIコードを返却）](#chr文字コードからasciiコードを返却)
- [３．解析用](#３．解析用)
    - [クエリ解析](#クエリ解析)
        - [稼働統計情報ビュー(pg_stat_activity)](#稼働統計情報ビューpg_stat_activity)

<!-- /TOC -->
---
<br>
<!-- NEXT INDENT -->

<a id="markdown-１．設定／全般" name="１．設定／全般"></a>
## １．設定／全般

<a id="markdown-接続" name="接続"></a>
### 接続

```postgres
--接続方法
$ psql -U [ユーザ]
```

<a id="markdown-情報表示オプションd" name="情報表示オプションd"></a>
### 情報表示オプション(d)

<a id="markdown-スキーマの確認" name="スキーマの確認"></a>
#### スキーマの確認 
```postgres
postgres=# \dn
   スキーマ一覧
  名前  |  所有者
--------+----------
 public | postgres
(1 行)
```

<a id="markdown-拡張機能の確認" name="拡張機能の確認"></a>
#### 拡張機能の確認
```postgres
postgres=# \dx
                          インストール済みの拡張一覧
   名前    | バージョン |  スキーマ  |                  説明
-----------+------------+------------+-----------------------------------------
 adminpack | 2.1        | pg_catalog | administrative functions for PostgreSQL
 plpgsql   | 1.0        | pg_catalog | PL/pgSQL procedural language
(2 行)
```

<a id="markdown-バックアップ" name="バックアップ"></a>
### バックアップ

```postgres
--INSERT形式で出力
> pg_dump -p [port] -n [xxx] -U [user] -d [xxx] -a --column-inserts -t [table] > dump.sql

/*
※-Fオプション
p: プレーンテキスト
t: tar
c: カスタム
d: ディレクトリ
*/
```

<a id="markdown-その他" name="その他"></a>
### その他

<a id="markdown-文字コード" name="文字コード"></a>
#### 文字コード

```postgres
--文字コード確認
postgres=# select * from information_schema.

```

<br>
<!-- NEXT INDENT -->

<a id="markdown-２．関数" name="２．関数"></a>
## ２．関数

<a id="markdown-日付／時刻" name="日付／時刻"></a>
### 日付／時刻

```postgres
--トランザクションの時刻
SELECT CURRENT_TIMESTAMP;
SELECT NOW();
 
--現在時刻
SELECT CLOCK_TIMESTAMP();

--フォーマット
SELECT CAST(CURRENT_TIMESTAMP AS DATE);
```

<a id="markdown-文字列関数と演算子" name="文字列関数と演算子"></a>
### 文字列関数と演算子

<a id="markdown-chr文字コードからasciiコードを返却" name="chr文字コードからasciiコードを返却"></a>
#### CHR（文字コードからASCIIコードを返却）

```postgres
--A
postgres=# SELECT CHR(65);
 chr
-----
 A
--CR（キャリッジリターン）
postgres=# SELECT CHR(13);
 chr
-----
 \r
--LF（ラインフィード）
postgres=# SELECT CHR(10);
 chr
-----
    +
```

<br>
<!-- NEXT INDENT -->

<a id="markdown-３．解析用" name="３．解析用"></a>
## ３．解析用

<a id="markdown-クエリ解析" name="クエリ解析"></a>
### クエリ解析

<a id="markdown-稼働統計情報ビューpg_stat_activity" name="稼働統計情報ビューpg_stat_activity"></a>
#### 稼働統計情報ビュー(pg_stat_activity)

```postgres
-- SQLテキストの確認
postgres=# SELECT pid, usename, application_name, query FROM pg_stat_activity;
  pid  | usename  | application_name |                                query
-------+----------+------------------+---------------------------------------------------------------------
 11004 | postgres | psql             | SELECT pid, usename, application_name, query FROM pg_stat_activity;

--接続元の確認
postgres=# SELECT pid, client_addr, client_hostname, client_port FROM pg_stat_activity;
  pid  | client_addr | client_hostname | client_port
-------+-------------+-----------------+-------------
 11004 | ::1         |                 |       63939

--開始時間の確認
postgres=# SELECT pid, backend_start, xact_start, wait_event, state FROM pg_stat_activity;
  pid  |         backend_start         |          xact_start           |     wait_event      | state
-------+-------------------------------+-------------------------------+---------------------+--------
 11004 | 2022-03-26 15:31:09.451152+09 | 2022-03-26 16:31:48.023901+09 |                     | active

--切断
select pg_terminate_backend(pid); 

--最大接続数の確認
postgres=# show max_connections;
 max_connections
-----------------
 100
 
```

<br>
<!-- NEXT INDENT -->