# C言語

<!-- TOC -->
- [1. コンパイル／ビルド](#1-コンパイルビルド)
  - [1.1. コンパイル](#11-コンパイル)
  - [1.2. ライブラリの作成](#12-ライブラリの作成)
    - [1.2.1. 静的ライブラリ](#121-静的ライブラリ)
    - [1.2.2. 共有ライブラリ](#122-共有ライブラリ)
    - [1.2.3. 動的ライブラリ(≒共有ライブラリ)](#123-動的ライブラリ共有ライブラリ)
- [2. メモリとスコープ](#2-メモリとスコープ)
  - [2.1. 静的(Static) / 大域(Global)](#21-静的static--大域global)
  - [2.2. 自動(Automatic)](#22-自動automatic)
  - [2.3. 動的(Dynamic)](#23-動的dynamic)
- [3. 自作ファイル](#3-自作ファイル)
  - [3.1. 基本](#31-基本)
  - [3.2. ポインタ](#32-ポインタ)
---
<br>
<!-- /TOC -->

## 1. コンパイル／ビルド

### 1.1. コンパイル

* 基本
    ```bash
    $ gcc sample1.c -o sample1.o
    ```

### 1.2. ライブラリの作成

#### 1.2.1. 静的ライブラリ
プログラムの構築時に組み込まれるライブラリ。(拡張子は .a)  
<br>

1. 通常ライブラリのコンパイル  
→ コンパイルするとオブジェクトファイル (.o) ができる  
    ```bash
    $ gcc -c greet.c
    $ ls | grep \.o$
    greet.o
    ```

2. 静的ライブラリの作成  
→ ar コマンドを使ってオブジェクトファイルをまとめる  
※ライブラリのファイル名は lib から始まるようにする
    ```bash
    $ ar rusv libgreet.a greet.o
    ar: libgreet.a を作成しています
    a - greet.o
    $ ls | grep \.a$
    libgreet.a
    ```

3. 静的ライブラリの確認
    ```bash
    $ ar tv libgreet.a
    rw-rw-r-- 1000/1000   1504 Oct 17 14:19 2020 greet.o
    ```

4. 静的ライブラリを使って実行ファイルを作る  
→ 静的ライブラリを使うには、それを使うアプリケーションをコンパイルするときに -l オプションを指定する。  
※指定するのは lib を除いたライブラリの名前  
※静的ライブラリ(.a)を受け取った場合は、未解決の参照を定義しているオブジェクトファイルのみを静的ライブラリから抜き出し、リンクを行う。
    ```bash
    $ gcc -o main main.c -L. -lgreet
    $ file main
    main: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=3dd427b0cfae516aa1e3a9c1acee0dd43653b1e7, not stripped
    ```

5. 実行ファイルの実行
    ```bash
    $ ./main
    Hello, World!
    ```

#### 1.2.2. 共有ライブラリ
プログラム実行と同時にメモリ上に展開されるライブラリ(拡張子は .so)  

1. 共有ライブラリの作成
    ```
    $ gcc -shared -fPIC -o libgreet.so greet.c
    $ file libgreet.so
    libgreet.so: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, BuildID[sha1]=8ca16b06f3784a2040f58528f711677b877c74a4, not stripped
    ```

#### 1.2.3. 動的ライブラリ(≒共有ライブラリ)
プログラム実行中の任意の時点で読み込まれるライブラリ。  

<br>

## 2. メモリとスコープ

### 2.1. 静的(Static) / 大域(Global)

 * プログラム開始時に割り当てられ、プログラム終了時まで維持される  
 * 静的変数は変数定義を行った関数内にアクセスが制限され、大域変数はすべての関数からアクセスすることができる

### 2.2. 自動(Automatic)

 * 普通のローカル変数のこと  
 * 関数の中で宣言され、関数が呼ばれた時に割り当てられる  
 * 変数定義を行った関数内にアクセスが制限される
 
### 2.3. 動的(Dynamic)

 * メモリはヒープから割り当てられ、必要に応じて解放される  
 * 割り当てられたメモリは、メモリを参照しているポインタのみアクセスできる
    |    |  アドレス例  |  備考  |
    | ---- | ---- | ---- |
    | heap | 0x16f4010<br>0x16f4030 | 【動的変数】<br>・動的に割り当てられたメモリはヒープから得られる(malloc)<br>・メモリの割り当てと開放をくりかえすことで、ヒープは断片化する<br>・ヒープは実行するたびにアドレスが変わる<br>※下に向かって大きくなる |
    | global | 0x60103c<br>0x601042 | 【大域変数】<br>・プログラム開始時に割り当てられる |
    | static | 0x601048<br>0x60104e | 【静的変数】<br>・プログラム開始時に割り当てられる |
    | stack<br><br>sub()<br>-str2<br>-str1<br>main()<br>-var2<br>-var1 | <br><br><br>0x7ffc03ffcc20<br>0x7ffc03ffcc30<br><br>0x7ffc03ffcc50<br>0x7ffc03ffcc60 | 【自動変数】<br>・関数開始時に割り当て（スタックのためアドレスが大きい）<br>・関数が開始すると、スタックフレームがプッシュされる<br>→main関数のアドレスは大きく、sub関数のアドレスが小さい<br>・関数が終了すると、スタックフレームがポップされる<br>→sub関数終了にスタックはポップされるため同じアドレスを使用<br>※上に向かって大きくなる |

変数のスコープを理解し、ポインタを通してメモリ管理することがC言語の基本！

<br>

## 3. 自作ファイル

### 3.1. 基本
    ```c
    #include<stdio.h>
    //##################################################
    //# 名前：hello.c
    //# 機能：「こんにちは」といいます。
    //# 概要：
    //##################################################

    //====================
    // メイン処理
    //====================
    int main(void)
    {

      printf("こんにちは\n");

      return 0;

    }
    ```

### 3.2. ポインタ

<br>