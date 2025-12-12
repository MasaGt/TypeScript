### ブジェクトのプロパティが存在しない場合でも、エラーを起こさずにプロパティを参照できる機能

ランタイムエラーが起きるケース
```TypeScript
type User = {
    name: string,
    hobbies?: string[]
}

let User1: User = {
    name: 'Sample',
    hobbies: ['music', 'art', 'food']
}

let User2: User = {
    name: 'John',
}

console.log(User1.hobbies.join('/'));

console.log(User2.hobbies.join('/'));
/**User2のhobbiesがundefinedなので、User2.hobbies.joinはundefined.joinと同義
=>エラー
*/
```
<br>

オプショナルチェーンを使うと
```TypeScript
console.log(User2.hobbies?.join('/'));
//エラーは起きず,undefinedが出力される
```
<br>

### オプショナルチェーンの使いどき  
参照したいプロパティがオプショナルなとき、オプショナルチェーンを使っておけば安心  