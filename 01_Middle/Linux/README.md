# Linux

<!-- TOC -->
- [1. 設定](#1-設定)
  - [1.1. bash設定](#11-bash設定)
  - [1.2. コマンドの実行パス](#12-コマンドの実行パス)
  - [1.3. cron](#13-cron)
  - [1.4. 特殊なデバイス（/dev/\*\*\*系）](#14-特殊なデバイスdev系)
  - [1.5. SSH鍵](#15-ssh鍵)
  - [1.6. 豆知識](#16-豆知識)
    - [1.6.1. ssh接続時に表示される文言 - motd](#161-ssh接続時に表示される文言---motd)
- [2. ショートカット](#2-ショートカット)
  - [2.1. ターミナル操作系](#21-ターミナル操作系)
  - [2.2. カーソル・文字操作系](#22-カーソル文字操作系)
  - [2.3. その他](#23-その他)
- [3. コマンド](#3-コマンド)
  - [3.1. 【ac】 ユーザの接続時間についての統計を表示する](#31-ac-ユーザの接続時間についての統計を表示する)
  - [3.2. 【awk】 パターン検索と文字処理](#32-awk-パターン検索と文字処理)
  - [3.3. 【bc】 任意精度の計算言語](#33-bc-任意精度の計算言語)
  - [3.4. 【cancel】 ジョブの取り消しを行う](#34-cancel-ジョブの取り消しを行う)
  - [3.5. 【cd】 カレントディレクトリの変更](#35-cd-カレントディレクトリの変更)
  - [3.6. 【chmod】 ファイルの権限を変更する](#36-chmod-ファイルの権限を変更する)
  - [3.7. 【cp】コピー](#37-cpコピー)
  - [3.8. 【cupsdisable】 プリンタ無効化](#38-cupsdisable-プリンタ無効化)
  - [3.9. 【cupsenable】 プリンタ有効化](#39-cupsenable-プリンタ有効化)
  - [3.10. 【curl 】HTTPなどの通信プロトコルでデータを転送する](#310-curl-httpなどの通信プロトコルでデータを転送する)
  - [3.11. 【cut】 各行から一部分を取り除く](#311-cut-各行から一部分を取り除く)
  - [3.12. 【dc】 無限精度の計算が行える卓上計算機](#312-dc-無限精度の計算が行える卓上計算機)
  - [3.13. 【dd】 ファイルの変換とコピーを行う](#313-dd-ファイルの変換とコピーを行う)
  - [3.14. 【df】 ディスク容量を確認する](#314-df-ディスク容量を確認する)
  - [3.15. 【echo】 テキストの行を表示する](#315-echo-テキストの行を表示する)
  - [3.16. 【eval】 引数を読み込み一つのコマンドとして実行する](#316-eval-引数を読み込み一つのコマンドとして実行する)
  - [3.17. 【find】 条件を満たすファイルを検索する](#317-find-条件を満たすファイルを検索する)
  - [3.18. 【grep】 パターンにマッチする行を表示する](#318-grep-パターンにマッチする行を表示する)
  - [3.19. 【head】 ファイルの最初の部分を表示する](#319-head-ファイルの最初の部分を表示する)
  - [3.20. 【hostname】 システムのホスト名（IPアドレス）を表示・設定する](#320-hostname-システムのホスト名ipアドレスを表示設定する)
  - [3.21. 【ifconfig】 ネットワークインターフェースの管理](#321-ifconfig-ネットワークインターフェースの管理)
  - [3.22. 【jobs】 アクティブなジョブリストの表示](#322-jobs-アクティブなジョブリストの表示)
  - [3.23. 【keytool】 鍵と証明書を管理](#323-keytool-鍵と証明書を管理)
  - [3.24. 【last】 直近のログイン履歴を表示](#324-last-直近のログイン履歴を表示)
  - [3.25. 【lastlog】 全てのユーザーの最終ログインを表示](#325-lastlog-全てのユーザーの最終ログインを表示)
  - [3.26. 【ls】 ファイルリストを表示する](#326-ls-ファイルリストを表示する)
  - [3.27. 【md5sum】 MD5メッセージダイジェストの計算と照合を行う](#327-md5sum-md5メッセージダイジェストの計算と照合を行う)
  - [3.28. 【mt】 磁気テープドライブの操作を制御する](#328-mt-磁気テープドライブの操作を制御する)
  - [3.29. 【nl】 ファイルに行番号を付与する](#329-nl-ファイルに行番号を付与する)
  - [3.30. 【nohup】 ログアウトの影響を受けずコマンドを実行する](#330-nohup-ログアウトの影響を受けずコマンドを実行する)
  - [3.31. 【od】 8進数やその他の形式でダンプする](#331-od-8進数やその他の形式でダンプする)
  - [3.32. 【openssl】 証明書の作成](#332-openssl-証明書の作成)
  - [3.33. 【ps】 現在実行されているプロセスのスナップショットを表示する](#333-ps-現在実行されているプロセスのスナップショットを表示する)
  - [3.34. 【pstree】 現在実行されているプロセスをツリー形式で表示する](#334-pstree-現在実行されているプロセスをツリー形式で表示する)
  - [3.35. 【route】 ルーティングテーブルの管理](#335-route-ルーティングテーブルの管理)
  - [3.36. 【script】 ターミナルの出力内容を記録（ログの代わりに）](#336-script-ターミナルの出力内容を記録ログの代わりに)
  - [3.37. 【sed】 文字列置換などのテキスト処理](#337-sed-文字列置換などのテキスト処理)
  - [3.38. 【tar】 アーカイブの作成](#338-tar-アーカイブの作成)
  - [3.39. 【tee】 出力を複数のファイルやプロセスにリダイレクトする](#339-tee-出力を複数のファイルやプロセスにリダイレクトする)
  - [3.40. 【umask】 デフォルトの権限を決定する](#340-umask-デフォルトの権限を決定する)
  - [3.41. 【unzip】 ファイル解凍をする（zipを参照）](#341-unzip-ファイル解凍をするzipを参照)
  - [3.42. 【vi】 vimを参照](#342-vi-vimを参照)
  - [3.43. 【vim】 高機能なテキストエディタ](#343-vim-高機能なテキストエディタ)
  - [3.44. 【xargs】 引数からコマンドを組み立て実行する](#344-xargs-引数からコマンドを組み立て実行する)
  - [3.45. 【xxd】 2進数でダンプする](#345-xxd-2進数でダンプする)
  - [3.46. 【yum】 RedHat系で利用されるパッケージ管理ツール](#346-yum-redhat系で利用されるパッケージ管理ツール)
  - [3.47. 【w】 ログインしている人とその人がやっていることを表示する](#347-w-ログインしている人とその人がやっていることを表示する)
  - [3.48. 【wc】 各ファイルの改行数、ワード数、バイト数を表示する](#348-wc-各ファイルの改行数ワード数バイト数を表示する)
  - [3.49. 【which】 コマンドのフルパスを表示する](#349-which-コマンドのフルパスを表示する)
  - [3.50. 【whoami】 実行ユーザ名を出力する](#350-whoami-実行ユーザ名を出力する)
  - [3.51. 【zgrep】 圧縮されている可能性のあるファイルで、正規表現の検索をする](#351-zgrep-圧縮されている可能性のあるファイルで正規表現の検索をする)
  - [3.52. 【zip】 ファイル圧縮をする](#352-zip-ファイル圧縮をする)
  - [3.53. 【!!】 直前のコマンドを実行](#353--直前のコマンドを実行)
  - [3.54. 【\> \>\>】 出力リダイレクト／追記](#354---出力リダイレクト追記)
  - [3.55. 【\< \<\<】 入力リダイレクト／追記](#355---入力リダイレクト追記)
  - [3.56. 【;】 コマンドを続けて実行](#356--コマンドを続けて実行)
  - [3.57. 【:】 何もせず正常ステータス(0)を返す](#357--何もせず正常ステータス0を返す)
  - [3.58. 【\&\&】 正常終了の場合実施（ANDリスト）](#358--正常終了の場合実施andリスト)
  - [3.59. 【||】 異常終了の場合実施（ORリスト）](#359--異常終了の場合実施orリスト)
- [4. 演算](#4-演算)
  - [4.1. 【n++ n--】 ポスト（後置）インクリメント／デクリメント](#41-n-n---ポスト後置インクリメントデクリメント)
  - [4.2. 【++n --n】 プレ（前置）インクリメント／デクリメント](#42-n---n-プレ前置インクリメントデクリメント)
  - [4.3. 【+ -】 加算／減算](#43----加算減算)
  - [4.4. 【\* / %】 乗算／除算／剰余](#44----乗算除算剰余)
  - [4.5. 【\*\*】 指数](#45--指数)
  - [4.6. 【\<\< \>\>】 シフト演算](#46---シフト演算)
  - [4.7. 【\&\& ||】論理積／論理和](#47--論理積論理和)
- [5. シェル](#5-シェル)
  - [5.1. 用語説明](#51-用語説明)
    - [5.1.1. シェバン](#511-シェバン)
    - [5.1.2. セカンダリプロンプト](#512-セカンダリプロンプト)
  - [5.2. 引数／特殊変数](#52-引数特殊変数)
  - [5.3. 比較](#53-比較)
    - [5.3.1. 文字列比較](#531-文字列比較)
    - [5.3.2. 数値比較](#532-数値比較)
  - [5.4. サンプル](#54-サンプル)
- [6. 組み合わせ便利コマンド](#6-組み合わせ便利コマンド)
  - [6.1. 無限ループ（while true）](#61-無限ループwhile-true)
  - [6.2. リスト読込（for ～ in）](#62-リスト読込for--in)
  - [6.3. ファイル読込（while read）](#63-ファイル読込while-read)
  - [6.4. ファイル存在確認（if）](#64-ファイル存在確認if)
  - [6.5. 文字列の比較（if）](#65-文字列の比較if)
---
<br>
<!-- /TOC -->

## 1. 設定

### 1.1. bash設定

* .bash_profile  
ログイン時にのみ実行される  
環境変数を設定する (export する変数)  

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

* .bashrc  
シェルを起動する度に実行される  
エイリアスを定義する  
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

### 1.2. コマンドの実行パス
コマンド実行時は左から順にパスを確認しコマンド実行する。  

* パスの確認
  ```bash
  $ echo $PATH
  /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
  ```

* パスの追加
  ```bash
  $ export PATH=$NODE_HOME/bin:$PATH
  ```

### 1.3. cron

* 基本
  ```bash
  # /etc/crontab システムジョブ(root権限で実行される)
  # /var/spool/cron/[user] ユーザジョブ

  # Example of job definition:
  # .---------------- minute (0 - 59)
  # |  .------------- hour (0 - 23)
  # |  |  .---------- day of month (1 - 31)
  # |  |  |  .------- month (1 - 12) OR jan,feb...
  # |  |  |  |  .---- day of week (0 - 6) OR sun,mon...
  # |  |  |  |  |
  # *  *  *  *  * user-name  command to be executed

  # 例）毎日0時にrootメールを削除する
  0 0 * * * cat /dev/null > /var/spool/mail/root
  ```

### 1.4. 特殊なデバイス（/dev/***系）

* /dev/null<br>
  書き込まれたデータをすべて破棄し、読み込んでも何もデータを返さない。<br>
  不要な出力を破棄する時に使用。

* /dev/zero<br>
  0x00（NULL文字）を常に出力し続ける特殊なデバイス。<br>
  NULL文字でデータ上書きする場合などで使用。

### 1.5. SSH鍵

```bash
# 鍵作成
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/takahana/.ssh/id_rsa):
Created directory '/home/takahana/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/takahana/.ssh/id_rsa
Your public key has been saved in /home/takahana/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:Xe2bhDnnSr4vICyVNE4BbKeNc5LcNlhHWjrqUwqrUY0 takahana@nok37
The keys randomart image is:
+---[RSA 3072]----+
|     ....oo      |
|      o *+.  .   |
|     o &++  . .  |
|     oO.Xo . +   |
|    E oBS.. + +  |
|   . +.oo .  = o |
|  . . +. . .. +  |
|   o   .   o..   |
|  .         ++.  |
+----[SHA256]-----+

# 鍵確認
$ ls -l .ssh/*
-rw------- 1 takahana takahana 2655 Mar 23 00:04 .ssh/id_rsa # 秘密鍵
-rw-r--r-- 1 takahana takahana  568 Mar 23 00:04 .ssh/id_rsa.pub # 公開鍵

# 接続先で設定する
$ echo 【公開鍵】 > ~/.ssh/rsa_pub_key
$ cat ~/.ssh/rsa_pub_key >> ~/.ssh/authorized_keys
```


### 1.6. 豆知識

#### 1.6.1. ssh接続時に表示される文言 - motd
Message of the dayの略

```bash
/etc/motd
```

## 2. ショートカット

### 2.1. ターミナル操作系

| ショートカット | 内容 |
| --- | --- |
| ctrl + d  | ログアウト |
| alt + v　 | ターミナルの複製 |
 
### 2.2. カーソル・文字操作系

| ショートカット | 内容 |
| --- | --- |
| ctrl + a | 行頭へ |
| ctrl + e | 行末へ |
| ctrl + w | 直前の単語を削除 |
| ctrl + u | 直前を削除 |

### 2.3. その他

| ショートカット | 内容 |
| --- | --- |
| ctrl + r　| コマンド履歴の検索(*1) |
| ctrl + l　| 画面クリア |

```bash
# *1
# ctrl + r → d
# 前に使用した d から始まるコマンドを呼び出し
(reverse-i-search)`d': date
```

<br>

## 3. コマンド

### 3.1. 【ac】 ユーザの接続時間についての統計を表示する

* 必須レベル：★☆☆☆☆
  
* 使い方
  ```bash
  $ ac -p
          takahana                           102.27
          root                                 0.01
          total      102.28
 
  # 以下バイナリファイルを参照している
  $ ls -l /var/log/wtmp
  -rw-rw-r--. 1 root utmp 26496  4月 21 21:25 /var/log/wtmp
  ```

### 3.2. 【awk】 パターン検索と文字処理

* 必須レベル：★★★★☆<br>
  ※オークと読みます

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | -F 区切り文字 | 区切り文字の指定（デフォルトは空白） |
  | -v 変数名=値 | 変数を定義する |

  |  組み込み変数  |  詳細  |
  | ---- | ---- |
  | ---- | ---- |

  |  文字列操作関数  |  詳細  |
  | ---- | ---- |
  | ---- | ---- |

* 使い方
  ```bash
  # 例１）コマンド実行結果の整形

  # lsコマンド
  $ ls -l /usr/bin/vim*
  -rwxr-xr-x. 1 root root 2337192  8月  9  2019 /usr/bin/vim
  lrwxrwxrwx. 1 root root       3 10月 24  2020 /usr/bin/vimdiff -> vim
  -rwxr-xr-x. 1 root root    2084  8月  9  2019 /usr/bin/vimtutor

  # 9番目（コマンド部分）のみを表示する
  $ ls -l /usr/bin/vim* | awk '{print $9}'
  /usr/bin/vim
  /usr/bin/vimdiff
  /usr/bin/vimtutor
  
  # ちなみに以下コマンドでも同様の操作が可能（9番目以降を取得）
  $ ls -l /usr/bin/vim* | sed -e 's/ \+/ /g'| cut -d' ' -f9-
  /usr/bin/vim
  /usr/bin/vimdiff -> vim
  /usr/bin/vimtutor
  ```

### 3.3. 【bc】 任意精度の計算言語

* 必須レベル：★☆☆☆☆

* 使い方
  ```bash
  # 単純な計算
  # 1 + 2 + 3 + 4 + 5
  $ bc
  bc 1.06.95
  Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
  This is free software with ABSOLUTELY NO WARRANTY.
  For details type `warranty'.
  1+2+3+4+5
  15
  ```

### 3.4. 【cancel】 ジョブの取り消しを行う

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # 印刷ジョブの取り消し
  # 「TESTPRT」のプリンタキューを全削除（※root権限）
  $ cancel -a TESTPRT
  ```

### 3.5. 【cd】 カレントディレクトリの変更

* 必須レベル：★★★★★

* 使い方
  ```bash
  # 絶対パスで移動
  $ cd /home
  $ pwd
  /home

  # 相対パスで移動
  $ cd ./takahana
  $ pwd
  /home/takahana

  # 直前のディレクトリに移動
  $ cd -
  $ pwd
  /home

  # ホームディレクトリに移動
  $ cd ~
  $ pwd
  /home/takahana

  # ホームディレクトリに移動（~は省略可能）
  $ cd
  $ pwd
  /home/takahana
  ```

### 3.6. 【chmod】 ファイルの権限を変更する

* 必須レベル：★★★★★
  
  Read 4, Write 2, eXute 1 の加算で表す<br>
  一般的にディレクトリの場合 755 、ファイルの場合 644<br>
  
  ```bash
  # ディレクトリの場合
  # ユーザ　：読み、書き、実行が可能
  # グループ：読み、実行が可能（移動するのに必要な実行権限がある）
  # その他　：読み、実行が可能（移動するのに必要な実行権限がある）
  drwxr-xr-x. 2 takahana takahana  40  4月 19 00:27 dir

  # ファイルの場合
  # ユーザ　：読み、書き、実行が可能
  # グループ：読みが可能
  # その他　：読みが可能
  -rwxr--r--. 1 takahana takahana 142  1月 24  2021 test.sh
  ```

* 使い方
  ```bash
  # ユーザに実行権限を付与する
  $ chmod u+x file

  # 全員に実行権限を付与する
  $ chmod +x file

  # グループに書き込み権限をその他のユーザーにはすべて禁止する
  $ chmod g+w,o= file

  # 再帰的に変更する
  $ chmod -R 777 dir
  ```
### 3.7. 【cp】コピー

* 必須レベル：★★★★★

* 使い方
  ```bash
  # 権限保持してコピー
  $ cp -p hogehege 【コピー元】 【コピー先】
  ```

* メモ
  * コピー速度<br>
    1. NAS間コピー：5.0～6.0 [GiB/min]　※I/O性能に依存
    2. ネットワーク転送：4.5～7.0 [GiB/min]　※I/O性能＋多重度に依存
  * 拡張ACL<br>
    cp: preserving permissions for 'hogehoge': サポートされていない操作です<br>
    →コピー先ディレクトリが拡張ACLに対応していない場合は警告が表示される

### 3.8. 【cupsdisable】 プリンタ無効化

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # ※root権限
  $ cupsdisable TESTPRT
  ```

### 3.9. 【cupsenable】 プリンタ有効化

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # ※root権限
  $ cupsenable TESTPRT
  ```

### 3.10. 【curl 】HTTPなどの通信プロトコルでデータを転送する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # 基本
  $ curl 'http://localhost:5050/api/' 

  # POSTでよく使う
  $ curl -v -X POST 'http://localhost:5050/api/' -H 'Content-Type: application/json' -H 'Authorization: Bearer XXXX' -d '{"name":"hello", "id":"100"}'

  # 詳細表示
  $ curl -v -X GET 'https://api.github.com/zen'
  Note: Unnecessary use of -X or --request, GET is already inferred.
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                  Dload  Upload   Total   Spent    Left  Speed
    0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 18.179.245.253:443...
  * Connected to api.github.com (18.179.245.253) port 443 (#0)
  * ALPN, offering h2
  * ALPN, offering http/1.1
  * successfully set certificate verify locations:
  *   CAfile: C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
    CApath: none
  } [5 bytes data]
  * TLSv1.3 (OUT), TLS handshake, Client hello (1):
  } [512 bytes data]
  * TLSv1.3 (IN), TLS handshake, Server hello (2):
  { [122 bytes data]
  * TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
  { [19 bytes data]
  * TLSv1.3 (IN), TLS handshake, Certificate (11):
  { [2362 bytes data]
  * TLSv1.3 (IN), TLS handshake, CERT verify (15):
  { [78 bytes data]
  * TLSv1.3 (IN), TLS handshake, Finished (20):
  { [36 bytes data]
  * TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
  } [1 bytes data]
  * TLSv1.3 (OUT), TLS handshake, Finished (20):
  } [36 bytes data]
  * SSL connection using TLSv1.3 / TLS_AES_128_GCM_SHA256
  * ALPN, server accepted to use h2
  * Server certificate:
  *  subject: C=US; ST=California; L=San Francisco; O=GitHub, Inc.; CN=*.github.com
  *  start date: Mar 25 00:00:00 2021 GMT
  *  expire date: Mar 30 23:59:59 2022 GMT
  *  subjectAltName: host "api.github.com" matched certs "*.github.com"
  *  issuer: C=US; O=DigiCert, Inc.; CN=DigiCert High Assurance TLS Hybrid ECC SHA256 2020 CA1
  *  SSL certificate verify ok.
  * Using HTTP2, server supports multi-use
  * Connection state changed (HTTP/2 confirmed)
  * Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
  } [5 bytes data]
  * Using Stream ID: 1 (easy handle 0x265e070)
  } [5 bytes data]
  > GET /zen HTTP/2
  > Host: api.github.com
  > user-agent: curl/7.71.1
  > accept: */*
  >
  { [5 bytes data]
  * TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
  { [57 bytes data]
  * TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
  { [57 bytes data]
  * old SSL session ID is stale, removing
  { [5 bytes data]
  * Connection state changed (MAX_CONCURRENT_STREAMS == 100)!
  } [5 bytes data]
  < HTTP/2 200
  < server: GitHub.com
  < date: Sun, 23 Jan 2022 10:46:05 GMT
  < content-type: text/plain;charset=utf-8
  < access-control-expose-headers: ETag, Link, Location, Retry-After, X-GitHub-OTP, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Used, X-RateLimit-Resource, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval, X-GitHub-Media-Type, X-GitHub-SSO, X-GitHub-Request-Id, Deprecation, Sunset
  < access-control-allow-origin: *
  < strict-transport-security: max-age=31536000; includeSubdomains; preload
  < x-frame-options: deny
  < x-content-type-options: nosniff
  < x-xss-protection: 0
  < referrer-policy: origin-when-cross-origin, strict-origin-when-cross-origin
  < content-security-policy: default-src 'none'
  < vary: Accept-Encoding, Accept, X-Requested-With
  < x-ratelimit-limit: 60
  < x-ratelimit-remaining: 53
  < x-ratelimit-reset: 1642938185
  < x-ratelimit-resource: core
  < x-ratelimit-used: 7
  < accept-ranges: bytes
  < content-length: 43
  < x-github-request-id: BB4E:5A97:18115BA:1B25EA7:61ED31EC
  <
  { [43 bytes data]
  100    43  100    43    0     0    123      0 --:--:-- --:--:-- --:--:--   123Half measures are as bad as nothing at all.
  * Connection #0 to host api.github.com left intact  

  # ヘッダ指定
  $ curl -X POST 'http://localhost:5050/api/' -H 'Content-Type: application/json' -H 'Authorization: Bearer XXXX'

  # ボディ指定
  $ curl -X POST 'http://localhost:5050/api/' -d '{"name":"hello", "id":"100"}'

  # SSL証明書エラーを無視
  $ curl --insecure -X POST 'http://localhost:5050/api/'
  $ curl -k -X POST 'http://localhost:5050/api/'

  # 証明書を指定
  $ curl --cacert ./server.crt -X POST 'http://localhost:5050/api/'

  # プロキシを指定
  $ curl --proxy 'http://【ユーザ名】:【パスワード】@proxy.co.jp:8080' 'http://localhost:5050/api/'
  ```

### 3.11. 【cut】 各行から一部分を取り除く

* 必須レベル：★★★☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | d | デリミタの指定 |
  | f | フィールド（何番目か）指定 |

* 使い方
  ```bash
  # 2番目を表示
  $ echo "1 2 3" | cut -d" " -f2
  2

  # 2番目以降を表示
  $ echo "1 2 3" | cut -d" " -f2-
  2 3

  # 2番目以前を表示
  $ echo "1 2 3" | cut -d" " -f-2
  1 2
  ```

### 3.12. 【dc】 無限精度の計算が行える卓上計算機

* 必須レベル：★☆☆☆☆

* 使い方<br>
  逆ポーランド形式で記述
  ```bash
  # 複雑な計算　(27/(1+2)^2)*2
  $ dc
  27 1 2 + 2 ^ / 2 * 
  p
  6
  ```

### 3.13. 【dd】 ファイルの変換とコピーを行う

* 必須レベル：★★☆☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | if=FILE  | 標準入力の代わりに FILE から読み込む |
  | of=FILE  | 標準出力の代わりに FILE に書き込む |
  | bs=BYTES | 一回に BYTES バイトずつ読み書きする |
  | count=N  | 入力ブロック N 個分だけコピーする |

* 使い方
  ```bash
  # 5Mbのファイル作成
  $ dd if=/dev/zero of=5Mb bs=1000 count=5000
  5000+0 レコード入力
  5000+0 レコード出力
  5000000 バイト (5.0 MB) コピーされました、 0.0286412 秒、 175 MB/秒

  $ ls -lh 5Mb
  -rw-rw-r--. 1 takahana takahana 4.8M  4月 24 22:27 5Mb

  # ちなみに0で埋まっている
  $ od ./5Mb
  0000000 000000 000000 000000 000000 000000 000000 000000 000000
  *
  23045500
  ```

### 3.14. 【df】 ディスク容量を確認する

* 必須レベル：★★★★☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | -h <br> (--human-readable) | 各サイズの後ろに見やすい単位をつける。MiBやGiBなどの1024の累乗が使われる。 |
  | --si <br> (-H) | 各サイズにの後ろにMBなら‘M’といった、SI形式の略号を付ける。1000の累乗が使われる。 |
  | -k | デフォルトのブロックサイズによらず、1ブロック1024バイトでサイズを表示する。デフォルトは環境変数「DF_BLOCK_SIZE」で定義されている。 |

* 使い方
  ```bash
  # 基本
  $ df -h
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/sdc        251G  1.5G  237G   1% /
  tmpfs           3.1G     0  3.1G   0% /mnt/wsl
  tools           914G  294G  620G  33% /init
  none            3.1G     0  3.1G   0% /dev
  none            3.1G  4.0K  3.1G   1% /run
  none            3.1G     0  3.1G   0% /run/lock
  none            3.1G     0  3.1G   0% /run/shm
  none            3.1G     0  3.1G   0% /run/user
  tmpfs           3.1G     0  3.1G   0% /sys/fs/cgroup
  drivers         914G  294G  620G  33% /usr/lib/wsl/drivers
  lib             914G  294G  620G  33% /usr/lib/wsl/lib
  C:\             914G  294G  620G  33% /mnt/c
  ```
  
### 3.15. 【echo】 テキストの行を表示する

* 必須レベル：★★★★★

* オプション
  | オプション  | 詳細  |
  | ---- | ---- |
  |  |  |

* 使い方
  ```bash
  # 基本
  $ echo "test"
  test

  # エスケープ文字の有効化
  $ echo -e "t\nest"
  t
  est

  # 末尾改行の削除
  $ echo -n "test"
  test
  ```

### 3.16. 【eval】 引数を読み込み一つのコマンドとして実行する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ eval echo test
  test
  ```

### 3.17. 【find】 条件を満たすファイルを検索する

* 必須レベル：★★★★★

* オプション
  ```bash
  # オプション指定
  $ find [検索パス] [検索条件] [アクション※任意]
  ```
  
* 使い方
  ```bash
  # ファイル名検索
  # 現ディレクトリ配下の「sample.txt」というファイルを検索
  $ find ./ -name sample.txt

  # ファイルタイプ検索（ファイル）
  # 「/home/takahana」配下のファイルを検索
  $ find /home/takahana -type f

  # ファイルタイプ検索（ディレクトリ）
  # 現ディレクトリ配下の「test」というディレクトリを検索
  $ find ./ -type d -name test

  # アクション指定
  ```

### 3.18. 【grep】 パターンにマッチする行を表示する

* 必須レベル：★★★★★

* オプション
  * 正規表現
    ```bash
    # 基本正規表現（デフォルトのため省略可能）
    $ grep -G "hoge"

    # 拡張正規表現
    $ grep -E "hoge"
    ```
  * マッチングの制御
    ```bash
    # 指定文字を含まない
    $ grep -v "nomatch"
    ```
    
* 使い方

### 3.19. 【head】 ファイルの最初の部分を表示する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # デフォルトは先頭10行表示
  $ head sample.c
  #include<stdio.h>
  //##################################################
  //# 名前：
  //# 機能：
  //# 概要：
  //##################################################

  //====================
  // メイン処理
  //====================

  # 行数指定
  $ head -n 1 sample.c
  #include<stdio.h>
  ```

### 3.20. 【hostname】 システムのホスト名（IPアドレス）を表示・設定する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # IPの表示
  $ hostname -I
  10.x.x.xx 192.168.122.1
  ```

### 3.21. 【ifconfig】 ネットワークインターフェースの管理

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ ifconfig -a
  virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
          inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
          ether 52:54:00:b2:bf:b7  txqueuelen 1000  (Ethernet)
          RX packets 0  bytes 0 (0.0 B)
          RX errors 0  dropped 0  overruns 0  frame 0
          TX packets 0  bytes 0 (0.0 B)
          TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
  ```

### 3.22. 【jobs】 アクティブなジョブリストの表示

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # 事前準備（vimコマンドを一時停止しておく）
  $ vi test
  [1]+  停止                  vim test
  $ vi test2
  [2]+  停止                  vim test2
  
  # ジョブの確認
  $ jobs
  [1]-  停止                  vim test
  [2]+  停止                  vim test2

  # フォアグラウンドでジョブを再開
  $ fg 2
  ```

### 3.23. 【keytool】 鍵と証明書を管理

* 必須レベル：★★☆☆☆

* 使い方<br>
※デフォルトのパスワードは「changeit」
  ```bash
  # 登録（jre）
  $ keytool -import -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts -file server.crt

  # 確認
  $ keytool -list -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts
  ```

### 3.24. 【last】 直近のログイン履歴を表示

* 必須レベル：★☆☆☆☆

* 使い方
  ```bash
  # ホスト名を最後に表示
  $ last -a
  takahana pts/0        Wed Sep  1 23:36   still logged in    gateway
  reboot   system boot  Wed Sep  1 23:35 - 23:36  (00:01)     3.10.0-1127.19.1.el7.x86_64

  wtmp begins Sat Oct 24 00:56:05 2020

  # リモートログイン時、ログイン元のIPを表示
  $ last -ai

  # リモートログイン時、ログイン元のIPをホスト名に変換
  $ last -ad

  # 以下ファイルを整形して表示している
  $ ls -l /var/log/wtmp
  ```

### 3.25. 【lastlog】 全てのユーザーの最終ログインを表示

* 必須レベル：★☆☆☆☆

* 使い方
  ```bash
  # ホスト名を最後に表示
  $ lastlog

  # 以下ファイルを整形して表示している
  $ ls -l /var/log/lastlog
  ```

### 3.26. 【ls】 ファイルリストを表示する

* 必須レベル：★★★★★

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | -h | MBやGBなど、人間が読みやすい形式で表示する（--human-readable） |

* 使い方
  ```bash
  # 
  ```

### 3.27. 【md5sum】 MD5メッセージダイジェストの計算と照合を行う

* 必須レベル：★★★★☆

* 使い方<br>
  バイナリファイル資産等の資産一致確認に使う
  ```bash
  # ファイルのハッシュ値を取得
  $ cat test123
  1234
  $ md5sum test123
  e7df7cd2ca07f4f1ab415d457a6e1c13  test123

  # ファイルの中身が変わればハッシュ値が全く異なる
  $ cat test123
  123
  $ md5sum test123
  ba1f2511fc30423bdbb183fe33f3dd0f  test123

  ```

### 3.28. 【mt】 磁気テープドライブの操作を制御する

* 必須レベル：★★☆☆☆

* オプション
  | オプション | 詳細 |
  | -f | 操作対象のテープドライブを指定 |
  | fsf | 引数で指定した数の分だけ先の EOF に移動 |

* 使い方
  ```bash
  # 磁気テープの取り扱い方
  # ドライブのデバイスファイル名を確認
  [takahana@localhost ~]$  lsscsi -g
  [1:0:0:0]    cd/dvd  VBOX     CD-ROM           1.0   /dev/sr0   /dev/sg0
  [2:0:0:0]    disk    ATA      VBOX HARDDISK    1.0   /dev/sda   /dev/sg1

  # 磁気テープに書き込み
  $ tar cvf /dev/nst0 -C /home/user file01

  # 磁気テープの内容確認
  $ tar tvf /dev/nst0
  -rw-r--r-- 1001/1001 3773378080 2014-01-12 19:41 file01

  # 磁気テープから復元
  $ tar xvf /dev/nst0

  # 磁気テープを進める
  $ mt -f /dev/nst0 status
  SCSI 2 tape drive:
  File number=0, block number=0, partition=0.
  Tape block size 0 bytes. Density code 0x58 (no translation).
  Soft error count since last status=0
  General status bits on (41010000):
  BOT ONLINE IM_REP_EN
  
  # 1進める
  $ mt -f /dev/nst0 fsf 1

  # numberが1増加
  $ mt -f /dev/nst0 status
  SCSI 2 tape drive:
  File number=1, block number=0, partition=0.
  Tape block size 0 bytes. Density code 0x58 (no translation).
  Soft error count since last status=0
  General status bits on (81010000):
  EOF ONLINE IM_REP_EN 

  # 磁気テープの巻き戻し
  $ mt -f /dev/nst0 rewind
  ```

### 3.29. 【nl】 ファイルに行番号を付与する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # 本文（Body）を全て（All）表示する
  $ nl -ba sample1.c
     1  #include<stdio.h>
     2  //##################################################
     3  //# 名前：hello.c
     4  //# 機能：「こんにちは」といいます。
     5  //# 概要：
     6  //##################################################
     7
     8  //====================
     9  // メイン処理
    10  //====================
    11  int main(void)
    12  {
    13
    14    printf("こんにちは\n");
    15
    16    return 0;
    17
    18  }
  ```

### 3.30. 【nohup】 ログアウトの影響を受けずコマンドを実行する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # pythonサーバの起動
  $ nohup pytohn -m swagger_server
    * Serving Flask app "__main__" (lazy loading)
    * Environment: production
    WARNING: This is a development server. Do not use it in a production deployment.
    Use a production WSGI server instead.
    * Debug mode: off
    * Running on https://localhost:8080/ (Press CTRL+C to quit)
  ```

  ```bash
  # バックグラウンド実行する場合
  $ (sleep_time=60; while true; do echo ${sleep_time}待機; sleep $sleep_time; done)&
  [1] 9992
  $ 60待機

  # 止める場合
  $ fg
  ( sleep_time=60; while true; do
      echo ${sleep_time}待機; sleep $sleep_time;
  done )
  ^C
  ```

### 3.31. 【od】 8進数やその他の形式でダンプする

* 必須レベル：★★☆☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | -t   | オプションで出力フォーマット指定 |  
  |  c   | ASCII 文字または \ エスケープ文字で表示する |  
  |  x   | 16進数2バイトで表示する（x2と同じ） |  
  |  d   | 10進数2バイトで表示する |  

* 使い方
  ```bash
  # １行目にASCII表示(c)
  # ２行目に16進数1バイト表示(x1)
  # ３行目に10進数1バイト表示(d1)
  $ echo '10AZaz-!'|od -tcx1d1
  0000000    1    0    A    Z    a    z    -    !   \n
            31   30   41   5a   61   7a   2d   21   0a
            49   48   65   90   97  122   45   33   10
  0000011

  # SJIS
  $ echo '09AZｱ'
  0000000 30 39 41 5a b1 0a
  0000010
  
  # UTF8
  # ef bdはBOM(バイトオーダーマーク)
  $ echo '09AZｱ'
  0000000 30 39 41 5a ef bd b1 0a
  0000010
  ```

### 3.32. 【openssl】 証明書の作成

* 必須レベル：★★☆☆☆

* 使い方<br>
ローカルでWEBサーバを公開する際に、以下手順で自己証明書を作成する。<br>
※Javaに取り込む場合は「[keytool](#keytool　鍵と証明書を管理)」コマンドを使用する。<br>
※登録時に指定した「CN」が公開するホスト名と一致する必要がある。<br>

  ```bash
  # 秘密鍵の作成
  $ openssl genrsa 2048 > server.key
  Generating RSA private key, 2048 bit long modulus (2 primes)
  ..........................+++++
  ..+++++
  e is 65537 (0x010001)

  # 証明書署名要求(CSR:Certificate Signing Request)の作成
  # サンプルなので適当な自己証明書を作る
  $ openssl req -new -key server.key > server.csr
  You are about to be asked to enter information that will be incorporated
  into your certificate request.
  What you are about to enter is what is called a Distinguished Name or a DN.
  There are quite a few fields but you can leave some blank
  For some fields there will be a default value,
  If you enter '.', the field will be left blank.
  -----
  Country Name (2 letter code) [AU]:JP
  State or Province Name (full name) [Some-State]:Kanagawa
  Locality Name (eg, city) []:Kawasaki
  Organization Name (eg, company) [Internet Widgits Pty Ltd]:Gunma
  Organizational Unit Name (eg, section) []:Kiryu
  Common Name (e.g. server FQDN or YOUR name) []:localhost
  Email Address []:hoge@email.com

  Please enter the following 'extra' attributes
  to be sent with your certificate request
  A challenge password []:

  # SSLサーバー証明書(crt形式)の作成
  $ openssl x509 -days 3650 -req -signkey server.key < server.csr > server.crt
  Signature ok
  subject=C = JP, ST = Kanagawa, L = Kawasaki, O = Gunma, OU = Kiryu, CN = localhost, emailAddress = hoge@email.com
  Getting Private key
  ```

### 3.33. 【ps】 現在実行されているプロセスのスナップショットを表示する

* 必須レベル：★★★☆☆

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | e | 全てのプロセスを表示 |
  | f | 完全なフォーマットでリストする |
  | o | フォーマット指定で表示する |
  | H | 階層表示する |
  | --sort | ソートキーを指定する |

* 使い方
  ```bash
  # 「 vim 」というプロセスを表示
  $ ps -ef | grep vim
  takahana  2640  2828  0 19:03 pts/0    00:00:00 grep --color=auto vim
  takahana  7042  2828  0 16:45 pts/0    00:00:00 vim test
  takahana  7043  2828  0 16:45 pts/0    00:00:00 vim test2

  #フォーマット指定で表示
  $ ps -eH -o etime,uid,pid,ppid,tty,args --sort start_time
    ELAPSED   UID     PID    PPID TT       COMMAND
      05:36  1000     377     374 pts/0            -bash
      05:00  1000     476     377 pts/0              sleep 500
      00:00  1000     762     377 pts/0              ps -eH -o etime,uid,pid,ppid,tty,args
  ```

### 3.34. 【pstree】 現在実行されているプロセスをツリー形式で表示する

* 必須レベル：★★☆☆☆

* オプション
  | オプション | 詳細 |
  | --- | --- |

* 使い方
  ```bash
  $ pstree -p takahana
  bash(322)---sleep(8821)
  ```

### 3.35. 【route】 ルーティングテーブルの管理

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  $ route
  Kernel IP routing table
  Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
  default         gateway         0.0.0.0         UG    100    0        0 enp0s3
  10.0.2.0        0.0.0.0         255.255.255.0   U     100    0        0 enp0s3
  192.168.122.0   0.0.0.0         255.255.255.0   U     0      0        0 virbr0
  ```

### 3.36. 【script】 ターミナルの出力内容を記録（ログの代わりに）

* 必須レベル：★☆☆☆☆

* 使い方
  ```bash
  # 基本
  $  script
  Script started, output log file is 'typescript'.
  $ whoami
  takahana
  $ date
  Sat Mar 23 00:32:00 JST 2024
  $ exit
  exit
  Script done.

  # 結果確認
  $ cat typescript
  Script started on 2024-03-23 00:31:56+09:00 [TERM="xterm-256color" TTY="/dev/pts/2" COLUMNS="120" LINES="30"]
  $ whoami
  takahana
  $ date
  Sat Mar 23 00:32:00 JST 2024
  $ exit
  exit
  Script done on 2024-03-23 00:32:01+09:00 [COMMAND_EXIT_CODE="0"]

  # 出力加工版
  $ script -fq >(awk '{print strftime("%F %T") $0}{fflush()}'>> test.log)
  ```


### 3.37. 【sed】 文字列置換などのテキスト処理

* 必須レベル：★★★☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  |  e  |  スクリプトコマンド実行  |
  |  r  |  拡張正規表現でスクリプトコマンド実行  |
  |  i  |  ファイルを直接編集  |
  |  i拡張子  |  ファイルを直接編集し、拡張子の退避ファイル作成  |
  |  n  |   pコマンドを指定された場合に限って出力を生成（sedはデフォルトで最後のパターンスペースを出力する）  |

* スクリプトコマンド
  |  コマンド  |  詳細  |
  | ---- | ---- |
  | s/regexp/replacement/(flag) | パターンスペースに対して、regexpのマッチを試みて、マッチした部分をreplacementに置換する。<br>【補足１】マッチした部分は特殊文字&、副表現()にマッチした部分は\1から\9で参照できる。<br>【補足２】flgaでn番目にマッチした文字列を置換する。デフォルトは1、gですべての文字列を対象とする。 |

  *スクリプトコマンドは「;」でつなげることが可能

* アドレス
  |  コマンド  |  詳細  |
  | ---- | ---- |
  | /regexp/ | 正規表現regexpにマッチした行にマッチする |

* 使い方
  ```bash
  # ===== 標準出力の置換 =====
  # 日付スラッシュの削除
  $ echo "2020/07/11" | sed -e 's/\///g'
  20200711

  # ※区切り文字はスラッシュ以外も使用可能
  $ echo "2020/07/11" | sed -e 's@/@@g'
  20200711

  # 正規表現を使用する場合
  $ ls -l /usr/bin/vi* | sed -r 's/ +/ /g'| cut -d' ' -f9-
  /usr/bin/vi
  /usr/bin/view -> vi
  /usr/bin/vim
  /usr/bin/vimdiff -> vim
  /usr/bin/vimtutor
  /usr/bin/vinagre

  # 特定文字の抽出（特殊文字、副表現の使用）
  $ $ echo "2024/02/06" | sed -r 's@([0-9]+)/([0-9]+)/([0-9]+)@\2-\3 old=&@g'
  02-06 old=2024/02/06
  ```

  ```bash
  # ===== ファイル内文字列の置換 =====
  # シェル内のuser1→user2に置換
  $ sed -i -e 's/user1/user2/g' test.sh

  # 拡張子（bk）付き退避ファイルを作成して置換
  $ sed -ibk -e 's/user1/user2/g' test.sh
  $ diff test.sh test.shbk
  1c1
  < user2
  ---
  > user1

  # 応用
  # バイナリファイルの編集
  $ xxd -p -c 1000000 ./before | sed "s/f2f0f2f1f0f9f0f1/${AFTER}/g" | xxd -p -r > ./after
  ```

  ```bash
  # ===== アドレスの指定 =====
  # 特定文字が含まれる行の置換
  $ sed -e '/matsuis/s/matsui/takaha/g' test.txt
  takahana
  naoki
  m21
  matsui
  takahas →ここだけ置換（置換前：matsuis）
  ```

  ```bash
  # ===== 指定行の取得 =====
  $ nl test.txt
      1  takahana
      2  naoki
      3  m21
      4  matsui
      5  matsuis
  #1行目を表示、4～5行目を表示
  $ sed -n "1p; 4,5p" test.txt
  takahana
  matsui
  matsuis
  ```
  
  ```bash
  # ===== コマンド作成・実行 =====
  # 拡張子の変更
  $ find ./ -name "test*.sh" | sed -nr 's/(.*)\.sh/mv & \1\.txt/p'
  mv ./test1.sh ./test1.txt
  mv ./test2.sh ./test2.txt

  $ find ./ -name "test*.sh" | sed -nr 's/(.*)\.sh/mv & \1\.txt/p' | bash
  ```

* tips
  1. sedは各レコードをパターンスペースに取り込み、パターンスペース(またはホールドスペース)に対して各コマンドを順次実行する。この際、ひとつ前に読み込んだ行は破棄される。
  2. アドレスを指定しない場合は、すべての入力行に対して実行する。アドレスを指定した場合は、マッチした入力行に対してのみ実行する。
  3. パターンスペースとは、入力された行の一時保存場所。sedはデフォルトでパターンスペースの内容を標準出力する。つまり、処理した行が２重に表示されてしまう。（⇒nオプションで出力抑止が可能）
  4. ホールドスペースとは、パターンスペースと独立した保存場所。パターンスペースと合わせて高度な処理が可能。

### 3.38. 【tar】 アーカイブの作成

* 必須レベル：★★★★☆

  ※tarコマンドはオプションの前に「-」は不要。<br>
　ただし、後述するオプション順番を意識する必要がある。

* オプション<br>

1. 目的
    | オプション | 詳細 |
    | --- | --- |
    | c | 作成（Create） |
    | t | 内容確認（lisT） |
    | x | 展開（eXtarct） |

2. 追加オプション
    | オプション | 詳細 |
    | --- | --- |
    | v | 結果を表示 |
    | z | zip圧縮 |

3. ファイル指定
    | オプション | 詳細 |
    | --- | --- |
    | f | 作成するアーカイブファイルの指定 |

4. さらなる追加オプション
    | オプション | 詳細 |
    | --- | --- |
    | --exclude=PATTERN | PATTERNを除外する |
    | C | 指定のディレクトリに移動してアーカイブする |

* 使い方
  ```bash
  # アーカイブの作成（圧縮あり）
  $ tar cvzf ./test.tar.gz ./test
  ./test/
  ./test/test1
  ./test/test2
  ./test/test3

  $ ls -l test.tar.gz
  -rw-r--r-- 1 naoki 197121   173  4月 24 09:37 test.tar.gz

  # アーカイブの作成（圧縮なし）
  $ tar cvf ./test.tar ./test
  ./test/
  ./test/test1
  ./test/test2
  ./test/test3

  # アーカイブの作（特定ファイルを除外）
  $ tar cvzf ./test.tar.gz --exclude=test1 ./test
  ./test/
  ./test/test2
  ./test/test3

  # アーカイブファイルの確認
  $ tar tvzf ./test.tar.gz
  drwxr-xr-x naoki/197121      0 2022-04-24 09:37 ./test/
  -rw-r--r-- naoki/197121      0 2022-04-24 09:36 ./test/test1
  -rw-r--r-- naoki/197121      0 2022-04-24 09:36 ./test/test2
  -rw-r--r-- naoki/197121      0 2022-04-24 09:37 ./test/test3

  # アーカイブの展開
  $ tar xvzf ../test.tar.gz ./
  ./test/
  ./test/test1
  ./test/test2
  ./test/test3

  # パスを含めずアーカイブする
  $ tar -C /path/to/ -czf /path/to/target.tar.gz target
  ```

### 3.39. 【tee】 出力を複数のファイルやプロセスにリダイレクトする

* 必須レベル：★★☆☆☆

* オプション<br>
    | オプション | 詳細 |
    | --- | --- |
    | -a <br> (--append) | 指定されたファイルの末尾に標準入力を追記する。 |

* 使い方
  ```bash
  #ツール実行結果を標準出力とログに出力する
  $ ./tool.sh 2>&1 | tee -a tool.log
  ```

### 3.40. 【umask】 デフォルトの権限を決定する

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  $ umask 022
  # ディレクトリの場合、777 - 022 = 755
  # ファイルの場合、666 - 022 = 644
  # umaskから引いた値がデフォルト権限となる
  # drwxr-xr-x. 2 taka taka   6  8月 11 23:12 dir
  # -rw-r--r--. 1 taka taka   0  8月 11 23:12 file

  # /etc/bashrcに記載されている
  if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
    umask 002
  else
    umask 022
  fi
  ```

### 3.41. 【unzip】 ファイル解凍をする（zipを参照）


### 3.42. 【vi】 vimを参照

### 3.43. 【vim】 高機能なテキストエディタ  

* 必須レベル：★★★★★

* コマンドライン
  ```vim
  " 行数表示
  :set number
  :se nu

  " 色付け
  :set syntax=ON

  " タブ整形
  :set ts=4

  " 大文字小文字区別なくす（ignorecase）
  :set ic
  :set noic

  " 垂直分割◎
  :vs

  " 垂直分割で指定のファイルを開く
  :vs {file}

  " 垂直分割で空ウィンドウ開く
  :vnew

  " 新規タブでファイルを開く
  :tabnew {file}
  ```

* 基本移動ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | h | 左へ一つ |
  | j | 下へ一つ |
  | k | 上へ一つ |
  | l | 右へ一つ |
  | gj | 下へ一つ ※gは表示上の移動 |

* 行移動ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | 0 | 行の先頭へ(インデント無視して先頭へ) |
  | ^ | 行の先頭へ◎ |
  | $ | 行の末尾へ◎ |
  | + | 下の行の先頭へ |
  | - | 上の行の先頭へ |

* ページ移動ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | :100 | 100行目へ ◎ |
  | ctrl + u | 半画面分 上へ ◎ |
  | ctrl + d | 半画面分 下へ ◎ |
  | ctrl + b | 一画面分 上へ |
  | ctrl + f | 一画面分 下へ |
  | { | 段落毎に上へ◎ |
  | } | 段落毎に下へ◎ |
  | gg | そのファイルの先頭へ◎ |
  | G | そのファイルの末尾へ◎ |
  | zz | 現在カーソルを画面中央へ |

* 単語移動ショートカット<br>
  ※大文字の場合はピリオドなど区切り文字もまとまりとみなす
  | コマンド | 内容 |
  | ---- | ---- |
  | w | 単語の先頭に進む◎ |
  | b | 単語の先頭に戻る |
  | e | 単語の末尾に進む |

* 行内検索ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | f | その行の順方向に一文字検索◎ |
  | F | その行の逆方向に一文字検索 |
  | ; | 順方向に繰り返し検索 |
  | , | 逆方向に繰り返し検索 |

* 検索ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | / | 順方向に文字列検索◎ |
  | ? | 逆方向に文字列検索◎ |
  | n | 順方向に繰り返し検索◎ |
  | N | 逆方向に繰り返し検索 |
  | % | 対となる括弧へ移動 |

* コピー／ペーストショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | yw | 1単語コピー◎ |
  | yy | 1行コピー◎ |

* cw

* vimrc
  ```vim
  # vimrc
  "-----Search------
  "インクリメンタルサーチを有効
  set incsearch
  "大文字小文字を区別しない
  set ignorecase
  "大文字で検索されたら対象を大文字限定にする
  set smartcase
  "検索終わりで先頭に戻らない
  set nowrapscan

  "-----Format------
  "行数表示
  set number
  "タブをスペースに置換
  set ts=4
  "ルーラーの設定
  set ruler
  "カーソルラインを表示する
  set cursorline
  "pcファイルをcファイルで読み込む
  autocmd BufRead,BufNewFile *.pc setfiletype c

  "ステータスラインにコマンドを表示
  set showcmd
  "ステータスラインを常に表示
  set laststatus=2
  "ファイル名表示
  set statusline+=%<%F
  "文字コード表示
  set statusline+=[%{has('multi_byte')&&\&fileencoding!=''?&fileencoding:&encoding}]
  "ファイルタイプ表示
  set statusline+=%y
  "ここからツールバー右側
  set statusline+=%=
  "現在行が全体行の何%か表示
  set statusline+=[%p%%]

  "-----Setting------
  "ESCボタンをqqqに割付
  inoremap <silent> qqq <ESC>

  "-----autoindent------
  if &term =~ "xterm"
      let &t_ti .= "\e[?2004h"
      let &t_te .= "\e[?2004l"
      let &pastetoggle = "\e[201~"

      function XTermPasteBegin(ret)
          set paste
          return a:ret
      endfunction

      noremap <special> <expr> <Esc>[200~ XTermPasteBegin("0i")
      inoremap <special> <expr> <Esc>[200~ XTermPasteBegin("")
      cnoremap <special> <Esc>[200~ <nop>
      cnoremap <special> <Esc>[201~ <nop>
  endif

  "-----Tab------
  function! s:SID_PREFIX()
    return matchstr(expand('<sfile>'), '<SNR>\d\+_\zeSID_PREFIX$')
  endfunction

  " Set tabline.
  function! s:my_tabline()  "{{{
    let s = ''
    for i in range(1, tabpagenr('$'))
      let bufnrs = tabpagebuflist(i)
      let bufnr = bufnrs[tabpagewinnr(i) - 1]  " first window, first appears
      let no = i  " display 0-origin tabpagenr.
      let mod = getbufvar(bufnr, '&modified') ? '!' : ' '
      let title = fnamemodify(bufname(bufnr), ':t')
      let title = '[' . title . ']'
      let s .= '%'.i.'T'
      let s .= '%#' . (i == tabpagenr() ? 'TabLineSel' : 'TabLine') . '#'
      let s .= no . ':' . title
      let s .= mod
      let s .= '%#TabLineFill# '
    endfor
    let s .= '%#TabLineFill#%T%=%#TabLine#'
    return s
  endfunction "}}}
  let &tabline = '%!'. s:SID_PREFIX() . 'my_tabline()'
  set showtabline=2 " 常にタブラインを表示

  " The prefix key.
  nnoremap    [Tag]   <Nop>
  nmap    t [Tag]
  " Tab jump
  for n in range(1, 9)
    execute 'nnoremap <silent> [Tag]'.n  ':<C-u>tabnext'.n.'<CR>'
  endfor
  " t1 で1番左のタブ、t2 で1番左から2番目のタブにジャンプ

  map <silent> [Tag]c :tablast <bar> tabnew<CR>
  " tc 新しいタブを一番右に作る
  map <silent> [Tag]x :tabclose<CR>
  " tx タブを閉じる
  map <silent> [Tag]n :tabnext<CR>
  " tn 次のタブ
  map <silent> [Tag]p :tabprevious<CR>
  " tp 前のタブ
  ```

### 3.44. 【xargs】 引数からコマンドを組み立て実行する

* 必須レベル：★★★★☆

* 使い方
  ```bash
  # 直前のコマンドの実行結果を渡す
  $ ls README.md | xargs md5sum
  ccd981a6716bb3b91569e45d336b28d0 *README.md
  ```

### 3.45. 【xxd】 2進数でダンプする  

* 必須レベル：★★☆☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  | -b | オプションでバイナリ（2進数）表示 |
  | -c | オプションで表示数変更 |
  | -p | ポストスクリプト形式の 16 進ダンプを出力する。 |
  | -r | 元に戻す: 16 進ダンプからバイナリ形式に変換 

* 使い方
  ```bash
  # 2進数ダンプ
  $ echo '10abAB' |xxd -b -c 8
  0000000: 00110001 00110000 01100001 01100010 01000001 01000010 00001010           10abAB.
  $ echo '10abAC' |xxd -b -c 8
  0000000: 00110001 00110000 01100001 01100010 01000001 01000011 00001010           10abAC.

  # 16進数ダンプ
  $ echo "AZaz09ｱア" |xxd -p
  415a617a3039efbdb1e382a20a

  # 16進数を元に戻す
  $ echo '415a617a3039efbdb1e382a20a' |xxd -p -r
  AZaz09ｱア

  # EBCDICファイルの確認方法
  $ xxd -E -g1 ./EBCDIC

  0000000: f2 f0 f2 f0 f0 f9 f2 f9 40 40 40 40 40 40 40 40 20200929
  ※EBCDICのf2⇒数値の2
  ```

### 3.46. 【yum】 RedHat系で利用されるパッケージ管理ツール

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # yumはパイソンで動いている
  $ head -n 1 /usr/bin/yum
  #!/usr/bin/python
  ```

### 3.47. 【w】 ログインしている人とその人がやっていることを表示する

* 必須レベル：★★☆☆☆

* 使い方<br>
  クラスタ切り替え時に他に作業者を確認するために使用。
  ```bash
  $ w
  19:20:48 up  9:54,  1 user,  load average: 0.00, 0.02, 0.05
  USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
  takahana pts/0    gateway          10:37    0.00s  1.42s  0.03s w
  ```

### 3.48. 【wc】 各ファイルの改行数、ワード数、バイト数を表示する

* 必須レベル：★★★☆☆

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | l | 改行の数を表示する |
  | c | バイト数を表示する |
  | m | 文字数を表示する |

* 使い方
  ```bash
  $ nl -ba sample1.c
      1  #include<stdio.h>
      2  //##################################################
      3  //# 名前：hello.c
      4  //# 機能：「こんにちは」といいます。
      5  //# 概要：
      6  //##################################################
      7
      8  //====================
      9  // メイン処理
      10  //====================
      11  int main(void)
      12  {
      13
      14    printf("こんにちは\n");
      15
      16    return 0;
      17
      18  }
  
  # 行番号を表示する
  $ wc -l sample1.c
  18 sample1.c
  ```

### 3.49. 【which】 コマンドのフルパスを表示する

* 必須レベル：★★★★★

* 使い方
  ```bash
  $ which echo
  /usr/bin/echo
  ```

### 3.50. 【whoami】 実行ユーザ名を出力する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ whoami
  takahana
  ```

### 3.51. 【zgrep】 圧縮されている可能性のあるファイルで、正規表現の検索をする

* 必須レベル：★★★☆☆
  
* 使い方
  ```bash

  ```

### 3.52. 【zip】 ファイル圧縮をする

* 必須レベル：★★★★☆

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | e | 暗号化 |
  
* 使い方
  ```bash
  # 通常
  $ zip ./5Mb.zip ./5Mb
    adding: 5Mb (deflated 100%)

  # 暗号化あり圧縮
  $ zip -e ./5Mb.zip ./5Mb
  Enter password:
  Verify password:
    adding: 5Mb (deflated 100%)

  $ ls -l 5Mb*
  -rw-rw-r--. 1 takahana takahana 5000000  4月 24 22:27 5Mb
  -rw-rw-r--. 1 takahana takahana    5045  4月 24 22:29 5Mb.zip
  ```
  
### 3.53. 【!!】 直前のコマンドを実行

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ find ./ -name "*md"
  ./README.md

  # !! 直前のコマンドを実行
  $ !!
  ./README.md

  # !! 直前のfから始まるコマンドを実行
  $ !f
  ./README.md

  # 応用
  # 直前のコマンド実行結果を他のコマンドに渡す
  $ vi `!!`
  vi `find ./ -name "*md"`
  ```

### 3.54. 【> >>】 出力リダイレクト／追記

* 必須レベル：★★★★★

### 3.55. 【< <<】 入力リダイレクト／追記

* 必須レベル：★★★☆☆

### 3.56. 【;】 コマンドを続けて実行

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  #ディレクトリ移動→カレントディレクトリを確認
  $ cd ~ ; pwd
  /home/takahana
  ```

### 3.57. 【:】 何もせず正常ステータス(0)を返す

* 必須レベル：★☆☆☆☆

* 使い方
  ```bash
  $ : ; echo $?
  0

  #if文で何もしたくないときに使用
  $ if [ $? = 0 ] ; then : 何もしない ; else  echo ng ; fi
  ```

### 3.58. 【&&】 正常終了の場合実施（ANDリスト）

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # コマンド1が正常ならコマンド2を実行する
  $ echo OK1 && echo OK2
  OK1
  OK2

  $ no && echo OK
  no: command not found
  ```

### 3.59. 【||】 異常終了の場合実施（ORリスト）

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # コマンド1が異常ならコマンド2を実行する
  $ echo OK1 || echo OK2
  OK1

  $ no || echo OK
  no: command not found
  OK
  ```

<br>

## 4. 演算

### 4.1. 【n++ n--】 ポスト（後置）インクリメント／デクリメント

* 使い方
  ```bash
  $ n=1
  $ echo $((n++))
  1
  $ echo $n
  2
  ```

### 4.2. 【++n --n】 プレ（前置）インクリメント／デクリメント

* 使い方
  ```bash
  $ n=1
  $ echo $((--n))
  0
  $ echo $n
  0
  ```

### 4.3. 【+ -】 加算／減算

### 4.4. 【* / %】 乗算／除算／剰余

### 4.5. 【**】 指数
* 使い方
  ```bash
  $ echo $((2**10))
  1024
  ```

### 4.6. 【<< >>】 シフト演算
* 使い方
  ```bash
  $ echo $((1024>>1))
  512
  ```

### 4.7. 【&& ||】論理積／論理和

* 使い方
  ```bash
  ```

<br>

## 5. シェル

### 5.1. 用語説明

#### 5.1.1. シェバン  
シェルの1行目に記載し、このシェルは「bin/bash」で動かしますの意味

  ```bash
  #!/bin/bash
  ```

#### 5.1.2. セカンダリプロンプト  
行末の「\」のことで、まだコマンドは終了していないことを意味する

  ```bash
  $ echo \
  "Hello, World!"
  ```

### 5.2. 引数／特殊変数

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

### 5.3. 比較

#### 5.3.1. 文字列比較

#### 5.3.2. 数値比較

### 5.4. サンプル

  ```bash
  #!/bin/bash
  ##############################
  # 名前：
  # 説明：
  # 引数：$1 xxx
  #       $2 xxx
  ##############################

  #====================
  # 変数設定
  #====================

  #====================
  # 初期関数
  #====================
  f_init () {
    echo "START 初期関数"
  }

  #====================
  # メイン関数
  #====================
  f_main () {
    echo "START メイン関数"

  }


  #====================
  # 実行
  #====================

  # 初期処理呼び出し
  f_init

  # メイン関数呼び出し
  f_main
  ```

<br>

## 6. 組み合わせ便利コマンド

### 6.1. 無限ループ（while true）

  ```bash
  # 無限ループ
  while true; do date; echo "hello !"; sleep 1s; done
  ```

### 6.2. リスト読込（for ～ in）

  ```bash
  # git最新化（※xxxフォルダを除く）
  for f in */.git;do (f=${f%/*}; if [ $f != "xxx" ]; then cd $f; git pull; fi);done;
  ```

### 6.3. ファイル読込（while read）

  ```bash
  # ファイルを読み込み、1行ずつ処理する
  while read line; do md5sum $line;done <bkup.txt
  ```

### 6.4. ファイル存在確認（if）

  ```bash
  # ファイル存在確認結果を表示
  if [ -e $FILE ];then echo "OK";else echo "NG";fi
  ```

### 6.5. 文字列の比較（if）

  ```bash
  # 文字列の比較結果を表示
  if [ "test" = "test" ];then echo "OK";else echo "NG";fi
  ```


<br>
