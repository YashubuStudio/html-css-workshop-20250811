# ステップ5：ポートフォリオ（自己紹介＋作品リンク）

**ねらい：** レイアウト、ナビゲーション、リンク。自分の作品をまとめる。

**作り方のおすすめ：** ステップ1〜4の`index.html`をそれぞれ別フォルダ（`step1/` など）に保存し、**このポートフォリオからリンク**します。

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>私のミニゲーム作品集</title>
  <style>
    :root{--bg:#0f172a; --card:#111827; --ink:#e5e7eb; --accent:#60a5fa}
    *{box-sizing:border-box}
    body{margin:0; font-family: system-ui, sans-serif; color:var(--ink); background:linear-gradient(120deg,#0f172a,#1f2937)}
    header{padding:32px 20px; text-align:center}
    h1{margin:0 0 8px}
    .sub{opacity:.8}
    .grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(240px,1fr)); gap:16px; padding:20px; max-width:1000px; margin:auto}
    .card{background:var(--card); border-radius:16px; padding:16px; box-shadow:0 10px 30px rgba(0,0,0,.25)}
    a.button{display:inline-block; margin-top:8px; background:var(--accent); color:#002; padding:10px 14px; border-radius:10px; text-decoration:none; font-weight:bold}
    footer{padding:24px; text-align:center; opacity:.7}
  </style>
</head>
<body>
  <header>
    <h1>○○のミニゲーム作品集</h1>
    <div class="sub">HTML/CSS/JavaScript で作ったゲームたち</div>
  </header>

  <main class="grid">
    <section class="card">
      <h2>ステップ1：ボタンカウンター</h2>
      <p>クリックでスコアUP！100点でごほうびメッセージ。</p>
      <a class="button" href="step1/index.html" target="_blank">あそぶ</a>
    </section>

    <section class="card">
      <h2>ステップ2：反射神経ゲーム</h2>
      <p>Ready → Go! 早押しに挑戦。</p>
      <a class="button" href="step2/index.html" target="_blank">あそぶ</a>
    </section>

    <section class="card">
      <h2>ステップ3：モグラたたきmini</h2>
      <p>3×3のモグラを素早くタップ！</p>
      <a class="button" href="step3/index.html" target="_blank">あそぶ</a>
    </section>

    <section class="card">
      <h2>ステップ4：メモリーカード</h2>
      <p>同じ絵文字をそろえよう。手数に挑戦！</p>
      <a class="button" href="step4/index.html" target="_blank">あそぶ</a>
    </section>
  </main>

  <footer>© 2025 ○○（なまえ）</footer>
</body>
</html>
```

### チャレンジ問題

* 自己紹介や写真を加えて**プロフィール**を作る。
* 作品の**スクリーンショット**を撮ってカードに表示。
