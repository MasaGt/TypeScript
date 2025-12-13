### 型定義ファイル中の import

- 型定義でも import キーワードが使える

    - 機能も ECMA Script と同じ

        <img src="./img/型定義ファイル中のimport/type-definition-import_1.svg" />

<br>

- しかし、型定義ファイルのトップレベルに import (export) がある場合は**モジュールと判断される**

    - ★「型定義ファイルをスクリプトとして扱いたい」 かつ 「他の型定義から型を読み込みたい」場合 **型ディレクティブ (トリプルスラッシュディレクティブ)** を利用するといい

        <img src="./img/型定義ファイル中のimport/type-definition-triple-slash-directives_2.svg" />

        <br>

        <img src="./img/型定義ファイル中のimport/type-definition-triple-slash-directives_1.svg" />

<br>

#### 注意事項

- モジュール型定義ファイルをトリプルスラッシュディレクティブを使って読み込むことはできない

    <img src="./img/型定義ファイル中のimport/type-definition-triple-slash-directives_3.svg" />

<br>
<br>

参考サイト

[サバイバルTypeScript - トリプルスラッシュ・ディレクティブ](https://typescriptbook.jp/reference/declaration-file#トリプルスラッシュディレクティブ)
