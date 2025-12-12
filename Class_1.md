#### TypeScriptでのクラスの書き方

基本的にはプレーンなJavaScriptと変わりない

- **違い**
    - TypeScriptではコンストラクタ内でのメンバ変数の初期化が初略できる

    <br>
    
    - getterでは戻り値のデータ型を指定すること

    <br>
    

    - setterでは戻り値のデータ型の指定はしてはいけない (: voidと記入するとコンパイルエラー)

    <br>

    - constructorにも戻り値のデータ型の指定はない

    <br>

    - setterでは引数のデータ型を指定すること

    <br>

    - アクセス修飾子については、[AccessorModifier.md](./AccessorModifier.md)を参照すること

<br>

- JavaScriptでクラスを書くと
    ```js
    Class Student {
        constructor (name) {
            this._name = name;
        }

        get name() {
            return this._name;
        }

        set name(name) {
            this._name = name;
        }
    }
    ```

<br>

- TypeScriptでクラスを書くと

    ```ts
    class Student {
        constructor(private _name: string) {}

        get name(): string {
            return this._name;
        }

        set name(name : string) {
            this._name = name;
        }
    }
    ```

---

### 継承の書き方

- `class <継承するクラス名> extends <継承元クラス名>` はJavaScriptと同じ  

- 親クラスのメソッドを呼びだす際には `super.メソッド()` なのも同じ  

    ```ts
    class Human {
        constructor (name: string) {}

        greet(): string {
            retturn `Hello, I am ${name}.`;
        }
    }

    class SuperHuman extends Human {
        constructor (name: string, skill: string) {
            super(name);
            this.skill = skill;
        }
            
        greet(): string {
            return super.greet() + `I can do ${skill} !!`;
        }
    }
    ```

<br>

- もしサブクラスの中で追加する処理がなければ、省略していい

    ```ts
    class Parent {
        constructor (name: string) {
            this.name = name;
        }
    }

    class Child {
        /**
         * 以下の記載はいらない
         * constructor (name: string) {
         *  super(name);
         * }
        */

        //以降Childクラスに必要なメソッドを追加していけば良い
    }
    ```