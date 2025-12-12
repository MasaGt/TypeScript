### モジュール化

- ts ファイルのモジュール化は ECMAScript と同じ方法で行う

    - TypeScript は EMSAScript に準拠してるから

---

### import 対象のファイル拡張子

    - tsconfig の設定によって ts ファイル中の import 文の書き方のルールが変わる

        - tsconfig の [moduleResolution](./tsconfig_moduleResolution.md) によって、ファイル拡張子の必要/不必要を決めることがきる

        - tsconfig の [moduleResolution](./tsconfig_moduleResolution.md) によって、package.json の import フィールド (import 対象のエイリアス) を 有効/無効 化することができる

        - tsconfig の path で 対象ディレクトリやファイルへのエイリアスを付与することができる (↑と同じ)

<br>
<br>

参考サイト

[Node.js v23.6.0：TypeScriptサポートが登場](https://note.com/leapcell/n/n87c87d6f2414)

[tsconfig.json の paths](https://zenn.dev/hayato94087/articles/9f3bf702543431)