# CLAUDE.md

UE5（Unreal Engine 5）初心者向けの学習クイズアプリ。

## ファイル構成

- `index.html` — 画面（HTML/CSS）と処理（JavaScript）をすべて含む。外部ライブラリは使わない。
- `questions.json` — 問題データ。
- `README.md` — 遊び方・起動方法。
- `CLAUDE.md` — このファイル。

2ファイル構成（index.html + questions.json）を維持すること。

## 問題データの形式（questions.json）

```json
{
  "beginner":     [ { "question": "...", "choices": ["A","B","C","D"], "answer": 0, "explanation": "..." } ],
  "intermediate": [ ... ],
  "advanced":     [ ... ]
}
```

- トップレベルのキーはレベル ID: `beginner`（初級）/ `intermediate`（中級）/ `advanced`（上級）。
- `question`: 問題文（文字列）
- `choices`: 選択肢（4つの文字列）
- `answer`: 正解の選択肢の 0 始まりインデックス（0〜3）
- `explanation`: 解説（文字列）
- 各レベルとも10問以上を用意する（出題時に各レベルからランダムで10問抽出。選択肢の順序も出題時にシャッフルされる）。

## アプリの仕様

- 出題数 10問 / 合格ライン 正答率70%以上（`index.html` 冒頭の定数 `QUESTIONS_PER_QUIZ`, `PASS_RATE`）。
- 1問ごとに正解/不正解と解説を表示し、「次へ」で進む。
- 成績は localStorage のキー `ue5quiz.results` に配列で保存（`level, correct, total, rate, passed, date`、最新50件）。
- `questions.json` は `fetch` で読み込むため、`file://` ではなくローカルサーバー経由で確認する（例: `python3 -m http.server`）。

## 開発ルール

- 応答は日本語で行う。
- 問題文・選択肢・解説の事実関係は勝手に変えない。誤りや古い情報の疑いがある場合は、変更せずユーザーに指摘・確認する。
- 外部ライブラリ・外部CDNは使わない。
- ユーザー由来でない文字列も含め、画面への出力は `textContent` を使う（`innerHTML` を避ける）。
- 問題データを編集したら、JSON として妥当か（各レベルの問題数、choices が4つ、answer が 0〜3）を確認する。
