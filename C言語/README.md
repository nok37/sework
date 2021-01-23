# C言語

## 目次
<!-- TOC -->

- [１．ライブラリについて](#１．ライブラリについて)
    - [◆ 静的ライブラリ](#◆-静的ライブラリ)
    - [◆ 共有ライブラリ](#◆-共有ライブラリ)
    - [◆ 動的ライブラリ(≒共有ライブラリ)](#◆-動的ライブラリ≒共有ライブラリ)

<!-- /TOC -->
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