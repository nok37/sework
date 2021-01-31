# Windows

## 目次
<!-- TOC -->

- [１．設定](#１．設定)
    - [◆ hoge](#◆-hoge)
- [２．コマンドプロンプト(cmd)](#２．コマンドプロンプトcmd)
    - [◆ 全般](#◆-全般)
    - [◆ tree](#◆-tree)
    - [◆ dir](#◆-dir)
    - [◆ find](#◆-find)
    - [◆ findstr](#◆-findstr)
    - [◆ fc](#◆-fc)
    - [◆ curl](#◆-curl)
    - [◆ doskey](#◆-doskey)
- [３．バッチファイル(bat)](#３．バッチファイルbat)
    - [◆ hoge](#◆-hoge-1)
- [４．プログラムから実行(win + r)](#４．プログラムから実行win--r)
    - [◆ ファイル操作系](#◆-ファイル操作系)

<!-- /TOC -->
<br>

<a id="markdown-１．設定" name="１．設定"></a>
### １．設定
---
<a id="markdown-◆-hoge" name="◆-hoge"></a>
#### ◆ hoge
<br>

<a id="markdown-２．コマンドプロンプトcmd" name="２．コマンドプロンプトcmd"></a>
### ２．コマンドプロンプト(cmd)
---

<a id="markdown-◆-全般" name="◆-全般"></a>
#### ◆ 全般
| コマンド | メモ（★便利度） |
| --- | --- |
| F7 | 履歴の表示 |
| hostname | ホスト名の表示 |
| systeminfo | システム情報の表示★★★ |




<a id="markdown-◆-tree" name="◆-tree"></a>
#### ◆ tree
配下のファイルをツリー階層で取得する。
```cmd
> tree /f
C:.
│  TEST1.xlsx
│  TEST2.xlsx
│
└─sub
        TEST3.xlsx
        TEST4.xlsx
```

<a id="markdown-◆-dir" name="◆-dir"></a>
#### ◆ dir
配下のファイルを一覧で取得する。
```cmd
rem ディレクトリのみ、ファイル名のみ
>dir /AD /B
sub

rem ディレクトリ以外（ファイルのみ）、ファイル名のみ
rem サブフォルダを含む、名前昇順
>dir /A-D /B /S /ON
C:\Users\naoki\Desktop\test\TEST1.xlsx
C:\Users\naoki\Desktop\test\TEST2.xlsx
C:\Users\naoki\Desktop\test\sub\TEST3.xlsx
C:\Users\naoki\Desktop\test\sub\TEST4.xlsx
```

<a id="markdown-◆-find" name="◆-find"></a>
#### ◆ find
ファイル内の文字列を検索する。
```cmd
rem 指定した単語の検索（grepに相当）
>find "ERROR" < debug.log
[0122/072347.188:ERROR:]
[0126/193107.304:ERROR:]
[0126/224203.298:ERROR:]
[0127/182118.424:ERROR:]

rem 指定した単語が含まない行を検索（grep -vに相当）
>find /V "424" < debug.log
[0122/072347.188:ERROR:]
[0126/193107.304:ERROR:]
[0126/224203.298:ERROR:]

rem ファイルの行数を表示（wc -lに相当）
>find /C /V "" < debug.log
10
```

<a id="markdown-◆-findstr" name="◆-findstr"></a>
#### ◆ findstr
findの多機能版。
```cmd
rem OR検索
>systeminfo | findstr "Host OS"
Host Name:                 ******
OS Name:                   Microsoft Windows 10 Pro
OS Version:                ******
OS Manufacturer:           ******
OS Configuration:          ******
OS Build Type:             ******
System Manufacturer:       ******
BIOS Version:              ******

rem 空白を含めて検索
>systeminfo | findstr /C:"Host Name" /C:"OS Name"
Host Name:                 ******
OS Name:                   Microsoft Windows 10 Pro
```

<a id="markdown-◆-fc" name="◆-fc"></a>
#### ◆ fc
ファイルの比較を行う。（※デフォルトはASCII）
```cmd
rem 行数表示
>fc /N debug.log debug3.log
ファイル debug.log と DEBUG3.LOG を比較しています
***** debug.log
    2:  [0126/193107.304:ERROR:]
    3:  [0126/224203.298:ERROR:]
    4:  [0127/182118.424:ERROR:]
***** DEBUG3.LOG
    2:  [0126/193107.304:ERROR:]
    3:  [0126/224201.298:ERROR:]
    4:  [0127/182118.424:ERROR:]
*****

rem バイナリ比較
>fc /B debug.log debug2.log
ファイル debug.log と DEBUG2.LOG を比較しています
FC: 相違点は検出されませんでした
```

<a id="markdown-◆-curl" name="◆-curl"></a>
#### ◆ curl
サーバへデータ転送を行う。
```cmd
rem メソッドの指定
>curl -X GET "http://localhost:8080/api?ymd=202012
[
  {
    "countA": 2,
    "countB": 14,
    "ymd": 202012
  }
]

rem ヘッダーの取得
>curl -I "http://localhost:8080/api?ymd=202012"
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 404
Access-Control-Allow-Origin: *
Server: Werkzeug/1.0.1 Python/3.8.3
Date: Sun, 31 Jan 2021 08:25:10 GMT
```

<a id="markdown-◆-doskey" name="◆-doskey"></a>
#### ◆ doskey
マクロ（エイリアス）の登録。
```cmd
rem マクロの登録
>doskey ls=dir $*
>ls /S /B
C:\Users\naoki\Desktop\test\sub
C:\Users\naoki\Desktop\test\TEST1.xlsx
C:\Users\naoki\Desktop\test\TEST2.xlsx
C:\Users\naoki\Desktop\test\sub\TEST3.xlsx
C:\Users\naoki\Desktop\test\sub\TEST4.xlsx

rem マクロの表示
>doskey /macros
ls=dir $*
```

rem マクロの読み込み
```cmd
>doskey /macrofile=c:\test\macros.txt
```
<br>

<a id="markdown-３．バッチファイルbat" name="３．バッチファイルbat"></a>
### ３．バッチファイル(bat)
---

<a id="markdown-◆-hoge-1" name="◆-hoge-1"></a>
#### ◆ hoge

<br>

<a id="markdown-４．プログラムから実行win--r" name="４．プログラムから実行win--r"></a>
### ４．プログラムから実行(win + r)
---

<a id="markdown-◆-ファイル操作系" name="◆-ファイル操作系"></a>
#### ◆ ファイル操作系
| コマンド | メモ |
| --- | --- |
| shell:startup | スタートアップ |
| shell:Desktop | デスクトップ |
| cmd | Ctrl + Shift + Enterで管理者として実行 |
| winver | Windowsのバージョン情報 |
| mstsc | リモートデスクトップ接続 |
| taskmgr | タスクマネージャー |
| control | コントロールパネル |
| control printers | プリンターとFAX |
| control /name Microsoft.CredentialManager | 資格情報マネージャー |
| inetcpl.cpl | インターネットオプション |
| ncpa.cpl | ネットワーク接続 |
| ms-settings:windowsupdate | Windows Update |

※エイリアスをスタートアップにおいておくと便利！  
```cmd
rem エイリアスファイル作成マクロ
echo @echo off> app.bat
echo start appwiz.cpl>> app.bat
echo @echo off> cm.bat
echo start control /name Microsoft.CredentialManager>> cm.bat
echo @echo off> fw.bat
echo start firewall.cpl>> fw.bat
echo @echo off> inet.bat
echo start inetcpl.cpl>> inet.bat
echo @echo off> proxy.bat
echo start ms-settings:network-proxy>> proxy.bat
echo @echo off> sendto2.bat
echo start shell:sendto>> sendto2.bat
echo @echo off> startup.bat
echo start shell:startup>> startup.bat
echo @echo off> sv.bat
echo start services.msc>> sv.bat
echo @echo off> sysver.bat
echo start msinfo32>> sysver.bat
echo @echo off> tm.bat
echo start taskmgr>> tm.bat
echo @echo off> ts.bat
echo start control schedtasks>> ts.bat
echo @echo off> wu.bat
echo start ms-settings:windowsupdate>> wu.bat
```
