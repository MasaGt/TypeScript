### tsconfig の compileOptions.typeRoots フィールドとは

- TypeScript コンパイラが**暗黙的に**読み込む型定義ファイル（.d.tsファイル）の**ディレクトリ**の場所を指定する項目

    <img src="./img/tsconfig_typeRoots_types/tsconfig-typeRoots_4.svg" />

    <br>

    - ★設定する値は tsconfig からの相対パス

        <img src="./img/tsconfig_typeRoots_types/tsconfig-typeRoots_1.svg" />

    <br>

    - ★モジュールの型定義ファイルには影響を及ぼさない

        - →typeRoots はグローバル型定義ファイル (スクリプト) の読み込みに影響する項目

        <img src="./img/tsconfig_typeRoots_types/tsconfig-typeRoots_2.svg" />

    <br>

    - ★デフォルトではプロジェクト直下とすべての親ディレクトリの `node_modules/@types` 暗黙的に読み込む

        - ★typeRoots を明示的に指定すると、そのディレクトリ以外のグローバルな型定義ファイル (スクリプト) は読み込まれなくなる

        <img src="./img/tsconfig_typeRoots_types/tsconfig-typeRoots_3.svg" />

<br>
<br>

参考サイト

[js STUDIO - tsconfig](https://js.studio-kingdom.com/typescript/project_configuration/tsconfig_json?utm_source=chatgpt.com#types_type_roots_and_types)

---

### tsconfig の compileOptions.types フィールドとは

- TypeScript コンパイラが**暗黙的に**読み込む型定義ファイル ().d.tsファイル）かある**パッケージ**を指定する項目

    <img src="./img/tsconfig_typeRoots_types/tsconfig-types_6.svg" />

    <br>

    - ★設定する値はパッケージ名

        <img src="./img/tsconfig_typeRoots_types/tsconfig-types_1.svg" />

    <br>

    - ★typeRoots フィールドと同様にモジュールの型定義ファイルには影響を及ぼさない

    <br>

    - デフォルト (= typesフィールドが指定されていなければ) は `@types`

        - ★★types フィールドに明示的に `@types` と指定すると、その tsconfig.json の位置にある node_modules/@types しか対象にしなくなるので注意

        <img src="./img/tsconfig_typeRoots_types/tsconfig-types_2.svg" />

    <br>

     - ★★★typeRoots が指定されていない場合は `./node_modules/@types<typesで指定したパッケージ名>` にあるグローバルな型定義ファイルを自動的に読み込む

        - ↑のパッケージ or グローバルな型定義ファイルが存在しない場合は `./node_modules/<typesで指定したパッケージ名>` にあるグローバルな型定義ファイルを自動的に読み込む

        <img src="./img/tsconfig_typeRoots_types/tsconfig-types_3.svg" />

    <br>

    - ★★★typeRoots が指定されている場合は `<typeRootsで指定したディレクトリ>/<typesで指定したパッケージ名>` を読み込む型定義 (グローバルな型定義のみ) の対象とする

        <img src="./img/tsconfig_typeRoots_types/tsconfig-types_4.svg" />

        <br>

        - しかし、typeRoots で指定したディレクトリに types で指定したパッケージが存在しない場合は tsconfig.json の設定エラーになり、型チェックやコンパイルでエラーが起きる

        <img src="./img/tsconfig_typeRoots_types/tsconfig-types_5.svg" />

<br>
<br>

参考サイト

[TypeScript Deep Dive 日本語版 - グローバルの制御](https://typescript-jp.gitbook.io/deep-dive/type-system/types#gurbaruno)

[TypeScript - Types](https://www.typescriptlang.org/ja/tsconfig/#types)

---

### tsconfig の typeRoot と types

#### 共通点

- 暗黙的 (自動的に) 読み込ませたいグローバルな型定義 (= スクリプト) の対象範囲を制限するための設定項目

- モジュールな型定義ファイルの読み込みには影響しない

<br>

#### 違い

- **typeRoots**

    - tsconfig.json からの相対パスでディレクトリを指定する

<br>

- **types**

    - パッケージ名を指定する

        - typeRoots が指定されていない場合は `./node_modules/<typesで指定したパッケージ名>` にあるグローバルな型定義ファイルを自動的に読み込む

            - ↑のパッケージ or グローバルな型定義ファイルが存在しない場合は `./node_modules/@types/<typesで指定したパッケージ名>` 

        <br>

        - typeRoots が指定されている場合は `<typeRootsで指定したディレクトリ>/<typesで指定したパッケージ名>` を読み込む型定義 (グローバルな型定義のみ) の対象とする


---

### 疑問

#### vite/clientの謎

- `npm create vite` コマンドで Vite プロジェクト (TypeScript) を作成すると自動で生成される tsconfig.app.json にて types に `vite/client` が指定されていた

    - Q: node_modules には vite/client なんてパッケージは存在しない。 vite/client って何を指定しているのか?

        <img src="./img/tsconfig_typeRoots_types/vie-tsconfig-app-json-types_1.svg" />

    <br>

    - A: node_modules/vite パッケージ直下 package.json の exports フィールドに ./client への型情報が定義されていた

        <img src="./img/tsconfig_typeRoots_types/vie-tsconfig-app-json-types_2.svg" />

    <br>

    - \[補足]: package.json の exports フィールドには、サブフィールドとして `import`, `require`, `types` などのフィールドが設定できる

        <img src="./img/tsconfig_typeRoots_types/package-json-exports-sub-fields_1.svg" />