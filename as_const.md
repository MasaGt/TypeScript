### as const とは

- 変数の値を readonly にする

    ```ts
    const val1 = 1 as const;
    //× val = 2;

    const obj = {
        name: "Bob",
        age: 200
    } as const;
    //× obj = { id: 1 } (constで宣言されているおかげでこの操作は不可能)
    //× obj.name = Andy" (as constのおかけでこの操作は不可能)
    ```

<br>

- 変数をその値の[リテラル型](https://typescriptbook.jp/reference/values-types-variables/literal-types)として扱う

    ```ts
    const obj = {
        name: "Bob",
        age: 200
    } as const;
    //★ obj.nameはstring型ではなく"Bob"型
    //★ obj.ageはnumber型ではなく200型
    ```

<br>

- 普通プリミティブ型に対して利用することはほとんどないが、オブジェクトや配列に利用する便利

<br>

#### readonly をつけたオブジェクトと as const をつけたオブジェクトの違い

- 変数のデータ型がリテラル型になるかどうか

    ```ts
    const obj1 = {
        readonly name: "Andy"
    };
    //obj1.nameはstring型

    const obj2 = {
        name: "Bob"
    } as const;
    //obj2.nameは"Bob"型

    //↑を利用したコードの例
    const OS = {
        mac: "Mac",
        windows: "Windows"
    } as const;

    type PC = {
        model: string,
        os: typeof OS.mac | typeof OS.windows //★osプロパティは"MAC"型と"Windows"型のユニオン
    }
    ```

<br>
<br>

参考サイト

[constアサーション「as const」 (const assertion)](https://typescriptbook.jp/reference/values-types-variables/const-assertion)

[リテラル型 (literal type)](https://typescriptbook.jp/reference/values-types-variables/literal-types)