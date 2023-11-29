# Oracle

<!-- TOC -->
- [1. 設定／全般／用語](#1-設定全般用語)
  - [1.1. バージョン](#11-バージョン)
  - [1.2. パスワード・プロファイル](#12-パスワードプロファイル)
  - [1.3. 起動・停止](#13-起動停止)
  - [1.4. 表領域](#14-表領域)
- [2. 基本](#2-基本)
  - [2.1. テーブル操作](#21-テーブル操作)
  - [2.2. データパンプ（データポンプ）](#22-データパンプデータポンプ)
  - [2.3. viewファイルの確認](#23-viewファイルの確認)
- [3. 関数](#3-関数)
- [4. 冗長性／可用性](#4-冗長性可用性)
  - [4.1. アーカイブログ](#41-アーカイブログ)
  - [4.2. Data Guard](#42-data-guard)
  - [4.3. パーテーション](#43-パーテーション)
- [5. 性能／パフォーマンス](#5-性能パフォーマンス)
  - [5.1. 実行計画・統計情報](#51-実行計画統計情報)
  - [5.2. 索引](#52-索引)
  - [5.3. AWR(Automatic Workload Repository)](#53-awrautomatic-workload-repository)
- [6. 用語](#6-用語)
  - [6.1. DWH （データウェアハウス）](#61-dwh-データウェアハウス)
  - [6.2. CWH （セントラルウェアハウス）](#62-cwh-セントラルウェアハウス)
  - [6.3. データマート](#63-データマート)
  - [6.4. マテビュー](#64-マテビュー)
  - [6.5. SCN （System Change Number）](#65-scn-system-change-number)
---
<br>
<!-- /TOC -->

## 1. 設定／全般／用語

### 1.1. バージョン

* バージョンの確認
    ```sql
    SQL> SELECT * FROM V$VERSION;
    ```

###  1.2. パスワード・プロファイル

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
    SQL> set lin 100
    SQL> col USERNAME for a20
    SQL> col PROFILE for a25
    SQL> col ACCOUNT_STATUS for a25
    SQL> col EXPIRY_DATE for a25
    
    -- DBA_USERSからプロファイルとアカウントステータスを取得
    SQL> SELECT USERNAME, PROFILE, ACCOUNT_STATUS, EXPIRY_DATE FROM DBA_USERS ORDER BY USERNAME;

    USERNAME             PROFILE                   ACCOUNT_STATUS            EXPIRY_DATE
    -------------------- ------------------------- ------------------------- -------------------------
    USER1                DEFAULT                   OPEN
    USER2                UNLOCKUSER                OPEN
    USER3                DEFAULT                   EXPIRED & LOCKED          2019/04/16

    --パスワード変更
    SQL> ALTER USER USER1 IDENTIFIED BY pass;

    --プロファイルの変更
    SQL> ALTER USER USER1 PROFILE UNLOCKUSER;
    ```

###  1.3. 起動・停止  

* インスタンスの起動<br>
バックグラウンド・プロセスを制御し、Oracle Databaseに接続するためのメモリー領域を割り当てること
* データベースのマウント<br>
データベースがすでに起動されているインスタンスと対応付けられる
* データベースのオープン<br>
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

###  1.4. 表領域

* 表領域（table space）とは、データ保管のためにストレージ上に確保した領域
    ```sql
    -- 書式設定
    SQL> col FILE_NAME for a60
    SQL> col SIZE(MB) for 99,999,999
    SQL> set linesize 120 pagesize 50000

    -- 表領域の確認
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

## 2. 基本

###  2.1. テーブル操作

* ALTER<br>
    オルターと読む
    ```sql
    ---カラムの変更
    ALTER TABLE table MODIFY (column VARCHAR2(45));
    ```

###  2.2. データパンプ（データポンプ）

* データエクスポート
    ```sql
    -- 基本
    SQL> expdp user/pass@db01 CONTENT=data_only DIRECTORY=dir01 DUMPFILE=data.dmp LOGFILE=exp.log
    
    -- テーブル指定
    TABLES=tbl01
    
    -- 指定された時刻に最も近いSCNを検出し、このSCNを使用してフラッシュバック・ユーティリティを使用可能にする
    FLASHBACK_TIME="TO_TIMESTAMP('27-10-2012 13:16:00', 'DD-MM-YYYY HH24:MI:SS')"
    
    -- デフォルトでログを作成するかどうか（YES指定で作成されない）
    NOLOGFILE=yes
    ```

* インポート
    ```sql
    -- 基本
    SQL> impdp user/pass@db01 TABLE_EXISTS_ACTION=truncate DIRECTORY=dir01 DUMPFILE=data.dmp LOGFILE=imp.log

    -- スキーマ変更
    REMAP_SCHEMA=source_schema:target_schema
    ```

* データポンプの停止
    ```sql
    -- 実行中のDATA PUMPを確認
    SQL> SELECT * FROM DBA_DATAPUMP_JOBS;

    -- 該当のジョブにアタッチ
    $ expdp user/pass@inst attach='job_name'
    $ impdp user/pass@inst attach='job_name'

    -- ジョブのキル
    $ kill_job
    ```

###  2.3. viewファイルの確認

```sql
SQL> set long 10000
SQL> set pagesize 0

SQL> SELECT TEXT FROM USER_VIEWS WHERE VIEW_NAME = '＜ビュー名（大文字）＞';
```

<br>

## 3. 関数

<br>

## 4. 冗長性／可用性  

###  4.1. アーカイブログ

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

###  4.2. Data Guard
自然災害などが発生した場合を想定し、遠隔地のスタンバイデータベースとネットワーク経由でフェイルオーバーを可能にする機能  

1. フィジカル・スタンバイ構成  
REDOデータをプライマリ・データベースからスタンバイ・データベースに転送し、適用（Redo Apply）していく構成。REDOデータはマウント状態で適用していく必要があるため、スタンバイ・データベースは通常マウント状態になる。スタンバイ・データベース側でデータを確認したいときは、REDOデータの適用を一時的に止めて、読み取り専用（READ ONLY）でスタンバイ・データベースをオープンする。

2. ロジカル・スタンバイ構成  
プライマリ・データベースから転送されたREDOデータをSQLに変換して、スタンバイ・データベースにSQLを実行（SQL Apply）してデータの同期を取る構成。スタンバイ・データベース側はオープンしている状態なので、いつでもデータの確認をすることができる。

### 4.3. パーテーション

* 概要<br>
パーティション化により、表、索引および索引構成表をより細かい単位に細分化できるようになる。

<br>

## 5. 性能／パフォーマンス

###  5.1. 実行計画・統計情報
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

### 5.2. 索引

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

### 5.3. AWR(Automatic Workload Repository)  
負荷状況・問題追及で使用する。

* 待機状況（Top 5 Timed Events）  
    時間が長かった待機イベントの上位５項目が表示される。  
    ⇒DB CPUが通常の処理時間なので、それ以上に割合を占めている待機イベントが

* 処理状況（Load Profile）  
    SQLの実行回数や1秒間のREDO生成量が表示される。  
    ⇒過去と比較して

* メモリ使用状況（Instance Efficiency Indicators）  


<br>


## 6. 用語

### 6.1. DWH （データウェアハウス）

* トランザクション処理用ではなく、問合せおよび分析用に設計されたリレーショナル・データベース。

### 6.2. CWH （セントラルウェアハウス）

* データウェアハウスの利用において、中心となるデータを統合管理する部分を指す。

### 6.3. データマート

* 販売、マーケティング、金融など、特定のビジネス分野に対して設計されたデータ・ウェアハウス。

### 6.4. マテビュー

* 調査や分析の対象となるデータ（通常は数値データや加算的データ）の集計データまたは結合データで構成される事前計算表。サマリーまたは集計表とも呼ばれえる。**リフレッシュ**することでマテリアライズド・ビューを変更して新しいデータを反映する。

### 6.5. SCN （System Change Number）

* トランザクションの毎に、シーケンシャルに割り振られる番号。この番号を元に障害の有無を判別し、リカバリも行ったりする非常に重要な番号。

<br>
