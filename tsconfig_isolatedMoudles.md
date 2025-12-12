### tscofig の isolatedModules とは

- .ts **ファイルをそれぞれ独立してコンパイ**できない場合に警告をするオプション

<br>

#### 独立してコンパイルとは?

- そもそも、tsc でのコンパイルはプロジェクト全体（複数ファイル）を一度のコンパイルで一度に読み込む

<br>

- しかし、esbuild や babel のような他の TypeScript コンパイラは 1 ts ファイルづつ独立してコンパイルする

    <br>

    → 他のコンパイラでは、以下のようなファイルのコンパイルの時に問題が生じる

    1. 型情報のエクスポート

    2. 

    従って、esbuild や tsc でのコンパイルの際にコンパイルエラーが出ないように前もって独立したコンパイルができないようなファイル

<br>
<br>

参考サイト

[TypeScriptを他のツールで取り扱うためのコンパイラオプションについて](https://qiita.com/uhyo/items/c33489155e1817479948)

[isolatedModules documentation still says that it bans non-modules #55785](https://github.com/microsoft/TypeScript/issues/55785?utm_source=chatgpt.com)

---

### isolatedModules について勘違いしていたこと

- isolatedModules を true にすると tsc でのコンパイルを off にする

    →×: isolatedModule を true にすると IDE や tsc での**静的チェック**で const enum を使っていたりモジュールファイルではないファイルを見つけると**警告を出すオプション**

    - そのため、isolatedModule を true にしたとて、以下のようなコードに対して警告は出るものの、tsc でのコンパイルは通る

        ```ts
        // exportがないため、モジュールとみなされないtsファイル
        function fn() {}
        ``` 

---

### const enum と declare const enum

