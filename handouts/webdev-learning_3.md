---
marp: true
theme: study
paginate: true
style: |
  * {
    font-size: 22px
  }
---

<!-- _class: title -->

# Webアプリ開発勉強会 第3回  
## ～HTML応用編～  
### セマンティックHTML・フォーム（詳しいけど軽め）・メディア要素

---

# 目次

1. `<div>`・`<span>`タグ  
2. セマンティックHTML  
3. フォーム要素（中間詳細）  
4. メディア要素

---

# 1. `<div>`・`<span>`タグ（おさらい）

- `<div>`：
  　ブロックレベルの「ただの箱」。大きな区切りやレイアウトラッパーに使う。  
- `<span>`：
  　インラインの「ただの箱」。文中の一部装飾に使う。  

使い分け：表示の「幅（ブロック/インライン）」で選ぶ。意味があるならセマンティック要素を優先。

```html
<div class="card">
  <h3>タイトル</h3>
  <p>本文… <span class="muted">補足</span></p>
</div>
```

---

# 2. セマンティックHTML（要点）

- 意味（Semantics）を持つ要素を使うと、構造が明確になりSEO・アクセシビリティが上がる。  
- 例：`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`

```html
<header>サイトヘッダー</header>
<nav>メニュー</nav>
<main>
  <article>記事本文</article>
  <aside>サイド情報</aside>
</main>
<footer>著作権等</footer>
```

ポイント：`<main>` は 1 ページに 1 つ。`<article>` は独立して再利用できる塊。

---

# 3. フォーム要素（中間詳細）
## 目的：
## 入力→送信の流れを押さえ、主要属性の意味と実用例を覚える

---

## フォームの基本（復習）

```html
<form action="/submit" method="post">
  <label for="name">名前</label>
  <input id="name" name="name" type="text" placeholder="山田 太郎" required>
  <button type="submit">送信</button>
</form>
```

- `<form>`：入力群をまとめるタグ。`action` と `method` が基本。
- `label` と `id` の対応はアクセシビリティ／操作性向上に必須級。

---

## 主要な属性と「何に使うか」（実務寄り短解説）

| 属性                    | ターゲット    | 役割 / 実例                                        |
| ----------------------- | ------------- | -------------------------------------------------- |
| `action`                | `<form>`      | 送信先URL。例：`/api/contact`                      |
| `method`                | `<form>`      | `get`（検索など） / `post`（送信・更新）           |
| `enctype`               | `<form>`      | ファイル送信なら `multipart/form-data`             |
| `name`                  | 入力要素      | サーバー側で受け取るキー名（例：`name="email"`）   |
| `id`                    | 任意          | ページ内で一意。`label for` と紐付け               |
| `for`                   | `<label>`     | 対応する入力の `id` を指定（クリックでフォーカス） |
| `required`              | 入力要素      | ブラウザに必須入力を要求                           |
| `placeholder`           | 入力要素      | 入力例の表示（値じゃない）                         |
| `pattern`               | 入力要素      | 正規表現で入力形式をチェック                       |

---

## 主要な属性と「何に使うか」（実務寄り短解説）

| 属性                    | ターゲット    | 役割 / 実例                                        |
| ----------------------- | ------------- | -------------------------------------------------- |
| `disabled` / `readonly` | 入力要素      | 無効化 / 読み取り専用（送信挙動注意）              |
| `autocomplete`          | `<form>`/入力 | ブラウザ自動補完の制御（`off` など）               |
| `novalidate`            | `<form>`      | 組み込み検証を無効化（JSでの検証に切替）           |

---

## `label` の使い方（なぜ重要か）

- 明示的結合（推奨）：
```html
<label for="email">メール</label>
<input id="email" name="email" type="email">
```
- ラップ方式（簡潔だが id がない）：
```html
<label>メール <input name="email" type="email"></label>
```
効果：ラベルクリックで入力にフォーカス、スクリーンリーダーが読み上げる。

---

## 入力タイプ別の注意点（代表的なもの）

