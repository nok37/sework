# Linux

## 目次
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc generated TOC please keep comment here to allow auto update -->

- [１．設定 ・ 豆知識](#%EF%BC%91%EF%BC%8E%E8%A8%AD%E5%AE%9A-%E3%83%BB-%E8%B1%86%E7%9F%A5%E8%AD%98)
  - [◆ コマンドの実行パス](#%E2%97%86-%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E5%AE%9F%E8%A1%8C%E3%83%91%E3%82%B9)
  - [◆ ssh接続時に表示される文言](#%E2%97%86-ssh%E6%8E%A5%E7%B6%9A%E6%99%82%E3%81%AB%E8%A1%A8%E7%A4%BA%E3%81%95%E3%82%8C%E3%82%8B%E6%96%87%E8%A8%80)
  - [◆ bash設定](#%E2%97%86-bash%E8%A8%AD%E5%AE%9A)
- [２．コマンド](#%EF%BC%92%EF%BC%8E%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89)
- [３．シェル](#%EF%BC%93%EF%BC%8E%E3%82%B7%E3%82%A7%E3%83%AB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
<br>

### １．設定 ・ 豆知識
---
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
#### ◆ ssh接続時に表示される文言
Message of the dayの略
```
/etc/motd
```
#### ◆ bash設定
・.bash_profile  
→ ログイン時にのみ実行される。  
→ 環境変数を設定する (export する変数)  
・.bashrc  
→ エイリアスを定義する  
→ 環境変数でない変数を設定する (export しない変数)

<br>

### ２．コマンド
---

<br>

### ３．シェル
---
