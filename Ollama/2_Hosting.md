# Raspberry Pi 5で「Ollama × Webクライアント」（ローカル利用）

### ゴール

* ブラウザ（Pi本体 or 同一LAN端末）から、**yuiseki/sarashina2.2:1b** を呼び出して返答を表示できるようにします。
* Webページは **lighttpd** で配信し、ページから **Ollama API**（ポート11434）を直接叩きます。

---

## 0. 事前準備（モデルの取得）

```bash
ollama pull yuiseki/sarashina2.2:1b
# 既定で API は 127.0.0.1:11434（localhost）で待機
```

---

## 1. Webサーバ（lighttpd）の用意

```bash
sudo apt update
sudo apt install -y lighttpd
sudo systemctl enable --now lighttpd
sudo systemctl status lighttpd   # Active: active (running) が出ればOK
```

配信フォルダは `/var/www/html/` です。
動作確認（Hello表示）：

```bash
echo "<h1>Hello Raspberry Pi!</h1>" | sudo tee /var/www/html/index.html
# Pi本体のブラウザで http://localhost/ を開く
```

（任意）ポート変更したい場合は `server.port = 8080` などを設定：

```bash
sudo nano /etc/lighttpd/lighttpd.conf
# server.port = 8080
sudo systemctl restart lighttpd
```

---

## 2. CORSを許可（ページ→Ollama APIへのアクセス許可）

ページ（[http://localhost](http://localhost) や http\://\<PiのIP>）から **http\://<ホスト>:11434** を呼ぶため、Ollamaに**許可オリジン**を設定します。

```bash
# 1) PiのIPをメモ（例：192.168.1.23）
hostname -I
# 2) systemd のドロップインを作成/編集
sudo systemctl edit ollama.service
```

エディタで以下を追加（\<PiのIP> は置き換えてください）：

```ini
[Service]
Environment="OLLAMA_ORIGINS=http://localhost,http://127.0.0.1,http://<PiのIP>"
```

> ※ lighttpd のポートを 8080 に変えた場合は
> `http://localhost:8080,http://<PiのIP>:8080` もカンマ区切りで追加してください。

反映：

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

### （必要な人だけ）LAN内の他端末からも使いたい場合

OllamaをLANから受けられるようにします。

```bash
sudo systemctl edit ollama.service
```

追記：

```ini
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

反映：

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

---

## 3. シングルHTML（完成品）を配置

同梱している **`index.html`** の中身を、`/var/www/html/` の`index.html`へコピーします。

---

## 4. 使い方

* **Pi本体のブラウザ**で開く：
  `http://localhost/` を開く → そのまま送信（Endpoint は自動で `http://localhost:11434/api` が入ります）
* **同一LANの別端末**で開く：
  `http://<PiのIP>/` を開く → Endpoint が自動で `http://<PiのIP>:11434/api` になります
  （※ その場合は事前に「2. CORS」「LAN利用の設定」を済ませてください）

---

## 5. 動作チェック（例）

1. Model：`yuiseki/sarashina2.2:1b`（初期値のまま）
2. Prompt：`こんにちは。自己紹介してください。`
3. 送信 → 出力に返答が出ればOK

---

## 6. よくあるつまずき（チェックリスト）

* **CORSエラー**が出る
  → `sudo systemctl edit ollama.service` で
  `Environment="OLLAMA_ORIGINS=..."` に **実際のページのOrigin**（`http://localhost` / `http://<PiのIP>` / 必要なら `:8080` 付き）を入れたか確認 → 再起動

  ```bash
  sudo systemctl daemon-reload
  sudo systemctl restart ollama
  ```
* **Failed to fetch** や接続できない
  → Endpoint のスペル/ポート（`:11434`）を確認
  → `systemctl status ollama` でOllamaが起動しているか確認
  → LANから使う場合は `Environment="OLLAMA_HOST=0.0.0.0:11434"` を設定済みか確認
* **モデルが見つからない**
  → `ollama pull yuiseki/sarashina2.2:1b` をもう一度実行
* **PiのIPがわからない**
  → `hostname -I` で確認

---

## 7. 最後に（チートシート）

| 項目          | コマンド/場所                                                                         |
| ----------- | ------------------------------------------------------------------------------- |
| モデル取得       | `ollama pull yuiseki/sarashina2.2:1b`                                           |
| Web配信フォルダ   | `/var/www/html/`                                                                |
| テスト表示       | `http://localhost/`                                                             |
| Ollama API  | デフォルト `127.0.0.1:11434`                                                         |
| CORS許可      | `Environment="OLLAMA_ORIGINS=http://localhost,http://127.0.0.1,http://<PiのIP>"` |
| LANからAPI受ける | `Environment="OLLAMA_HOST=0.0.0.0:11434"`                                       |
| 再読み込み       | `sudo systemctl daemon-reload && sudo systemctl restart ollama`                 |
