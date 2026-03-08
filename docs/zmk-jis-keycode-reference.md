# ZMKキーコードとJISキーボードの対応表

`config/ZaruBall.keymap` を JIS 配列前提で編集するときの早見表です。

## 前提

- ZMK の `&kp` は、基本的に US 配列ベースの HID usage 名を使います。
- `AT_SIGN` や `CARET` のような記号名は、「US 配列でその記号になる修飾付きキー」の別名です。
- そのため、ホスト OS が JIS 配列のときは、キーコード名と実際に入力される文字がずれます。
- JIS 前提で記号を置くときは、`AT_SIGN` のような記号別名よりも、`LEFT_BRACKET` や `LS(SEMI)` のように「元キー + Shift」で書くほうが安全です。

この表は、Windows の日本語キーボードレイアウト (`00000411`) を基準に整理しています。

## まず結論

| 入力したい文字/キー | 推奨 ZMK キーコード | 補足 |
| --- | --- | --- |
| `@` | `LEFT_BRACKET` | `AT_SIGN` ではなくこちら |
| `` ` `` | `LS(LEFT_BRACKET)` | JIS の `@` キーの Shift |
| `[` | `RIGHT_BRACKET` | |
| `{` | `LS(RIGHT_BRACKET)` | |
| `]` | `BACKSLASH` | US 名と見た目がずれる代表例 |
| `}` | `LS(BACKSLASH)` | |
| `^` | `EQUAL` | `CARET` ではなくこちら |
| `~` | `LS(EQUAL)` | |
| `;` | `SEMI` | |
| `+` | `LS(SEMI)` | `PLUS` より明示的で安全 |
| `:` | `SQT` | `COLON` ではなくこちら |
| `*` | `LS(SQT)` | |
| `-` | `MINUS` | |
| `=` | `LS(MINUS)` | |
| `/` | `FSLH` | |
| `?` | `LS(FSLH)` | |
| `\` / `¥` キー | `INTERNATIONAL_3` | JIS の最上段右端の `¥` キー |
| `|` | `LS(INTERNATIONAL_3)` | |
| `\` / `_` キー | `INTERNATIONAL_1` | JIS の `ろ` キー |
| `_` | `LS(INTERNATIONAL_1)` | |
| IME ON / かな | `LANG1` | Windows では IME ON 用として扱うのが無難 |
| IME OFF / 英数 | `LANG2` | Windows では IME OFF 用として扱うのが無難 |
| 半角/全角 | `GRAVE` | Windows JIS では文字ではなくこのキーになる |

## Windows JIS での主な実出力

| ZMK キーコード | Shift なし | Shift あり | JIS 側の見方 |
| --- | --- | --- | --- |
| `N1` | `1` | `!` | `1` キー |
| `N2` | `2` | `"` | `2` キー |
| `N3` | `3` | `#` | `3` キー |
| `N4` | `4` | `$` | `4` キー |
| `N5` | `5` | `%` | `5` キー |
| `N6` | `6` | `&` | `6` キー |
| `N7` | `7` | `'` | `7` キー |
| `N8` | `8` | `(` | `8` キー |
| `N9` | `9` | `)` | `9` キー |
| `N0` | `0` | なし | `0` キー |
| `MINUS` | `-` | `=` | `-` キー |
| `EQUAL` | `^` | `~` | `^` キー |
| `LEFT_BRACKET` | `@` | `` ` `` | `@` キー |
| `RIGHT_BRACKET` | `[` | `{` | `[` キー |
| `SEMI` | `;` | `+` | `;` キー |
| `SQT` | `:` | `*` | `:` キー |
| `BACKSLASH` | `]` | `}` | `]` キー |
| `COMMA` | `,` | `<` | `,` キー |
| `DOT` | `.` | `>` | `.` キー |
| `FSLH` | `/` | `?` | `/` キー |
| `GRAVE` | 文字なし | 文字なし | `半角/全角` キー |
| `INTERNATIONAL_1` | `\` | `_` | `ろ` キー |
| `INTERNATIONAL_3` | `\` / `¥` | `|` | `¥` キー |

## US 別名でハマりやすいもの

以下は「US 配列ではその記号になるが、JIS では別の文字になる」ものです。

| US 寄りの別名 | 実体 | Windows JIS で出るもの | JIS で欲しいものを出すなら |
| --- | --- | --- | --- |
| `AT_SIGN` | `LS(N2)` | `"` | `@` が欲しいなら `LEFT_BRACKET` |
| `CARET` | `LS(N6)` | `&` | `^` が欲しいなら `EQUAL` |
| `AMPERSAND` | `LS(N7)` | `'` | `&` が欲しいなら `LS(N6)` |
| `LEFT_PAREN` | `LS(N9)` | `)` | `(` が欲しいなら `LS(N8)` |
| `RIGHT_PAREN` | `LS(N0)` | 文字なし | `)` が欲しいなら `LS(N9)` |
| `UNDERSCORE` | `LS(MINUS)` | `=` | `_` が欲しいなら `LS(INTERNATIONAL_1)` |
| `PLUS` | `LS(EQUAL)` | `~` | `+` が欲しいなら `LS(SEMI)` |
| `COLON` | `LS(SEMI)` | `+` | `:` が欲しいなら `SQT` |
| `ASTERISK` | `LS(N8)` | `(` | `*` が欲しいなら `LS(SQT)` |
| `PIPE` | `LS(BACKSLASH)` | `}` | `|` が欲しいなら `LS(INTERNATIONAL_3)` |

## このリポジトリで特に見直し候補になりやすい箇所

`config/ZaruBall.keymap` のベースレイヤーには、US 名のまま置くと JIS で解釈がずれるキーがいくつかあります。

| 現在の記述 | Windows JIS での見え方 | JIS 意味で書き直すなら |
| --- | --- | --- |
| `&kp AT_SIGN` | `"` | `@` を置きたいなら `&kp LEFT_BRACKET` |
| `&kp CARET` | `&` | `^` を置きたいなら `&kp EQUAL` |
| `&kp SQT` | `:` | `'` を置きたいなら `&kp LS(N7)` |
| `&kp BACKSLASH` | `]` | `¥` キーなら `&kp INTERNATIONAL_3` |
| `&kp INTERNATIONAL_3` | `¥` キー相当 | ホスト依存があるので実機確認推奨 |

## 運用メモ

- JIS 記号を狙うなら、`AT_SIGN` や `PLUS` のような英語名より、`LS(SEMI)` のような書き方を優先する。
- Windows では `LANG1` / `LANG2` が IME ON / OFF に対応しやすい。
- `INTERNATIONAL_*` 系は JIS 固有キーの名前として分かりやすい一方、ホスト OS によって挙動差が出やすいので、最終的には実機で確認する。
