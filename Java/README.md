# Java

## 目次
<!-- TOC -->

- [１．ビルド](#１．ビルド)
    - [◆ JARファイル](#◆-jarファイル)
    - [◆ WARファイル](#◆-warファイル)
    - [◆ EARファイル](#◆-earファイル)

<!-- /TOC -->
<br>

<a id="markdown-１．ビルド" name="１．ビルド"></a>
### １．ビルド
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