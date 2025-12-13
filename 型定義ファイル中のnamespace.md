### 型定義ファイルで見かける namespace キーワード

- グローバルスコープ中に任意の名前空間を作ることのできるキーワード

    - 基本的に declare キーワードと一緒に使われる

    - namespace に属するデータ型は export キーワードで外部に公開する

        - ★ファイルのトップレベルで import/export が使われていなければその型ファイルはスクリプトと認識される

    - 利用する側は `<namespaceで指定された名前空間>.<その名前空間に属しているデータ型>` で参照する

    <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_1.svg" />

<br>

- ★namespace キーワード自体は普通の ts ファイルでも使うことができるが、型定義ファイルのみで使うのがベター

<br>

- TypeScript v1.5 以前は `declare module` が名前空間の確保に使われていたが、v1.5 以降は代わりに `decalre namespace` が推奨されている

<br>
<br>

参考サイト

[令和5年に知っているべきTypeScriptのnamespaceの知識](https://zenn.dev/uhyo/articles/ts-namespace-2023)

[サバイバルTypeScript - namespace](https://typescriptbook.jp/reference/declaration-file#namespace)

[TypeScriptの名前空間とモジュールの違いと使い方](https://kazu-oji.com/jsts_typescript_namespace/)

---

### 普通の ts ファイル中で使われる namespace

- 型定義する機能を持つキーワード

    - interface や type みたいなもの

        <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_2.svg" />

<br>

- interface, type と何が違うのか

    - 同じ = なんも違わない = 型を定義するためのキーワード

        - ★ts → cjs にコンパイルされるとコードが残る

            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_3.svg" />

            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_4.svg" />

            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_5.svg" />

        <br>

        - ts → esm にコンパイルされるとコードは消える
            
            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_6.svg" />

            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_7.svg" />

            <img src="./img/型定義ファイル中のnamespace/type-definition-namespace_8.svg" />