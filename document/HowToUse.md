## 公開のしかた（かんたん）

1. フォルダ構成を作る：

   ```
   portfolio/  ← ポートフォリオフォルダを作って公開
     ├─ index.html
     ├─ step1/index.html
     ├─ step2/index.html
     ├─ step3/index.html
     └─ step4/index.html
   ```
2. フォルダごとUSBメモリで友だちに配る／学校PCで開く。
3. 可能なら**GitHub Pages**や**Netlify**で公開（先生・保護者サポート推奨）。

---

## よくあるエラーと直し方

* 画面が真っ白：**保存してない／拡張子が .html じゃない**。
* 文字化け：`<meta charset="utf-8">` があるか確認。
* クリックしても動かない：`id`の名前がJSと一致しているか確認。

---

## 次のステップ（発展）

* スマホでも遊びやすい**タッチ操作**対応（`touchstart`）。
* **音**や**効果音**を追加（`<audio>`とJS）。
* スコア保存に**localStorage**を使う。
