### 変数宣言とデータ型の定義

- l`et/var 変数名:データ型 = 初期値` で宣言する
    
- 定義できる型はstring, number(整数,浮動小数点数), boolean, any, 配列, タプル, nulll, undefined

---


### 配列の使い方  
1. 配列の宣言  

    - `変数名:データ型[]` か `変数名:Array<データ型>` で宣言する

        ```TypeScript
        let array1: string[] = ['a', 'b'];
        let array2: Array<string> = ['c', 'd'];
        ```

<bt>

2. 配列の操作方法  

    - pop, push, shift, unshiftで要素の操作ができる

        ```TypeScript
        array1.push('e'); //末尾に追加
        // 'a', 'b', 'e'

        array2.unshift('f'); //先頭に追加
        // 'f', 'c', 'd'
        ```

<br>

3. 要素へのアクセス  

    - JavaScriptと同じ方法でアクセス
    
        ```TypeScript
        array1[0]; //1番目の要素にアクセス
        // 'a'
        ```

---

### タプル　　
- タプルとは、異なる複数のデータ型を持つことができる固定長の配列のようなもの

1. タプルの宣言  

    - `変数名: [要素１のデータ型, 要素2のデータ型] = [要素1の初期値, 要素2の初期値];`  

        ```TypeScript
        let t: [number, string, number] = [1, 'hoge', 200];
        ```