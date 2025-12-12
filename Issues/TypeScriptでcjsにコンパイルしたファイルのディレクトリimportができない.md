### 事象

#### やりたかったこと

- [tsconfig の "moduleResolution": "nodenext"](../tsconfig_moudleとmoduleResolution.md#node16-nodenext) に設定し、cts ファイルでディレクトリインポートをしたかった

    <img src="../img/Issues/Issue-CTS-Directory-Import_1.svg" />

#### 再現条件

- tsconfig の module と moduleResolution に nodenext を指定

    ```json
    //tsconfig
    {
        "compilerOptions": {
            "outDir": "./out",
            "module": "nodenext",
            "moduleResolution": "nodenext"
        }
    }
    ```

<br>

- import 対象のディレクトリ直下には package.json を作成

    - exports フィールドと main フィールドにエントリポイントとして greet.js を指定 

    ```json
    //libディレクトリ直下のpackage.json
    {
    "name": "lib",
    "version": "1.0.0",
    "description": "",
    "main": "greet.js",
    "exports": {
        ".": "./greet.js"
    },
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
    },
    "keywords": [],
    "author": "",
    "license": "ISC"
    }
    ```

<br>

- tsc でコンパイルしたファイル (cjs) を実行しようとするとエラーが発生

    <img src="../img/Issues/Issue-CTS-Directory-Import_2.svg" />

---

### 原因

- lib ディレクトリ配下の package.json がコンパイルされたファイルが出力されるディレクトリにコピーされていなかったから

    <img src="../img/Issues/Issue-CTS-Directory-Import_3.svg" />

---

### 解決策

- 以下の3つの方法がある

    1. インポート対象にファイル名まで指定する

        <img src="../img/Issues/Issue-CTS-Directory-Import_4.svg" />

    <br>

    2. インポート対象のファイル名を指定したくない場合

        - tsconfig に include フィールドを追加し、import 対象ディレクトリ配下の package.json もコンパイル結果が出力されるディレクトリにコピーするよう設定

            - ★include に何か1つでも指定したら、その他のファイルはコンパイル対象にならなくなるため、コンパイル対象を網羅するように指定すること

            - ★`lib/*` の対象は .ts/.tsx/.d.ts のため、package.json を明示的に指定する

         <img src="../img/Issues/Issue-CTS-Directory-Import_5.svg" />
    
    <br>

    3. インポート対象のファイル名を index.ts (.mst や .cts、.js) に修正する (利用する側の import 文は修正しなくていい)

         <img src="../img/Issues/Issue-CTS-Directory-Import_6.svg" />