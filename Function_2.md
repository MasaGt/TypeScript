#### 関数のオーバーロード  
同名で異なる引数の関数の定義を複数行い、  
実装は一つの関数内で行う  

```TypeScript
    function func(x: string): void;
    function func(x: number, y: number): number;
    function func(): void;

    //関数の実装
    function func(x: any, y?: number): any {
        if (typeof x == 'string') {
            //xが文字列の時の処理
        } else if (typeof x == 'number') {
            //xが数字の時の処理
        } else if (typeof x == 'undefined') {
            //xがundefined (3番目に定義した関数)の時の処理
        } else {
            //その他の時の処理
        }
    }
```