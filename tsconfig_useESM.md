### ts-jest

- useESM とは

    - ts-jest が**テストファイル(ts)やテスト対象ファイルをESMとしてテストするか、CJSとしてテストするか**を決める設定項目

        - ts ファイルがESM or CJS にコンパイルされるかどうかを決めるのは pacakage.jsonのtypeフィールドやファイル拡張子(.mts, .mcts)では?

            →上記の項目は「Node.js がどう実行するか」を決める項目であり、「ts-jest がどうトランスパイルするか」は別の話

        - ts-jest では、テストファイル（*.test.ts）が ESM として解釈されるか CJS として解釈されるかは、useESM の設定によって決まります。
