#### TypeScriptでは、引数と戻り値の型を指定できる
定義方法:
```ts
function 関数名(引数: 引数のデータ型): 関数の戻り値のデータ型 {  
    処理  
}
```

```ts
function func_name(arg1: string, arg2: number): string {
    return `${arg1}  ${arg2}`;
}
```

<br>

戻り値がない場合は:voidと指定する

```ts
function void_func(): void {
    console.log(戻り値のない関数);
}
```

---

### アロー関数

- 普通のJavaScriptの場合  

    ```JavaScript
    let add = (num1, num2) => {
        return num1 + num2;
    }
    ```

<br>

- TypeScriptの場合  

    ```TypeScript
        let add = (num1: number, num2: number): number => {
            return num1 + num2;
        }
    ```

---

### 関数を変数に代入するケース

- JavaScriptの場合  
   
    ```js
    let sayHello = function (name) {
        return `Hello ${name}!`;
    }
    ```

<br>    

- TypeScriptの場合  

    ```ts
    let sayHello = function (name: string): string {
        return `${Hello ${name}}`;
    }
    ```


---

### タプルで複数の値を返却する  

```ts
function func(): [number, string, number] {
    return [1, 'hoge', 200];
}
```