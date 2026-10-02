# ue5-quiz

UE5（Unreal Engine 5）初心者向けの学習クイズアプリです。ブラウザだけで動作します（外部ライブラリ不使用）。

## 公開URL

GitHub Pages で公開しています。スマホのブラウザでも遊べます。

https://tkzdesign.github.io/ue5-quiz/

## 遊び方

1. 開始画面でレベル（初級・中級・上級）を選びます。
2. 選んだレベルからランダムに10問出題されます（4択）。
3. 回答するたびに正解/不正解と解説が表示されます。「次へ」で次の問題に進みます。
4. 10問終了後に正答率が表示されます。**正答率70%以上で合格**です。
5. 成績はブラウザの localStorage に保存され、開始画面でベスト成績や最近の履歴を確認できます。

## ローカルで動かす場合

`questions.json` を `fetch` で読み込むため、`index.html` をダブルクリックで開くのではなく、ローカルサーバー経由で開いてください。

```sh
python3 -m http.server 8000
# ブラウザで http://localhost:8000/ を開く
```

## 問題の差し替え

`questions.json` を編集します。形式の詳細は [CLAUDE.md](CLAUDE.md) を参照してください。

```json
{
  "beginner": [
    { "question": "問題文", "choices": ["A", "B", "C", "D"], "answer": 0, "explanation": "解説" }
  ],
  "intermediate": [],
  "advanced": []
}
```

`answer` は正解の選択肢の番号（0〜3）です。各レベル10問以上用意してください。
