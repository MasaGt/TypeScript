### ES Module とは

- JavaScript のモジュールシステムの1つ

<br>

- 他のプログラムファイルを読み込みには `import`、 他のプログラムファイルから利用可能にするには `export` を使う

<br>

- ★ECMA Scrtip に則って書かれたファイルが ES Module になるわけではなく、ファイルの拡張子が .mjs だったり、package.json の type や \<script\> タグの type 属性などで指定されて初めて ES Module として扱われる (=実行される)

    - ファイル拡張子が .mjs のファイルは Node.js での実行時に ES Module として実行される

    <br>
    

    - package.json の type に "module" が指定されている場合、ファイル拡張子が .js のファイルは Node.js での実行時にデフォルトで ES Module として実行される

    <br>

    - \<script\> タグの type 属性に module が指定されている場合、そのコードは Node.js での実行時に ES Module として実行される

        ```html
        <script type="module">
            const res = await fetch("...");
            const data = await res.json();
            console.log(data);
        </script>
        ```

<br>

- ファイル内で宣言する変数や関数はそのファイルのスコープに限定される = モジュールスコープ

<br>

- グローバルな変数や関数を宣言したい場合は、window オブジェクトにプロパティとして追加する (ブラウザ上で実行する時のみ)

    ```ts
    // module.ts
    const val1 = "hello";
    let val2 = "world";
    window.val3 = "!!!!!"
    ```

    ```ts
    // other.ts

    console.log(val1);
    //undefined

    console.log(val2);
    //undefined

    console.log(val3);
    //!!!!!
    ```

<br>
<br>

参考サイト

[【js】ESModules使用してみたメモ](https://qiita.com/__knm__/items/c08e9b20df9fbfe9f889)

[【JavaScript】グローバルスコープ/モジュールスコープの違い](https://qiita.com/daiki99s/items/6764b4c4b7c1226d16ca)

---

### Common JS とは

- JavaScript のモジュールシステムの1つ

<br>

- 他のプログラムファイルを読み込みには `require`、 他のプログラムファイルから利用可能にするには `module.expors` を使う

<br>

- トップレベルで (修飾子なし or var) 宣言された変数はグローバル変数になる

    - トップレベルで宣言されていても、const や let で宣言された変数はローカルスコープになる

---

### Node.js のモジュールシステム

- Node.js はバージョン14から ECMA Script と Common JS の両方のモジュールシステムを利用できるようになった (それまでは Common JS のみ)

<br>

- package.json の type フィールドに `module` か `commonjs` を指定することができ、**.jsファイルをどちらのモジュールシステムを利用したものとして扱うか**を指定できる

    - ★デフォルトは `commonjs` = .js ファイルを Common JS のモジュールシステムを利用したファイルとして扱う

<br>

- **package.json に type フィールドを指定していない場合**、デフォルトでは .js ファイルは CommonJS のモジュールを利用したファイルとして認識するが、**まずCommonJSとして実行し、途中で ES modulesの記法を検知したら ES modules に fallback して実行する**

    <img src="./img/ESModuleとCommonJS/package-json-type-none_1.svg" />

<br>

- 一方、pakcage.json に `type: commonjs` と明示的に指定されている場合、実行ファイルの途中で ES modules の記法を検知するとエラーになる

    <img src="./img/ESModuleとCommonJS/package-json-type-commonjs_1.svg" />

<br>
<br>

参考サイト

[package.jsonにtype: moduleを指定して、CommonJSへの依存を減らしました](https://developers.prtimes.jp/2025/05/26/package-json-type-module/#index_id4)

---

### モジュールシステムとは

- プログラムを部品化する仕組み

<br>

- ★「どうやってどうやって他のプログラムファイルを読み込むか」のルール

<br>
<br>

参考サイト

[【js】ESModules使用してみたメモ](https://qiita.com/__knm__/items/c08e9b20df9fbfe9f889)

---

### ECMA Script と ES Module、 Common JS

<img src="./img/ESModuleとCommonJS/ESModule-CommonJS-Venn-Diagram_1.svg" />

<br>

- #### ECMA Script

    - JavaScript 言語の全体の仕様（文法や機能すべて）

        - = JavaScript の基本文法

<br>

- #### ES Module

    - ECMAScript の仕様の中のモジュール（import/export）に関する機能部分

    <br>
    
    - ES Modules (import/export) は ECMAScript 2015 (ES6) から仕様として取り入れられた

<br>

- #### Common JS

    - 「JavaScript のモジュールシステムの一つ」で、言語仕様ではなく 実装の規約・仕様（モジュールの仕組み）

        - そのため、CommonJS ファイルでも、const や let などの ECMA Script の新しい文法や機能を利用することができる
    