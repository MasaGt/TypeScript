### TypeScript の record とは

- TypeScript で利用できるデータ型の1つ

    - ★オブジェクトのプロパティの Key と Value のデータ型の型づけをする仕組み

- `Record<Keyのデータ型, Valueのデータ型>` で宣言する

    ```ts
    //型アノテーションでRecordを使用するケース
    let myObj: Record<string, number>;
    myObj = {};
    myObj.a = 100;
    console.log(myObj.a);
    //100


    //typeキーワードを使った型定義でRecordを使用するケース
    type Todo = Record<string, boolean>;
    //Todo型はキーがstringで、バリューがboolean型のオブジェクト
    const myTodo: Todo = {
        studyReact: true,
        studyGrapgQL: false,
        studyTypeScript: true
    };
    console.log(myTodo.studyReact);
    //true
    ```

<br>

- (普通のオブジェクトの型定義と異なり) Record はプロパティのキーの値も制限できる

    ```ts
    //キー名が"a"と"b"に限定されたオブジェクト型
    type myObj = Record<"a"|"b", number>

    //イメージ的には以下と同じだが、↓の宣言は有効ではない
    type myObj = {
        "a"|"b": number //キーの型定義の仕方が有効ではない旨のエラーが表示される
    }

    //↓myObjにプロパティ"b"がないというエラーメッセージが表示される
    let obj1: myObj = {a: 10}; //×

    //↓myObjにプロパティ"a"と"b"以外が存在しちゃっているというエラーメッセージが表示される
    const obj1: myObj = {
        a:100,
        b:200,
        c:300 //×
    }

    //↓OK
    const obj1 = {
        a:1,
        b:2
    }

    //↓myObjにプロパティ"a"と"b"以外が存在しちゃっているというエラーメッセージが表示される
    const obj1.c = 3; //×

    console.log(obj1.a);
    //1

    console.log(obj1["b"]);
    //2
    ```

<br>

- Record のキーの型定義に指定できるのは **string、number、symbolとそれぞれのリテラル型**

    ```ts
    //キーのデータ型をstringで指定
    type obj1 = Record<string, number>
    //キーのデータ型をstring型のリテラルで指定 ("1","2","3"に制限)
    type obj2 = Record<"1"|"2"|"3", number>


    //キーのデータ型をnumber型で指定
    type obj3 = Record<number, number>
    //キーのデータ型をnumber型のリテラルで指定 (1,2,3に制限)
    type obj4 = Record<1|2|3, number>


    //★キーのデータ型をsymobl型で指定
    type obj5 = Record<symbol, number>
    //具体的な利用例
    const mySymbol = Symbol("TypeScript")
    const myObj: obj5 = {
        mySymbol: 100
    }
    console.log(myObj.mySymbol)
    //100
    console.log(myObj["mySymbol"])
    //100 

    //キーのデータ型をsymobl型のリテラル(?)で指定 (Symbol("A")とSymbol("B")に制限)
    const s1 = Symbol("A");
    const s2 = Symbol("B");
    type obj6 = Record<s1|s2, number>

    //↓はダメな書き方
    type obj7 = Record<Symonl("C")|Symonl("D"), number>
    ```

<br>

#### 注意点

- キーのデータ型の指定に[リテラル](https://typescriptbook.jp/reference/values-types-variables/literal-types)ではなく、string, number, symobol を指定した場合、**存在しないキーにアクセスしても、それが存在しているかのように推論されてしまう**

    ```ts
    //キーのデータ型にstringを指定
    type MyType1 = Record<string, number>
    const obj1: MyType1 = {
        "val1": 1,
        "val2": 20,
        "val3": 300
    }
    //↓IDEやコンパイルが通ってしまう
    let myVal:number = obj1.val4;
    console.log(myVal);
    //undefined


    type MyType2 = Record<"a"|"b", number>
    const obj2: MyType2 = {
        "a": 1,
        "b": 20,
        "c": 300 //この時点で"a","b"以外のプロパティは存在しちゃだめエラーが表示される
    }
    obj2.d = 4000; //この時点で"a","b"以外のプロパティは存在しちゃだめエラーが表示される
    ```

---

### Map や インデックス型 と Record の違い

<img src="./img/Record/Map-IndexSignature-Record_1.svg" />

<br>

- Map は key と value からなる**データ構造 (クラス)**

    - コンパイル後の js ファイルに残る

<br>

- インデックス型や Record は**型定義**

    - 型情報なのでコンパイル後の js ファイルに残らない

<br>

- Map と Record はキーのデータ型にリテラルを書くことができる

    - さらにリテラルを `|` で union することで、キー名を制限することもできる

    ```ts
    //キー名は "a" か "b" に制限される
    const myMap = new Map<"a"|"b", number>;
    myMap.set("a", 100);// OK
    myMap.set("c",3000);// NG

    //キー名は 1 か 2 か 3 に制限される
    type myType = Record<1|2|3, bookean>;
    const myObj: myType = {
        1: true, //OK
        2: false, //OK
        3: false, //OK
        4: true //NG
    }
    ```