# JavaScript

<!-- TOC -->

- [１．概要](#１．概要)
- [２．変数宣言／データ型](#２．変数宣言／データ型)
    - [変数宣言](#変数宣言)
    - [データ型](#データ型)
- [３．関数／クラス](#３．関数／クラス)
    - [関数の定義](#関数の定義)
    - [関数のさまざまな引数](#関数のさまざまな引数)
    - [クラスの定義](#クラスの定義)
- [４．その他構文](#４．その他構文)
    - [ラッパーオブジェクト](#ラッパーオブジェクト)
    - [等価／厳密等価](#等価／厳密等価)
    - [分割代入／スプレッド構文](#分割代入／スプレッド構文)
    - [繰り返し処理](#繰り返し処理)
    - [オブジェクトのマージとコピー](#オブジェクトのマージとコピー)
    - [プロトタイプ](#プロトタイプ)
    - [同期／非同期とプロミス](#同期／非同期とプロミス)
- [５．Node.js](#５．nodejs)
    - [概要](#概要)
    - [npm／yarn](#npm／yarn)
    - [package.jsonの記載方法](#packagejsonの記載方法)
- [６．React](#６．react)
    - [Reactの歴史](#reactの歴史)
    - [Reactの特徴](#reactの特徴)
    - [他のフレームワークとの比較](#他のフレームワークとの比較)
    - [create-react-appによるひな型作成](#create-react-appによるひな型作成)
    - [Virtual DOM（仮想DOM）](#virtual-dom仮想dom)
    - [Reactの仕組み](#reactの仕組み)
    - [関数型コンポーネント](#関数型コンポーネント)
    - [クラス型コンポーネント](#クラス型コンポーネント)
    - [その他](#その他)
- [７．Web技術トレンド](#７．web技術トレンド)
    - [CSR(Client Side Rendering)](#csrclient-side-rendering)
    - [SPA(Single Page Application)](#spasingle-page-application)
    - [SSR(Server Side Rendering)](#ssrserver-side-rendering)
    - [SSG(Static Site Generator)](#ssgstatic-site-generator)

<!-- /TOC -->
---
<br>

## １．概要
言語仕様はECMAScriptによって標準化され、実装は各種のJavaScriptエンジンによって提供されている。（Google ChromeのV8など）

<br>

## ２．変数宣言／データ型

###  変数宣言
var / let / constとあるが、varは以下の理由から使ってはいけない。※昔は変数宣言で使えるのはvarのみだったが、今は基本的にconstを使用する。  

1. 再宣言が可能
    ```javascript
    > var a=123
    > a=456  // 再代入OK
    > var a=789  // 再宣言OK
  
    > let b=123
    > b=456  // 再代入OK
    > let b=789  // 再宣言NG
    Uncaught SyntaxError: Identifier 'b'  hasalready     been declared
  
    > const c=123
    > c=456  // 再代入NG
    Uncaught TypeError: Assignment to   constantvariable.
    > const c=789  // 再宣言NG
    Uncaught SyntaxError: Identifier 'c'  hasalready     been declared
    ```

2. 変数の参照が巻き上げられる(hoisting)
    ```javascript
    // 関数内で宣言されたローカル変数はすべてその関数の先頭で宣言されたものとみなされる
    var myname = "global";
    function func() {
      console.log(myname);  // undefined
      var myname = "local";
      console.log(myname);  // local
    }
    func();

    // そのため、以下のコードと同じ挙動となる
    var myname = "global";
    function func() {
      var myname;  // 巻き上げ(hoisting)

      console.log(myname);  // undefined
      myname = "local";
      console.log(myname);  // local
    }
    ```

3. スコープ単位が関数  
  Rubyなど大多数の言語の変数スコープはブロック単位
    ```javascript
    var n = 0;

    if(true){
      var n = 50;
      var m = 100;
      console.log(n);  // 50
    }
    
    console.log(n);  // 50
    console.log(m);  // 100
    ```

###  データ型
Javascriptは動的型付言語であり、データ型は「プリミティブ型」と「オブジェクト型」に大別される。  

**・プリミティブ型（基本型）**

1. Boolean 型  
  → 真偽値を扱う。  
  → *真偽値リテラル*（true / false）
2. Number 型  
  → 小数を含む数値を扱う。（最大値は2^53-1）  
  → *数値リテラル*（ex. 18）  
  → *浮動小数点リテラル*（ex. 3.14）
3. BigInt 型  
  → Number型より大きな数値を扱う。（Number型との互換性はなく、扱える環境も少ない）  
  → *数値リテラル*（ex. 100n）
4. String 型  
  → 文字列を扱う。  
  → *文字列リテラル*（ex. 'test' , "hoge"）※どちらでもよいが、文字列に現れない方を使うとよい  
  → *テンプレートリテラル*（ex. \`I am ${name}\`）※式展開ができる
5. Symbol 型  
  → 「シンボル値」という固有の識別子を表現する。（Symbol()関数から生成されて、オブジェクトのプロパティとして使用される）
6. Null 型  
  → 何のデータも存在しないことを明示的に表す。  
  → *nullリテラル*（null）
7. Undefined 型  
  → 宣言のみが行われた変数や、オブジェクト内の存在しないプロパティへのアクセスに割り当てられる。（メモリは確保したが、値は未確定）

**・オブジェクト型（複合型）**
1. 配列リテラル  
    ```javascript
    > const array=[1,2,3]
    > array[1]
    2
    ```
2. オブジェクトリテラル  
    ```javascript
    > const myCar = new Object();
    > myCar.make = 'Ford';
    > myCar.model = 'Mustang';
    > myCar.year = 1969;
    > myCar
    { make: 'Ford', model: 'Mustang', year: 1969 }

    > myCar.model
    'Mustang'
    > myCar['year']
    1969
    ```
3. 正規表現リテラル  
    ※詳細割愛

<br>

## ３．関数／クラス

###  関数の定義
JavaScriptの関数は第一級オブジェクトであり、関数を第一級オブジェクトとして扱うことができる言語の性質を第一級関数ともいう。
* 第一級関数とは  
変数へ代入したり、他の関数の引数として渡したりできる関数のこと。（基本的な操作を制限なしに使用できる）

  ```Javascript
  // 一般的な関数
  function add(n, m) {
    return n + m;
  }
  > add(1,2)  // 3
  
  // 関数（無名関数）を変数に代入
  const sum = function(n, m){
    return n + m;
  }
  > sum(1,2)  // 3
  ```

* アロー関数とは  
より短く記述できる、通常の function 式の代替構文のこと。

  ```Javascript
  // アロー関数
  const sum2 = (n,m) => {
    return n + m;
  }
  > sum2(1,2) // 3

  // アロー関数（本文がreturn文のみの場合は省略できる）
  const sum3 = (n,m) => n + m;
  > sum3(1,2) // 3
  ```

###  関数のさまざまな引数
* デフォルト引数  
デフォルト引数は省略可能で、省略された場合はデフォルト値が適用される。  

  ```javascript
  const raise = (n, m = 2) => n ** m;
  > raise(2,3)  // 8
  > raise(2)  // 4
  ```

* 残余引数（レストパラメータ）  

  ```javascript
  // 残余は配列として受け取る
  const showNames = (a, b, ...rest) =>{
    console.log(a);
    console.log(b);
    console.log(rest);
  }
  > showNames('ta','ka','ha','shi')
  ta
  ka
  [ 'ha', 'shi' ]

  // 可変長引数も実現できる
  const showArgs = (...args) =>{
    console.log(args);
  }
  > showArgs('ta','ka','ha','shi')
  [ 'ta', 'ka', 'ha', 'shi' ]
  ```

###  クラスの定義
* 一般的なクラス

  ```javascript
  class Bird{
    constructor(name){
      this.name = name;
    }

    chirp = () =>{
      console.log(`${this.name}が鳴きました`);
    }
  }
  > const penguin = new Bird('ペンギン');
  > penguin.chirp();  // ペンギンが鳴きました

  class FlyableBird extends Bird{
    constructor(name){
      super(name);
    }

    fly = () =>{
      console.log(`${this.name}が飛びました`);
    }
  }
  > haw.chirp();  // タカが鳴きました
  > haw.fly();  //タカが飛びました
  ```

<br>

## ４．その他構文

###  ラッパーオブジェクト
nullとundefinedを除くプリミティブ型には、それらの値を包括するラッパーオブジェクトが存在する。プリミティブ型の値に対してプロパティアクセスするとき、自動で対応するラッパーオブジェクトに変換される。

```javascript
> const str1='hoge'
> str1.toUpperCase()
'HOGE'
// toUpperCaseメソッドはStringオブジェクトのインスタンスメソッドである
// 内部で以下のように変換されている
> (new String('hoge')).toUpperCase()
```

###  等価／厳密等価
* 等価演算子（==）  
 → 型が異なる場合には型の変換を試みてから比較を行う　　
  1. 数値と文字列を比較する場合、文字列を数値に変換
  2. 1つがBooleanである場合、trueは1に、falseは+0に変換
  3. 1つがオブジェクトで、もう一方が数値または文字列である場合は、プリミティブ型に変換  

* 厳密等価演算子（===）  
 → 二つのオペランドが等しいことを検査する

```javascript
> const str1='hoge'  // string
> const str2=new String('hoge')  // object
> str1
'hoge'
> str2
[String: 'hoge']

// 等価演算子
> str1==str2 // この場合[3]
true

// 厳密等価演算子
> str1===str2
false
> str1===str2.valueOf()
true
```

###  分割代入／スプレッド構文

```javascript
// オブジェクトの基本的な表現方法
> const keyName = 'bar'
> const baz = 123
> const obj1 = { foo: 256, [keyName]: 4096, baz: baz }
> obj1
{ foo: 256, bar: 4096, baz: 123 }

// プロパティ名のショートハンド
// 変数名がプロパティのキー名となり、値がプロパティ値となる
> const obj2 = { baz }
> obj2
{ baz: 123 }

// 分割代入（基本）
// オブジェクトから値を取り出す
> const obj3 = { name: 'Taka', age: 25 }
> const { name, age } = obj3
> name  // 'Taka'
> age  // 25
> typeof name  // 'string'
> typeof age  // 'number'

// 分割代入（応用）
> const response ={
  data: [
    {
      id: 1,
      name: 'Taka',
    },
    {
      id: 2,
      name: 'Nao',
    },
  ],
}

// 通常の分割代入
> const { data } = response;
> data
[ { id: 1, name: 'Taka' }, { id: 2, name: 'Nao' } ]

// キー値をusersに変更し、デフォルト引数（空配列）を与える
> const { data: users = [] } = response;
> users
[ { id: 1, name: 'Taka' }, { id: 2, name: 'Nao' } ]
```

###  繰り返し処理

```javascript
const iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}

// 参考（昔の書き方）
var iterable = [10, 20, 30];

for (var i = 0; i < iterable.length; i++) {
  var value = iterable[i];
  console.log(value);
}
```


###  オブジェクトのマージとコピー

* Object.assign()メソッド
  ```javascript
  // オリジナル
  > const org = { a: 1, b: 2, c: 3 }
  
  // 空配列にオリジナルを追加してcpy1を作成
  > const cpy1 = Object.assign({}, org)
  > cpy1
  { a: 1, b: 2, c: 3 }
  
  // オリジナルにcとdを追加してcpy2を作成
  > const cpy2 = Object.assign(org, { c: 5 }, {d:10})
  > cpy2
  { a: 1, b: 2, c: 5, d: 10 }
  > org
  { a: 1, b: 2, c: 5, d: 10 }  // オリジナルも更新してしまう
  ```

* スプレッド構文  
  シャローコピー（コピーの深さは1段階）なのでプロパティ値が配列やオブジェクトの場合は参照のコピーとなる。  
  ※回避策としてJSON.parse()を使う方法があるが、Dateオブジェクトや関数が入っていた場合はうまく動かない
  ```javascript
  > const org = { a: 1, b: 2, c: 3 }
  
  > const cpy3 = { ...org }
  > cpy3
  { a: 1, b: 2, c: 3 }
  
  > const cpy4 = { ...org, c: 5 }
  > cpy4
  { a: 1, b: 2, c: 5 }
  > org
  { a: 1, b: 2, c: 3 }  // オリジナルは更新されない

  // シャローコピーについて
  > const user = {
    id: 1,
    name: 'Taka',
    address: { town: 'Gunma' },
  }
  > const taka = { ...user }
  > taka.name = 'Nao'
  > taka.address.town = 'Tokyo'

  > taka
  { id: 1, name: 'Nao', address: { town: 'Tokyo' } }
  > user
  { id: 1, name: 'Taka', address: { town: 'Tokyo' } }  // オリジナルも更新してしまう 
  ```

###  プロトタイプ
オブジェクトは直接、他のオブジェクトを継承し、その継承元となったオブジェクトをプロトタイプという。JavaScriptではあらゆるオブジェクトは何らかのプロトタイプを継承していて、その「プロトタイプチェーン」は最終的に空オブジェクトを経てnullに到達する。  
※classは単なるシンタックスシュガー  
※昔はclass表現がなく、プロトタイプをいじくり回してclassを表現していた

```javascript
> [ 1, 2 ].__proto__
[]
> {id: 1, name: 'Taka'}.__proto__
{}
> 'JavaScript'.__proto__
[String: '']
> (123).__proto__
[Number: 0]

```

###  同期／非同期とプロミス
* Promise  
Promiseオブジェクトは非同期処理の最終的な完了処理 (もしくは失敗) およびその結果の値を表現する。  
  * pending: 未解決 (処理が終わるのを待っている状態)
  * resolved: 解決済み (処理が終わり、無事成功した状態)
  * rejected: 拒否 (処理が失敗に終わってしまった状態)

  ```javascript
  // JavaScriptは非同期処理なので、処理を待たない
  console.log('1番目');
  
  setTimeout(() => {
    console.log('2番目(1秒後に実行)');
  }, 1000); 
  
  console.log('3番目');
  // 1番目
  // 3番目
  // 2番目(1秒後に実行)
  
  // プロミスを使って非同期処理を待つ
  console.log('1番目');
  
  new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log('2番目(1秒後に実行)');
      resolve('resolveしたよ');
      reject('rejectしたよ');
    }, 1000);
  })
    .then((val) => {
      console.log(val);
      console.log('3番目');
    })
    .catch((val) => {
      console.log(val);
  });
  // 1番目
  // 2番目(1秒後に実行)
  // resolveしたよ
  // 3番目
  ```

* async / await  
async関数は、非同期関数のことで、結果として暗黙のPromiseを返す。  
await演算子は、async関数によってPromiseが返されるのを待機するために使用する。

  ```javascript
  // API実行の非同期処理の例
  const useApi = url => {
    const [data, setData] = useState([]);
  
    useEffect(() => {
      (async () => {
        const response = await fetch(url);
        const responseJson = await response.json();
        if (response.ok) {
          setData(responseJson);
        }
      })();
    }, [url]);
  
    return data;
  };
  ```

<br>

## ５．Node.js

###  概要
サーバサイドのJavaScriptのこと。
これまでブラウザ上で動かしていたものを、サーバサイドで動かせるようにしたプラットフォーム。

###  npm／yarn
* npm（Node Package Manager）  
Node.jsのモジュール管理ツール。
フロントエンドで使用するJavascriptのパッケージのインストールとバージョン管理に使う。

* yarn  
Facebook製のnpm改良版コマンドで、npmより高速でタイピング数が少なく使い勝手がよい。
またyarn.lockが作成されて、誰でも同じバージョンの依存をインストールできるように各依存のバージョンを管理できる。

* インストール
  ```cmd
  rem ローカルインストール（--saveはデフォルトで有効）
  > npm install --save { package }
  > yarn add { package }

  rem ローカルインストール（開発環境のみ適用）
  > npm install --save-dev { package }
  > yarn add --dev { package }

  rem グローバルインストール
  > npm install -g { package }
  > yarn global add { package }

  rem package.json記載のパッケージをインストール
  > npm install
  > yarn install
  > yarn
  ```

* アンインストール
  ```cmd
  rem ローカルアンインストール
  > npm uninstall --save { package }
  > yarn remove { package }

  rem ローカルアンインストール（開発環境のみ適用）
  > npm uninstall --save-dev { package }
  > yarn remove { package }

  rem グローバルアンインストール
  > npm uninstall -g { package }
  > yarn global remove { package }
  ```

* node_modulesの場所
  ```cmd
  > npm root -g
  > npm root
  ```

* 設定
  ```cmd
  rem 一覧
  > npm config list
  > yarn config list

  rem プロキシ設定
  > npm -g config set proxy http:// user:pass@proxy-host:8080
  > npm -g config set https-proxy http:// user:pass@proxy-host:8080
  > yarn config set proxy http:// user:pass@proxy-host:8080 -g
  > yarn config set https-proxy http:// user:pass@proxy-host:8080 -g

  rem 企業ネットワークで必要の場合あり
  > npm -g config set registry http://registry.npmjs.org/
  > npm -g config set strict-ssl=false
  ```

* 一回限りの実行
  ```cmd
  rem グローバルインストールをしないで実行する
  > npx create-react-app hello-world
  ```

###  package.jsonの記載方法

* バージョンの見方  
**1.2.3**  
 1 -> Major Release：仕様そのものの変更。upgradeする場合はアプリケーションの改修が必要になる可能性がある。  
 2 -> Minor Release：仕様を維持した状態での機能追加。upgradeしてもアプリケーションは壊れない。  
 3 -> Patch Release：バグ修正。upgradeしてもアプリケーションは壊れない。  
**^1.1.2 = 1.x**  
 最新のマイナーバージョンをインストールする  
**~1.1.2 = 1.1.x**  
 最新のマイナーバージョンをインストールする

* package.jsonの例（create-react-appの場合）
  ```json
  {
    "name": "hello_world",
    "version": "0.1.0",
    "private": true,
    "dependencies": {
      "@testing-library/jest-dom": "^5.11.4",
      "@testing-library/react": "^11.1.0",
      "@testing-library/user-event": "^12.1.10",
      "react": "^17.0.2",
      "react-dom": "^17.0.2",
      "react-scripts": "4.0.3",
      "web-vitals": "^1.0.1"
    },
    "scripts": {
      "start": "react-scripts start",
      "build": "react-scripts build",
      "test": "react-scripts test",
      "eject": "react-scripts eject"
    },
    "eslintConfig": {
      "extends": [
        "react-app",
        "react-app/jest"
      ]
    },
    "browserslist": {
      "production": [
        ">0.2%",
        "not dead",
        "not op_mini all"
      ],
      "development": [
        "last 1 chrome version",
        "last 1 firefox version",
        "last 1 safari version"
      ]
    }
  }
  ```

<br>

## ６．React

### Reactの歴史
  - Google マップショック  
  従来のサーバーサイドの地図サービス（静的リンクで読み込み待ちがストレスフルなもの）に対して、2005年にGoogle がインタラクティブな地図サービスを提供。非同期通信を行いながら、動的にページを更新するAjax (Asynchronous JavaScript And XML) とよばれる技術が使われた。
  - フロントエンド第一世代  
  Google マップをきっかけに、Ajax を用いて高度なフロントエンドアプリケーションを作ろうという機運が高まっていた。Ajax フレームワークを始めとし、JavaScript アプリケーション開発のためのさまざまな機能を提供するprototype.js (Prototype JavaScript Framework)や、DOM操作にブラウザ依存をなくしたjQuery などがある。一方このようなフロントエンドの動向に呼応して、2008年にFlash などのプラグインに置き換わるHTML5 が発表される。またGoogle がChrome のJavaScript エンジンであるV8 をオープンソース化し、実行環境であるNode.js がリリースされる。さらに1999年の3rd Edition から更新されていなかったECMAScript （⇒JavaScript の仕様のこと）が10年の歳月を経て2009年にECMAScript 5th Edition(ES5) が発表された。
  - フロントエンド第二世代  
  2010年後半にMVC デザインを適用したフレームワークが登場する。Backbone.js は、従来のjQuery によるDOM 操作をベースとしたアプリケーションにModel とView の秩序を与えるための最低限の実装に、REStful API とルーティングの機能を加えたものだった。Knockout は、HTML テンプレートとそれに対する単方向および双方向のデータバインディング機能を持っていて、このMVVM（Model- View - View Model）のパターンは、後のVue.js にも影響を与えてる。AngularJS は、双方向データバインディングを前提としたカスタムタグ属性によるHTML テンプレートに加え、ルーティング機能や独自のモジュールシステムなどを備えた、フルスタックのフレームワークだった。さらにGoogle が提供していることのブランド力と安心感もあいまって、2012年ごろにはもっとも人気の高いフロントエンドフレームワークの座を獲得してた。
- React の誕生  
  2011年Google のエンジニアから「HTML をプログラマブルに拡張し、開発者が自ら作成したカスタムタグを読み込んで使えるようにする**Web Components** という技術をWeb 標準の仕様として広くブラウザに実装しよう」という内容の提唱があった。これは従来用いられていたような、ひとつの長大なHTML と全体に適用されるこれまた長大なCSS を、これらの技術を用いることでカプセル化された**再利用可能なコンポーネント**に分割し、それらの組み合わせでWeb コンテンツを表現するしくみを作ろうというGoogle からの夢の提案だった。Web Components の理想自体は多くの人が共感するものだったが、実装に時間がかかる中でFacebook によるReact が誕生する。もともと社内のMVCフレームワークを改善し、FaxJS（後にReact に改名されるプロトタイプ零号機のようなもの）を作成。さらにXHP（PHP のコード内でXML リテラルを記述してUI を作成するフレームワーク）をJavaScript に移植したjs-xml-literal というプロダクトをフォークしてJSX 作り、React をオープンソース化するための下準備となった。2012年にInstagram を買収し現在のロゴが作成され、2013年にバージョン0.3.0でオープンソース化した。

### Reactの特徴
- Declarative（宣言的なView）  
  最終的な出力を得るために、時系列に沿って直前の状態に依存しながら命令を順番に記述していく「**命令型プログラミング**」に対して、出力の性質やあるべき状態を記述する「**宣言型プログラミング**」がある。従来の命令型DOM 操作に対して、React は各状態に対応するシンプルなView を設計するだけでデータの変更を検知し、関連するコンポーネントだけを効率的に更新、描画できる。
- Component-Based（コンポーネントベース）  
  見た目と機能がカプセル化されたコンポーネントというアプリケーションの部品を作成し、それらを組み合わせることで複雑なUI を構築するという設計思想のこと。従来のフロントエンドフレームワークのほとんどが採用していたようなMV＊ のデザインパターンは存在せず、むしろ当初は説明のために『MVC のV だけ』という言い方もしていた。
- Learn Once, Write Anywhere（一度学習すればこでも使える）  
  Reactは当初よりレンダラーを本体から分離する設計となっていて、レンダラーを入れ替えることで様々なプラットフォームのアプリケーションを表現できる。各種レンダラーは以下の通り。  
  ※ちなみに、Javaのキャッチフレーズの「Write once, run anywhere」をもじったものらしい

    - **React DOM** ： HTML DOM （公式標準パッケージ）
    - **React Native** ： iOS やAndroid のネイティブアプリケーション
    - React 360 ： ブラウザ上で動くVR アプリケーション
    - React Native for Windows + macOS ： Windows  / macOS のネイティブアプリ
    - React-pdf ： PDF ドキュメント

### 他のフレームワークとの比較
- Angula  
    React が公開された翌年にAngularJS チームがこれまでと互換性のない新しいフレームワーク作成を発表した。React は進化が速いため、プロダクトの性質や将来性を考慮して適切なライブラリを選定する必要があるのに対して、Angular はフルスタックなフレームワークで、ファーストリリースから基本的な枠組みが変わってないので安定している。
- Vue.js  
    Angular の下位互換性を捨てたアップグレードに対して不満をかかえたコミュニティベースで開発された。React と同じくらい人気のあるフレームワークであるが、開発者が中国人という組織的な色合いが強いとの見方もある。AngularJS の直感性を残しつつ、Reactのコンポーネントベースを取り入れた『いいとこ取り』のフレームワークだが、結局はMVVM デザインパターンのオールドタイプの技術であると言える。


### create-react-appによるひな型作成

```cmd
> npx create-react-app sample
npx: installed 67 in 11.19s

Creating a new React app in C:\Users\naoki\Documents\sample.

rem ...省略...

Success! Created sample at C:\Users\naoki\Documents\sample

rem ...省略...

We suggest that you begin by typing:

  cd sample
  yarn start

Happy hacking!

> cd sample
> tree /F

rem 重要な箇所のみ抜粋
sample
│  package.json
│  yarn.lock
│  
├─node_modules
│  │  
│  ├─ react
│  ├─ react-dom
│  └─ react-scripts
│  
├─public
│  └─ index.html
│      
└─src
   ├─ App.js
   ├─ App.css
   ├─ index.js
   └─ index.css
```

public/index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>  <!-- アプリ名 -->
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>  <!-- rootの空divがある -->
  </body>
</html>
```

src/index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

// APPコンポーネントをDOMに描画しなおして、root要素に上書きする
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

reportWebVitals();
```

src/App.js

```javascript
import logo from './logo.svg';
import './App.css';

// 実際にCRAで表示される内容は以下となる
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

### Virtual DOM（仮想DOM）
※DOMとは  
「Document Object Model」の略。  
JavaScriptがHTMLの要素を操作する際、このDOMを通して画面上の要素をJavaScriptのオブジェクトとして扱っている。  

JavaScriptのDOM操作はレンダリングの負荷が高くなるので、ReactではまずVirtual DOM(仮想DOM)というReactが管理するDOMを操作し、差分がある箇所だけをHTMLのDOMでレンダリングするので効率的である。



### Reactの仕組み
Reactは仮想DOMをリアルなDOMにレンダリングすることでWebアプリケーションとして動作する。その仮想DOMを構成するのがReact Elements。React Elementsはコンポーネントを任意のpropsでコールするための実行リンクのようなもの。また、コンポーネントが持つ状態のことをstateという。

JSX
HTML to JSX

### 関数型コンポーネント

### クラス型コンポーネント

### その他


コンポーネントライフサイクル
React 応用
React Hook
FluxとRedux
ユニットテスト方法

<br>

## ７．Web技術トレンド

###  CSR(Client Side Rendering)
ブラウザからリクエストされると、サーバーはJS のビルドされたファイルと必要最小限のHTML要素しか含まれないHTMLファイルを返却する。HTMLファイルの中身はほぼないので、初期表示は何も表示されない。それから、ブラウザ上でAPIなどを使い、初期データを取得して、HTML 要素をレンダリングする。  
* メリット  
  * ユーザーに優れた UX 提供が可能（ページ遷移ごとにリクエストしないため、）ページ遷移が高速  
  * ネイティブアプリの代わりとして提供可能  
  * HTMLとJSファイルのみがホスティングサーバーにあれば、ページ配信が可能
* デメリット  
  * 初期ローディングにかかる時間が増える  
  * SEO(Search Engine Optimization:検索エンジン最適化)で不利な場合がある　※最近は改善されいている  
  * 動的なOGP(Open Graph Protocol:オープン・グラフ・プロトコル)対応ができない場合がある  
  ※オープン・グラフ・プロトコルとは、Facebook、TwitterなどのSNS上でシェアされた時やシェアされたい時に、ページのタイトル、URL、概要、画像（サムネイル）を正しく伝えるためにHTMLソースに記述するタグ情報です。

###  SPA(Single Page Application)
CSRと同じ意味

###  SSR(Server Side Rendering)
SPAと対比して、ブラウザ上で初期データをレンダリングするのではなく、サーバー側でデータ取得、レンダリングまでを行い、HTMLファイルを配信する。
ただし、初期データ以外のデータはAPIなどを用いて取得を行い、SPA同様に、ブラウザ上でレンダリングを行う。

* メリット  
  * コンテンツ表示までの時間を短縮できる（ブラウザ上でレンダリングしないので）  
  * （SPAと比較して）SEOが向上する、動的なOGP対応が可能
* デメリット
  * SSRするためのWebサーバーが必要になる

※以下のフレームワークで実現可能  
Nuxt.js、Next.js


###  SSG(Static Site Generator)
アプリケーションのビルド時に、APIなどからデータを取得し、HTMLを最初に生成しておく。サーバーへのリクエストがあった場合には、この生成されたHTMLファイルを返却する。
このように、ブラウザではなく、サーバーで先にビルド時にデータを取得してレンダリングを行っておくことを「プリレンダリング」という。また、生成された各 HTML はそのページに必要な最小限の JavaScript コードと関連づけられる。  
ブラウザによってページが読み込まれると、そのページの JavaScript コードが実行される。（このプロセスは ハイドレーション と呼ばれる。）  
一番の特徴は、アプリケーションをビルドした際に、データベースなどからデータを取得することである。そのため、利用されるアプリケーションとしては、更新頻度の少ないサイト（例えば、ヘルプページ）やブログなどが挙げられる。

* メリット  
  * 静的サイトを配信するので、レスポンスが高速
  * （SPAと比較して）SEOが向上する、動的なOGP対応が可能
  * HTMLとJSファイルのみがホスティングサーバーにあれば、ページ配信が可能
* デメリット
  * ページ量が多いWebサイトには向かない
  * ページ数が多くなればなるほど、ビルド時間が遅くなる
  * 頻繁にデータ更新があるサイトには向かない（データ更新の度に、再ビルドが必要。）
  * APIを頻繁にリクエストするサイトには向かない

※以下のフレームワークで実現可能
Nuxt.js、Next.js、Gatsby.jsなど

<br>
