### 抽象クラス  
- 抽象クラス、抽象メソッドには `abstract` をつけて宣言する  

<br>

- Java等と同様に、**抽象クラスをインスタンス化することはできない ** 

<br>

- 抽象メソッドは、処理内容がないので `{}` は付けない  

    ```ts
    // 抽象クラス
    abstract class Human {
        //抽象メソッド
        abstract greet (): string;
    }

    class Japanese extends Human {
        greet (): string {
            return 'こんにちは'
        }
    }

    class Kiwi extends Human {
        greet (): string {
            return 'Kia Ora';
        }
    }

    let j = new Japanese();
    console.log(j.greet()); //こんにちは

    let k = new Kiwi();
    console.log(k.greet());//Kia Ora
    ```

---

### インターフェース　　

- ★Javaと同様に `interface` で宣言し、`implements` で実装する  

<br>

- Javaと同様に1つのクラスに複数のインターフェースを実装できる  

<br>

- インターフェースのメソッドも処理内容が無いため、`{}` を省略するが、abstractキーワードは付けない  

    ```ts
    interface Human {
        name: string;
        
        greet(): string;
    }

    class Andy implements Human {
        constructor(public name: string) {}

        greet(): string {
            return `Hello, My name is ${this.name}.`;
        }
    }
    ```

<br>

- メンバ/メソッドに`?`キーワードをつけると、そのメンバ/メソッドの実装は任意になる  

    ```ts
    interface Human {
        name: string;
        age?: number

        greet? (): string;
    }

    class Andy implements Human {

        constructor(public name: string) {}
        //name　プロパティだけは実装しないとコンパイルエラーになる
    }
    ```

<br>

- 実装したクラスでインターフェースのメンバをpublic以外にするとコンパイルエラー  

    ```ts
    interface Person{
        name:string;
    }

    class Mark implements Person{
        private name:string; //コンパイルエラー
        /** これもコンパイルエラー
        constructor (name: string) {}
        constructor (private name: string) {}
        */

        /**これはOK
        * construtor (public name: string) {} 
        */
    }
    ```

<br>

- インターフェースの継承もできる

    ```ts
    interface InterfaceA {
        sampleProperty: string
    }

    interface InterfaceB extends InterfaceA {
        sampleFunction(x: number): boolean
    }

    class ClassB implements InterfaceB {
        sampleProperty: string = 'hello';

        sampleFunction(x: number): boolean {
            return x > 0
        }
    }

    const classB = new ClassB();
    console.log(classB.sampleProperty);         // hello
    console.log(classB.sampleFunction(100));    // true
    ```