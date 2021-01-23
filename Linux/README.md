# Linux

## 目次
<!-- TOC -->

- [１．設定 ・ 豆知識](#１．設定-・-豆知識)
    - [◆ コマンドの実行パス](#◆-コマンドの実行パス)
    - [◆ ssh接続時に表示される文言](#◆-ssh接続時に表示される文言)
    - [◆ bash設定](#◆-bash設定)
- [２．コマンド](#２．コマンド)
    - [◆ vim](#◆-vim)
    - [◆ sed](#◆-sed)
    - [◆ od](#◆-od)
    - [◆ xxd](#◆-xxd)
    - [◆ yum](#◆-yum)
    - [◆ bc](#◆-bc)
    - [◆ dc](#◆-dc)
- [３．シェル](#３．シェル)
    - [◆ 用語説明](#◆-用語説明)
    - [◆ 引数／特殊変数](#◆-引数／特殊変数)

<!-- /TOC -->
<br>


<a id="markdown-１．設定-・-豆知識" name="１．設定-・-豆知識"></a>
### １．設定 ・ 豆知識
---
<a id="markdown-◆-コマンドの実行パス" name="◆-コマンドの実行パス"></a>
#### ◆ コマンドの実行パス
コマンド実行時は左から順にパスを確認しコマンド実行する。  
・ パスの確認
```bash
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```
・ パスの追加
```bash
$ export PATH=$NODE_HOME/bin:$PATH
```
<a id="markdown-◆-ssh接続時に表示される文言" name="◆-ssh接続時に表示される文言"></a>
#### ◆ ssh接続時に表示される文言
Message of the dayの略
```bash
/etc/motd
```
<a id="markdown-◆-bash設定" name="◆-bash設定"></a>
#### ◆ bash設定
・.bash_profile  
→ ログイン時にのみ実行される  
→ 環境変数を設定する (export する変数)  
```bash
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/.local/bin:$HOME/bin

export PATH
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

・.bashrc  
→ シェルを起動する度に実行される  
→ エイリアスを定義する  
```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
```
まとめると  
・ログインシェル→ .bash_profile(→ .bashrc)  
・インタラクティブシェル→ .bashrc  
・非インタラクティブシェル→ なし
<br>

<a id="markdown-２．コマンド" name="２．コマンド"></a>
### ２．コマンド
---
<a id="markdown-◆-vim" name="◆-vim"></a>
#### ◆ vim
高機能なテキストエディタ  

・オプション  
```bash
#行数表示
set number
se nu
#色付け
:set syntax=ON
#タブ整形
set ts=4
#大文字小文字区別なくす（ignorecase）
:set ic
:set noic
#ファイル名表示
ctrl + g
```

<a id="markdown-◆-sed" name="◆-sed"></a>
#### ◆ sed
文字操作

|  オプション  |  詳細  |
| ---- | ---- |
|  e  |  スクリプトコマンド実行  |
|  r  |  拡張正規表現でスクリプトコマンド実行<br>※スクリプトコマンド例（s:/置換前/置換後/g）  |
|  i  |  ファイルを直接編集  |
|  i拡張子  |  ファイルを直接編集し、拡張子の退避ファイル作成  |
<br>

・コマンド実行例
```bash
#標準出力の編集
$ echo "2020/07/11" | sed -e 's/\///g'
20200711
#ファイルの編集
$ grep user *sh
test1.sh:echo "user1"
test2.sh:echo "user1"
$ sed -i -e 's/user1/user2/g' ./*.sh
$ grep user *sh
test1.sh:echo "user2"
test2.sh:echo "user2"
#スペース削除と任意箇所切り取り
$ ls -l /usr/bin/vi* | sed -e 's/ \+/ /g'| cut -d' ' -f9-
/usr/bin/vi
/usr/bin/view -> vi
/usr/bin/vim
/usr/bin/vimdiff -> vim
/usr/bin/vimtutor
/usr/bin/vinagre
```
<a id="markdown-◆-od" name="◆-od"></a>
#### ◆ od
8進数やその他の形式でダンプする

|  オプション  |  詳細  |
| ---- | ---- |
| -t   | オプションで出力フォーマット指定 |  
|  c   | ASCII 文字または \ エスケープ文字で表示する |  
|  x   | 16進数2バイトで表示する（x2と同じ） |  
|  d   | 10進数2バイトで表示する |  
<br>
・コマンド実行例

```bash
$ echo 'AZaz-!'|od -tcx1d1
0000000    A    Z    a    z    -    !   \n
          41   5a   61   7a   2d   21   0a
          65   90   97  122   45   33   10
0000007
#１行目にASCII表示
#２行目に16進数1バイト表示(x1)
#３行目に10進数1バイト表示(x1)
$ cat utf8
AZaz09ｱア
$ od -tx1 utf8
41 5a 61 7a 30 39 ef bd b1 e3 82 a2 0a
$ od -tx1 sjis
41 5a 61 7a 30 39 b1 83 41 0a
#ef bdはBOM(バイトオーダーマーク)
```

<a id="markdown-◆-xxd" name="◆-xxd"></a>
#### ◆ xxd
2進数でダンプする  

|  オプション  |  詳細  |
| ---- | ---- |
| -b | オプションでバイナリ（2進数）表示 |
| -c | オプションで表示数変更 |
| -p | ポストスクリプト形式の 16 進ダンプを出力する。 |
| -r | 元に戻す: 16 進ダンプからバイナリ形式に変換 
<br>
・コマンド実行例

```bash
$ echo "abcdefghijklmn" |xxd -b
0000000: 01100001 01100010 01100011 01100100 01100101 01100110  abcdef
0000006: 01100111 01101000 01101001 01101010 01101011 01101100  ghijkl
000000c: 01101101 01101110 00001010                             mn.
$ echo "AZaz09ｱア" |xxd -p
415a617a3039efbdb1e382a20a
$ echo '415a617a3039efbdb1e382a20a' |xxd -p -r
AZaz09ｱア
```
<a id="markdown-◆-yum" name="◆-yum"></a>
#### ◆ yum
yumはパイソンで動いている
```bash:/usr/bin/yum
#!/usr/bin/python
```

<a id="markdown-◆-bc" name="◆-bc"></a>
#### ◆ bc
任意精度の計算言語

```bash
#単純な計算　1+2+3+4+5
$ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
1+2+3+4+5
15
```

<a id="markdown-◆-dc" name="◆-dc"></a>
#### ◆ dc
逆ポーランド形式の無限精度の計算が行える卓上計算機

```bash
#複雑な計算　(27/(1+2)^2)*2
$ dc
27 1 2 + 2 ^ / 2 * 
p
6
```

<br>

<a id="markdown-３．シェル" name="３．シェル"></a>
### ３．シェル
---
<a id="markdown-◆-用語説明" name="◆-用語説明"></a>
#### ◆ 用語説明
・シェバン  
シェルの1行目に記載し、このシェルは「bin/bash」で動かしますの意味
```bash
#!/bin/bash
```
・セカンダリプロンプト  
行末の「\」のことで、まだコマンドは終了していないことを意味する
```bash
echo \
"Hello, World!"
```
<a id="markdown-◆-引数／特殊変数" name="◆-引数／特殊変数"></a>
#### ◆ 引数／特殊変数
```bash
$ ./test.sh 1 2 3
#「$0」は特殊な引数で、シェル名が格納されてる
$0 = ./test.sh
#「$1」は引数の値で「位置パラメータ」という
$1 = 1
$2 = 2
$3 = 3
#「$#」は引数の個数
$# = 3
#「$$」は現在実行しているプロセスID
$$ = 3854
#「#@」はすべての位置パラメータ("$1" "$2" ..."$N")
$@ = 1 2 3
#「#*」はすべての位置パラメータ("$1 $2 $N")
$* = 1 2 3
#「$?」直前コマンドの「終了ステータス（正常=0）」
$? = 0
```

