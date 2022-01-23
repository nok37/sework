# Oracle

## 目次
<!-- TOC -->

- [１．設定／全般](#１．設定／全般)
    - [◆ パスワード・プロファイル](#◆-パスワード・プロファイル)
    - [◆ 起動・停止](#◆-起動・停止)
    - [◆ 表領域](#◆-表領域)
- [２．基本](#２．基本)
    - [◆ テーブル操作](#◆-テーブル操作)
    - [◆ エクスポート](#◆-エクスポート)
    - [◆ viewファイルの確認](#◆-viewファイルの確認)
- [３．関数](#３．関数)
- [４．冗長性／可用性](#４．冗長性／可用性)
    - [◆ アーカイブログ](#◆-アーカイブログ)
    - [◆ Data Guard](#◆-data-guard)
    - [◆ パフォーマンス](#◆-パフォーマンス)
- [５．性能](#５．性能)
    - [◆ 実行計画・統計情報](#◆-実行計画・統計情報)

<!-- /TOC -->
<br>


<a id="markdown-１．設定／全般" name="１．設定／全般"></a>
### １．設定／全般
---
<a id="markdown-◆-パスワード・プロファイル" name="◆-パスワード・プロファイル"></a>
#### ◆ パスワード・プロファイル

```sql
--プロファイル／パスワード期限の確認
SQL> set lin 100
SQL> col USERNAME for a20
SQL> col PROFILE for a25
SQL> col ACCOUNT_STATUS for a25
SQL> col EXPIRY_DATE for a25
SQL> SELECT USERNAME, PROFILE, ACCOUNT_STATUS, EXPIRY_DATE FROM DBA_USERS ORDER BY USERNAME;

USERNAME             PROFILE                   ACCOUNT_STATUS            EXPIRY_DATE
-------------------- ------------------------- ------------------------- -------------------------
USER1                DEFAULT                   OPEN
USER2                UNLOCKUSER                OPEN
USER3                DEFAULT                   EXPIRED & LOCKED          2019/04/16

--アカウントステータスの補足
OPEN：正常
EXPIRED：パスワード期限切れまたは管理者による手動期限切れ
EXPIRED(GRACE)：パスワード期限切れ後で、アカウント使用不可になるまでの猶予期間
LOCKED(TIMED)：パスワードの繰り返し入力ミスのため、ロック
LOCKED：管理者による手動ロック

--パスワード変更
SQL> ALTER USER USER1 IDENTIFIED BY pass;

--プロファイルの変更
SQL> ALTER USER USER1 PROFILE UNLOCKUSER;
```


<a id="markdown-◆-起動・停止" name="◆-起動・停止"></a>
#### ◆ 起動・停止  

* インスタンスの起動  
バックグラウンド・プロセスを制御し、Oracle Databaseに接続するためのメモリー領域を割り当てること
* データベースのマウント  
データベースがすでに起動されているインスタンスと対応付けられる
* データベースのオープン  
通常のデータベース操作が可能になる

```sql
-- インスタンスを起動し、データベースをマウントしてオープンする方法
SQL> STARTUP

-- インスタンスを起動するが、データベースをマウントしない方法
SQL> STARTUP NOMOUNT

-- インスタンスを起動し、データベースをマウントする方法（オープンはしない）
SQL> STARTUP MOUNT

-- インスタンスにデータベースをマウントする方法
SQL> ALTER DATABASE MOUNT;

-- クローズしているデータベースをオープンする方法
SQL> ALTER DATABASE OPEN;

-- NORMALモードによる停止（接続しているすべてのユーザーが切断するまで待機してから、データベースが停止）
SQL> SHUTDOWN [NORMAL]

-- IMMEDIATEモードによる停止（実行中のSQL文を終了、ユーザーを切断、アクティブなトランザクションを終了し、コミットされていない変更をロールバックして停止）
SQL> SHUTDOWN IMMEDIATE

-- TRANSACTIONALモードによる停止（現在のトランザクションがすべて完了するまで待機してから停止）
SQL> SHUTDOWN TRANSACTIONAL
```
<br>

<a id="markdown-◆-表領域" name="◆-表領域"></a>
#### ◆ 表領域

```sql
-- 確認
SQL> col FILE_NAME for a60
SQL> col SIZE(MB) for 99,999,999
SQL> set linesize 120 pagesize 50000

SQL> select TABLESPACE_NAME, FILE_NAME, BYTES/1024/1024 "SIZE(MB)" from DBA_DATA_FILES;

TABLESPACE_NAME   FILE_NAME                                         SIZE(MB)
----------------- ---------------------------------------------- -----------
SYSTEM            /DB/oracle/idx/idx001_tsp01.db                         870
SYSAUX            +DATA/ORCL/DATAFILE/sysaux.262.1012010305              600
UNDOTBS1          +DATA/ORCL/DATAFILE/undotbs1.263.1012010333            130
USERS             +DATA/ORCL/DATAFILE/users.274.1012011961                 5

-- 拡張
SQL> alter tablespace TEST_SMALL add datafile size 4096M;

-- 削除
SQL> alter tablespace TEST_SMALL drop datafile size 4096M;

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

-- 使用量の確認
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
```

<br>

<a id="markdown-２．基本" name="２．基本"></a>
### ２．基本
---
<a id="markdown-◆-テーブル操作" name="◆-テーブル操作"></a>
#### ◆ テーブル操作
```sql
---カラムの変更
ALTER TABLE table MODIFY (column VARCHAR2(45));
```

<a id="markdown-◆-エクスポート" name="◆-エクスポート"></a>
#### ◆ エクスポート

```sql
-- 実行中のDATA PUMPを確認
SQL> SELECT * FROM DBA_DATAPUMP_JOBS;

-- 該当のジョブにアタッチ
$ expdp user/pass@inst attach='job_name'
$ impdp user/pass@inst attach='job_name'

-- ジョブのキル
$ kill_job
```

<a id="markdown-◆-viewファイルの確認" name="◆-viewファイルの確認"></a>
#### ◆ viewファイルの確認

```sql
SQL> set long 10000
SQL> set pagesize 0

SQL> SELECT TEXT FROM USER_VIEWS WHERE VIEW_NAME = '＜ビュー名（大文字）＞';
```

<br>

<a id="markdown-３．関数" name="３．関数"></a>
### ３．関数
---

<br>

<a id="markdown-４．冗長性／可用性" name="４．冗長性／可用性"></a>
### ４．冗長性／可用性  
---

<a id="markdown-◆-アーカイブログ" name="◆-アーカイブログ"></a>
#### ◆ アーカイブログ

```sql
--oracleユーザで接続
$ sqlplus / as sysdba

--【確認】
SQL> select log_mode from v$database;
 LOG_MODE
 ------------
 ARCHIVELOG

--【変更】（必要に応じてクラスタをメンテナンスにする）
--Oracleの停止をする
SQL> shutdown immediate

--Oracleの起動（マウント状態）をする
SQL> startup mount

--noarchivelogモードに変更する
SQL> alter database noarchivelog;

--Oracleの起動をする。
SQL> alter database open;

--現在の状態を確認
SQL> select log_mode from v$database;
 LOG_MODE
 ------------
 NOARCHIVELOG

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

<a id="markdown-◆-data-guard" name="◆-data-guard"></a>
#### ◆ Data Guard
自然災害などが発生した場合を想定し、遠隔地のスタンバイデータベースとネットワーク経由でフェイルオーバーを可能にする機能  

1. フィジカル・スタンバイ構成  
REDOデータをプライマリ・データベースからスタンバイ・データベースに転送し、適用（Redo Apply）していく構成。REDOデータはマウント状態で適用していく必要があるため、スタンバイ・データベースは通常マウント状態になる。スタンバイ・データベース側でデータを確認したいときは、REDOデータの適用を一時的に止めて、読み取り専用（READ ONLY）でスタンバイ・データベースをオープンする。

2. ロジカル・スタンバイ構成  
プライマリ・データベースから転送されたREDOデータをSQLに変換して、スタンバイ・データベースにSQLを実行（SQL Apply）してデータの同期を取る構成。スタンバイ・データベース側はオープンしている状態なので、いつでもデータの確認をすることができる。

<a id="markdown-◆-パフォーマンス" name="◆-パフォーマンス"></a>
#### ◆ パフォーマンス

* 待機イベント  
    ```sql
    -- 確認
    SQL> select program, event from v$session where EVENT='Streams AQ: enqueue blocked on low memory';
    SQL> select shrink_phase_knlasg from X$KNLASG;

    -- 削除
    SQL> alter system set events 'immediate trace name mman_create_def_request level 6';
    ```

<a id="markdown-５．性能" name="５．性能"></a>
### ５．性能
---
<a id="markdown-◆-実行計画・統計情報" name="◆-実行計画・統計情報"></a>
#### ◆ 実行計画・統計情報
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

<br>