### 事象

- 以下の tsconfig.json を作成した

    ```json
    //tsconfig.json
    {
        "compilerOptions": {
            "target": "esnext",
            "moduleResolution": "node",
            "noEmit": true
        }
    }
    ```

<br>

- tsc コマンドで ts ファイルをコンパイルしたが、tsconfig.json の設定が反映されていなかった

    ```bash
    npx tsc src/foo.ts
    ```

    <img src="../img/Issues/Issue-tsconfig-ignored_1.svg" width="50%"/>


---

### 原因

- ファイルを指定しての tsc コマンドでのコンパイルは tsconfig.json を無視する

    - ★tsc コマンドの -p オプションで利用したい tsconfig.json のディレクトリを指定できる**が、任意のファイルを指定 + -p オプションの利用はできない**

        <img src="../img/Issues/Issue-tsc-witgh-p_1.svg" />

        *-pオプション: コンパイル時に利用したい tsconfig.json のディレクトリを指定すことができるオプション
<br>
<br>

参考サイト

[【TypeScript】tscでtsconfig.jsonが無視される問題](https://qiita.com/matoruru/items/b89abd4ddaaa4ec453ea)

[js STUIDO - tsconfig.json](https://js.studio-kingdom.com/typescript/project_configuration/tsconfig_json)

[【TypeScript】tsconfig.jsonで出力先を設定したのに反映されないあなたへ](https://qiita.com/RyosukeSomeya/items/3ef53eb42b890f419472)

[TypeScript Ninja - 第5章　オプションを知り己のコードを知れば百戦危うからず](http://typescript.ninja/typescript-in-definitelyland/tsc-options.html#project)

---

### 解決策

- tsc コマンドで任意のファイルを指定したい場合

    - tsconfig.json で設定している項目全てを tsc コマンドのオプションとして実行する

    - この場合、tsconfig.json の設定は無視されるので、tsc コマンドのオプションを何か1つでもつけ忘れると、意図したコンパイル結果にならないことがあるので注意

        ```json
        //tsconfig.json
        {
            "compilerOptions": {
                "target": "esnext",
                "moduleResolution": "node",
                "noEmit": true
            }
        }
        ```

        ```bash
        #上記の内容をオプションで実行したい場合
        npx tsc --target esnext --moduleResolution node --noEmit src/main.ts
        ```
    
<br>
<br>

- tsconfig.json でコンパイル対象を指定する場合

    - include フィールドにコンパイル対象のファイルを指定する

        ```json
        //tsconfig.json
        {
            "compilerOptions": {
                "target": "esnext",
                "moduleResolution": "node",
                "noEmit": true
            },
            "include": ["src/main.ts"] //ここ
        }
        ```
    
    - tsc コマンドは対象ファイルを指定せずに実行する

        ```bash
        #src/main.tsだけがコンパイルされる
        npx tsc
        ```

