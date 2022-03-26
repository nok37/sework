# Git

<!-- TOC -->

- [１．設定](#１．設定)
- [２．コマンド](#２．コマンド)
    - [ブランチ操作](#ブランチ操作)
    - [追加／コミット](#追加／コミット)
    - [最新化](#最新化)
    - [豆知識](#豆知識)
    - [その他](#その他)

<!-- /TOC -->
---
<br>

<a id="markdown-１．設定" name="１．設定"></a>
## １．設定
---
<br>

<a id="markdown-２．コマンド" name="２．コマンド"></a>
## ２．コマンド
---
<br>

<a id="markdown-ブランチ操作" name="ブランチ操作"></a>
### ブランチ操作

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

<a id="markdown-追加／コミット" name="追加／コミット"></a>
### 追加／コミット

<a id="markdown-最新化" name="最新化"></a>
### 最新化

```bash
# 変更したファイルの一覧を確認
> git status

# 変更したファイルのソースコードを確認
> git diff

# ファイル追加
> git add hoge

# コミット
> git commit -m"コメント"

rem コミットの修正
> git commit --amend

rem ローカルリポジトリのブランチをリモートリポジトリへアップロードする（ブランチの更新）
> git push origin sample1

rem マスターをチェックアウトする
> git checkout master

rem 指定したブランチを現在のブランチに統合する
> git merge sample1

rem ローカルリポジトリのブランチをリモートリポジトリへアップロードする（masterの更新）
> git push origin master

rem ローカルのmaster「情報」を更新
> git fetch -p

rem ローカルのmaster情報を最新に更新したものをローカルのmasterに反映
> git merge origin/master

rem ローカルリポジトリのmasterブランチを最新化（上記二つの合体版）
> git pull origin master

rem ローカルの変更を元に戻す方法
> git checkout .

```

<a id="markdown-豆知識" name="豆知識"></a>
### 豆知識

```bash
# 改行コード変換しないよう設定
> git config --global core.autocrlf false

# SSL認証の無効化
> git config --global http.sslVerify false
```

<a id="markdown-その他" name="その他"></a>
### その他

```bash
# リモートリポジトリをローカルにダウンロード
> git clone <URL>

# originはリモートリポジトリのURLの別名を指す
> git remote get-url origin
```