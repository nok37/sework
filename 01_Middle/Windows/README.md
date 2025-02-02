# Windows

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. プロキシ](#11-プロキシ)
- [2. ショートカット](#2-ショートカット)
  - [2.1. 基本](#21-基本)
  - [2.2. リモートPCの操作](#22-リモートpcの操作)
- [3. コマンドプロンプト(cmd)](#3-コマンドプロンプトcmd)
  - [3.1. 設定](#31-設定)
  - [3.2. 変数](#32-変数)
  - [3.3. 【curl】 サーバへデータ転送を行う](#33-curl-サーバへデータ転送を行う)
  - [3.4. 【dir】 配下のファイルを一覧で取得](#34-dir-配下のファイルを一覧で取得)
  - [3.5. 【doskey】 マクロ（エイリアス）の登録](#35-doskey-マクロエイリアスの登録)
  - [3.6. 【fc】 ファイルの比較を行う](#36-fc-ファイルの比較を行う)
  - [3.7. 【find】 ファイル内の文字列を検索する](#37-find-ファイル内の文字列を検索する)
  - [3.8. 【findstr】 findの多機能版](#38-findstr-findの多機能版)
  - [3.9. 【net】 ネットワーク関係の設定や現在の状態を表示する](#39-net-ネットワーク関係の設定や現在の状態を表示する)
  - [3.10. 【netsh】 ネットワーク関係のパラメータの設定](#310-netsh-ネットワーク関係のパラメータの設定)
  - [3.11. 【pushd／popd】 カレントディレクトリを変更](#311-pushdpopd-カレントディレクトリを変更)
  - [3.12. 【ssh】 SSHで接続（TeraTermの代替）](#312-ssh-sshで接続teratermの代替)
  - [3.13. 【tree】 配下のファイルをツリー階層で取得](#313-tree-配下のファイルをツリー階層で取得)
  - [3.14. 【where】 検索パターンに一致するファイルリストを表示](#314-where-検索パターンに一致するファイルリストを表示)
- [4. バッチファイル(bat)](#4-バッチファイルbat)
  - [4.1. コメント](#41-コメント)
  - [4.2. 独自のバッチファイル](#42-独自のバッチファイル)
    - [4.2.1. 仕事開始（start.bat）](#421-仕事開始startbat)
- [5. プログラムから実行(win + r)](#5-プログラムから実行win--r)
  - [5.1. 設定系](#51-設定系)
  - [5.2. アプリ起動系](#52-アプリ起動系)
  - [5.3. 独自コマンドの実行](#53-独自コマンドの実行)
- [6. PowerShell](#6-powershell)
  - [6.1. tnc　#テスト接続Test-NetConnection](#61-tncテスト接続test-netconnection)
- [7. ツール](#7-ツール)
  - [7.1. 7zip](#71-7zip)
  - [7.2. 他](#72-他)
---
<br>
<!-- /TOC -->

## 1. 設定

### 1.1. プロキシ

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

## 2. ショートカット

### 2.1. 基本
* 整理中
    | コマンド | メモ |
    | --- | --- |
    | win + 1（～9） | タスクバーのアプリを実行 |
    | ctrl + win + o | スクリーンキーボード開く |

### 2.2. リモートPCの操作

* ウィンドウの切り替え 
    | コマンド | メモ |
    | --- | --- |
    | Alt + PgUp | アクティブウィンドウの切り替え（Alt + Tab） |

* スクリーンショット
    | コマンド | メモ |
    | --- | --- |
    | Ctrl + Alt + 「+」 | 全画面 |
    | Ctrl + Alt + 「-」 | アクティブウインドウのみ |

<br>

## 3. コマンドプロンプト(cmd)
ctrl + r → cmd で起動する。<br>
※ctrl + shift + Enterで管理者権限で起動できる。

### 3.1. 設定
* 基本
    | コマンド | メモ |
    | --- | --- |
    | F7 | 履歴の表示 |
    | hostname | ホスト名の表示 |
    | winver | Windowsのバージョン情報 |
    | systeminfo | システム情報の表示 |

### 3.2. 変数

* 切り出し
    | コマンド | メモ |
    | --- | --- |
    | %STR:~m% | m文字目から最後まで |
    | %STR:~m,n% | m文字目からn文字分 |
    | %STR:~-m% | 後ろからm文字目から最後まで |
    | %STR:~-m,n% | 後ろからm文字目からn文字分 |
    ※開始位置は0文字目

    ```bat
    > set STR=12345678
    > echo %STR:~5%
    678
    > echo %STR:~5,2%
    67
    > echo %STR:~-2%
    78
    > echo %STR:~-2,1%
    7
    ```

### 3.3. 【curl】 サーバへデータ転送を行う

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

### 3.4. 【dir】 配下のファイルを一覧で取得

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

### 3.5. 【doskey】 マクロ（エイリアス）の登録

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

### 3.6. 【fc】 ファイルの比較を行う
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

### 3.7. 【find】 ファイル内の文字列を検索する

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

### 3.8. 【findstr】 findの多機能版

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

### 3.9. 【net】 ネットワーク関係の設定や現在の状態を表示する

* 基本
    ```bat
    rem ネットワークドライブの割当・削除
    >net use p: \\192.168.11.2\share1\VIDEO
    >net use p: /delete

    rem 認証ありの場合
    >net use p: \\192.168.11.2\share password /user:naoki
    ```

### 3.10. 【netsh】 ネットワーク関係のパラメータの設定

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

### 3.11. 【pushd／popd】 カレントディレクトリを変更

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

### 3.12. 【ssh】 SSHで接続（TeraTermの代替）

* 基本
    ```bat
    > ssh 【IP】-l 【ユーザ名】
    ```

### 3.13. 【tree】 配下のファイルをツリー階層で取得

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

### 3.14. 【where】 検索パターンに一致するファイルリストを表示
C:\Users\dues1\Documents\github\sework>WHERE /R .\04_Other * /T
      1350   2023/11/29      10:00:09  C:\Users\dues1\Documents\github\sework\04_Other\README.md
       571   2024/02/24       3:02:02  C:\Users\dues1\Documents\github\sework\04_Other\c4\README.md


<br>

## 4. バッチファイル(bat)

### 4.1. コメント

```bat
rem コメント
```

### 4.2. 独自のバッチファイル

#### 4.2.1. 仕事開始（start.bat）

```bat
@echo off
rem ########################################
rem # 名前：仕事開始
rem # 機能：仕事開始用にプロセスを起動する。
rem # 備考：
rem ########################################


```

<br>

## 5. プログラムから実行(win + r)

### 5.1. 設定系
| コマンド | 実行内容 |
| --- | --- |
| winver | Windowsのバージョン情報 |
| control | コントロールパネル |
| taskmgr | タスクマネージャー |
| control printers | プリンターとFAX |
| ncpa.cpl | ネットワーク接続 |
| msinfo32 | システム情報 |
| \ | Cドライブを開く |

### 5.2. アプリ起動系

| コマンド | メモ |
| --- | --- |
| cmd | ctrl + Shift + Enterで管理者として実行 |
| shell:startup | スタートアップ※PC起動で実行されるファイル |
| mstsc | リモートデスクトップ接続(MicroSoft Terminal Services Client) |

powershell.exe start shell:AppsFolder\Microsoft.MicrosoftEdge_8wekyb3d8bbwe!MicrosoftEdge '-private %OPENFILE%'　Edgeのプライベート起動


### 5.3. 独自コマンドの実行

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

## 6. PowerShell

### 6.1. tnc　#テスト接続Test-NetConnection

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

## 7. ツール

### 7.1. 7zip
* ファイルの使用用途
    | exeファイル | 用途 |
    | --- | --- |
    | 7z.exe | 7-Zip Console |
    | 7zG.exe | 7-Zip GUI |
    | 7zFM.exe | 7-Zip File Manager |

* 使用例
    ```cmd
    rem zipファイルの中身リスト取得
    "C:\Program Files\7-Zip\7z.exe" l aaa.zip
    ```

### 7.2. 他
```cmd
--SVNの指定日以降のログ履歴を取得
svn log svn://xx.xx.xxx.xx/hoge -r {2024-01-01}:HEAD -v
```

<br>
