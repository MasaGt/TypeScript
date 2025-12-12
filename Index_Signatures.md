#### Index Signaturesとは  
- オブジェクトのフィールド名をあえて指定せず、プロパティのみを指定したい時に役立つ記法らしい   
- この時のプロパティ名の型はstring、number、または、symbol じゃないといけない  
- **フィールドに [仮キー名: キーのデータ型(String|number|symbol)]: データ型**

```TypeScript

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