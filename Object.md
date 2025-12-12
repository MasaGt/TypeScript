#### Objectの書き方  

```TypeScript
//オブジェクトの生成
//型定義のイメージ(以降で実際のオブジェクトを代入するため)
//constで定義はできない ->初期化もしないと、値の代入ができなくなるから
let obj: {
    age: number,
    name: string
};

//実数(を持ったオブジェクト)の代入
obj = {
    age: 30,
    name: 'Mark',
}
```

<br>

もう一つの書き方  
Objectをnewで生成する方法  

```TypeScript
let obj = new Object();
obj.age = 30;
obj.name = 'Mark';
```

---

#### メソッドの定義もできる　　

```TypeScript
let person: {
    greet(msg: string): void;
}

person = {
    greet: (msg: string): void => {
        console.log(`Hello, ${msg}`);
    }
}
```

---

#### エラーケース  

- let 変数名: {} で宣言したのに, obj.プロパティ名 = で値を代入しようとするとコンパイルエラー  


```TypeScript
let sample: {
    name: string,
    sayHi: (target: string): string,
}

sample.name = 'Sample'; //エラー
sample.sayHi("Bob"); //エラー
```

- 原因: 宣言しただけで、実体を代入していないのでエラーになる

```ts
let sample: {
    name: string,
    sayHi: (target: string): string,
}

sample = {
    name: "sample",
    sayHi: (target: string): string => {
        return `Hi, ${target}`;
    }
}

sample.name; // "sample"
sample.sayHi("Bob"); // "Hi, Bob"
```

---

#### object、Object、{}の違い  
どれもオブジェクト型のデータを代入できる  

```TypeScript
let obj1: object = {};
let obj2: Object = {};
let obj3: {} = {};
```

- object型のみプリミティブ型の代入はできない  

```TypeScript
let obj: object = 1;
```

- Object, {} はプリミティブ型を代入するとオートボクシングされる
    - オートボクシング=代入されたデータ型に拡張解釈される

```TypeScript
let obj1: Object = 1; // obj1は number型で1を値として持つ
let obj2: {} = 1; // obj2は number型で1を値として持つ
```

- object, Object, {} のいずれもnullとundefinedは代入不可

---

#### interface

implementするinterfaceとは異なり、オブジェクトの型の定義をするためのキーワード(TypeScript独自)  

```TypeScript
interface Person {
    name: string,
    age: number,
    greet (): string;
}

let p1: Person = {
    name: 'sample1',
    age: 30,
    greet: (): string => {
        retrun `Hello`;
    }
}
```

---

#### オブジェクト内での自身のプロパティへのアクセス方法  
classのようにthisキーワードを使うのでなく、変数名.プロパティ名でアクセスする  

```TypeScript
interface Person {
    name: string,
    greet:(): void;
}

let sample: Person = {
    name: 'Sample1',
    greet: (): void => {
        console.log(`Hi, my name is ${sample.name}`);
    }
};

sample.greet();
//Hi, my name is Sample1
```

---

#### readonly 修飾子

- <font color="red">type や interface で宣言する</font>オブジェクトのプロパティを再代入不可にするキーワード

- プロパティ名の前に readonly をつける

```ts
type Obj = {
    readonly prop1: string,
    readonly prop2: number,
};

interface Obj2 {
    readonly prop1: string;
    readonly prop2: number;
}
```

<br>

- readonly で宣言されたプロパティの値を更新(再代入)しようとするとエラー

- const でも let でも readonly のプロパティは再代入できない

```ts
// let obj でも再代入不可
// let の場合、 obj に新しいオブジェクトの再代入はできる
const obj: Obj = {
    prop1: "obj",
    prop2: 1,
}
inst.prop1 = "update"; // エラー

const obj2: Obj2 = {
    prop1: "obj2",
    prop2: 2,
}

obj2.prop2 = 1; // エラー
```

---

#### 補足

#### 普通の const で宣言されたオブジェクトへの再代入について

- 宣言された変数へ新しいオブジェクトの再代入はできない

- しかし、オブジェクトのプロパティは再代入できる

```ts
const obj = {
    name: "Sam"
}

// 以下はエラー
obj = {
    name: "Bob"
}

// 以下は可能
obj.name = "New Sam";
```

<br>

#### 配列への readonly の利用について

- 型としての配列の前に readonly をつけることで、その配列は読み取り専用になる
    - しかし、配列全体の更新は可能
```ts
// 配列型の変数にreaonlyを利用する
let arr: readonly number[] = [1, 2, 3];
arr[0] = 100; // エラー
arr.push(4); // エラー
arr = [100, 200, 300]; // 可能

// 配列型のプロパティを持つオブジェクトにreadonlyを利用する
type Obj = {
  arr: readonly number[];
};

let obj: Obj = {
  arr: [2, 3, 4],
};
obj.arr[0] = 100; // エラー
obj.arr.push(); // エラー
obj.arr = [2]; // 可能
```