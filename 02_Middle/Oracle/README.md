# Oracle

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. バージョン](#11-バージョン)
  - [1.2. 構成](#12-構成)
    - [1.2.1. ノード](#121-ノード)
    - [1.2.2. インスタンス](#122-インスタンス)
  - [1.3. ユーザ](#13-ユーザ)
    - [1.3.1. 権限・ロール](#131-権限ロール)
    - [1.3.2. パスワード・プロファイル](#132-パスワードプロファイル)
  - [1.4. 起動・停止](#14-起動停止)
  - [1.5. 表領域](#15-表領域)
- [2. SQL](#2-sql)
  - [2.1. データ操作言語（DML）](#21-データ操作言語dml)
    - [2.1.1. SELECT](#211-select)
    - [2.1.2. INSERT](#212-insert)
  - [2.2. データ定義（DDL）](#22-データ定義ddl)
    - [2.2.1. CREATE](#221-create)
    - [2.2.2. DROP](#222-drop)
    - [2.2.3. ALTER](#223-alter)
- [3. オブジェクト](#3-オブジェクト)
  - [3.1. テーブル](#31-テーブル)
  - [3.2. ビュー](#32-ビュー)
  - [3.3. マテビュー](#33-マテビュー)
  - [3.4. DBリンク](#34-dbリンク)
  - [3.5. ディレクトリ](#35-ディレクトリ)
  - [3.6. シーケンス](#36-シーケンス)
  - [3.7. パッケージ・ファンクション](#37-パッケージファンクション)
  - [3.8. シノニム](#38-シノニム)
  - [3.9. その他](#39-その他)
- [4. ユーティリティ](#4-ユーティリティ)
  - [4.1. 【expdp】データエクスポート](#41-expdpデータエクスポート)
  - [4.2. 【impdp】インポート](#42-impdpインポート)
- [5. 冗長性／可用性](#5-冗長性可用性)
  - [5.1. アーカイブログ](#51-アーカイブログ)
  - [5.2. Data Guard](#52-data-guard)
- [6. 性能／パフォーマンス](#6-性能パフォーマンス)
  - [6.1. 実行計画・統計情報](#61-実行計画統計情報)
  - [6.2. 索引](#62-索引)
  - [6.3. AWR(Automatic Workload Repository)](#63-awrautomatic-workload-repository)
  - [6.4. パーテーション](#64-パーテーション)
- [7. 用語](#7-用語)
  - [7.1. DWH （データウェアハウス）](#71-dwh-データウェアハウス)
  - [7.2. CWH （セントラルウェアハウス）](#72-cwh-セントラルウェアハウス)
  - [7.3. データマート](#73-データマート)
  - [7.4. SCN （System Change Number）](#74-scn-system-change-number)
---
<br>
<!-- /TOC -->

## 1. 設定

### 1.1. バージョン

* バージョンの確認
    ```sql
    SELECT * FROM V$VERSION;
    ```

### 1.2. 構成

#### 1.2.1. ノード

* サーバやホストなどのネットワークリソース。

#### 1.2.2. インスタンス

* データベース・ファイルを管理する一連のメモリー構造。
* インスタンスが起動されると、システム・グローバル領域(SGA)と呼ばれるメモリー領域が割り当てられ、1つ以上のバックグラウンド・プロセスが起動する。
* 単一インスタンス構成またはOracle Real Application Clusters (Oracle RAC)構成のいずれかで実行される。

###  1.3. ユーザ

#### 1.3.1. 権限・ロール
```sql
-- 権限の確認
SQL> col USERNAME for a16
SQL> SELECT * FROM user_sys_privs ORDER BY 1, 2;

USERNAME         PRIVILGE                         ADM COM INH
---------------- -------------------------------- --- --- ---
ユーザ名          CREATE ANY DIRECTORY             NO  NO  NO
ユーザ名          CREATE ANY SYNONYM               NO  NO  NO
ユーザ名          CREATE DATABASE LINK             NO  NO  NO
ユーザ名          DROP ANY DIRECTORY               NO  NO  NO
ユーザ名          SELECT ANY DIRECTORY             NO  NO  NO
ユーザ名          UNLIMITED TABLESPACE             NO  NO  NO
```

```sql
-- 付与されたロールの確認
SQL> col USERNAME for a16
SQL> col GRANTED_ROLE for a32
SQL> SELECT * FROM user_role_privs ORDER BY 1, 2;

USERNAME         GRANTED_ROLE                     ADM DEL DEF OS_ COM INH
---------------- -------------------------------- --- --- --- --- --- --- 
ユーザ名          SELECT_CATALOG_ROLE (*1)         NO  NO  YES NO  NO  NO 
ユーザ名          業務AP用権限                      NO  NO  YES NO  NO  NO 

*1 データ・ディクショナリ内のオブジェクトに対するSELECT権限

-- ロール内容の確認
SQL> col ROLE for a16
SQL> col PRIVILEGE for a32
SQL> SELECT * FROM ROLE_SYS_PRIVS WHERE ROLE='ロール名' ORDER BY 2;

USERNAME         PRIVILEGE                        ADM COM INH
---------------- -------------------------------- --- --- --- 
ロール名          ALTER SESSION                    NO  NO  NO 
ロール名          CREATE SEQUENCE                  NO  NO  NO 
ロール名          CREATE TABLE                     NO  NO  NO 
ロール名          CREATE VIEW                      NO  NO  NO 
```

#### 1.3.2. パスワード・プロファイル

* プロファイル／パスワード期限の確認<br>
    ※アカウントステータスについて
    | 状態 | 意味 |
    | --- | --- |
    | OPEN | 正常 |
    | EXPIRED | パスワード期限切れまたは管理者による手動期限切れ |
    | EXPIRED(GRACE) | パスワード期限切れ後で、アカウント使用不可になるまでの猶予期間 |
    | LOCKED(TIMED) | パスワードの繰り返し入力ミスのため、ロック |
    | LOCKED | 管理者による手動ロック |
    ```sql
    -- 書式設定
    set lin 100
    col USERNAME for a20
    col PROFILE for a25
    col ACCOUNT_STATUS for a25
    col EXPIRY_DATE for a25
    
    -- DBA_USERSからプロファイルとアカウントステータスを取得
    SELECT USERNAME, PROFILE, ACCOUNT_STATUS, EXPIRY_DATE FROM DBA_USERS ORDER BY USERNAME;

    USERNAME             PROFILE                   ACCOUNT_STATUS            EXPIRY_DATE
    -------------------- ------------------------- ------------------------- -------------------------
    USER1                DEFAULT                   OPEN
    USER2                UNLOCKUSER                OPEN
    USER3                DEFAULT                   EXPIRED & LOCKED          2019/04/16

    --パスワード変更
    ALTER USER USER1 IDENTIFIED BY pass;

    --プロファイルの変更
    ALTER USER USER1 PROFILE UNLOCKUSER;
    ```

###  1.4. 起動・停止  

* インスタンスの起動<br>
バックグラウンド・プロセスを制御し、Oracle Databaseに接続するためのメモリー領域を割り当てること
* データベースのマウント<br>
データベースがすでに起動されているインスタンスと対応付けられる
* データベースのオープン<br>
通常のデータベース操作が可能になる

    ```sql
    -- インスタンスを起動し、データベースをマウントしてオープンする方法
    STARTUP

    -- インスタンスを起動するが、データベースをマウントしない方法
    STARTUP NOMOUNT

    -- インスタンスを起動し、データベースをマウントする方法（オープンはしない）
    STARTUP MOUNT

    -- インスタンスにデータベースをマウントする方法
    ALTER DATABASE MOUNT;

    -- クローズしているデータベースをオープンする方法
    ALTER DATABASE OPEN;

    -- NORMALモードによる停止（接続しているすべてのユーザーが切断するまで待機してから、データベースが停止）
    SHUTDOWN [NORMAL]

    -- IMMEDIATEモードによる停止（実行中のSQL文を終了、ユーザーを切断、アクティブなトランザクションを終了し、コミットされていない変更をロールバックして停止）
    SHUTDOWN IMMEDIATE

    -- TRANSACTIONALモードによる停止（現在のトランザクションがすべて完了するまで待機してから停止）
    SHUTDOWN TRANSACTIONAL
    ```

###  1.5. 表領域

* 表領域（table space）とは、データ保管のためにストレージ上に確保した領域

    ```sql
    -- 書式設定
    col FILE_NAME for a60
    col SIZE(MB) for 99,999,999
    set linesize 120 pagesize 50000

    -- 表領域の確認
    select TABLESPACE_NAME, FILE_NAME, BYTES/1024/1024 "SIZE(MB)" from DBA_DATA_FILES;

    TABLESPACE_NAME   FILE_NAME                                         SIZE(MB)
    ----------------- ---------------------------------------------- -----------
    SYSTEM            /DB/oracle/idx/idx001_tsp01.db                         870
    SYSAUX            +DATA/ORCL/DATAFILE/sysaux.262.1012010305              600
    UNDOTBS1          +DATA/ORCL/DATAFILE/undotbs1.263.1012010333            130
    USERS             +DATA/ORCL/DATAFILE/users.274.1012011961                 5
    ```

    ```sql
    -- 拡張
    alter tablespace TEST_SMALL add datafile size 4096M;

    -- 削除
    alter tablespace TEST_SMALL drop datafile size 4096M;

    set lines 120
    set pages 100
    set term off
    tti off
    clear col
    col TABLESPAVE_NAME format a15
    col "SIZE(MB)" format a20
    col "USED(MB)" format a20
    col "FREE(MB)" format a20
    col "USED(%)" format 990.99
    ```
    
    ```sql
    -- 容量の確認
    select
    tablespace_name,
    to_char(nvl(total_bytes / 1024 /1024,0),'999,999,999') as "size(MB)",
    to_char(nvl((total_bytes - free_total_bytes) / 1024 /1024,0),'999,999,999') as "used(MB)",
    to_char(nvl(free_total_bytes / 1024 /1024,0),'999,999,999') as "free(MB)",
    round(nvl((total_bytes - free_total_bytes) / total_bytes * 100,100),2) as "rate(%)"
    from
    (select tablespace_name,sum(bytes) total_bytes from dba_data_files group by tablespace_name),
    (select tablespace_name free_tablespace_name,sum(bytes) free_total_bytes from dba_free_space group by tablespace_name)
    where tablespace_name = free_tablespace_name(+)
    /
    ★表示例を追記する
    ```

<br>

## 2. SQL

### 2.1. データ操作言語（DML）

#### 2.1.1. SELECT
レコードを抽出する。
```sql
-- 全カラムを取得
SQL> SELECT * FROM table A;

-- テーブル件数を取得
SQL> SELECT /*+ parallel(8) full(A) */ count(1) FROM table A;

-- ヒント句についての補足
/*+ parallel(8) */
/*+ full(A) */
```

#### 2.1.2. INSERT
データを登録する。
```sql
SQL> INSERT

```

* ダイレクト・パス・インサート<br>
  大量にデータをインサートする際に使用する。<br>

  * 特徴
  1. 初期データエントリ
  2. パーティション単位のデータエントリ
  3. Oracle内で処理するので高速

  * 注意事項
  1. テーブル（またはパーティション）が排他ロックされる。
  2. コミット完了しないと、INSERTしたレコードを参照できない。
  3. インデックス再構築などにより、多くの一時表領域を消費する。

  ```sql
  --使用例
  INSERT /*+ APPEND */ INTO テーブル名 SELECT * FROM 引用元テーブル名;
  ```

### 2.2. データ定義（DDL）

#### 2.2.1. CREATE
データオブジェクトを作成する。
```sql
SQL> CREATE TABLE


-- CTAS(既存テーブルからデータを引き継いで新規テーブル作成)
SQL> CREATE TABLE 新テーブル名 AS SELECT * FROM 旧テーブル名;

-- CTAS(既存テーブルから新規テーブル作成)
SQL> CREATE TABLE 新テーブル名 AS SELECT * FROM 旧テーブル名 WHERE 1<>2; 
```

* 遅延セグメント作成<br>
  表作成でセグメントを作成せず、データが挿入された場合にセグメントを実体化する。デフォルトで有効になっている。
  ```sql
  ★確認方法を追記する
  ```

#### 2.2.2. DROP
データオブジェクトを削除する。
```sql
-- テーブル削除
SQL> DROP TABLE テーブル名;

-- テーブル完全削除
SQL> DROP TABLE テーブル名 PURGE;
```

#### 2.2.3. ALTER
データオブジェクトを変更する。（※オルターと読む）
```sql
-- カラムの変更
ALTER TABLE テーブル名 MODIFY (カラム名 VARCHAR2(45));

-- DMLのパラレル有効化　※SELECTは宣言不要でパラレル動作する
ALTER SESSION ENABLE PARALLEL DML;

-- テーブル圧縮解除
ALTER TABLE テーブル名 MOVE PARTITION パーティション名 NOCOMPRESS UPDATE INDEX PARALLEL 8:

-- テーブル圧縮（HCC圧縮　※他にOLTPなど）
ALTER TABLE テーブル名 MOVE PARTITION パーティション名 COMPRESS FOR QUERY HIGH UPDATE INDEX PARALLEL 8:
```

<br>

## 3. オブジェクト

### 3.1. テーブル
```sql
-- テーブル一覧
SQL> col table_name for a32
SQL> SELECT count(1) FROM user_tables WHERE table_name LIKE 'T%';
SQL> SELECT table_name FROM user_tables;

TABLE_NAME
----------------
TABLE0000
```


### 3.2. ビュー
```sql
-- ビュー一覧
SQL> col view_name for a32
SQL> SELECT view_name FROM user_views;
```

### 3.3. マテビュー

* マテビューとは
  * 調査や分析の対象となるデータ（通常は数値データや加算的データ）の集計データまたは結合データで構成される事前計算表。サマリーまたは集計表とも呼ばれえる。***リフレッシュすることでマテリアライズド・ビューを変更して新しいデータを反映する***。

```sql
-- マテビュー一覧
SQL> col owner for a16
SQL> col mview_name for a32
SQL> col master_link for a32
SQL> SELECT owner,mview_name,master_link FROM user_mviews ORDER BY 1,2,3;

OWNER            MVIEW_NAME                       MASTER_LINK
---------------- -------------------------------- ----------------
SCXXX111         MV0000                           @"LINK0000"
```

* マテビューログ作成
  ```sql
  -- マテビューのスキーマに接続
  SQL> conn ユーザ名/スキーマ名@サービス名

  -- マテビューログ作成
  SQL> CREATE MATERIALIZED VIEW LOG ON マテビュー名;

  -- マテビューログ作成確認
  SQL> col MASETER for a32
  SQL> col LOG_TABLE for a32
  SQL> SELECT maseter, log_table FROM user_mview_logs;
  ★出力例を追記する

  -- テーブル確認
  SQL> col TABLE_NAME for a32
  SQL> SELECT table_name FROM user_tables order by 1;

  TABLE_NAME
  --------------------------------
  MLOG$_テーブル名　★差分格納テーブル
  RUPD$_テーブル名　★差分格納一時テーブル
  テーブル名
  ```

* マテビューリフレッシュ
  ```sql
  -- リフレッシュ
  -- ※1回目は完全リフレッシュ、2回目以降は差分リフレッシュ（高速リフレッシュ）となる。
  SQL> EXECUTE DBMS_MVIEW.REFRESH('マテビュー名');

  -- 完全リフレッシュ 
  SQL> EXECUTE DBMS_MVIEW.REFRESH('マテビュー名', 'c');

  -- リフレッシュ状態の確認
  SQL> col MVIEW_NAME for a32
  SQL> SELECT mview_name, last_refresh_type, last_refresh_date FROM ALL_MVIEWS ORDER BY 1;
  ```

### 3.4. DBリンク
```sql
-- DBリンク一覧
SQL> col object_name for a16
SQL> SELECT object_name FROM user_objects WHERE object_type = 'DATABASE LINK';

OBJECT_NAME
----------------
LINK0000
```

### 3.5. ディレクトリ
```sql
-- ディレクトリ一覧
SQL> col owner for a16
SQL> col directory_name for a32
SQL> col directory_path for a64
SQL> SELECT owner,directory_name,directory_path FROM all_directories;

OWNER            DIRECTORY_NAME
---------------- --------------------------------
DIRECTORY_PATH
----------------------------------------------------------------
SYS              DIRXXX111
/opt1/xxx/oracleio
```

### 3.6. シーケンス
```sql
-- シーケンス一覧
SQL> SELECT object_name, status FROM user_objects WHERE object_type = 'SEQUENCE';
```

### 3.7. パッケージ・ファンクション
```sql
-- パッケージ・ファンクション一覧
SQL> SELECT object_name, status FROM user_objects WHERE object_type = 'PACKAGE' OR object_type = 'FUNCTION' OR object_type = 'PACKAGE_BODY';
```

### 3.8. シノニム
```sql
-- シノニム一覧
SQL> SELECT object_name FROM user_objects where object_type = 'SYNONYM';
```

### 3.9. その他
```sql
-- 無効オブジェクト確認
SQL> SELECT object_type, object_name, status FROM dba_objects WHERE status = 'INVALID' ORDER BY 1,2;
```

<br>

## 4. ユーティリティ

### 4.1. 【expdp】データエクスポート

* 基本コマンド
  ```bash
  # エクスポート
  $ expdp user/pass@db01 CONTENT=data_only DIRECTORY=dir01 DUMPFILE=data.dmp LOGFILE=exp.log
  ```

* オプション
  ```bash
  # テーブル指定
  TABLES=tbl01

  # パラレル度指定　※dmpファイルは%uで可変となる（01～08）
  PARALLEL=8

  # 他のRACインスタンスで実施できるか指定　※デフォルトYES
  CLUSTER=NO

  # 使用するサービス名を指定　※CLUSTER=YESと合わせて使用
  SERVICE_NAME=service001

  # ログ作成有無の指定（YES指定で作成されない）
  NOLOGFILE=YES
  ```

* 豆知識
  * PARALLELオプションについて<br>
    以下のような抽出オブジェクトが複数の場合効果あり。<br>
    1. パーティションテーブル
    2. コンポジットパーティションテーブルのメインパーティション

  * PARALLELで作成されるdmpファイル<br>
    PARALLEL=8でdmpファイル名に%uを使用すると、通常01～08のファイルが作成されるが、***PARALLEL数以上（または未満）のファイルが作成されることがある***。ファイル名を固定（dmp01,dmp02...）することで回避可能。
  
  * CLUSTERオプション未指定の場合、全ノードで分散処理される。効率的に抽出できるが、処理負荷が想定できない。これを避ける場合はSERVICE_NAMEのオプションで抽出ノードを指定する。

### 4.2. 【impdp】インポート

* 基本コマンド
  ```bash
  # インポート
  $ impdp user/pass@db01 TABLE_EXISTS_ACTION=truncate DIRECTORY=dir01 DUMPFILE=data.dmp LOGFILE=imp.log
  ```

* オプション
  ```bash
  # スキーマ変更
  REMAP_SCHEMA=source_schema:target_schema
  ```

* 豆知識
  * データポンプの停止
    ```sql
    -- 実行中のDATA PUMPを確認
    SQL> SELECT * FROM DBA_DATAPUMP_JOBS;
    ```

    ```bash
    # 該当のジョブにアタッチ(Linuxの場合)
    $ expdp user/pass@inst attach='job_name'
    $ impdp user/pass@inst attach='job_name'

    # ジョブのキル
    $ kill_job
    ```

<br>

## 5. 冗長性／可用性  

###  5.1. アーカイブログ

* 確認
  ```sql
  --oracleユーザで接続
  $ sqlplus / as sysdba

  --状態の確認
  SQL> select log_mode from v$database;
  LOG_MODE
  ------------
  ARCHIVELOG
  ```

* 変更
  ```sql
  --※必要に応じてクラスタをメンテナンスにする
  --Oracleの停止をする
  shutdown immediate

  --Oracleの起動（マウント状態）をする
  startup mount

  --noarchivelogモードに変更する
  alter database noarchivelog;

  --Oracleの起動をする。
  alter database open;

  --現在の状態を確認
  select log_mode from v$database;
  LOG_MODE
  ------------
  NOARCHIVELOG
  ```

* 削除
  ```sql
  --【削除】
  --アーカイブログの確認
  $ rman target /
  RMAN> list archivelog all;

  --アーカイブログの削除
  RMAN> delete archivelog all;

  --アーカイブログの確認
  RMAN> list archivelog all;

  --※インポート中に実施した際に必要
  RMAN> CROSSCHECK ARCHIVELOG ALL;
  RMAN> DELETE EXPIRED ARCHIVELOG ALL;
  ```

###  5.2. Data Guard
自然災害などが発生した場合を想定し、遠隔地のスタンバイデータベースとネットワーク経由でフェイルオーバーを可能にする機能  

1. フィジカル・スタンバイ構成  
  REDOデータをプライマリ・データベースからスタンバイ・データベースに転送し、適用（Redo Apply）していく構成。REDOデータはマウント状態で適用していく必要があるため、スタンバイ・データベースは通常マウント状態になる。スタンバイ・データベース側でデータを確認したいときは、REDOデータの適用を一時的に止めて、読み取り専用（READ ONLY）でスタンバイ・データベースをオープンする。

2. ロジカル・スタンバイ構成  
  プライマリ・データベースから転送されたREDOデータをSQLに変換して、スタンバイ・データベースにSQLを実行（SQL Apply）してデータの同期を取る構成。スタンバイ・データベース側はオープンしている状態なので、いつでもデータの確認をすることができる。


<br>

## 6. 性能／パフォーマンス

###  6.1. 実行計画・統計情報
具体的なSQL実行の流れは以下の通り  

1. パーサーがSQL文の構文解析(パース)を実行
    - SQL文の整合性チェック  
    - 後続処理の効率化
2. オプティマイザ  
　最適なデータアクセス方法(**実行計画**)の決定  
3. カタログマネージャ  
　カタログとはRDBMSの内部情報を集めたテーブル群で、テーブルやインデックスの統計情報が格納されてる。そのため、このカタログの情報を単に「**統計情報**」とも呼ぶ。
4. 統計情報とは  
    - 各テーブルのレコード数
    - 各テーブルの列数と列のサイズ
    - 列値のカーディナリティ(値の個数)
    - 列値のデータ分布(どの値がいくつあるかのヒストグラム)
    - 列内のNULLの数
    - インデックス情報

※インデックスとは  
インデックス(索引)とはテーブルに格納されているデータを高速に取り出す為の仕組み。

※実行計画  
どうしたらより短い時間でSQLを実行できるか（例,フルスキャン, INDEX参照）オプティマイザが実行計画の候補をいくつか作成し、最速の候補が選択すること。  
この基となる情報を「統計情報」という。

※統計情報  
表統計、列統計、索引統計、システム統計から構成される。  
* 自動的に取得
* 手動で取得
* SQL実行時に取得（動的サンプリング）  
    などがある
  
<u>実行計画と統計情報とデータベースの三者は整合性取れてる必要がある。</u>  

### 6.2. 索引

* 説明<br>
テーブル内の特定のデータだけにアクセスする場合に、索引を使用することで効果的にアクセスできる。数%のデータにアクセスする場合は索引スキャンは非常に高速だが、アクセスするデータが多いと逆にフル・スキャンより遅くなる。

* 索引の作成<br>
基本は、主キー以外で頻繁にWHERE句に指定されている列に作成する。ただし、索引が多すぎると更新のオーバーヘッドになるので最小限の索引にするようにします。索引を効率よく活用する必要がある。
    1. 一意性の高い索引を<br>
        複数の列を条件に指定している場合はできるだけ全ての列で複数索引を作成する。一意性が高いのでアクセスするブロック数を少なくできる。
    2. 使用頻度の高い列を先頭に<br>
        作成する索引の先頭には頻繁に使用する列を持ってきて、多くのSQL文で使用されるようにする。
    3. 選択率の低い列を先頭に<br>
        選択率の低い列（ユニーク性の高い列）から指定する。これは、索引は先頭から比較していきますので、目的のキーにたどり着くまでのキー比較を少なくできる。
    4. 非ユニーク索引にはキー圧縮<br>
        ss

* 索引のメンテナンス<br>

### 6.3. AWR(Automatic Workload Repository)  
負荷状況・問題追及で使用する。

* 待機状況（Top 5 Timed Events）  
    時間が長かった待機イベントの上位５項目が表示される。  
    ⇒DB CPUが通常の処理時間なので、それ以上に割合を占めている待機イベントが

* 処理状況（Load Profile）  
    SQLの実行回数や1秒間のREDO生成量が表示される。  
    ⇒過去と比較して

* メモリ使用状況（Instance Efficiency Indicators）  

### 6.4. パーテーション

* 概要<br>
パーティション化により、表、索引および索引構成表をより細かい単位に細分化できるようになる。


<br>


## 7. 用語

### 7.1. DWH （データウェアハウス）

* トランザクション処理用ではなく、問合せおよび分析用に設計されたリレーショナル・データベース。

### 7.2. CWH （セントラルウェアハウス）

* データウェアハウスの利用において、中心となるデータを統合管理する部分を指す。

### 7.3. データマート

* 販売、マーケティング、金融など、特定のビジネス分野に対して設計されたデータ・ウェアハウス。

### 7.4. SCN （System Change Number）

* トランザクションの毎に、シーケンシャルに割り振られる番号。この番号を元に障害の有無を判別し、リカバリも行ったりする非常に重要な番号。

<br>