- `text`：汎用。`maxlength` で長さ制限。  
- `email`：簡易チェックあり（ただしサーバー側でも検証）。  
- `number`：`min`/`max`/`step` を使えるが、文字列挙動に注意。  
- `password`：ブラウザの自動保存振る舞いに留意。`autocomplete`制御可。  
- `file`：ファイル選択。**必ず** `enctype="multipart/form-data"` をフォームに指定。`accept` で許可MIMEを制限できる（提示のみ）。

---

## 選択系（select / radio / checkbox）のポイント

- `select`（プルダウン）は選択肢が多い時に便利。`value` が送信される。
```html
<select name="pref">
  <option value="">選んでください</option>
  <option value="tokyo">東京</option>
</select>
```
- `radio`：同じ `name` を揃えることでグループ化（1つ選択）。  
- `checkbox`：複数選択可。配列で送る場合は `name="hobby[]"` のように扱うことも。

---

## ファイルアップロード例（必須注意点）

```html
<form action="/upload" method="post" enctype="multipart/form-data">
  <label for="avatar">画像</label>
  <input id="avatar" name="avatar" type="file" accept="image/*">
  <button type="submit">アップロード</button>
</form>
```
- `enctype` 忘れずに。  
- サーバーで MIME/type と拡張子を二重確認する（セキュリティ）。

---

## バリデーション（軽く触れる範囲）

- HTMLだけでできる簡易検証：`required` / `type` / `pattern` / `min`/`max` / `minlength`/`maxlength`  
- 実務では：**クライアント検証はユーザービリティ向上用** → サーバーで必ず再検証（セキュリティ）。

例（郵便番号フォーマット）：
```html
<input name="zipcode" pattern="^\d{3}-\d{4}$" title="123-4567 の形式で入力してください">
```

---

## GET と POST の使い分け（要点）

- `GET`：検索やフィルタなど、結果をブックマーク・共有したい場合に使用（URLにクエリが付く）。機密データは不可。  
- `POST`：データ作成・機密情報・ファイル送信に使う。HTTPS と併用。

---

## アクセシビリティの実務ポイント（押さえておきたいもの）

- `label` と `id` を対応させる。  
- グループ（ラジオやチェック）は `fieldset` + `legend` でまとめる。  
- 補助文（例：入力例、エラーメッセージ）は `aria-describedby` で関連付ける。

```html
<input id="email" aria-describedby="emailHelp">
<div id="emailHelp">例：example@mail.com</div>
```

---

## JavaScript と連携するとき

- カスタム検証や非同期送信（fetch / XHR）で UX を向上できる。  
- ブラウザの組み込み検証を無効にするには `<form novalidate>`（ただし代替検証を実装すること）。

---

## まとめ：勉強会で伝えたい“ここだけは”ポイント

1. `label for="id"` と `input id="..."` のペアは必須に近い（操作性とアクセシビリティ）。  
2. `name` がサーバーに送られるキーになる（見落としやすいが重要）。  
3. `enctype` はファイル送信時に必ず指定。  
4. HTML検証は補助。**最終的なデータの検証はサーバーで**。  
5. GET/POST の使い分けを理解しておく。

---

# 4. メディア要素（簡潔）

## 画像とキャプション

```html
<figure>
  <img src="cat.jpg" alt="座っている灰色の猫">
  <figcaption>猫（撮影：2025）</figcaption>
</figure>
```
- `alt` は必須。簡潔で内容を伝えるテキストを。

---

## 音声・動画（ポイント）

```html
<audio controls>
  <source src="sound.mp3" type="audio/mpeg">
</audio>

<video controls width="400">
  <source src="movie.mp4" type="video/mp4">
  <track kind="subtitles" srclang="ja" src="subs-ja.vtt" label="日本語">
</video>
```
- 字幕（`<track>`）でアクセシビリティ向上。

---

## iframe（外部埋め込み）

```html
<iframe src="https://example.com" sandbox="allow-scripts allow-same-origin"></iframe>
```
- `sandbox` で権限制限。必要最低限だけ許可する。

---

<!-- _class: section -->

# 第3回終了（中間詳細版）  
## ご確認ください！
