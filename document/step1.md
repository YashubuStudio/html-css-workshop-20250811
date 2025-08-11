
# ステップ1：はじめてのページ & ボタンカウンター

**ねらい：** HTMLの基本タグ、CSSで見た目を整える、JSでイベント（クリック）を扱う。

**完成イメージ：** ボタンを押すと数字が増えるミニゲーム。

**ファイル名：** `index.html`

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>ステップ1：ボタンカウンター</title>
  <style>
    body{font-family: system-ui, sans-serif; margin:0; padding:24px; background:#f6f7fb;}
    .card{max-width:600px; margin:auto; background:#fff; border-radius:16px; padding:24px; box-shadow:0 6px 18px rgba(0,0,0,.08);}
    h1{margin-top:0}
    .counter{font-size:48px; margin:16px 0;}
    button{font-size:18px; padding:12px 20px; border-radius:12px; border:none; cursor:pointer}
    .primary{background:#4f46e5; color:#fff}
    .ghost{background:#eef2ff; color:#3730a3}
    .note{color:#555; font-size:14px}
  </style>
</head>
<body>
  <div class="card">
    <h1>ボタンカウンター</h1>
    <p>ボタンを押すとスコアが増えるよ！</p>
    <div class="counter" id="score">0</div>
    <button class="primary" id="btnAdd">+1する</button>
    <button class="ghost" id="btnReset">リセット</button>
    <p class="note">100点で「天才！」メッセージがでるよ。</p>
  </div>

  <script>
    const scoreEl = document.getElementById('score');
    const btnAdd = document.getElementById('btnAdd');
    const btnReset = document.getElementById('btnReset');
    let score = 0;

    btnAdd.addEventListener('click', () => {
      score += 1;
      scoreEl.textContent = score;
      if (score === 100) {
        alert('天才！100点達成！');
      }
    });

    btnReset.addEventListener('click', () => {
      score = 0;
      scoreEl.textContent = score;
    });
  </script>
</body>
</html>
```

### チャレンジ問題

1. ボタンを押すごとに、**背景色**を少しずつ変えてみよう。
2. 10点ごとに違うメッセージ（例：10点「いいね！」、20点「最高！」…）。

**難易度ダイヤル**：100→50点でクリアに変更／メッセージを増やす。

