# Linux

## 目次
<!-- TOC -->

- [１．設定 ・ 豆知識](#１．設定-・-豆知識)
    - [◆ コマンドの実行パス](#◆-コマンドの実行パス)
    - [◆ ssh接続時に表示される文言](#◆-ssh接続時に表示される文言)
    - [◆ bash設定](#◆-bash設定)
- [２．コマンド](#２．コマンド)
- [３．シェル](#３．シェル)

<!-- /TOC -->
<br>

<a id="markdown-１．設定-・-豆知識" name="１．設定-・-豆知識"></a>
### １．設定 ・ 豆知識
---
<a id="markdown-◆-コマンドの実行パス" name="◆-コマンドの実行パス"></a>
#### ◆ コマンドの実行パス
コマンド実行時は左から順にパスを確認しコマンド実行する。  
・ パスの確認
```
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```
・ パスの追加
```
$ export PATH=$NODE_HOME/bin:$PATH
```
<a id="markdown-◆-ssh接続時に表示される文言" name="◆-ssh接続時に表示される文言"></a>
#### ◆ ssh接続時に表示される文言
Message of the dayの略
```
/etc/motd
```
<a id="markdown-◆-bash設定" name="◆-bash設定"></a>
#### ◆ bash設定
・.bash_profile  
→ ログイン時にのみ実行される。  
→ 環境変数を設定する (export する変数)  
・.bashrc  
→ エイリアスを定義する  
→ 環境変数でない変数を設定する (export しない変数)

<br>

<a id="markdown-２．コマンド" name="２．コマンド"></a>
### ２．コマンド
---

<br>

<a id="markdown-３．シェル" name="３．シェル"></a>
### ３．シェル
---
