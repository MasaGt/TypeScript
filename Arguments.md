#### デフォルト引数
引数がundefinedの場合にデフォルト値が適用される

 - JavaScriptの場合

```JavaScript
    function greet(name = 'hoge') {
        console.log(`Hello ${hoge}`);
    }

    greet('Mark'); //Hello Mark
    greet(); //Hello hoge
```

 - TypeScriptの場合  
    func 関数名(引数名: データ型 = デフォルトの値) で定義する  

```TypeScript
    function greet (name: strng = 'hoge'): void {
        console.log(`Hello ${hoge}`);
    }

    greet('Mark'); //Hello Mark
    greet(); ///Hello hoge
```

#### オプション引数　　
引数がundefined時にundefinedがそのまま適用される  

 - TypeScriptの場合  
    func 関数名(引数名?: データ型) で定義する  

```TypeScript
    //name: string|undefinedのイメージ
    function greet (name?: string): void { 
        console.log(`Hello ${name}`)
    }

    greet('Mark'); //Hello Mark
    greet(); //Hello undefined
```

#### 可変超引数  
 func 関数名 (...引数名: 型(配列)) で定義する  
 呼び出す側は複数の引数を渡す形で呼び出す  

 ```TypeScript
    function func(...nums: number[]): void {
        let sum: number = 0;
        for (let num of nums) {
            sum += num;
        }
    }

    func(1,2,3,4,5,6); //配列ではなく、複数の引数で渡す
 ```
