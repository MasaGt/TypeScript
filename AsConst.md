### as const とは

- const アサーションと呼ばれるキーワード

- オブジェクトの全てのプロパティを readonly にするキーワード
    - プロパティがオブジェクトや配列でも、再起的に readonly が付与されるイメージ

- **オブジェクト変数の初期化の時**に使えるキーワード

```ts
const obj = {
    prop: type
} as const;
```

<br>

例: string の name プロパティと object の parents プロパティを持つ person オブジェクトを作ってみた

```ts
const Person = {
    name: "sam",
    parents: {
        father: "Andy",
        mother: "Jasmin",
    },
    hobby: ["game", "music"]
} as const;

// 以下のようなイメージ(以下の文法は実際にはコンパイルエラー)
const Person: {
    readonly name: "sam",
    readonly parents: {
        readonly father: "Andy",
        readonly mother: "Jasmin"
    },
    readonly hobby: readonly ["game", "music"]
}
```


---

### readonly と　as const の違い

- readonly はそのプロパティがオブジェクトや配列の場合、**内部の値は更新できてしまった**

```ts
type Person = {
    readonly name: string
    readonly parents: {
        father: string,
        mother: string,
    },
    readonly hobby: string[],
}

const sam: Person = {
    name: "Sam",
    parents: {
        father: "Ben",
        mother: "Maria",
    },
    hobby: ["game", "music"],
}

// samのname,parents,hobbyは再代入できない
sam.name = "new sam"; // エラー
sam.parents = {father: "Dany", mother: "Anne"}; // エラー
sam.hobby = ["sports"]; // エラー

// しかし、parents.fatherとpamrents.otherやsam.hobby[x]は再代入可能
sam.parents.father = "nobody"; // 可能
sam.parents.mother = "nobody"; // 可能
sam.hobby[0] = "sports"; // 可能
```

<br>

- readyonly では以下の通り

```ts
sam.parents.father = "nobody"; // エラー
sam.parents.mother = "nobody"; // エラー
sam.hobby[0] = "sports"; // エラー
```


----

### as と as const の違い

- as と as const は全く機能が違うキーワード

- as はコンパイラに型を明示するキーワード (型アサーション)

- 変数の後ろで as DataType でその変数のデータ型は~~だとコンパイラに伝える

```ts
let val: string | number = "Hello";
let len = (val as string).length
```

<br>

- as ~~ でデータ型を伝えたにも関わらず、実際の変数と整合性が取れないとランタイムエラーを起こす可能性がある

- 以下の例では val の実体は number で length プロパティを持っていないので、 len ヘは undefned が入る

```ts
let val: any = 234;
let len: number = (val as string).length; // undefined
```

<br>

- as での型アサーションは最終手段で、**基本的には使わないほうがいい**

---

### satisfies との組み合わせう

- 詳しくは[こちら](./Satisfies.md)

