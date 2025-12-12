### 事象

- jsx ファイルを含めて tsc コンパイルをしようとしたが、 jsx はコンパイルされず、出力もされなかった

- tsconfig.json は以下のとおり

    ```json
    {
        "compilerOptions": {
            "target": "esnext",
            "module": "nodenext",
            "jsx": "react-jsx", //jsxの変換方法は指定している
            "outDir": "./dist"
        }
    }
    ```

---

### 原因

- jsx はコンパイル対象になっていなかった

    - ★include や files に jsx と指定してもだめ

        ```json
        {
            "include": ["./scr/*.jsx"], //×
            "files": ["myComponent.jsx"] //×
        }
        ```

    <br>

    - ★★jsx (js) ファイルをコンパイル&出力対象にしたい場合は `allowJs` フィールドに true を指定する必要がある

<br>
<br>

参考サイト

[allowJs](https://zenn.dev/hayato94087/books/b174f8b1cd80db/viewer/v00-05-11-v6dyqjd1hlu3)


[【TypeScript】tsconfig.jsonの設定](https://qiita.com/crml1206/items/8fbfbecc0b40968bfc42#include)

---

### 解決方法

- tsconfig.json に `allowJs` フィールド追加 + true を指定

    ```diff
    {
        "compilerOptions": {
            "target": "esnext",
            "module": "nodenext",
    +       "allowJs": true,
            "jsx": "react-jsx",
            "outDir": "./dist"
        },
    -   "include": ["./scr/*.jsx"],
    -   "files": ["myComponent.jsx"]
    }
    ```

