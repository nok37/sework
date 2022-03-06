# Windows

## 目次
<!-- TOC -->

- [１．設定](#１．設定)
    - [◆ プロキシ](#◆-プロキシ)
- [２．コマンドプロンプト(cmd)](#２．コマンドプロンプトcmd)
    - [◆ 全般](#◆-全般)
    - [◆ curl　#サーバへデータ転送を行う](#◆-curl　サーバへデータ転送を行う)
    - [◆ dir　#配下のファイルを一覧で取得](#◆-dir　配下のファイルを一覧で取得)
    - [◆ doskey　#マクロ（エイリアス）の登録](#◆-doskey　マクロエイリアスの登録)
    - [◆ fc　#ファイルの比較を行う](#◆-fc　ファイルの比較を行う)
    - [◆ find　#ファイル内の文字列を検索する](#◆-find　ファイル内の文字列を検索する)
    - [◆ findstr　#findの多機能版](#◆-findstr　findの多機能版)
    - [◆ net　ネットワーク関係の設定や現在の状態を表示する](#◆-net　ネットワーク関係の設定や現在の状態を表示する)
    - [◆ netsh　#ネットワーク関係のパラメータの設定](#◆-netsh　ネットワーク関係のパラメータの設定)
    - [◆ pushd / popd　#カレントディレクトリを変更](#◆-pushd--popd　カレントディレクトリを変更)
    - [◆ tree　#配下のファイルをツリー階層で取得](#◆-tree　配下のファイルをツリー階層で取得)
- [３．バッチファイル(bat)](#３．バッチファイルbat)
    - [◆ 全般・設定](#◆-全般・設定)
- [４．プログラムから実行(win + r)](#４．プログラムから実行win--r)
    - [◆ まとめ](#◆-まとめ)
- [５．PowerShell](#５．powershell)
    - [◆ tnc](#◆-tnc)
- [６．その他ショートカット](#６．その他ショートカット)
    - [◆ win](#◆-win)

<!-- /TOC -->
<br>

<a id="markdown-１．設定" name="１．設定"></a>
### １．設定
---
<a id="markdown-◆-プロキシ" name="◆-プロキシ"></a>
#### ◆ プロキシ

```cmd
rem ユーザ／パスワードの設定
set HTTP_PROXY=http://username:password@proxyhost:port
set HTTPS_PROXY=http://username:password@proxyhost:port
```
※WinHTTPを利用したHTTP通信が発生する場合

```cmd
rem IEからプロキシ設定を読み込む
> netsh winhttp import proxy source=ie

rem 手書きで設定する
> netsh winhttp set proxy proxy-server="http://proxyserver:8080"
```

<br>

<a id="markdown-２．コマンドプロンプトcmd" name="２．コマンドプロンプトcmd"></a>
### ２．コマンドプロンプト(cmd)
---

<a id="markdown-◆-全般" name="◆-全般"></a>
#### ◆ 全般
| コマンド | メモ |
| --- | --- |
| F7 | 履歴の表示 |
| hostname | ホスト名の表示 |
| winver | Windowsのバージョン情報 |
| systeminfo | システム情報の表示 |

<a id="markdown-◆-curl　サーバへデータ転送を行う" name="◆-curl　サーバへデータ転送を行う"></a>
#### ◆ curl　#サーバへデータ転送を行う

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

<a id="markdown-◆-dir　配下のファイルを一覧で取得" name="◆-dir　配下のファイルを一覧で取得"></a>
#### ◆ dir　#配下のファイルを一覧で取得

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

<a id="markdown-◆-doskey　マクロエイリアスの登録" name="◆-doskey　マクロエイリアスの登録"></a>
#### ◆ doskey　#マクロ（エイリアス）の登録

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

rem マクロの読み込み
>doskey /macrofile=c:\test\macros.txt
```

<a id="markdown-◆-fc　ファイルの比較を行う" name="◆-fc　ファイルの比較を行う"></a>
#### ◆ fc　#ファイルの比較を行う
※デフォルトはASCII

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

<a id="markdown-◆-find　ファイル内の文字列を検索する" name="◆-find　ファイル内の文字列を検索する"></a>
#### ◆ find　#ファイル内の文字列を検索する

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

<a id="markdown-◆-findstr　findの多機能版" name="◆-findstr　findの多機能版"></a>
#### ◆ findstr　#findの多機能版

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



<a id="markdown-◆-net　ネットワーク関係の設定や現在の状態を表示する" name="◆-net　ネットワーク関係の設定や現在の状態を表示する"></a>
#### ◆ net　ネットワーク関係の設定や現在の状態を表示する

```cmd
rem ネットワークドライブの割当・削除
>net use p: \\192.168.11.2\share1\VIDEO
>net use p: /delete

rem 認証ありの場合
>net use p: \\192.168.11.2\share password /user:naoki
```

<a id="markdown-◆-netsh　ネットワーク関係のパラメータの設定" name="◆-netsh　ネットワーク関係のパラメータの設定"></a>
#### ◆ netsh　#ネットワーク関係のパラメータの設定

```cmd
rem 変数設定
>set interface_name=イーサネット
>set ip_address=192.xx
>set subnet_mask=255.255.255.0
>set default_gateway=192.xx
>set dns_server1=192.xx
>set dns_server2=192.xx

rem IP アドレスを固定
>netsh interface ipv4 set add name="%interface_name%" source=static addr="%ip_address%" mask="%subnet_mask%" gateway="%default_gateway%" gwmetric=1

rem IP アドレスを動的に変更
>netsh interface ipv4 set add name="%interface_name%" source=auto gwmetric=1

rem DNS1を変更
netsh interface ipv4 set dns name="%interface_name%" source=static addr="%dns_server1%" register=non validate=no

rem DNS2を変更
netsh interface ipv4 add dns name="%interface_name%" addr="%dns_server2%" index=2 validate=no

rem 状態確認
netsh interface ip show config
```

<a id="markdown-◆-pushd--popd　カレントディレクトリを変更" name="◆-pushd--popd　カレントディレクトリを変更"></a>
#### ◆ pushd / popd　#カレントディレクトリを変更
拡張機能では一時的にネットワークドライブの作成が可能。

```cmd
>pushd \\192.168.11.2\share1\VIDEO

Z:\VIDEO>
Z:\VIDEO>popd

C:\Users\naoki>
```

<a id="markdown-◆-tree　配下のファイルをツリー階層で取得" name="◆-tree　配下のファイルをツリー階層で取得"></a>
#### ◆ tree　#配下のファイルをツリー階層で取得

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

<br>

<a id="markdown-３．バッチファイルbat" name="３．バッチファイルbat"></a>
### ３．バッチファイル(bat)
---

<a id="markdown-◆-全般・設定" name="◆-全般・設定"></a>
#### ◆ 全般・設定
| コマンド | メモ |
| --- | --- |

<br>

<a id="markdown-４．プログラムから実行win--r" name="４．プログラムから実行win--r"></a>
### ４．プログラムから実行(win + r)
---

<a id="markdown-◆-まとめ" name="◆-まとめ"></a>
#### ◆ まとめ
| コマンド | メモ |
| --- | --- |
| cmd | Ctrl + Shift + Enterで管理者として実行 |
| cmd.exe /k ini.bat | バッチファイルを実行して起動※１ |
| shell:startup | スタートアップ |
| shell:Desktop | デスクトップ |
| winver | Windowsのバージョン情報 |
| mstsc | リモートデスクトップ接続 |
| taskmgr | タスクマネージャー |
| control | コントロールパネル |
| control printers | プリンターとFAX |
| ncpa.cpl | ネットワーク接続 |
| msinfo32 | システム情報 |


<br>
※１　初期バッチファイルの例

```bat
@echo off
rem ini.bat(sjisで保存すること)
doskey app=appwiz.cpl
doskey cm=control /name Microsoft.CredentialManager
doskey fw=firewall.cpl
doskey inet=inetcpl.cpl
doskey wu=start ms-settings:windowsupdate
doskey about=start ms-settings:about

echo *****ショートカット一覧*****
echo プログラムと機能[app]
echo 資格情報マネージャー[cm]
echo ファイヤーウォール[fw]
echo インターネットオプション[inet]
echo Windowsアップデート[wu]
echo システムバージョン情報[about]
```

<br>

<a id="markdown-５．powershell" name="５．powershell"></a>
### ５．PowerShell
---

<a id="markdown-◆-tnc" name="◆-tnc"></a>
#### ◆ tnc
Test-NetConnection

```ps
> tnc 127.0.0.1 -p 443
ComputerName           : 127.0.0.1
RemoteAddress          : 127.0.0.1
RemotePort             : 443
InterfaceAlias         : Loopback Pseudo-Interface 1
SourceAddress          : 127.0.0.1
PingSucceeded          : True
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : False
```

<br>

<a id="markdown-６．その他ショートカット" name="６．その他ショートカット"></a>
### ６．その他ショートカット  
---

<a id="markdown-◆-win" name="◆-win"></a>
#### ◆ win
| コマンド | メモ |
| --- | --- |
| win + 1（～9） | タスクバーのアプリを実行 |
| ctrl + win + o | スクリーンキーボード開く |

