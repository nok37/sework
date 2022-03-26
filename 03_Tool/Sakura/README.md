# サクラエディタ

<!-- TOC -->

- [１．設定](#１．設定)
    - [トピックツリー](#トピックツリー)
- [２．マクロ](#２．マクロ)
    - [よく使うやつ](#よく使うやつ)
        - [選択文字をハイライト・コピーする](#選択文字をハイライト・コピーする)
        - [選択文字をハイライト・全てマークする](#選択文字をハイライト・全てマークする)
        - [行を選択して外部コマンド(cmd_exe)を実行する](#行を選択して外部コマンドcmd_exeを実行する)
- [３．便利な使い方](#３．便利な使い方)

<!-- /TOC -->
---
<br>
<!-- NEXT INDENT -->

<a id="markdown-１．設定" name="１．設定"></a>
## １．設定

<a id="markdown-トピックツリー" name="トピックツリー"></a>
### トピックツリー
```
★★★★★タグ★★★★★
====================================================================================================
★大見出し（凡例）
====================================================================================================
--------------------------------------------------
◆見出し
--------------------------------------------------
■小見出し
・リスト
```

<br>
<!-- NEXT INDENT -->

<a id="markdown-２．マクロ" name="２．マクロ"></a>
## ２．マクロ

<a id="markdown-よく使うやつ" name="よく使うやつ"></a>
### よく使うやつ

<a id="markdown-選択文字をハイライト・コピーする" name="選択文字をハイライト・コピーする"></a>
#### 選択文字をハイライト・コピーする

```java
// highlight.mac
// 選択文字をハイライト・コピーする
S_SelectWord(0);
S_SearchClearMark(0);
S_Copy();
```

<a id="markdown-選択文字をハイライト・全てマークする" name="選択文字をハイライト・全てマークする"></a>
#### 選択文字をハイライト・全てマークする

```java
// booking.mac
// 選択文字をハイライト・全てマークする
S_SelectWord(0);
S_SearchClearMark(0);
S_BookmarkPattern('', 0);
```

<a id="markdown-行を選択して外部コマンドcmd_exeを実行する" name="行を選択して外部コマンドcmd_exeを実行する"></a>
#### 行を選択して外部コマンド(cmd_exe)を実行する
```java
// cmd_exe.mac
// 行を選択して外部コマンド(cmd_exe)を実行する
GoLineTop(0);
GoLineEnd_Sel(0);
ExecCommand('cmd_exe "$C"', 0);
```

<br>
<!-- NEXT INDENT -->

<a id="markdown-３．便利な使い方" name="３．便利な使い方"></a>
## ３．便利な使い方

<br>
<!-- NEXT INDENT -->