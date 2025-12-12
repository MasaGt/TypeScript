#### Type Alias  
- 型に名前をつけることができる  
- **type 付けたい名前 = データ型(もしくはデータ)**

```TypeScript

    type CardId = string | number;
    let id1: CardId = 100;

    //これもOK
    // リテラル型
    type OK = 200;
    // 配列型
    type Numbers = number[];
    // オブジェクト型
    type UserObject = { id: number; name: string };
    // ユニオン型
    type NumberOrNull = number | null;
    // 関数型
    type CallbackFunction = (value: string) => boolean;

```

#### interfceとtypeの違い  
- オブジェクト型にtypeを使うのとinterfaceを使うのでは違いがある  

|               | interface | type |
| ------------- | --------- | ---- | 
|      継承      |      可能     | 不可。ただし交差型で表現は可能 | 
| 同名のものを宣言 | 定義がマージされる | エラー | 
| Mapped Types  |    使用不可    |  使用可能  | 


<br>

#### 継承について  

- インターフェースは、インターフェースや型エイリアスを継承できる  

```TypeScript

    interface Animal {
    name: string;
    }
    type Creature = {
    dna: string;
    };
    interface Dog extends Animal, Creature {
    dogType: string;
    }

    let hachi: Dog = {
        name: 'Kuma',
        dna: '',
        dogType: 'chow chow',
    }

```

- 一方、型エイリアスは継承は行えない

```TypeScript

    type Animal = {
        name: string;
    };

    type Creature = {
        dna: string;
    };

    type Dog extends Animal, Creaturre {
        //エラー
    }

```

    しかし、代わりに交差型(&)を使用することで、継承と似たことを実現できる  

```TypeScript

    type Animal = {
        name: string;
    };

    type Creature = {
        dna: string;
    };

    type Dog = Animal & Creature & {
        dogType: string;
    };

    let dog = {
        name: 'Kuma',
        dna: '',
        dogType: 'chow chow'
    }

    //しかし、interfaceとは異なり、各プロパティは設定してもしなくてもよい

    //これでもコンパイルは通る(intefaceの時ではコンパイルエラー)
    /** nameだけ設定
     * let dog = {
        name: 'Kuma',
    }
    */

```

#### 同名のものを宣言について  

- typeでは同名のものを定義しようとするとコンパイルエラー

```TypeScript

    type Animal = {
    name: string;
    };

    //識別子 'Animal' が重複しています。
    type Animal = {
    age: number;
    };

```

- interfaceでは同名フィールドが同じ型の場合はOK, 異なっていたらコンパイルエラー
- 同名インターフェースを複数宣言し、上記のエラーがない場合は、同名のインターフェースを統合したものになる

```TypeScript

    interface Animal {
    name: string;
    };

    interface Animal {
    age: number;
    };

    //下記は1番目のAnimalのnameのデータ型と異なるのでコンパイルエラー
    /**
     * interface Animal {
     *  name: number;
     * }
    */


   //Animalは1番目と2番目の統合したものなので、nameとageのプロパティの設定が必要(でなければコンパイルエラー)
   let dog: Animal = {
        name: 'sample',
        age: 1,
    }
    
```