# PostgreSQL

## 目次
<!-- TOC -->

- [１．設定／全般](#１．設定／全般)
- [２．基本](#２．基本)
- [３．関数](#３．関数)

<!-- /TOC -->
<br>


<a id="markdown-１．設定／全般" name="１．設定／全般"></a>
### １．設定／全般
---

```postgres
# 情報表示(d)
# スキーマ一覧
postgres=# \dn
   スキーマ一覧
  名前  |  所有者
--------+----------
 public | postgres
(1 行)

# 拡張機能一覧
postgres=# \dx
                          インストール済みの拡張一覧
   名前    | バージョン |  スキーマ  |                  説明
-----------+------------+------------+-----------------------------------------
 adminpack | 2.1        | pg_catalog | administrative functions for PostgreSQL
 plpgsql   | 1.0        | pg_catalog | PL/pgSQL procedural language
(2 行)

```

<a id="markdown-２．基本" name="２．基本"></a>
### ２．基本

<a id="markdown-３．関数" name="３．関数"></a>
### ３．関数
