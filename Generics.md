#### Genericsとは  
- Genericsは抽象的な型引数を使用して、実際に利用されるまで型が確定しないクラス/関数/インターフェースを作成してきる仕組み
- これによって、汎用的な処理を持つクラス/関数/インターフェースを作ることができる  


##### Genericsを使ったクラス定義
```TypeScript

    class Sample <T, U> {
        
        constructor(private _val1: T, private _val2: U) {}

        public getVal1: T {
            return this._val1;
        }

        public getVal2: U {
            retturn this._val2;
        }
    }

    let sample1 = new Sample(1, 'Hi'); //OK
    let sample1 = new Sample<string,number>('Yo' 2); //OK

```


##### Genericsを使った関数定義

```TypeScript

    //return val1 with 50% or val2 with 50%
    function chooseRandomly<T> (val1: T, val2: T) {
        return Math.random() <= 0.5 ? val1: val2;
    }

    let result1: string = chooseRandomly<string> ('A', 'B');

    let result2: number = chooseRandomly<number> (100, 200);

```


##### Genericsを使ったインターフェース定義

```TypeScript

    interface ValueObject<T> {
        value: T;
    
        toString(): string;
    }
    
    class UserID implements ValueObject<number> {
        public value: number;
    
        public constructor(value: number) {
            this.value = value;
        }
    
        public toString(): string {
            return `${this.value}`;
        }
    }

```


##### 型引数(パラメータ)に制約をつける

```TypeScript

    interface ValueObject<T> {
        value: T;
        
        toString(): string;
    }
    
    class UserID implements ValueObject<number> {
        public value: number;
        
        public constructor(value: number) {
            this.value = value;
        }
        
        public toString(): string {
            return `${this.value}`;
        }
    }
    
    class Entity<ID extends ValueObject<unknown>> {
        private id: ID;
        
        public constructor(id: ID) {
            this.id = id;
        }
    }
```
**EntityクラスはValueObjectインターフェースを実装しているクラスのみをIDとして受ける構造になっていますが,このときの型引数の制約はimplementsではなくextendsでなければなりません。**


