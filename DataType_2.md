### ユニオン　  

- 指定したいずれかの型として振る舞うような型の指定方法

    - 例: 数値でも文字列でも扱いたいユーザーID  

        ```TypeScript
        let userID: number | string;

        userID = 123; //数字を代入できる
        userID = '001'; //文字列も代入できる
        ```


<br>

- ユニオン型の変数に現在どの型のデータが含まれているかをチェックしたい場合はtypeof関数を利用する  

    ```TypeScript
    if(typeof(userID) == 'string') {
        //文字列でのユーザーIDでの処理
    }
    ```

---

### enum  

- 複数の定数を一つのまとまりとして扱うことができる  

- `enum 変数名 {名前, 名前, ...}` で宣言する  

- 参照したいときは 変数名.名前 で指定する

- ↓のように初期値を設定しないと、値は0からスタートする

    ```TypeScript
    enum Color {
        RED,
        GREEN,
        BLUE
    };

    Color.RED //0
    Color.GREEN //1
    ```

<br>

- ↓のように初期値を設定することも可能,設定しなければ前の定数からの連番になる

    ```TypeScript
    enum Color {
        RED = 10,
        GREEN,
        BLUE
    };

    Color.RED //10
    Color.GREEN //11
    ```

<br>

- また、enumのそれぞれの項目に値を個別に設定することも可能

    ```TypeScript
    enum Color {
        RED = 1,
        GREEN = 10,
        BLUE = 100
    };

    Color.RED //1
    Color.GREEN //10```
    ```

---

### リテラル型 (Literal type)

- **const** で値の宣言と代入を行うと、その変数のデータ型は、値の型に<font color="red">推論される</font>

    ```ts
    const val1 = "123"; // val1は"123"型と推論される
    // X val1 = "321"

    const val2 = true; // val2はtrue型と推論される
    // X val2 = false

    const val3 = 123; // val3は123型と推論される
    // X val3 = 321
    ```

<br>

- ↓の書き方をしても同じ (let じゃなく const に書き換えても)

    ```ts
    let val1: "123" = "123";
    // X let val1: "123" = "321";

    let val2: true = true;
    // X let val2: true = false;

    let val3:123 = 123;
    // X let val3: 123 = 321;
    ```

---

### Type Widening & Narrowing

#### Widening

- 変数のデータ型がより緩いものに拡張されてしまうこと

<br>

Wideningの事例その1

- const で宣言したリテラル型変数がプリミティブ型の let 変数に代入できてしまうこと

- また、let 変数に代入すると、対応するプリミティブ型に拡張されてしまうこと

    ```ts
    const num = "123"; // "123" 型(リテラル型)
    let num2: string = num; // 代入できてしまう -> "123" 型は string 型に拡張できると判断される

    let val1: "123" = "123"; // "123" 型(リテラル型)
    let val2: string = val2; // 代入できてしまう

    // let 変数に代入すると、対応するプリミティブ型に拡張されてしまう
    let num3 = num; // num3 は string 型と推論される
    ```

<br>

Wideningの事例その2.

- const で宣言したオプジェクトのリテラル型プロパティは、より緩いプリミティブ型の変数に拡張されてしまう

    ```ts
    // const でオブジェクトを宣言する
    const obj = {
        name: "sam", // name　は "sam" 型のつもり
        age: 20, // age が "20" 型のつもり
    };

    // しかし、実体は以下の通り
    /**
     * obj: {
     *     name: string
     *     age: number
     * }
     */

    // よって、以下の操作が可能になってしまう
    obj.name = "Bob";
    obj.age = 30;
    ```

<br>

- リテラル型配列も同様に、const で宣言されても、対応するプリミティブ型の配列に拡張されてしまう

    ```ts
    // ["a", "b", "c"] 型 (リテラル型) のつもり
    const arr = ["a", "b", "c"];

    // しかし、実体は以下の通り
    /**
     * arr: string[]
     */

    // よって、以下の操作が可能になってしまう
    arr[0] = "A";
    ```

<br>

- Widening 対策としては型アノテーションで指定するか、as const キーワードを利用する

    - 基本的には入力する文字数も少なく明示的なので as const を使うべき

        ```ts
        // 型アノテーションで型を指定する
        const obj: {name: "sam", age:20} = {
            name: "sam",
            age: 20,
        }
        // すると以下の通り、プロパティはリテラル型になる
        // (元々プリミティブ型のプロパティは除く)
        /**
         * obj: {
        *     name: "sam",
        *     age: 20,
        * }
        */

        // エラー
        obj.name = "bob";　


        // 型アノテーションで指定する
        const arr: ["a", "b", "c"] = ["a", "b", "c"]
        // すると以下の通り、プロパティはリテラル型になる
        // (元々プリミティブ型のプロパティは除く)
        /**
         * arr: ["a", "b", "c"]
        */

        // エラー
        arr.[0] = "A";

        // もしくは as const を使う
        const obj = {
            name: "sam",
            age: 20
        } as const;

        const arr = ["a", "b", "c"] as const;
        ```

<br>
<br>

#### Narrowing

- ユニオン型の変数のデータ型を具体的なものに絞り込むこと

- 以下のように、ユニオン型の引数を受け取り、内部でどちらかの型でしかできない処理を行う関数があるとする

    - Property ~~ does not exist　エラーが発生する

        ```ts
        let val: string = "hi";

        const sayHi = (arg: string | number): void => {
            console.log(arg.toUpperCase());
            // Property 'toUpperCase' does not exist on type 'string | number'.
            // Property 'toUpperCase' does not exist on type 'number'.
        };

        sayHi(val);
        ```

        <br>

        - 上記エラーを解消するには、 arg が toUpperCase() を持つデータ型であることを確実にしなくてはならない
            - データの絞り込みを行う = type narrowing 必要になる

                ```ts
                const sayHi = (arg: string | number): void => {
                    typeof arg === "string" && console.log(arg.toUpperCase());
                };
                ```
