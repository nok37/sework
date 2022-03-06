# Java

## 目次
<!-- TOC -->

- [１．設定／全般／環境](#１．設定／全般／環境)
- [２．基本クラス](#２．基本クラス)
    - [◆豆知識](#◆豆知識)
    - [◆Integerクラス](#◆integerクラス)
    - [◆Stringクラス](#◆stringクラス)
    - [◆StringBufferクラス](#◆stringbufferクラス)
    - [◆StringBuilderクラス](#◆stringbuilderクラス)
- [３．ビルド](#３．ビルド)
    - [◆ JARファイル](#◆-jarファイル)
    - [◆ WARファイル](#◆-warファイル)
    - [◆ EARファイル](#◆-earファイル)
- [４．用語集](#４．用語集)
    - [◆staticメソッド](#◆staticメソッド)
    - [◆ラッパークラス](#◆ラッパークラス)

<!-- /TOC -->
<br>

<a id="markdown-１．設定／全般／環境" name="１．設定／全般／環境"></a>
### １．設定／全般／環境
---

<br>

<a id="markdown-２．基本クラス" name="２．基本クラス"></a>
### ２．基本クラス
---

<a id="markdown-◆豆知識" name="◆豆知識"></a>
#### ◆豆知識
```java
// 型の確認
Object.getClass().getSimpleName()

```

<a id="markdown-◆integerクラス" name="◆integerクラス"></a>
#### ◆Integerクラス  
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

<a id="markdown-◆stringクラス" name="◆stringクラス"></a>
#### ◆Stringクラス  
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

<a id="markdown-◆stringbufferクラス" name="◆stringbufferクラス"></a>
#### ◆StringBufferクラス  
スレッドセーフな可変の文字列。  
⇒文字列バッファは複数のスレッドによって安全に使用することができる。  
⇒安全だが高速に処理できるStringBuilderでいい

<a id="markdown-◆stringbuilderクラス" name="◆stringbuilderクラス"></a>
#### ◆StringBuilderクラス  
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



<a id="markdown-３．ビルド" name="３．ビルド"></a>
### ３．ビルド
---
javaファイルをコンパイルするとclassファイルが作成され、以下ZIP形式の圧縮ファイルとして各サービスに配布される。
<a id="markdown-◆-jarファイル" name="◆-jarファイル"></a>
#### ◆ JARファイル
複数のJavaクラスや、それに関連するメタデータファイル、テキストやイメージファイル、設定ファイル(XML)をひとつのファイルに統合した形式。  
※Java ARchiveの略
<a id="markdown-◆-warファイル" name="◆-warファイル"></a>
#### ◆ WARファイル
JavaベースのWebアプリケーションやコンポーネントを圧縮した形式で、Webサーバ上で動作する。  ApacheのTomcatのようなWebアプリケーションを導入したWebサーバ上で動作させることができる。  
※Web Application Resources(Web ARchive)の略
<a id="markdown-◆-earファイル" name="◆-earファイル"></a>
#### ◆ EARファイル
J2EEサーバー上にアプリケーションをデプロイするのに適した形式で、J2EEサーバーはエンタープライズシステム向けのJavaプラットフォームのこと。  
※Enterprise Archiveの略

<a id="markdown-４．用語集" name="４．用語集"></a>
### ４．用語集
<a id="markdown-◆staticメソッド" name="◆staticメソッド"></a>
#### ◆staticメソッド
* 複数のインスタンスの間で共有されつづける情報、共有資源にして欲しいフィールドに static をつける。
* インスタンスを生成しなくても呼び出せる。  
* 定数定義の際にfinal static で宣言することで、new する度に同じ値がインスタンスに複製されることが防止され、メモリの節約ができる。
* static が付かない一般のメソッドは非 static メソッド、インスタンスメソッドという

<a id="markdown-◆ラッパークラス" name="◆ラッパークラス"></a>
#### ◆ラッパークラス
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