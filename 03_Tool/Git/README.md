# Git

<!-- TOC -->
- [1. 設定](#1-設定)
- [2. コマンド](#2-コマンド)
  - [2.1. ブランチ操作](#21-ブランチ操作)
  - [2.2. 追加／コミット](#22-追加コミット)
  - [2.3. 豆知識](#23-豆知識)
  - [2.4. その他](#24-その他)
---
<br>
<!-- /TOC -->

## 1. 設定

<br>

## 2. コマンド

### 2.1. ブランチ操作

```bash
# ブランチ作成
> git branch sample1

# ブランチ一覧確認(リモート追跡ブランチも出力)
# ※ローカルにリモートリポジトリの情報を保持しているので、適宜手動で最新化する必要がある
> git branch --all
* master
  sample1
  remotes/origin/HEAD -> origin/master
  remotes/origin/master

# ブランチ一覧の表示
> git branch
* master
  sample1

# ブランチ変更(チェックアウト)
> git checkout sample1
> git branch
  master
* sample1

# ブランチ作成とチェックアウト
> git checkout -b sample2
Switched to a new branch 'sample2'
> git branch
  master
  sample1
* sample2

# ブランチ削除
> git branch -d sample1
Deleted branch sample1 (was b1eca08).
> git branch
  master
  sample1
```

### 2.2. 追加／コミット

```bash
# 変更したファイルの一覧を確認
> git status

# 変更したファイルのソースコードを確認
> git diff

# ファイル追加
> git add hoge

# コミット
> git commit -m"コメント"

# コミットの修正
> git commit --amend

# ローカルリポジトリのブランチをリモートリポジトリへアップロードする（ブランチの更新）
> git push origin sample1

# マスターをチェックアウトする
> git checkout master

# 指定したブランチを現在のブランチに統合する
> git merge sample1

# ローカルリポジトリのブランチをリモートリポジトリへアップロードする（masterの更新）
> git push origin master

# ローカルのmaster「情報」を更新
> git fetch -p

# ローカルのmaster情報を最新に更新したものをローカルのmasterに反映
> git merge origin/master

# ローカルリポジトリのmasterブランチを最新化（上記二つの合体版）
> git pull origin master

# ローカルの変更を元に戻す方法
> git checkout .

```

### 2.3. 豆知識

```bash
# 改行コード変換しないよう設定
> git config --global core.autocrlf false

# SSL認証の無効化
> git config --global http.sslVerify false
```

### 2.4. その他

```bash
# リモートリポジトリをローカルにダウンロード
> git clone <URL>

# originはリモートリポジトリのURLの別名を指す
> git remote get-url origin
```

<br>
