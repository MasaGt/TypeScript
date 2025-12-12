### @types/node モジュールとは何か?

- TypeScript で Node.js の機能を利用するために必要なモジュール

    - 具体的には、@types/node = Node.jsの型情報

    <img src="./img/@types／nodeとは/@types:node_1.svg" />

    <br>

    <img src="./img/@types／nodeとは/@types:node_2.svg" />

---

### 誤解していたこと

- @types/node と ts-node は一緒にインストールする必要がある

    - 2つは異なる機能のパッケージのため、目的に応じてどちらか1つ、もしくは両方インストールしなくてもいいケースもある

        <br>

        - ts-node は ts ファイルの実行に必要なモジュール


        - @types/node は typeScript で Node の機能を利用するために必要なモジュール