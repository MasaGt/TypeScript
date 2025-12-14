### tsconfig の rootDir フィールド

- 型チェック&コンパイル対象となる範囲の**構造の基準点**を指定する項目

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDir_1.svg" />

    <br>

    - [この記事](https://qiita.com/ryokkkke/items/390647a7c26933940470#rootdir)の説明がわかりやすかった

        > コンパイル結果をoutDirで出力する際に、どのディレクトリ配下のディレクトリ構造で出力するかを指定する。

        →その構造の範囲外にコンパイル対象が存在する場合はエラーが発生する

    <br>

    - ★コンパイル対象の範囲を決める項目では無いことに注意 (コンパイル対象を決めるのは `include` フィールド)

<br>

- rootDir が指定されていない場合、コンパイル対象のファイルの「**共通の親ディレクトリ**」が rootDir に推論される

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDir_2.svg" />

<br>

- rootDir が指定されていていながら、コンパイル対象がその範囲外に存在する場合はエラー

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDir_3.svg" />

<br>
<br>

参考サイト

[tsconfig.jsonの主要オプションを理解する](https://qiita.com/ryokkkke/items/390647a7c26933940470#rootdir)

[tsconfigのディレクトリ系オプション](https://zenn.dev/mosh/scraps/3ab9557921c5b2)

---

### tsconfig の rootDirs フィールド

- 指定したディレクトリを仮想的に同じディレクトリにあると見なすよう設定する項目

    - ★[`rootDir`](#tsconfig-の-rootdir-フィールド) とは機能が全く異なるので注意

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDirs_1.svg" />

<br>

- ★`rootDirs` を指定したからといって、仮想的なディレクトリからのパスでしかモジュールを指定してはいけない**ということではない**

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDirs_2.svg" />

<br>

- ★`rootDirs` を指定しただけでは実行時にエラーが発生する可能性が高い

    <img src="./img/tsconfig_rootDir_rootDirs/tsconfig_rootDirs_3.svg" />

    <br>

    - ★★仮想ディレクトリとコンパイル&ビルド後のディレクトリ構造を合わせるには、 webpack や Vite, Rollup などのモジュールバンドラーやビルドツールを利用する必要がある

<br>
<br>

参考サイト

[ハイラル勇者のためのTypeScript：rootDirsの活用術と代替手段](https://runebook.dev/ja/docs/typescript/tsconfig/rootDirs-config)