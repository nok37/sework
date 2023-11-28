# Eclipse

<!-- TOC -->

- [１．設定](#１．設定)
- [２．ショートカット](#２．ショートカット)
    - [ファイル操作系](#ファイル操作系)
- [３．デバッグ](#３．デバッグ)
    - [リモートJavaアプリケーション](#リモートjavaアプリケーション)

<!-- /TOC -->
---
<br>

## １．設定

<br>

## ２．ショートカット
### ファイル操作系

```java
// リソースを開く
ctrl + shift + r

// 呼び出し階層を開く
ctrl + alt + h

// 次のエディタへ
ctrl + F6 (ctrl + e)

// 次のビュー
ctrl + F7

// 次のパースペクティブ
ctrl + F8

// ショートカット一覧表示
ctrl + shift + l

// クイックアウトライン
ctrl + o

// クイック階層
ctrl + t
```

<br>

## ３．デバッグ

### リモートJavaアプリケーション
ローカルマシン以外のjvmに接続してデバッグする。

```bash
# リモートアプリのデバッグ起動
$ java -cp xxx.jar -Xdebug -Xrunjdwp:transport=dt_socket,server=y,address=8000,suspend=n
# その後、eclipseからデバッグ接続を受け入れる
```

<br>
