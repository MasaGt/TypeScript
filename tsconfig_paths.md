### tsconfig.json の paths フィールド

- ★任意のパスにエイリアスを設定することができる項目

    <img src="./img/tsconfig_paths/tsconfig-paths_1.svg" />

<br>

- TypeScript 4.1 以前は paths フィールドを設定するには baseUrl フィールドの設定も必要だった

    - 2025/12/15 現在 (TypeScript 5.9) では paths だけでの指定も可能になった

        <img src="./img/tsconfig_paths/tsconfig-paths_2.svg" />

<br>

- ★★[baseUrl](./tsconfig_baseUrl.md) が設定されている場合、そこを**基準**として対象パスをエイリアスにマッピングされる

    <img src="./img/tsconfig_paths/tsconfig-paths_3.svg" />

<br>

- ★★★[baseUrl](./tsconfig_baseUrl.md#tsconfigjson-の-baseurl-フィールド) と同様に、paths エイリアスはコンパイルされる時は書き換えられずそのまま出力されることに注意

    <img src="./img/tsconfig_paths/tsconfig-paths_4.svg" />

    <br>

    - 他のモジュールバンドラーやビルドツール、もしくはパッケージ (ツール) をインストールして解決する必要がある (詳しくは[こちら](#path-で指定したエイリアスの書き換え))


<br>
<br>

参考サイト

[tsconfig.json の paths](https://zenn.dev/hayato94087/articles/9f3bf702543431)

[TypeScript の paths はパスを解決してくれないので注意すべし！](https://www.agent-grow.com/self20percent/2019/03/11/typescript-paths-work-careful/)

[TypeScript 4.1からはbaseUrlは指定不要](https://minerva.mamansoft.net/Notes/TypeScript+4.1からはbaseUrlは指定不要)

---

### path で指定したエイリアスの解決

#### Vite の場合

- #### Vite プラグイン (vite-tsconfig-paths) を使う方法

    - `vite-tsconfig-paths` をインストール

        ```bash
        npm install -D vite-tsconfig-paths
        ```

    <br>

    - vite.config.js の plugins フィールドに vite-tsconfig-paths を使用するよう設定

        ```js
        //vite.config.js
        import { defineConfig } from 'vite';
        import tsconfigPath from "vite-tsconfig-paths";

        export default defineConfig({
            plugins: [
                tsconfigPath()
            ]
        });
        ```

<br>

- #### vite.config.js でエイリアスを設定する方法

    - vite.config.js の [resolve.alias](https://ja.vite.dev/config/shared-options#resolve-alias) に tsconfig で設定したエイリアスとそのマッピング対象となるパスを設定する

    <br>

    - ★reslve.alias で指定するマッピング対象となるディレクトリは絶対パスで指定する必要があるらしい (by 公式)

        <img src="./img/tsconfig_paths/tsconfig-paths_5.svg" />

<br>

#### Next.js の場合

- (Next.js 9.4 以降であれば) 特に next.config.js を修正する必要は無く、Next.js が tsconfig.json のbaseUrl, paths を見て自動で解決してくれるとのこと

<br>

#### パッケージを利用する場合 (Node.js + TypeScript の超シンプルな構成の場合など)

- [`tsc-alias`](https://www.npmjs.com/package/tsc-alias?activeTab=readme、[`tsconfig-paths`](https://www.npmjs.com/package/tsconfig-paths)、[`typescript-transform-paths`](https://www.npmjs.com/package/typescript-transform-paths) などさまざまなパッケージが存在する

<br>

- 今回は `tsc-alias` を紹介する

    - `tsc-alias` のインストール

        ```bash
        npm install -D tsc-alias
        ```

    <br>

    - package.json に 以下のコマンドを追加
        ```json
        {
            "scripts": {
              "build": "tsc && tsc-alias",
            }
        }
        ```

<br>
<br>

参考サイト

[Next.jsでエイリアスpathを使用する](https://qiita.com/yukiji/items/b29e497aca45e7dc878e)

[【Vite】Viteの便利機能alias（エイリアス）を使用してpath（パス）を設定する方法](https://mitsutano-oshiro.com/archives/2681#alias_paths)

[vite-tsconfig-pathsを使ったエイリアス設定方法](https://qiita.com/kenogi/items/74d7f87e5dc18a926441)

[Vite - resolve.alias](https://ja.vite.dev/config/shared-options#resolve-alias)

[typescript-transform-paths](https://www.npmjs.com/package/typescript-transform-paths)

[tsc で transpile 時に paths alias を相対 path に変換したい](https://zenn.dev/nbstsh/scraps/c0cef5a90c5329)

[TypeScript で paths を解決してビルドする](https://tech.natsuneko.blog/entry/2020/03/29/typescript-resolve-paths)