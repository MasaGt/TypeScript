### tsconfig.json と tsconfig.app.json と tsconfig.node.json

- Vite プロジェクト (TypeScript) を作成すると、tsconfig.json だけではなく tsconfig.app.json と tsconfig.node.json というファイルも作成されていた

    <img src="./img/いろんなtsconfig/Vite-Multi-tsconfigs_1.svg" width="50%" />

<br>

- #### tsconfig.json

    - tsconfig.app.json と tsconfig.node.json を参照してるだけ

        ```json
        {
            "files": [],
            "references": [ //ここ
                { "path": "./tsconfig.app.json" },
                { "path": "./tsconfig.node.json" }
            ]
        }
        ```

    <br>

    - ★これは TypeScript の[プロジェクト参照 (project references)](#project-references) っぽいが、参照先の tsconfig.app.json, tsconfig.node.json の中身を見るとちょっと違うことがわかる

        - tsconfig.json で references を使っているが、**参照先のtsconfig.~~.json では composite を有効にしていない** のでプロジェクト参照の機能は利用できない

            <img src="./img/いろんなtsconfig/Vite-Multi-tsconfigs_2.svg" />

        <br>

        - ★★ではなぜプロジェクト参照っぽく tsconfig.json を分けているのかというと、IDE 上でそれぞれのファイル対して別の tsconfig で設定した型チェックを効かせたいから

            <img src="./img/いろんなtsconfig/Vite-Multi-tsconfigs_3.svg" />

<br>

- #### tsconfig.app.json

    ```json
    //tsconfig.app.json
    {
        "compilerOptions": {
            "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo",
            "target": "ES2022",
            "useDefineForClassFields": true,
            "lib": ["ES2022", "DOM", "DOM.Iterable"], //ポイント2
            "module": "ESNext",
            "types": ["vite/client"], //ポイント3
            "skipLibCheck": true,

            /* Bundler mode */
            "moduleResolution": "bundler",
            "allowImportingTsExtensions": true,
            "verbatimModuleSyntax": true,
            "moduleDetection": "force",
            "noEmit": true,
            "jsx": "react-jsx",

            /* Linting */
            "strict": true,
            "noUnusedLocals": true,
            "noUnusedParameters": true,
            "erasableSyntaxOnly": true,
            "noFallthroughCasesInSwitch": true,
            "noUncheckedSideEffectImports": true
        },
        "include": ["src"] //ポイント1
    }
    ```

    <br>

    - (`include` フィールドより) src 配下を対象にしたコンパイル設定であることがわかる

    <br>

    - (`lib` フィールドより) DOM API (window や document など) の型チェックを有効にしていることがわかる

    <br>

    - (`types` フィールドより) `vite/client` の型定義ファイルを暗黙的に読み込むことがわかる

        - → src 配下のファイルで `import.meta.env` や `import.meta.glob` の型情報が IDE 上で参照できるようになる

        - なぜ `vite/client` という指定になっているかは[こちら](./tsconfig_typeRoots_types.md#疑問)を参照

    <br>

    - ★プロジェクト参照っぽかったが、`composite` フィールドが有効になっていなので、**プロジェクト参照ではない** = tsc コンパイルでプロジェクト参照の機能が使えない

        - そもそも Vite は tsc でのビルドは行わないので、プロジェクト参照を使う意味がない
        
        - ★★上記 [tsconfig.json](#tsconfigjson) の説明でも書いたが、src 配下のファイルでは tsconfig.app.json の設定で型チェック (import.meta.env など) を効かせたいからわざわざ tsconfig.app.json を作成しているっぽい

<br>

- #### tsconfig.node.json

    ```json
    //tsconfig.node.json
    {
        "compilerOptions": {
            "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.node.tsbuildinfo",
            "target": "ES2023",
            "lib": ["ES2023"], //ポイント2
            "module": "ESNext",
            "types": ["node"], //ポイント3
            "skipLibCheck": true,

            /* Bundler mode */
            "moduleResolution": "bundler",
            "allowImportingTsExtensions": true,
            "verbatimModuleSyntax": true,
            "moduleDetection": "force",
            "noEmit": true,

            /* Linting */
            "strict": true,
            "noUnusedLocals": true,
            "noUnusedParameters": true,
            "erasableSyntaxOnly": true,
            "noFallthroughCasesInSwitch": true,
            "noUncheckedSideEffectImports": true
        },
        "include": ["vite.config.ts"] //ポイント1
    }
    ```

    <br>

     - (`include` フィールドより) vite.config.ts を対象にしたコンパイル設定であることがわかる

    <br>

    - (`lib` フィールドより) ES2023 バージョンの JavaScript のビルトインオブジェクトの型チェック**のみ**を有効にしていることがわかる

        - DOM (window, object など) の型チェックは無効

    <br>

    - (`types` フィールドより) `node` の型定義ファイルを暗黙的に読み込むことがわかる

        - → vite.config.js で `process`, `__dirname`, `__filename` など Node.js 特有の型情報が IDE 上で参照できるようになる

    <br>

    - こちらの tsconfig.node.json は vite.config.js 用の tsconfig ファイル

<br>
<br>

参考サイト

[tsconfig.jsonの最近の新機能　ファイルパス編](https://speakerdeck.com/uhyo/tsconfig-dot-jsonnozui-jin-noxin-ji-neng-huairupasubian)

[プロジェクト参照 (project references)](https://typescriptbook.jp/reference/advanced-topics/project-references)

---

### Project References

- ★1つの TypeScript プロジェクトに複数のサブプロジェクを持つような場合にプロジェクト参照が役立つ

    <img src="./img/いろんなtsconfig/typescript-project-references_1.svg" />

<br>

- ★サブプロジェクトを持たない1つのプロジェクトであれば基本的にはプロジェクト参照を使う必要は無い

    <img src="./img/いろんなtsconfig/typescript-project-references_2.svg" />

<br>

#### ポイント

- ビルドの依存関係を管理できる

    <img src="./img/いろんなtsconfig/typescript-project-references_3.svg" />


<br>

- それぞれの tsconfig に特定の範囲のコンパイル設定を担わせることが可能

    <img src="./img/いろんなtsconfig/typescript-project-references_4.svg" />

<br>

- 2回目以降のコンパイルは、前回のコンパイルからの差分が発生したもののみを対象とするため、コンパイル時間の短縮が期待できる

    <img src="./img/いろんなtsconfig/typescript-project-references_5.svg" />

<br>

- ★references フィールドの要素である `{ "path": "~~" }` の \~\~ には**参照したいプロジェクトへのパス (その中のtsconfig.json が参照される)** or **参照したいプロジェクトのtsconfigファイルへのパス** を指定する

    - 参照するだけの tsconfig には `"include": []` のように、コンパイル対象を明示に空にする必要がある

        ```json
        // プロジェクトルート直下のtsconfig.json
        // ./src を参照する
        // ./core を参照する (そのプロジェクトのtsconfigのファイル名がtsconfig.core.json)
        {
            "references": [
                { "path": "./scripts" }
                { "path": "./core/tsconfig.core.json" }
            ],
            "include": []
        }
        ```

<br>

- ★参照されるプロジェクトの tsconfig では `"composite": true` を指定しないとうまく Project References が機能しないので注意すること

<br>

- ★Project References を利用したビルド (各 tsconfig に従ったコンパイルや増分コンパイルなど) をしたい場合は `tsc --build` でコンパイル&ビルドを実行する必要がある

    - 普通の `tsc` ではダメ

    - `tsc --build` のビルド結果を全て削除したい場合は `tsc --build --clean` で実行することができる

<br>

参考サイト

[サバイバルTypeScript - プロジェクト参照 (project references)](https://typescriptbook.jp/reference/advanced-topics/project-references)

[TypeScriptのプロジェクトリファレンス(Project References)について](https://zenn.dev/suin/scraps/6dca9d5514f3cf)

[TypeScriptで外部プロジェクトの参照設定とエイリアスをつける方法](https://www.aruse.net/entry/2022/10/25/001104)