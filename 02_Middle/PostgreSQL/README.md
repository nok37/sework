# PostgreSQL

<!-- TOC -->
- [1. 設定／全般](#1-設定全般)
  - [1.1. 接続](#11-接続)
  - [1.2. 情報表示オプション(d)](#12-情報表示オプションd)
    - [1.2.1. スキーマの確認](#121-スキーマの確認)
    - [1.2.2. 拡張機能の確認](#122-拡張機能の確認)
  - [1.3. バックアップ](#13-バックアップ)
  - [1.4. その他](#14-その他)
    - [1.4.1. 文字コード](#141-文字コード)
- [2. 関数](#2-関数)
  - [2.1. 日付／時刻](#21-日付時刻)
  - [2.2. 文字列関数と演算子](#22-文字列関数と演算子)
    - [2.2.1. CHR（文字コードからASCIIコードを返却）](#221-chr文字コードからasciiコードを返却)
- [3. 解析用](#3-解析用)
  - [3.1. クエリ解析](#31-クエリ解析)
    - [3.1.1. 稼働統計情報ビュー(pg\_stat\_activity)](#311-稼働統計情報ビューpg_stat_activity)
---
<br>
<!-- /TOC -->


## 1. 設定／全般

### 1.1. 接続

```postgres
--接続方法
$ psql -U [ユーザ]
```

### 1.2. 情報表示オプション(d)

#### 1.2.1. スキーマの確認 
```postgres
postgres=# \dn
   スキーマ一覧
  名前  |  所有者
--------+----------
 public | postgres
(1 行)
```

#### 1.2.2. 拡張機能の確認
```postgres
postgres=# \dx
                          インストール済みの拡張一覧
   名前    | バージョン |  スキーマ  |                  説明
-----------+------------+------------+-----------------------------------------
 adminpack | 2.1        | pg_catalog | administrative functions for PostgreSQL
 plpgsql   | 1.0        | pg_catalog | PL/pgSQL procedural language
(2 行)
```

### 1.3. バックアップ

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

### 1.4. その他

#### 1.4.1. 文字コード

```postgres
--文字コード確認
postgres=# select * from information_schema.

```

<br>

## 2. 関数

### 2.1. 日付／時刻

```postgres
--トランザクションの時刻
SELECT CURRENT_TIMESTAMP;
SELECT NOW();
 
--現在時刻
SELECT CLOCK_TIMESTAMP();

--フォーマット
SELECT CAST(CURRENT_TIMESTAMP AS DATE);
```

### 2.2. 文字列関数と演算子

#### 2.2.1. CHR（文字コードからASCIIコードを返却）

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

## 3. 解析用

### 3.1. クエリ解析

#### 3.1.1. 稼働統計情報ビュー(pg_stat_activity)

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
