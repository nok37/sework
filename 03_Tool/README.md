# Tool

## 目次
<!-- TOC -->

- [１．サクラエディタ](#１．サクラエディタ)
    - [◆ マクロ](#◆-マクロ)
- [２．Eclipse](#２．eclipse)
    - [◆ ショートカットコマンド](#◆-ショートカットコマンド)
- [３．Excel](#３．excel)
    - [◆ アクセスキー一覧](#◆-アクセスキー一覧)
- [４．Git](#４．git)
    - [◆ 基本操作](#◆-基本操作)
    - [◆ 豆知識](#◆-豆知識)

<!-- /TOC -->
<br>

<a id="markdown-１．サクラエディタ" name="１．サクラエディタ"></a>
### １．サクラエディタ
---
<a id="markdown-◆-マクロ" name="◆-マクロ"></a>
#### ◆ マクロ

```java
//highlight.mac
//選択文字をハイライト・コピーする
S_SelectWord(0);
S_SearchClearMark(0);
S_Copy();

//booking.mac
//選択文字をハイライト・全てマークする
S_SelectWord(0);
S_SearchClearMark(0);
S_BookmarkPattern('', 0);

//cmd_exe.mac
//行を選択して外部コマンド(cmd_exe)を実行する
GoLineTop(0);
GoLineEnd_Sel(0);
ExecCommand('cmd_exe "$C"', 0);
```
<br>

<a id="markdown-２．eclipse" name="２．eclipse"></a>
### ２．Eclipse
---
<a id="markdown-◆-ショートカットコマンド" name="◆-ショートカットコマンド"></a>
#### ◆ ショートカットコマンド

```java
// リソースを開く
ctrl + shift + r

//呼び出し階層を開く
ctrl + alt + h
```
<br>


<a id="markdown-３．excel" name="３．excel"></a>
### ３．Excel
---
<a id="markdown-◆-アクセスキー一覧" name="◆-アクセスキー一覧"></a>
#### ◆ アクセスキー一覧
書式(Option)

|  コマンド  |  意味  |
| ---- | ---- |
| ALT → O → R → E | 行高の任意編集（Row hEight） |
| ALT → O → R → A | 行高の自動編集（Row Auto） |
| ALT → O → R → H | 行の非表示（Row Hide） |
| ALT → O → R → U | 行非表示の取消（Row Undo） |
| ALT → O → C → W | セル幅の任意編集（Cell Width） |
| ALT → O → C → A | セル幅の自動編集（Cell Auto） |
| ALT → O → C → H | 行の非表示（Cell Hide） |
| ALT → O → C → U | 行非表示の取消（Cell Undo） |

挿入(Insert)
|  コマンド  |  意味  |
| ---- | ---- |
| ALT → I → B | 改ページの挿入 |

<a id="markdown-４．git" name="４．git"></a>
### ４．Git
---
<a id="markdown-◆-基本操作" name="◆-基本操作"></a>
#### ◆ 基本操作

```cmd
rem SSL認証の無効化
> git config --global http.sslVerify false

rem リモートリポジトリをローカルにダウンロード
> git clone <URL>

rem ブランチ作成
> git branch sample1

rem ブランチ一覧の表示
> git branch
* master
  sample1

rem ブランチ一覧確認(リモート追跡ブランチも出力)
rem ※ローカルにリモートリポジトリの情報を保持しているので、適宜手動で最新化する必要がある
> git branch --all
* master
  sample1
  remotes/origin/HEAD -> origin/master
  remotes/origin/master

rem originはリモートリポジトリのURLの別名を指す
> git remote get-url origin

rem ブランチ変更(チェックアウト)
> git checkout sample1
> git branch
  master
* sample1

rem ブランチ作成とチェックアウト
> git checkout -b sample2
Switched to a new branch 'sample2'
> git branch
  master
  sample1
* sample2

rem ブランチ削除
> git branch -d sample1
Deleted branch sample1 (was b1eca08).
> git branch
  master
  sample1

rem 変更したファイルの一覧を確認
> git status

rem 変更したファイルのソースコードを確認
> git diff

rem ファイル追加
> git add hoge

rem コミット
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

<a id="markdown-◆-豆知識" name="◆-豆知識"></a>
#### ◆ 豆知識

```cmd

rem 改行コード変換しないよう設定
> git config --global core.autocrlf false

```