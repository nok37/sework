# Linux

<!-- TOC -->

- [１．設定](#１．設定)
    - [コマンドの実行パス](#コマンドの実行パス)
    - [bash設定](#bash設定)
    - [cron](#cron)
    - [ショートカット](#ショートカット)
        - [ターミナル操作系](#ターミナル操作系)
        - [カーソル・文字操作系](#カーソル・文字操作系)
        - [その他](#その他)
    - [特殊なデバイス（/dev/***系）](#特殊なデバイスdev系)
    - [豆知識](#豆知識)
        - [ssh接続時に表示される文言 - motd](#ssh接続時に表示される文言---motd)
- [２．コマンド](#２．コマンド)
    - [ac - ユーザの接続時間についての統計を表示する](#ac---ユーザの接続時間についての統計を表示する)
    - [awk - パターン検索と文字処理](#awk---パターン検索と文字処理)
    - [bc - 任意精度の計算言語](#bc---任意精度の計算言語)
    - [cancel - ジョブの取り消しを行う](#cancel---ジョブの取り消しを行う)
    - [cd - カレントディレクトリの変更](#cd---カレントディレクトリの変更)
    - [chmod - ファイルの権限を変更する](#chmod---ファイルの権限を変更する)
    - [cupsdisable - プリンタ無効化](#cupsdisable---プリンタ無効化)
    - [cupsenable - プリンタ有効化](#cupsenable---プリンタ有効化)
    - [curl - HTTPなどの通信プロトコルでデータを転送する](#curl---httpなどの通信プロトコルでデータを転送する)
    - [cut - 各行から一部分を取り除く](#cut---各行から一部分を取り除く)
    - [dc - 無限精度の計算が行える卓上計算機](#dc---無限精度の計算が行える卓上計算機)
    - [dd - ファイルの変換とコピーを行う](#dd---ファイルの変換とコピーを行う)
    - [df - ディスク容量を確認する](#df---ディスク容量を確認する)
    - [echo - テキストの行を表示する](#echo---テキストの行を表示する)
    - [eval - 引数を読み込み一つのコマンドとして実行する](#eval---引数を読み込み一つのコマンドとして実行する)
    - [find - 条件を満たすファイルを検索する](#find---条件を満たすファイルを検索する)
    - [grep - パターンにマッチする行を表示する](#grep---パターンにマッチする行を表示する)
    - [head - ファイルの最初の部分を表示する](#head---ファイルの最初の部分を表示する)
    - [hostname - システムのホスト名（IPアドレス）を表示・設定する](#hostname---システムのホスト名ipアドレスを表示・設定する)
    - [ifconfig - ネットワークインターフェースの管理](#ifconfig---ネットワークインターフェースの管理)
    - [jobs - アクティブなジョブリストの表示](#jobs---アクティブなジョブリストの表示)
    - [keytool - 鍵と証明書を管理](#keytool---鍵と証明書を管理)
    - [last - ログイン履歴を表示する](#last---ログイン履歴を表示する)
    - [ls - ディレクトリの内容を表示する](#ls---ディレクトリの内容を表示する)
    - [md5sum - MD5メッセージダイジェストの計算と照合を行う](#md5sum---md5メッセージダイジェストの計算と照合を行う)
    - [mt - 磁気テープドライブの操作を制御する](#mt---磁気テープドライブの操作を制御する)
    - [nl - ファイルに行番号を付与する](#nl---ファイルに行番号を付与する)
    - [nohup - ログアウトの影響を受けずコマンドを実行する](#nohup---ログアウトの影響を受けずコマンドを実行する)
    - [od - 8進数やその他の形式でダンプする](#od---8進数やその他の形式でダンプする)
    - [openssl - 証明書の作成](#openssl---証明書の作成)
    - [ps - 現在実行されているプロセスのスナップショットを表示する](#ps---現在実行されているプロセスのスナップショットを表示する)
    - [route - ルーティングテーブルの管理](#route---ルーティングテーブルの管理)
    - [sed - 文字列置換などのテキスト処理](#sed---文字列置換などのテキスト処理)
    - [tar - アーカイブの作成](#tar---アーカイブの作成)
    - [tee - 出力を複数のファイルやプロセスにリダイレクトする](#tee---出力を複数のファイルやプロセスにリダイレクトする)
    - [umask - デフォルトの権限を決定する](#umask---デフォルトの権限を決定する)
    - [unzip - ファイル解凍をする（zipを参照）](#unzip---ファイル解凍をするzipを参照)
    - [vi - vimを参照](#vi---vimを参照)
    - [vim - 高機能なテキストエディタ](#vim---高機能なテキストエディタ)
    - [xargs - 引数からコマンドを組み立て実行する](#xargs---引数からコマンドを組み立て実行する)
    - [xxd - 2進数でダンプする](#xxd---2進数でダンプする)
    - [yum - RedHat系で利用されるパッケージ管理ツール](#yum---redhat系で利用されるパッケージ管理ツール)
    - [w - ログインしている人とその人がやっていることを表示する](#w---ログインしている人とその人がやっていることを表示する)
    - [wc -各ファイルの改行数、ワード数、バイト数を表示する](#wc--各ファイルの改行数ワード数バイト数を表示する)
    - [which - コマンドのフルパスを表示する](#which---コマンドのフルパスを表示する)
    - [whoami - 実効ユーザ名を出力する](#whoami---実効ユーザ名を出力する)
    - [zgrep - 圧縮されている可能性のあるファイルで、正規表現の検索をする](#zgrep---圧縮されている可能性のあるファイルで正規表現の検索をする)
    - [zip - ファイル圧縮をする](#zip---ファイル圧縮をする)
    - [!! - 直前のコマンドを実行](#---直前のコマンドを実行)
    - [> - 出力リダイレクト](#---出力リダイレクト)
    - [>> - 出力リダイレクト（追記）](#---出力リダイレクト追記)
    - [< - 入力リダイレクト](#---入力リダイレクト)
    - [<< - 入力リダイレクト（追記）](#---入力リダイレクト追記)
- [３．シェル](#３．シェル)
    - [用語説明](#用語説明)
        - [シェバン](#シェバン)
        - [セカンダリプロンプト](#セカンダリプロンプト)
    - [引数／特殊変数](#引数／特殊変数)
    - [比較](#比較)
        - [文字列比較](#文字列比較)
        - [数値比較](#数値比較)
    - [サンプル](#サンプル)
- [４．組み合わせ便利コマンド](#４．組み合わせ便利コマンド)
    - [無限ループ（while true）](#無限ループwhile-true)
    - [リスト読込（for ～ in）](#リスト読込for--in)
    - [ファイル読込（while read）](#ファイル読込while-read)
    - [ファイル存在確認（if）](#ファイル存在確認if)
    - [文字列の比較（if）](#文字列の比較if)

<!-- /TOC -->
---
<br>

## １．設定

### コマンドの実行パス
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

### bash設定

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

### cron

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

### ショートカット

#### ターミナル操作系

| ショートカット | 内容 |
| --- | --- |
| ctrl + d  | ログアウト |
| alt + v　 | ターミナルの複製 |
 
#### カーソル・文字操作系

| ショートカット | 内容 |
| --- | --- |
| ctrl + a | 行頭へ |
| ctrl + e | 行末へ |
| ctrl + w | 直前の単語を削除 |
| ctrl + u | 直前を削除 |

#### その他

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

### 特殊なデバイス（/dev/***系）

* /dev/null<br>
  書き込まれたデータをすべて破棄し、読み込んでも何もデータを返さない。<br>
  不要な出力を破棄する時に使用。

* /dev/zero<br>
  0x00（NULL文字）を常に出力し続ける特殊なデバイス。<br>
  NULL文字でデータ上書きする場合などで使用。

### 豆知識

#### ssh接続時に表示される文言 - motd
Message of the dayの略

```bash
/etc/motd
```

<br>

## ２．コマンド

### ac - ユーザの接続時間についての統計を表示する

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

### awk - パターン検索と文字処理

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
  $ ls -l /usr/bin/vim*
  -rwxr-xr-x. 1 root root 2337192  8月  9  2019 /usr/bin/vim
  lrwxrwxrwx. 1 root root       3 10月 24  2020 /usr/bin/vimdiff -> vim
  -rwxr-xr-x. 1 root root    2084  8月  9  2019 /usr/bin/vimtutor

  # 9番目（コマンド）のみを表示する
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

### bc - 任意精度の計算言語

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

### cancel - ジョブの取り消しを行う

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # 印刷ジョブの取り消し
  # 「TESTPRT」のプリンタキューを全削除（※root権限）
  $ cancel -a TESTPRT
  ```

### cd - カレントディレクトリの変更

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

### chmod - ファイルの権限を変更する

* 必須レベル：★★★★★<br>
  Read 4, Write 2, eXute 1 の加算で表す<br>
  一般的ににディレクトリの場合 755 、ファイルの場合 644<br>
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

### cupsdisable - プリンタ無効化

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # ※root権限
  $ cupsdisable TESTPRT
  ```

### cupsenable - プリンタ有効化

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # ※root権限
  $ cupsenable TESTPRT
  ```

### curl - HTTPなどの通信プロトコルでデータを転送する

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
  $ curl --proxy 'http://★user:★pass@proxy.co.jp:8080' 'http://localhost:5050/api/'
  ```

### cut - 各行から一部分を取り除く

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

### dc - 無限精度の計算が行える卓上計算機

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

### dd - ファイルの変換とコピーを行う

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

### df - ディスク容量を確認する

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
  
### echo - テキストの行を表示する

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

### eval - 引数を読み込み一つのコマンドとして実行する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ eval echo test
  test
  ```

### find - 条件を満たすファイルを検索する

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

### grep - パターンにマッチする行を表示する

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
    ```
    
* 使い方

### head - ファイルの最初の部分を表示する

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

### hostname - システムのホスト名（IPアドレス）を表示・設定する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  # IPの表示
  $ hostname -I
  10.x.x.xx 192.168.122.1
  ```

### ifconfig - ネットワークインターフェースの管理

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

### jobs - アクティブなジョブリストの表示

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

### keytool - 鍵と証明書を管理

* 必須レベル：★★☆☆☆

* 使い方<br>
※デフォルトのパスワードは「changeit」
  ```bash
  # 登録（jre）
  $ keytool -import -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts -file server.crt

  # 確認
  $ keytool -list -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts
  ```

### last - ログイン履歴を表示する

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
  ```

### ls - ディレクトリの内容を表示する

* 必須レベル：★★★★★

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | -h | MBやGBなど、人間が読みやすい形式で表示する（--human-readable） |

* 使い方
  ```bash
  # 
  ```

### md5sum - MD5メッセージダイジェストの計算と照合を行う

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

### mt - 磁気テープドライブの操作を制御する

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

### nl - ファイルに行番号を付与する

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

### nohup - ログアウトの影響を受けずコマンドを実行する

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

### od - 8進数やその他の形式でダンプする

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

### openssl - 証明書の作成

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

### ps - 現在実行されているプロセスのスナップショットを表示する

* 必須レベル：★★☆☆☆

* オプション
  | オプション | 詳細 |
  | --- | --- |
  | e | 全てのプロセスを表示 |
  | f | 完全なフォーマットでリストする |


* 使い方
  ```bash
  # 「 vim 」というプロセスを表示
  $ ps -ef | grep vim
  takahana  2640  2828  0 19:03 pts/0    00:00:00 grep --color=auto vim
  takahana  7042  2828  0 16:45 pts/0    00:00:00 vim test
  takahana  7043  2828  0 16:45 pts/0    00:00:00 vim test2
  ```

### route - ルーティングテーブルの管理

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

### sed - 文字列置換などのテキスト処理

* 必須レベル：★★☆☆☆

* オプション
  |  オプション  |  詳細  |
  | ---- | ---- |
  |  e  |  スクリプトコマンド実行  |
  |  r  |  拡張正規表現でスクリプトコマンド実行<br>※スクリプトコマンド例（s:/置換前/置換後/g）  |
  |  i  |  ファイルを直接編集  |
  |  i拡張子  |  ファイルを直接編集し、拡張子の退避ファイル作成  |

* 使い方
  ```bash
  # 標準出力の編集
  $ echo "2020/07/11" | sed -e 's/\///g'
  20200711

  # 区切りはスラッシュ以外でも可能
  $ echo "2020/07/11" | sed -e 's%/%%g'
  20200711

  # ファイルの編集
  $ grep user *sh
  test1.sh:echo "user1"
  test2.sh:echo "user1"
  $ sed -i -e 's/user1/user2/g' ./*.sh
  $ grep user *sh
  test1.sh:echo "user2"
  test2.sh:echo "user2"

  # スペース削除と任意箇所切り取り
  $ ls -l /usr/bin/vi* | sed -e 's/ \+/ /g'| cut -d' ' -f9-
  /usr/bin/vi
  /usr/bin/view -> vi
  /usr/bin/vim
  /usr/bin/vimdiff -> vim
  /usr/bin/vimtutor
  /usr/bin/vinagre

  #バイナリファイルの編集
  $ xxd -p -c 1000000 ./before | sed "s/f2f0f2f1f0f9f0f1/${AFTER}/g" | xxd -p -r > ./after

  # ファイル操作
  # 拡張子の変更
  $ find ./ -name "test*.sh"
  ./test1.sh
  ./test2.sh

  $ find ./ -name "test*.sh" | sed -nr 's/(.*)\.sh/mv & \1\.txt/p'
  mv ./test1.sh ./test1.txt
  mv ./test2.sh ./test2.txt

  $ find ./ -name "test*.sh" | sed -nr 's/(.*)\.sh/mv & \1\.txt/p' | bash

  $ ls -1
  test1.txt
  test2.txt
  ```

### tar - アーカイブの作成

* 必須レベル：★★★★☆<br>
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

### tee - 出力を複数のファイルやプロセスにリダイレクトする

* 必須レベル：★★☆☆☆<br>

* オプション<br>
    | オプション | 詳細 |
    | --- | --- |
    | -a <br> (--append) | 指定されたファイルの末尾に標準入力を追記する。 |

* 使い方
  ```bash
  #ツール実行結果を標準出力とログに出力する
  $ ./tool.sh 2>&1 | tee -a tool.log
  ```

### umask - デフォルトの権限を決定する

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

### unzip - ファイル解凍をする（zipを参照）


### vi - vimを参照

### vim - 高機能なテキストエディタ  

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

  " 垂直分割★
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
  | ^ | 行の先頭へ★ |
  | $ | 行の末尾へ★ |
  | + | 下の行の先頭へ |
  | - | 上の行の先頭へ |

* ページ移動ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | :100 | 100行目へ ★ |
  | ctrl + u | 半画面分 上へ ★ |
  | ctrl + d | 半画面分 下へ ★ |
  | ctrl + b | 一画面分 上へ |
  | ctrl + f | 一画面分 下へ |
  | { | 段落毎に上へ★ |
  | } | 段落毎に下へ★ |
  | gg | そのファイルの先頭へ★ |
  | G | そのファイルの末尾へ★ |
  | zz | 現在カーソルを画面中央へ |

* 単語移動ショートカット<br>
  ※大文字の場合はピリオドなど区切り文字もまとまりとみなす
  | コマンド | 内容 |
  | ---- | ---- |
  | w | 単語の先頭に進む★ |
  | b | 単語の先頭に戻る |
  | e | 単語の末尾に進む |

* 行内検索ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | f | その行の順方向に一文字検索★ |
  | F | その行の逆方向に一文字検索 |
  | ; | 順方向に繰り返し検索 |
  | , | 逆方向に繰り返し検索 |

* 検索ショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | / | 順方向に文字列検索★ |
  | ? | 逆方向に文字列検索★ |
  | n | 順方向に繰り返し検索★ |
  | N | 逆方向に繰り返し検索 |
  | % | 対となる括弧へ移動 |

* コピー／ペーストショートカット
  | コマンド | 内容 |
  | ---- | ---- |
  | yw | 1単語コピー★ |
  | yy | 1行コピー★ |

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

### xargs - 引数からコマンドを組み立て実行する

* 必須レベル：★★★★☆

* 使い方
  ```bash
  # 直前のコマンドの実行結果を渡す
  $ ls README.md | xargs md5sum
  ccd981a6716bb3b91569e45d336b28d0 *README.md
  ```

### xxd - 2進数でダンプする  

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

### yum - RedHat系で利用されるパッケージ管理ツール

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  # yumはパイソンで動いている
  $ head -n 1 /usr/bin/yum
  #!/usr/bin/python
  ```

### w - ログインしている人とその人がやっていることを表示する

* 必須レベル：★★☆☆☆

* 使い方
  ```bash
  $ w
  19:20:48 up  9:54,  1 user,  load average: 0.00, 0.02, 0.05
  USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
  takahana pts/0    gateway          10:37    0.00s  1.42s  0.03s w
  ```

### wc -各ファイルの改行数、ワード数、バイト数を表示する

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

### which - コマンドのフルパスを表示する

* 必須レベル：★★★★★

* 使い方
  ```bash
  $ which echo
  /usr/bin/echo
  ```

### whoami - 実効ユーザ名を出力する

* 必須レベル：★★★☆☆

* 使い方
  ```bash
  $ whoami
  takahana
  ```

### zgrep - 圧縮されている可能性のあるファイルで、正規表現の検索をする

* 必須レベル：★★★☆☆
  
* 使い方
  ```bash

  ```

### zip - ファイル圧縮をする

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
  
### !! - 直前のコマンドを実行

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

### > - 出力リダイレクト

### >> - 出力リダイレクト（追記）

* 必須レベル：★★★★★

* 使い方

### < - 入力リダイレクト

### << - 入力リダイレクト（追記）

* 必須レベル：★★★☆☆

* 使い方

<br>

## ３．シェル

### 用語説明

#### シェバン  
シェルの1行目に記載し、このシェルは「bin/bash」で動かしますの意味

  ```bash
  #!/bin/bash
  ```

#### セカンダリプロンプト  
行末の「\」のことで、まだコマンドは終了していないことを意味する

  ```bash
  $ echo \
  "Hello, World!"
  ```

### 引数／特殊変数

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

### 比較

#### 文字列比較

#### 数値比較

### サンプル

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

## ４．組み合わせ便利コマンド

### 無限ループ（while true）

  ```bash
  # 無限ループ
  while true; do date; echo "hello !"; sleep 1s; done
  ```

### リスト読込（for ～ in）

  ```bash
  # git最新化（※xxxフォルダを除く）
  for f in */.git;do (f=${f%/*}; if [ $f != "xxx" ]; then cd $f; git pull; fi);done;
  ```

### ファイル読込（while read）

  ```bash
  # ファイルを読み込み、1行ずつ処理する
  while read line; do md5sum $line;done <bkup.txt
  ```

### ファイル存在確認（if）

  ```bash
  # ファイル存在確認結果を表示
  if [ -e $FILE ];then echo "OK";else echo "NG";fi
  ```

### 文字列の比較（if）

  ```bash
  # 文字列の比較結果を表示
  if [ "test" = "test" ];then echo "OK";else echo "NG";fi
  ```


<br>
