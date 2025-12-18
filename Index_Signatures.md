#### Index Signaturesとは

- オブジェクトのフィールド名をあえて指定せず、プロパティのみを指定したい時に役立つ記法らしい

    - `{[K: キーのデータ型], プロパティのデータ型}` で型宣言する (Kは別にKである必要はなくなんでもいい)

- この時のプロパティ名の型はstring、number、または、symbol じゃないといけない

- **フィールドに [仮キー名: キーのデータ型(String|number|symbol)]: データ型**

```TypeScript
//インデックス型を使った型アノテーション
let obj: {
    [K: string]: number;
};

obj = { a: 1, b: 2 }; // OK
obj.c = 4; // OK
obj["d"] = 5; // OK

console.log(obj.a); //1
console.log(obj.b); //2
console.log(obj.c); //4
console.log(obj.d); //5
```

<br>

```TypeScript
let obj: {
    [key: number]: string;
}

obj = {};
obj[1] = 'aaaa';
obj[2] = 'zzz';
console.log(obj[1]); //aaaa
console.log(obj[2]); //zzz
```