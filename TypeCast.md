#### データ型のキャスト  

**stringからnumberへキャストはできない。そのようなキャストはNumber関数を使うなど他の方法を使う**


ここでのキャストができるのは val: string | number　のように　ユニオン型のデータタイプを利用していたり、  
クラスのアップキャスト: サブクラスをスーパークラスの型で使いたい  
クラスのダウンキャスト: スーパークラスをサブクラスの型で使いたい(多分あまり使わない)  


- <> を使う方法  
<キャストしたいデータ型>ターゲットの変数 でキャストする  

```TypeScript
    let val: number | string = '123';
    let len: number = (<string>val).length; //numberをstringにキャスト
```

- as を使う方法  
ターゲットの変数 as キャストしたいデータ型 でキャストする  

```TypeScript
    let val: number | string = '123';
    let sum = val as number + 111; //stringをnumberにキャスト
    // *しかし計算結果は12311で　文字列+数字になる
    // 123 + 111をしたければNumber関数を使うこと
```

- stringからnumber また その逆でのキャストをする方法
unknown を経由する

```TypeScript
    let val: string = '12';
    let sum : number = (val as unknown as number) + 12;
```
