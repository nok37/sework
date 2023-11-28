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

## １．設定／全般

### 接続

```postgres
--接続方法
$ psql -U [ユーザ]
```

### 情報表示オプション(d)

#### スキーマの確認 
```postgres
postgres=# \dn
   スキーマ一覧
  名前  |  所有者
--------+----------
 public | postgres
(1 行)
```

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

### その他

#### 文字コード

```postgres
--文字コード確認
postgres=# select * from information_schema.

```

<br>

## ２．関数

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

### 文字列関数と演算子

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

## ３．解析用

### クエリ解析

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
