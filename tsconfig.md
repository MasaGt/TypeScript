### tsconfig.jsonとは

- typescriptのコンパイル時の設定ファイル

---

### 主な設定項目
```
{
    "compilerOptions": {
        "target": "コンパイルして出力するJSファイルのバージョン",
        "lib": "「指定した target にはないけど使いたい機能がある」というときに、指定する",
        "jsx": "jsxをどのような構成の出力にするか",
        "allowJs": "tsファイルがプレーンなjsで書かれたモジュールを読み込める(importできる)ようにする設定",
        "strict": "いろいろなstrictな設定をtrueにする",
        "module": "コンパイルして出力するJSファイルがどのようなモジュールシステムを使うか指定",
    },
    "include": "コンパイルする対象ファイルを記述する",
    "files": "コンパイルするファイルを直接指定する(includeと違ってwild card使えない)",
    "exclude": "コンパイル対象から外すファイルを指定する(wild card使える)"

}
```
*libに関して:  
1.target を指定すればそのバージョンで使われているライブラリは自動的に追加される  
2.指定した target のバージョンでは実装されていないライブラリの追加や、必要がないライブラリを除外に使う(例: 最新バージョンにはある、または現時点では実装には至っていないが提案中(proposal)である機能を取り入れて使えるようにする物)

*moduleに関して:  
"commonJS", "none"だったら、出力されるjsファイルはmodule.exports/requireを使う  
"es2015", "es2020", "esnext"だったら、export/importを使う

*includeに関して:  
filesもincludeも指定しない場合、tsconfig.jsonが置かれているディレクトリ配下の全てのTypeScriptファイル（拡張子が.ts、.d.ts、.tsxであるファイル）のうち、excludeに含まれるファイル以外がコンパイル対象になる。

---

### tsconfig のセットアップコマンド

#### 前提条件

- tsc がインストールされていること

    - typescript をインストールしていれば tsc も一緒にインストールされているので別途 tsc のインストールは不要

<br>

```bash
npx tsc --init
```