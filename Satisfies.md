### satisfies とは

- exp satisfies type の形で利用し、 exp が type にマッチしているかをチェックする演算子

- 主にオブジェクト型のプロパティの過不足をチェックするときなどに利用される
    - プロパティの過不足チェックだけなら型アノテーションでもできる

```ts
type Color = {
    rgb: number[] | string,
    example: string,
}

// example が不足しているエラーが起こる
const sky = {
    rgb: [135, 206, 235],
} satisfies Color;

// cmyk は存在しないエラーが起こる
const coral = {
    rgb: [248, 131, 121],
    example: "Flamingos",
    cmyk: [0, 47, 51, 3]
} satisfies Color;
```

---

### 型アノテーションとの違い

- プロパティの型チェックや、プロパティの過不足のチェックは型アノテーションと satisfies は同じように機能する

- **プロパティにユニオン型や any などを使用していた場合**、型アノテーションは変数の初期化以降、型推測が効かない

```ts
// 型アノテーションの場合
type Color = {
    rgb: number[] | string,
}

const pink: Color = {
    rgb: [255,192,203],
}

// 'map' does not exist in 'number[] | string'
pink.rgb.map((val) => {
    console.log(val);
});
```

- satisfies は初期化後も型推測が効く

```ts
const gray = {
    rgb: [220,220,220],
} satisfies Color

// rgb: string | number[] で実際にgrayに代入された値から型を推測している
// エラーにならない
gray.rgb.map((val) => {
    console.log(val);
});
```

<br>

- export した時も同じ

```ts
// export側
type Color = {
    rgb: string | number[];
}

export const pink: Color = {
    rgb: [255,192,203],
}

export const gray = {
    rgb: [220,220,220]
} satisfies Color;
```

```ts
// import側
import { pink, gray} from "import側のパス"

// エラー: map は string | number[] に存在しない
pink.map((val) => {
    console.log(val);
});

// 可能
gray.map((val) => {
    console.log(val);
}):
```

<br>

- また、両者のイメージは以下の通り
    - 型アノテーション: 明示的に変数の型を宣言するのに用いる
    - satsfies: 変数が型の条件を満たしているかを検証するのに用いる

---

### as const との組み合わせ

- satisfies と as const を組み合わせることで、
    1. export する側で変数の型チェックができる (satisfies)
    2. import する側で型推測ができる (satisfies)
    3. import する側でwideningされない (as const)  
        => プロパティの値などを変更される心配がない

```ts
// export する側
type Person = {
    name: string,
    favColor: string | number;
    paretns: {
        father: string,
        mother: string,
    }
}
export const sam: {
    name: "Sam",
    favColor: [100, 100, 100],
    parents: {
        father: "Bob",
        mother: "Anna",
    },
} satisfies Person; // 1. 型チェックができる (satisfies)
```

```ts
// import する側
import { sam } from "ファイルのパス";

// 2. 型推測ができる (satisfies)
// しかし、ランタイムエラーの可能性があるのでやっちゃいけない
sam.map((val) => {
    console.log(val)
});

// 3. wideningされない
sam.parent.father = "nobody"; // エラー "father" 型に "nobody" は代入できない
```