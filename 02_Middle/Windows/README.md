# Windows

<!-- TOC -->

- [１．設定](#１．設定)
    - [プロキシ](#プロキシ)
- [２．コマンドプロンプト(cmd)](#２．コマンドプロンプトcmd)
    - [全般](#全般)
    - [curl　#サーバへデータ転送を行う](#curl　サーバへデータ転送を行う)
    - [dir　#配下のファイルを一覧で取得](#dir　配下のファイルを一覧で取得)
    - [doskey　#マクロ（エイリアス）の登録](#doskey　マクロエイリアスの登録)
    - [fc　#ファイルの比較を行う](#fc　ファイルの比較を行う)
    - [find　#ファイル内の文字列を検索する](#find　ファイル内の文字列を検索する)
    - [findstr　#findの多機能版](#findstr　findの多機能版)
    - [net　#ネットワーク関係の設定や現在の状態を表示する](#net　ネットワーク関係の設定や現在の状態を表示する)
    - [netsh　#ネットワーク関係のパラメータの設定](#netsh　ネットワーク関係のパラメータの設定)
    - [pushd / popd　#カレントディレクトリを変更](#pushd--popd　カレントディレクトリを変更)
    - [tree　#配下のファイルをツリー階層で取得](#tree　配下のファイルをツリー階層で取得)
- [３．バッチファイル(bat)](#３．バッチファイルbat)
    - [コメント](#コメント)
    - [独自のバッチファイル](#独自のバッチファイル)
        - [仕事開始（start.bat）](#仕事開始startbat)
- [４．プログラムから実行(win + r)](#４．プログラムから実行win--r)
    - [設定系](#設定系)
    - [アプリ起動系](#アプリ起動系)
    - [独自コマンドの実行](#独自コマンドの実行)
- [５．PowerShell](#５．powershell)
    - [tnc　#テスト接続Test-NetConnection](#tnc　テスト接続test-netconnection)
- [６．その他ショートカット](#６．その他ショートカット)
    - [win](#win)

<!-- /TOC -->
---
<br>
<!-- NEXT INDENT -->

<a id="markdown-１．設定" name="１．設定"></a>
## １．設定

<a id="markdown-プロキシ" name="プロキシ"></a>
### プロキシ

* 基本的な設定
    ```bat
    rem ユーザ／パスワードの設定
    set HTTP_PROXY=http://username:password@proxyhost:port
    set HTTPS_PROXY=http://username:password@proxyhost:port
    ```

* WinHTTPを利用したHTTP通信が発生する場合
    ```bat
    rem IEからプロキシ設定を読み込む
    > netsh winhttp import proxy source=ie

    rem 手書きで設定する
    > netsh winhttp set proxy proxy-server="http://proxyserver:8080"
    ```

<br>
<!-- NEXT INDENT -->

<a id="markdown-２．コマンドプロンプトcmd" name="２．コマンドプロンプトcmd"></a>
## ２．コマンドプロンプト(cmd)

<a id="markdown-全般" name="全般"></a>
### 全般

* 基本
    | コマンド | メモ |
    | --- | --- |
    | F7 | 履歴の表示 |
    | hostname | ホスト名の表示 |
    | winver | Windowsのバージョン情報 |
    | systeminfo | システム情報の表示 |

<a id="markdown-curl　サーバへデータ転送を行う" name="curl　サーバへデータ転送を行う"></a>
### curl　#サーバへデータ転送を行う

* 基本
    ```bat
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

<a id="markdown-dir　配下のファイルを一覧で取得" name="dir　配下のファイルを一覧で取得"></a>
### dir　#配下のファイルを一覧で取得

* 基本
    ```bat
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

<a id="markdown-doskey　マクロエイリアスの登録" name="doskey　マクロエイリアスの登録"></a>
### doskey　#マクロ（エイリアス）の登録

* 基本
    ```bat
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

<a id="markdown-fc　ファイルの比較を行う" name="fc　ファイルの比較を行う"></a>
### fc　#ファイルの比較を行う
※デフォルトはASCII

* 基本
    ```bat
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

<a id="markdown-find　ファイル内の文字列を検索する" name="find　ファイル内の文字列を検索する"></a>
### find　#ファイル内の文字列を検索する

* 基本
    ```bat
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

<a id="markdown-findstr　findの多機能版" name="findstr　findの多機能版"></a>
### findstr　#findの多機能版

* 基本
    ```bat
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

<a id="markdown-net　ネットワーク関係の設定や現在の状態を表示する" name="net　ネットワーク関係の設定や現在の状態を表示する"></a>
### net　#ネットワーク関係の設定や現在の状態を表示する

* 基本
    ```bat
    rem ネットワークドライブの割当・削除
    >net use p: \\192.168.11.2\share1\VIDEO
    >net use p: /delete

    rem 認証ありの場合
    >net use p: \\192.168.11.2\share password /user:naoki
    ```

<a id="markdown-netsh　ネットワーク関係のパラメータの設定" name="netsh　ネットワーク関係のパラメータの設定"></a>
### netsh　#ネットワーク関係のパラメータの設定

* 便利な使い方
    ```bat
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

<a id="markdown-pushd--popd　カレントディレクトリを変更" name="pushd--popd　カレントディレクトリを変更"></a>
### pushd / popd　#カレントディレクトリを変更

* 基本
    ```bat
    rem スタックに保存
    C:\Users\naoki>pushd C:\Users

    rem 他の作業等実施
    C:\Users>cd C:\Users\naoki\Desktop
    ...

    rem スタックから取り出し
    C:\Users\naoki\Desktop>popd
    C:\Users\naoki>
    ```

* 拡張機能では一時的にネットワークドライブの作成が可能
    ```bat
    rem ネットワークドライブの割り当て
    >pushd \\192.168.11.2\share1\VIDEO

    rem 一次的にzドライブが割り当てられた
    Z:\VIDEO>

    rem 割り当て解除
    Z:\VIDEO>popd
    C:\Users\naoki>
    ```

<a id="markdown-tree　配下のファイルをツリー階層で取得" name="tree　配下のファイルをツリー階層で取得"></a>
### tree　#配下のファイルをツリー階層で取得

* 基本
    ```bat
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
<!-- NEXT INDENT -->

<a id="markdown-３．バッチファイルbat" name="３．バッチファイルbat"></a>
## ３．バッチファイル(bat)

<a id="markdown-コメント" name="コメント"></a>
### コメント

```bat
rem コメント
```

<a id="markdown-独自のバッチファイル" name="独自のバッチファイル"></a>
### 独自のバッチファイル

<a id="markdown-仕事開始startbat" name="仕事開始startbat"></a>
#### 仕事開始（start.bat）

```bat
@echo off
rem ########################################
rem # 名前：仕事開始
rem # 機能：仕事開始用にプロセスを起動する。
rem # 備考：
rem ########################################


```

<br>
<!-- NEXT INDENT -->

<a id="markdown-４．プログラムから実行win--r" name="４．プログラムから実行win--r"></a>
## ４．プログラムから実行(win + r)

<a id="markdown-設定系" name="設定系"></a>
### 設定系
| コマンド | 実行内容 |
| --- | --- |
| winver | Windowsのバージョン情報 |
| control | コントロールパネル |
| taskmgr | タスクマネージャー |
| control printers | プリンターとFAX |
| ncpa.cpl | ネットワーク接続 |
| msinfo32 | システム情報 |
| \ | Cドライブを開く |

<a id="markdown-アプリ起動系" name="アプリ起動系"></a>
### アプリ起動系

| コマンド | メモ |
| --- | --- |
| cmd | ctrl + Shift + Enterで管理者として実行 |
| shell:startup | スタートアップ※PC起動で実行されるファイル |
| mstsc | リモートデスクトップ接続(MicroSoft Terminal Services Client) |

powershell.exe start shell:AppsFolder\Microsoft.MicrosoftEdge_8wekyb3d8bbwe!MicrosoftEdge '-private %OPENFILE%'　Edgeのプライベート起動


<a id="markdown-独自コマンドの実行" name="独自コマンドの実行"></a>
### 独自コマンドの実行

1. 任意のコマンド格納フォルダを用意

    ```bat
    rem 例
    C:\shortcut
    ```

2. 先ほどのフォルダにパスを通す  
⇒ ユーザの環境変数の「Path」に1のフォルダを追加

3. 以下のbatファイルを格納しておく
	```bat
	@echo off
	rem #######################################################
	rem # ファイル名：ini.bat
	rem # ファイル概要：任意のコマンドを作成し表示する。
	rem # 備考：sjisで保存してください。
	rem #######################################################

	rem ====================
	rem = メイン処理
	rem ====================
	cd %~dp0
	echo ★★★★★設定一覧★★★★★
	call :s_set 設定 set ms-settings:
	call :s_set Windows更新 wu ms-settings:windowsupdate
	call :s_set ファイヤーウォール fw firewall.cpl
	call :s_set アプリ app appwiz.cpl
	call :s_set エクスプローラー exp explorer
	echo ★★★★★★★★★★★★★★
	echo;
	pause

	rem ====================
	rem = 設定処理
	rem ====================
	:s_set
	echo ・%1 [%2]
	echo start "" %3 > %2.bat
	exit /b
	```
4. win + r　から「ini」と入力する  
⇒ 実行ファイルが作成され、作成されたコマンド内容が表示される。

5. win + r　から「set」などの独自のコマンドを実行できる！

<br>
<!-- NEXT INDENT -->

<a id="markdown-５．powershell" name="５．powershell"></a>
## ５．PowerShell

<a id="markdown-tnc　テスト接続test-netconnection" name="tnc　テスト接続test-netconnection"></a>
### tnc　#テスト接続Test-NetConnection

* 基本
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
<!-- NEXT INDENT -->

<a id="markdown-６．その他ショートカット" name="６．その他ショートカット"></a>
## ６．その他ショートカット  

<a id="markdown-win" name="win"></a>
### win
| コマンド | メモ |
| --- | --- |
| win + 1（～9） | タスクバーのアプリを実行 |
| ctrl + win + o | スクリーンキーボード開く |

<br>
<!-- NEXT INDENT -->