---
marp: true
theme: study
paginate: true
---
<!-- _class: title -->

# Webアプリ開発勉強会 第1回
## ～環境構築～

---

# 目次

- [1. Node.jsのインストール](#1-nodejsのインストール)
- [2. pnpmのインストール](#2-pnpmのインストール)
- [3. gitのインストール](#3-gitのインストール)
- [4. VSCodeのインストール](#4-vscodeのインストール)

---

# 1. Node.jsのインストール
Reactを利用する際に必要。

下記公式webサイトからインストーラを取得しインストールする  

https://nodejs.org/ja/download
  
※Node.jsのパッケージ管理ツールである`npm`は自動的にインストールされる

---

# 2. pnpmのインストール

npmを利用してインストールする  
（基本的には`npm`でもよいが、多くのプロジェクトで**node_modules**を利用するなら、  
パッケージの再利用を適切に行ってくれる`pnpm`の方がよい。）

```powershell
npm install -g pnpm
```

---

# 3. gitのインストール

作成したファイルのバージョン管理（履歴を残しておく感じ）をするためのツールである**git**をインストールする。  
下記の公式webサイトから入手する。  

https://git-scm.com/

---

# 4. VSCodeのインストール
下記公式webサイトからインストールする  

https://code.visualstudio.com/

  
※Microsoft Storeからでもよいが、公式サイトのやつの方がなんか好き（？）

---

## 4-1-1. VSCode拡張機能をインストール

<div class="h-small">必須</div>

- **Prettier**：  
  　コードをフォーマットしてくれる
- **TypeScript Extension Pack**：  
  　TypeScriptまわりの拡張機能をまとめて導入できる
- **ESLint**：  
  　ESLintをVSCodeで利用できるようにする
- **git**：
  　ファイルのバージョン管理ツールをVSCodeで利用できるようにする


---

## 4-1-2. VSCode拡張機能をインストール

<div class="h-small">推奨</div>

- **HTML CSS Support**：  
  　HTML、CSSの入力補間などを行ってくれる
- **Node.js Modules Intellisense**：  
  　Node.jsのモジュールを補完してくれる

---

## 5. gitアカウントを設定する（VSCode）

VSCode内にあるアカウント（Accounts）ボタンから、Gitアカウントを追加する。
<!-- ここは適宜加筆してください -->

---

## 6. gitアカウントを設定する（コマンドライン）

コマンドラインから、下記コマンドを実行する。
`--global`オプションをつけると、ユーザ全体でアカウント情報が設定される。

```bash
git config --global user.name "ユーザー名"
git config --global user.email "メールアドレス"
```
※オプションの詳細については以下を参考にすると良い
https://tech-broccoli.life/articles/engineer/gitconfig-level/

---

<!-- _class: section -->

### **これでひとまずは環境構築終わりです。**
### **次回からコードを書いていきます。お楽しみに。**


