### rewriteRelativeImportExtensions とは

- TypeScript 5.7 から導入された機能

- ★ts ファイル中の import 文の中の .ts (.mts, .cts. tsx) 拡張子を、**tsc コンパイル時に対応する .js (.mjs, .cjs, .jsx) 拡張子に変換する機能**

    <img src="./img/tsconfig_rewriteRelativeImportExtensions/tsconfig-rewriteRelativeImportExtensions_1.svg" />

    <br>

- ★★ただし、.ts 拡張子の書き換え対象となる import 文は**相対パスで指定されたものである必要がある**

    ```js
    // Under --rewriteRelativeImportExtensions...

    // these will be rewritten.
    import * as foo from "./foo.ts";
    import * as bar from "../someFolder/bar.mts";

    // these will NOT be rewritten in any way.
    import * as a from "./foo";
    import * as b from "some-package/file.ts";
    import * as c from "@some-scope/some-package/file.ts";
    import * as d from "#/file.ts";
    import * as e from "./file.js";
    ```

    引用: [Announcing TypeScript 5.7](https://devblogs.microsoft.com/typescript/announcing-typescript-5-7/) 

<br>
<br>

参考サイト

[TS 5.7の --rewriteRelativeImportExtensions オプションを使う前に読む記事](https://zenn.dev/uhyo/articles/rewrite-relative-import-extensions-read-before-use)

[「TypeScriptが当たり前」になった世界において、ESモジュール本来の運用に必要な考え方と設定とは](https://findy-code.io/media/articles/gfx-esm)

---

### allowImportingTsExtensions との併用

- allowImportingTsExtensions と rewriteRelativeImportExtensions の両方を有効にすることで、.ts (.mts, .cts, .tsx) 拡張子をimportの対象として相対パスの中にそのまま書くことができ、tsc コンパイル時には対応した .js (.mjs, .cjs, jsx) に変換させることが可能になる

    → [今までの .ts ファイルを対象とした import の書き方](./tsconfig_moduleResolution.md#疑問1)ではなく、直感的に .ts を対象とした import を書けるようになった


    <img src="./img/tsconfig_moudleとmoduleResolution/TypeScript-Import-File-Extensions_3.svg" />

<br>

- ★rewriteRelativeImportExtensions を有効 (true) にすると、allowImportingTsExtensions も暗黙的かつ自動的に true になる

<br>
<br>

参考サイト

[Compiler Options Allow Importing TS Extensions - allowImportingTsExtension](https://www.typescriptlang.org/tsconfig/#allowImportingTsExtensions)