# 日本語の文字数と内訳 / Japanese Text Breakdown

## 日本語

開いているノートか選択範囲の文字を数えて、数だけを表示します。

- ステータスバー（デスクトップ版）：「文字 1,234」。選択があれば「選択 56 / 文字 1,234」。数は「文字（書記素）」です。UTF-16 のコードユニットで 1,000,000 を超えるノートは、ステータスバーでは数えず、コマンドで数えます。
- コマンド「文字数の内訳を表示」（ステータスバーの数をクリックしても開きます）：次の数を、テキストで表示します。
  - 文字（書記素）、文字（改行を除く）、文字（空白と改行を除く）、行、文、いちばん長い文（書記素）
  - 種類ごと：ひらがな（Script=Hiragana）、カタカナ（Script=Katakana）、漢字（Script=Han）、英字 A-Z a-z、全角英字 Ａ-Ｚ ａ-ｚ、数字 0-9、全角数字 ０-９、「、」「。」「，」「．」、空白と改行、その他
- モバイル版では確かめていません。

### 数え方

内訳の画面の「数え方」と同じ文です。

- 文字は、Intl.Segmenter（granularity "grapheme"）で分けた書記素です。CR LF は 1 つです。
- 改行は CR LF、LF、CR です。空白は Unicode の White_Space です。「文字（改行を除く）」は改行を除き、「文字（空白と改行を除く）」は、最初のコードポイントが空白の書記素もすべて除きます。
- 行は改行で分けた数で、空の行を含みます。空のノートは 0 行です。
- 文は、最初のコードポイントが「。」「！」「？」「!」「?」の書記素の後、改行、テキストの終わりで区切ります。空白でない書記素がある文を数えます。長さは、両端の空白を除いた書記素の数で、区切りの記号があれば含みます。例：`「行く。」` は 2 文です（`「行く。` の 4 と `」` の 1）。
- 各書記素は、最初のコードポイントで、ちょうど 1 つの種類に入ります。ひらがな・カタカナ・漢字は、Unicode の Script の値 Hiragana・Katakana・Han です。「々」は Script=Han なので漢字に、長音符「ー」は Script=Common なので「その他」に入ります。「その他」は、ほかのどの種類にも入らない書記素です。
- ノートは Markdown の元のテキストのまま数えます。「#」や「*」などの記号も、ほかの文字と同じように数えます。
- 選択が複数あるときは、選択ごとに数えて足します。いちばん長い文は、そのうちの最大の数です。
- 選択は、編集の画面（ソースモードとライブプレビュー）でだけ数えます。閲覧モードでは、ノートの全体を数えます。
- これは数だけです。文章の良し悪しや正しさは表しません。

**通信も保存もしません。** このプラグインは、ネットワークに接続せず、ファイルに書き込まず、設定や履歴も保存しません。数えた結果は、ステータスバーと内訳の画面に表示している間だけあります。

## English

Counts the characters in the open note or the selection and shows the numbers only.

- Status bar (desktop): "Characters 1,234", or "Selection 56 / Characters 1,234" when text is selected. The number is "Characters (graphemes)". Notes longer than 1,000,000 UTF-16 code units are not counted in the status bar; run the command.
- Command "Show the character count breakdown" (also opened by clicking the status bar item) shows, as text:
  - Characters (graphemes), Characters without line breaks, Characters without white space and line breaks, Lines, Sentences, Longest sentence (graphemes)
  - By kind: Hiragana (Script=Hiragana), Katakana (Script=Katakana), Kanji (Script=Han), Letters A-Z a-z, Fullwidth letters Ａ-Ｚ ａ-ｚ, Digits 0-9, Fullwidth digits ０-９, 、 。 ， ．, White space and line breaks, Other
- Not tested on mobile.

### How it counts

The same sentences as "How it counts" in the breakdown.

- A character is a grapheme as split by Intl.Segmenter (granularity "grapheme"); CR LF is one grapheme.
- Line breaks are CR LF, LF and CR. White space is Unicode White_Space. "Characters without line breaks" leaves out the line breaks; "Characters without white space and line breaks" also leaves out every grapheme whose first code point is white space.
- Lines are the pieces between line breaks, empty lines included; an empty note has 0 lines.
- A sentence ends after a grapheme whose first code point is 。 ！ ？ ! or ?, at a line break, or at the end of the text. A sentence counts when it has a grapheme that is not white space. Its length is its grapheme count without white space at both ends, the end mark included when there is one. For example, `「行く。」` is 2 sentences (`「行く。` with 4 and `」` with 1).
- Each grapheme is counted in exactly one kind, decided by its first code point. Hiragana, katakana and kanji are the Unicode Script values Hiragana, Katakana and Han: 々 is Script=Han and counts as kanji, and the long vowel mark ー is Script=Common and counts as Other. Other holds every grapheme that is in none of the other kinds.
- The note is counted as Markdown source text: markup such as # or * is counted like any other character.
- With several selections, each selection is counted on its own and the numbers are added; the longest sentence is the largest of them.
- A selection is counted only in the editing view (source mode and live preview). In reading view, the whole note is counted.
- These are counts only. They do not say whether a text is good or correct.

**No network, nothing stored.** The plugin makes no network connection, writes no files and stores no settings or history. The counts exist only while the status bar and the breakdown show them.

## ライセンス / License

MIT License（全文は `LICENSE`）。 / MIT License (full text in `LICENSE`).

## Author

sitebuild-note — https://sitebuild-note.pages.dev/
