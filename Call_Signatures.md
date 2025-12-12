#### Call Signaturesとは　　
- オブジェクトを関数として呼び出せるようにする書き方  
- オブジェクト生成の際に、以下の形でCall Signaturesを書く  
- **(引数名: 引数の型名): 戻り値の型名;**

```TypeScript

    let obj: {
        // (引数名: 引数の型名): 戻り値の型名;
        (msg: string): string;
    }

    //Call Signatureの定義に合致する関数を代入する
    obj = (msg: string): string => {
        return `Hi ${msg}`;
    }

    /**
     * 以下の書き方でもいい
     * obj = function (msg: string): string {
     *      return `Hi ${msg}`;
     * }
    */

    console.log(obj('Konnichiha'));
    //Hi, Konnichiha
```


##### Call Signatureがなぜあるのかについての説明(typescriptlang.org)  
- 関数リテラルではプロパティを持つことができず、Call Signaturesで自身(関数)について説明するプロパティを持つCallableなものを作ることができる  


#### 複数のCall Signaturesを持たせることもできる　　　
- 複数のコールシグネチャを定義することで、オーバーロードに対応できる

```TypeScript

    let obj: {
        (x: number): number;
        (x: number, y: boolean): number;
        (x: string): string;
    };

    obj = (x: any, y?: boolean): any => {
        if (typeof x === 'number') {
            if (typeof y === 'boolean') {
                return x;
            }
            return x*2;
        } else if (typeof x === 'string') {
            return 'Hi, ' + x;
        }
    };


    console.log(obj(2)); //4
    console.log(obj(2, true)); //2
    console.log(obj('Mark')); //Hi, Mark

```


#### interfaceでもCall Signatures使える

```TypeScript
    interface Human {
        (msg: string): void;
    }

    let sample: Human = (msg: string): void => {
        console.log(`Hello, ${msg}`);
    };

    sample('konbanha');
    //Hello, konbanha
```

#### いつCall Signaturesを使うのか  
- 関数を引数として渡す時
- 関数を別の関数から渡す場合に型付けが欲しい時

```TypeScript

    interface callbackType { 
    (arg: string) : string //Call Signature
    };

    // func関数はcalllbackという関数を引数として受け取る
    function func(arg: string, callback: callbackType) {
    return callback(arg)
    }

    console.log(func('hello Callback!!', (arg) => arg))

```