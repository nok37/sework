# Linux

<!-- TOC -->

- [１．設定 ・ 豆知識](#１．設定-・-豆知識)
    - [コマンドの実行パス](#コマンドの実行パス)
    - [ssh接続時に表示される文言](#ssh接続時に表示される文言)
    - [bash設定](#bash設定)
    - [cron](#cron)
- [２．コマンド](#２．コマンド)
    - [ac　#ユーザのログイン時間を表示する](#ac　ユーザのログイン時間を表示する)
    - [bc　#任意精度の計算言語](#bc　任意精度の計算言語)
    - [cancel　#印刷ジョブを取り消す](#cancel　印刷ジョブを取り消す)
    - [chmod　#ファイルの権限を変更する](#chmod　ファイルの権限を変更する)
    - [cupsdisabl　#プリンタ無効化](#cupsdisabl　プリンタ無効化)
    - [cupsenable　#プリンタ有効化](#cupsenable　プリンタ有効化)
    - [curl  #HTTPなどの通信プロトコルでデータを転送する](#curl--httpなどの通信プロトコルでデータを転送する)
    - [dc　#無限精度の計算が行える卓上計算機](#dc　無限精度の計算が行える卓上計算機)
    - [ifconfig　#ネットワークインターフェースの管理](#ifconfig　ネットワークインターフェースの管理)
    - [keytool　#鍵と証明書を管理](#keytool　鍵と証明書を管理)
    - [last　#ログイン履歴を表示する](#last　ログイン履歴を表示する)
    - [od　#8進数やその他の形式でダンプする](#od　8進数やその他の形式でダンプする)
    - [openssl　#証明書の作成](#openssl　証明書の作成)
    - [route　#ルーティングテーブルの管理](#route　ルーティングテーブルの管理)
    - [sed　#文字列置換などのテキスト処理](#sed　文字列置換などのテキスト処理)
    - [umask　#デフォルトの権限を決定する](#umask　デフォルトの権限を決定する)
    - [vim　#高機能なテキストエディタ](#vim　高機能なテキストエディタ)
    - [yum　#RedHat系で利用されるパッケージ管理ツール](#yum　redhat系で利用されるパッケージ管理ツール)
    - [xxd　#2進数でダンプする](#xxd　2進数でダンプする)
- [３．シェル](#３．シェル)
    - [用語説明](#用語説明)
        - [シェバン](#シェバン)
        - [セカンダリプロンプト](#セカンダリプロンプト)
        - [引数／特殊変数](#引数／特殊変数)
        - [サンプル](#サンプル)
- [４．組み合わせ便利コマンド](#４．組み合わせ便利コマンド)
    - [無限ループ](#無限ループ)
    - [リスト読込](#リスト読込)
    - [ファイル読込](#ファイル読込)
    - [ファイル存在確認](#ファイル存在確認)

<!-- /TOC -->
---
<br>
<!-- NEXT INDENT -->

<a id="markdown-１．設定-・-豆知識" name="１．設定-・-豆知識"></a>
## １．設定 ・ 豆知識

<a id="markdown-コマンドの実行パス" name="コマンドの実行パス"></a>
### コマンドの実行パス
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

<a id="markdown-ssh接続時に表示される文言" name="ssh接続時に表示される文言"></a>
### ssh接続時に表示される文言
Message of the dayの略
```bash
/etc/motd
```

<a id="markdown-bash設定" name="bash設定"></a>
### bash設定
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

<a id="markdown-cron" name="cron"></a>
### cron

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

<br>
<!-- NEXT INDENT -->

<a id="markdown-２．コマンド" name="２．コマンド"></a>
## ２．コマンド

<a id="markdown-ac　ユーザのログイン時間を表示する" name="ac　ユーザのログイン時間を表示する"></a>
### ac　#ユーザのログイン時間を表示する
※/var/log/wtmp 」を参照している

```bash
$ ac -p
        takahana                            81.90
        root                                 0.01
        total       81.91
```

<a id="markdown-bc　任意精度の計算言語" name="bc　任意精度の計算言語"></a>
### bc　#任意精度の計算言語

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

<a id="markdown-cancel　印刷ジョブを取り消す" name="cancel　印刷ジョブを取り消す"></a>
### cancel　#印刷ジョブを取り消す

```bash
# キュー全削除（※root権限）
$ cancel -a TESTPRT
```

<a id="markdown-chmod　ファイルの権限を変更する" name="chmod　ファイルの権限を変更する"></a>
### chmod　#ファイルの権限を変更する

```bash
# ユーザに実行権限を付与する
$ chmod u+x file

#グループに書き込み権限をその他のユーザーにはすべて禁止する
$ chmod g+w,o= test

# 再帰的に変更する（ディレクトリも含めて）
$ chmod -R 777 dir
```

<a id="markdown-cupsdisabl　プリンタ無効化" name="cupsdisabl　プリンタ無効化"></a>
### cupsdisabl　#プリンタ無効化

```bash
# ※root権限
$ cupsdisable TESTPRT
```

<a id="markdown-cupsenable　プリンタ有効化" name="cupsenable　プリンタ有効化"></a>
### cupsenable　#プリンタ有効化

```bash
# ※root権限
$ cupsenable TESTPRT
```

<a id="markdown-curl--httpなどの通信プロトコルでデータを転送する" name="curl--httpなどの通信プロトコルでデータを転送する"></a>
### curl  #HTTPなどの通信プロトコルでデータを転送する

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

<a id="markdown-dc　無限精度の計算が行える卓上計算機" name="dc　無限精度の計算が行える卓上計算機"></a>
### dc　#無限精度の計算が行える卓上計算機
※逆ポーランド形式

```bash
#複雑な計算　(27/(1+2)^2)*2
$ dc
27 1 2 + 2 ^ / 2 * 
p
6
```

<a id="markdown-ifconfig　ネットワークインターフェースの管理" name="ifconfig　ネットワークインターフェースの管理"></a>
### ifconfig　#ネットワークインターフェースの管理

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

<a id="markdown-keytool　鍵と証明書を管理" name="keytool　鍵と証明書を管理"></a>
### keytool　#鍵と証明書を管理
※デフォルトのパスワードは「changeit」

```bash
# 登録（jre）
$ keytool -import -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts -file server.crt

# 確認
keytool -list -alias xxxCA -keystore ${JAVA_HOME}\jre\lib\security\cacerts
```

<a id="markdown-last　ログイン履歴を表示する" name="last　ログイン履歴を表示する"></a>
### last　#ログイン履歴を表示する

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

<a id="markdown-od　8進数やその他の形式でダンプする" name="od　8進数やその他の形式でダンプする"></a>
### od　#8進数やその他の形式でダンプする

|  オプション  |  詳細  |
| ---- | ---- |
| -t   | オプションで出力フォーマット指定 |  
|  c   | ASCII 文字または \ エスケープ文字で表示する |  
|  x   | 16進数2バイトで表示する（x2と同じ） |  
|  d   | 10進数2バイトで表示する |  
<br>

```bash
#１行目にASCII表示
#２行目に16進数1バイト表示(x1)
#３行目に10進数1バイト表示(x1)
$ echo '10AZaz-!'|od -tcx1d1
0000000    1    0    A    Z    a    z    -    !   \n
          31   30   41   5a   61   7a   2d   21   0a
          49   48   65   90   97  122   45   33   10
0000011

#SJIS
$ echo '09AZｱ'
0000000 30 39 41 5a b1 0a
0000010
#UTF8
#ef bdはBOM(バイトオーダーマーク)
$ echo '09AZｱ'
0000000 30 39 41 5a ef bd b1 0a
0000010
```

<a id="markdown-openssl　証明書の作成" name="openssl　証明書の作成"></a>
### openssl　#証明書の作成
ローカルでWEBサーバを公開する際に、以下手順で自己証明書を作成する。  
※Javaに取り込む場合は「keytool」コマンドを使用する。  
※登録時に指定した「CN」が公開するホスト名と一致する必要がある。

```bash
# 秘密鍵の作成
openssl genrsa 2048 > server.key

# CSRの作成
openssl req -new -key server.key > server.csr

# SSLサーバー証明書(crt形式)の作成
openssl x509 -days 3650 -req -signkey server.key < server.csr > server.crt
```

<a id="markdown-route　ルーティングテーブルの管理" name="route　ルーティングテーブルの管理"></a>
### route　#ルーティングテーブルの管理

```bash
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         gateway         0.0.0.0         UG    100    0        0 enp0s3
10.0.2.0        0.0.0.0         255.255.255.0   U     100    0        0 enp0s3
192.168.122.0   0.0.0.0         255.255.255.0   U     0      0        0 virbr0
```

<a id="markdown-sed　文字列置換などのテキスト処理" name="sed　文字列置換などのテキスト処理"></a>
### sed　#文字列置換などのテキスト処理

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

#バイナリファイルの編集
$ xxd -p -c 1000000 ./before | sed "s/f2f0f2f1f0f9f0f1/${AFTER}/g" | xxd -p -r > ./after
```

<a id="markdown-umask　デフォルトの権限を決定する" name="umask　デフォルトの権限を決定する"></a>
### umask　#デフォルトの権限を決定する

```bash
$ umask 022
# ディレクトリの場合、777 - 022 = 755
# ファイルの場合、666 - 022 = 644
# umaskから引いた値がデフォルト権限となる
drwxr-xr-x. 2 taka taka   6  8月 11 23:12 dir
-rw-r--r--. 1 taka taka   0  8月 11 23:12 file

# /etc/bashrcに記載されている
if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
   umask 002
else
   umask 022
fi
```

<a id="markdown-vim　高機能なテキストエディタ" name="vim　高機能なテキストエディタ"></a>
### vim　#高機能なテキストエディタ  

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

・コマンド

★よく使うやつ
| 基本移動 | 内容 |
| ---- | ---- |
| h | 左へ一つ |
| j | 下へ一つ |
| k | 上へ一つ |
| l | 右へ一つ |
| gj | 下へ一つ ※gは表示上の移動 |

| 行移動 | 内容 |
| ---- | ---- |
| 0 | 行の先頭へ(インデント無視して先頭へ) |
| ^ | 行の先頭へ★ |
| $ | 行の末尾へ★ |
| + | 下の行の先頭へ |
| - | 上の行の先頭へ |

| ページ移動 | 内容 |
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

| 単語移動 | 内容 |
| ---- | ---- |
| w | 単語の先頭に進む★ |
| b | 単語の先頭に戻る |
| e | 単語の末尾に進む |

※大文字の場合はピリオドなど区切り文字もまとまりとみなす。

| 行内検索 | 内容 |
| ---- | ---- |
| f | その行の順方向に一文字検索★ |
| F | その行の逆方向に一文字検索 |
| ; | 順方向に繰り返し検索 |
| , | 逆方向に繰り返し検索 |

| 検索 | 内容 |
| ---- | ---- |
| / | 順方向に文字列検索★ |
| ? | 逆方向に文字列検索★ |
| n | 順方向に繰り返し検索★ |
| N | 逆方向に繰り返し検索 |
| % | 対となる括弧へ移動 |

| コマンドライン | 内容 |
| ---- | ---- |
| :vs | 垂直分割★ |
| :vnew  | 垂直分割で空ウィンドウ開く |
| :vs {file}  | 垂直分割で指定のファイルを開く |
| :tabnew {file} | 新規タブでファイルを開く |

・vimrc

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

<a id="markdown-yum　redhat系で利用されるパッケージ管理ツール" name="yum　redhat系で利用されるパッケージ管理ツール"></a>
### yum　#RedHat系で利用されるパッケージ管理ツール

```bash
# yumはパイソンで動いている
$ head -n 1 /usr/bin/yum
#!/usr/bin/python
```

<a id="markdown-xxd　2進数でダンプする" name="xxd　2進数でダンプする"></a>
### xxd　#2進数でダンプする  

|  オプション  |  詳細  |
| ---- | ---- |
| -b | オプションでバイナリ（2進数）表示 |
| -c | オプションで表示数変更 |
| -p | ポストスクリプト形式の 16 進ダンプを出力する。 |
| -r | 元に戻す: 16 進ダンプからバイナリ形式に変換 
<br>
・コマンド実行例

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

<br>
<!-- NEXT INDENT -->

<a id="markdown-３．シェル" name="３．シェル"></a>
## ３．シェル

<a id="markdown-用語説明" name="用語説明"></a>
### 用語説明

<a id="markdown-シェバン" name="シェバン"></a>
#### シェバン  
シェルの1行目に記載し、このシェルは「bin/bash」で動かしますの意味

```bash
#!/bin/bash
```
<a id="markdown-セカンダリプロンプト" name="セカンダリプロンプト"></a>
#### セカンダリプロンプト  
行末の「\」のことで、まだコマンドは終了していないことを意味する

```bash
echo \
"Hello, World!"
```

<a id="markdown-引数／特殊変数" name="引数／特殊変数"></a>
#### 引数／特殊変数

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

<a id="markdown-サンプル" name="サンプル"></a>
#### サンプル

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
<!-- NEXT INDENT -->

<a id="markdown-４．組み合わせ便利コマンド" name="４．組み合わせ便利コマンド"></a>
## ４．組み合わせ便利コマンド

<a id="markdown-無限ループ" name="無限ループ"></a>
### 無限ループ

```bash
# 無限ループ
while true; do date; echo "hello !"; sleep 1s; done
```

<a id="markdown-リスト読込" name="リスト読込"></a>
### リスト読込

```bash
# git最新化（※xxxフォルダを除く）
for f in */.git;do (f=${f%/*}; if [ $f != "xxx" ]; then cd $f; git pull; fi);done;
```

<a id="markdown-ファイル読込" name="ファイル読込"></a>
### ファイル読込

```bash
# ファイルを読み込み、1行ずつ処理する
while read line; do md5sum $line;done <bkup.txt
```

<a id="markdown-ファイル存在確認" name="ファイル存在確認"></a>
### ファイル存在確認

```bash
# ファイル存在確認結果を表示
if [ -e $FILE ];then echo "OK";else echo "NG";fi
```

<br>
<!-- NEXT INDENT -->