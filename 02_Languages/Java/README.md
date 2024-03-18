# Java

<!-- TOC -->
- [1. 設定](#1-設定)
- [2. 基本クラス](#2-基本クラス)
  - [2.1. 豆知識](#21-豆知識)
  - [2.2. Integerクラス](#22-integerクラス)
  - [2.3. Stringクラス](#23-stringクラス)
  - [2.4. StringBufferクラス](#24-stringbufferクラス)
  - [2.5. StringBuilderクラス](#25-stringbuilderクラス)
- [3. ビルド](#3-ビルド)
  - [3.1. JARファイル](#31-jarファイル)
  - [3.2. WARファイル](#32-warファイル)
  - [3.3. EARファイル](#33-earファイル)
- [4. 用語集](#4-用語集)
  - [4.1. staticメソッド](#41-staticメソッド)
  - [4.2. ラッパークラス](#42-ラッパークラス)
---
<br>
<!-- /TOC -->

## 1. 設定

<br>

## 2. 基本クラス

### 2.1. 豆知識

```java
// 型の確認
Object.getClass().getSimpleName()
```

### 2.2. Integerクラス  
プリミティブ型intの値をオブジェクトにラップする。  
intをStringに、Stringをintに変換するなど各種メソッドを提供する。

```java
/** コンストラクタ **/

// int型から生成
Integer intSample2 = new Integer(123);
// String型から生成
Integer intSample3 = new Integer("123");

/** 主要メソッド **/

// toString()
// Stringオブジェクトを返す
String strNumber1 = intSample1.toString();
// parseInt(String s)
// 10進数の整数型として返す
Integer intNumber1 = Integer.parseInt("123");
// valueOf(int i)
// Integerインスタンスを返す
Integer intNumber2 = Integer.valueOf(123);
// valueOf(String s)
// Integerインスタンスを返す
Integer intNumber3 = Integer.valueOf("123");
```

### 2.3. Stringクラス  
Stringクラスは文字列を表す。リテラル文字列はすべて、このクラスのインスタンスとして実行される。
Stringクラスには、文字列の比較、文字列の検索など各種メソッドを提供する。

```java
/** コンストラクタ **/

// 初期化して、空の文字シーケンスを表す。
// ※Stringは不変なので、このコンストラクタを使う必要はない。
String strSample = new String();

/** 主要メソッド **/
String str0 = "";
String str1 = "TEST1";
String str2 = "TEST2";
String str3 = "TEST0,TEST1,TEST2";
// concat(String str) 文字連結
System.out.println(str1.concat(str2));  // TEST1TEST2
// equals(Object anObject) 文字列比較
System.out.println(str1.equals(str2));  // false
// length() 長さを取得
System.out.println(str2.length());  // 5
// isEmpty() length()が0の場合にのみtrue
System.out.println(str0.isEmpty());  // true
// split(String regex) 指定された正規表現に一致する位置で分割
String[] strArray = str3.split(",");
System.out.println(strArray[0]);  // TEST0
```

### 2.4. StringBufferクラス  
スレッドセーフな可変の文字列。  
⇒文字列バッファは複数のスレッドによって安全に使用することができる。  
⇒安全だが高速に処理できるStringBuilderでいい

### 2.5. StringBuilderクラス  
文字の可変シーケンス。StringBufferと互換性があるが、同期化は保証ない。

```java
/** コンストラクタ **/

// 初期容量が16文字である文字列ビルダーを構築
StringBuilder sql1 = new StringBuilder();
// 指定された容量の文字列ビルダーを構築
StringBuilder sql2 = new StringBuilder(1024);

/** 主要メソッド **/
// append(String str) 文字の追加
sql1.append("SELECT ");
sql1.append("* ");
sql1.append("FROM ");
sql1.append("dual ");
System.out.println(sql1);  // SELECT * FROM dual 
// toString() 文字列を返す
String sql1 = sql.toString();
```

<br>

## 3. ビルド

javaファイルをコンパイルするとclassファイルが作成され、以下ZIP形式の圧縮ファイルとして各サービスに配布される。

### 3.1. JARファイル
複数のJavaクラスや、それに関連するメタデータファイル、テキストやイメージファイル、設定ファイル(XML)をひとつのファイルに統合した形式。  
※Java ARchiveの略

### 3.2. WARファイル
JavaベースのWebアプリケーションやコンポーネントを圧縮した形式で、Webサーバ上で動作する。  ApacheのTomcatのようなWebアプリケーションを導入したWebサーバ上で動作させることができる。  
※Web Application Resources(Web ARchive)の略

### 3.3. EARファイル
J2EEサーバー上にアプリケーションをデプロイするのに適した形式で、J2EEサーバーはエンタープライズシステム向けのJavaプラットフォームのこと。  
※Enterprise Archiveの略

<br>

## 4. 用語集

### 4.1. staticメソッド
* 複数のインスタンスの間で共有されつづける情報、共有資源にして欲しいフィールドに static をつける。
* インスタンスを生成しなくても呼び出せる。  
* 定数定義の際にfinal static で宣言することで、new する度に同じ値がインスタンスに複製されることが防止され、メモリの節約ができる。
* static が付かない一般のメソッドは非 static メソッド、インスタンスメソッドという

### 4.2. ラッパークラス
プリミティブ型をラップしているクラスのことで、それぞれのクラスで便利なメソッドが容易されている。

| プリミティブ型 | ラッパークラス |
| --- | --- |
| boolean | Boolean |
| byte | Byte |
| char | Character |
| short | Short |
| int | Integer |
| float | Float |
| long | Long |
| double | Double |  
※Stringは当初からオブジェクト

<br>
