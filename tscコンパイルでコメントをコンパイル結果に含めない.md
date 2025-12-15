### コンパイル結果にコメントを含めない方法

- tsconfi.json にて compoileOptions.removeComments フィールドを有効にする

    ```json
    {
        "compilerOptions": {
            "removeComments": true
        }
    }
    ```