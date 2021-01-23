# C言語

## 目次
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [１．ライブラリについて](#%EF%BC%91%EF%BC%8E%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
  - [◆ 静的ライブラリ](#%E2%97%86-%E9%9D%99%E7%9A%84%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA)
  - [◆ 共有ライブラリ](#%E2%97%86-%E5%85%B1%E6%9C%89%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA)
  - [◆ 動的ライブラリ(≒共有ライブラリ)](#%E2%97%86-%E5%8B%95%E7%9A%84%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA%E2%89%92%E5%85%B1%E6%9C%89%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
<br>

### １．ライブラリについて
---

#### ◆ 静的ライブラリ
プログラムの構築時に組み込まれるライブラリ。(拡張子は .a)  
<br>
①通常ライブラリのコンパイル  
→ コンパイルするとオブジェクトファイル (.o) ができる  
```bash
$ gcc -c greet.c
$ ls | grep \.o$
greet.o
```
②静的ライブラリの作成  
→ ar コマンドを使ってオブジェクトファイルをまとめる  
※ライブラリのファイル名は lib から始まるようにする
```bash
$ ar rusv libgreet.a greet.o
ar: libgreet.a を作成しています
a - greet.o
$ ls | grep \.a$
libgreet.a
```
③静的ライブラリの確認
```bash
$ ar tv libgreet.a
rw-rw-r-- 1000/1000   1504 Oct 17 14:19 2020 greet.o
```
④静的ライブラリを使って実行ファイルを作る  
→ 静的ライブラリを使うには、それを使うアプリケーションをコンパイルするときに -l オプションを指定する。  
※指定するのは lib を除いたライブラリの名前  
※静的ライブラリ(.a)を受け取った場合は、未解決の参照を定義しているオブジェクトファイルのみを静的ライブラリから抜き出し、リンクを行う。
```bash
$ gcc -o main main.c -L. -lgreet
$ file main
main: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=3dd427b0cfae516aa1e3a9c1acee0dd43653b1e7, not stripped
```
⑤実行ファイルの実行
```bash
$ ./main
Hello, World!
```

#### ◆ 共有ライブラリ
プログラム実行と同時にメモリ上に展開されるライブラリ(拡張子は .so)  
①共有ライブラリの作成
```
$ gcc -shared -fPIC -o libgreet.so greet.c
$ file libgreet.so
libgreet.so: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, BuildID[sha1]=8ca16b06f3784a2040f58528f711677b877c74a4, not stripped
```

#### ◆ 動的ライブラリ(≒共有ライブラリ)
プログラム実行中の任意の時点で読み込まれるライブラリ。