### 事象

- tsconfig の moduleResolution を nodenext に指定しても、拡張子を省略した import ができてしまう

    <img src="../img/Issues/Issue-moduleResolution-nodenext-extensionless-import_1.svg" />

    <br>

- `moduleResolution: nodenext` の時は import 対象の指定に拡張子は必須では?

---

### 原因

- `moduleResolution: nodenext (node16)` は、Common JS と ES Modules の両方をサポートしている

    - ★コンパイル結果が Common JS となる ts ファイルでは import の対象の拡張子を省略することができる

    - 詳しくは[こちら](../tsconfig_moduleResolution.md#node16-nodenext)を参照

---

### 解決策

- まず、この事象は仕様のうちで、**バグではない**

    - その上で、拡張子付き import を強制したいのであればファイルを EMS として扱うように設定すればいい

        1. package.json の type フィールドに "module" を設定し、`.ts` ファイルを ESM として扱うようにする

            or

        2. 拡張子付き import を強制したい (=ESM として扱いたい) ファイルの拡張子を `.mts` にする