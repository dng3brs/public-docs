# [MCP] Codex CLI で Computer Use

`MCP` `Computer Use`

## 📋 概要

- Codex CLIにWindows操作とブラウザ操作それぞれに特化したMCPをセットアップしてComputer Use Agent(CUA)にしてみる
- デバイス認証のようにブラウザのログイン過程でデスクトップアプリも操作するような挙動を期待
- 全く問題なく動作した

---

## 🎬 生成させてみた例

### CUAにさせたいこと

![1-usecase.png](1-usecase.png)

### CUAに操作させるサンプルアプリ

#### ログイン時にデスクトップアプリが開いて「ログイン」ボタンをクリックする必要がある(playwrightでは操作不可)

![2-target.png](2-target.png)

#### 経費の登録と一覧表示を行う画面を持つ

![2-target-2.png](2-target-2.png)

### Codex CLIに`windows-mcp`と`playwright-mcp`を設定

![3-config.png](3-config.png)

### [AGENTS.md](AGENTS.md)に前提情報を記述

![4-instruction.png](4-instruction.png)

### プロンプトの実行結果（ちゃんと指示したことを完遂！すごい！）

![5-result.png](5-result.png)

### 料金はトークン数でAPI単価で計算すると0.3ドル弱（45円くらい）

![6-cost.png](6-cost.png)

---

## 🛠️ 再現手順

### 前提環境

- **使用ツール：** OpenAI Codex CLI（gpt-6.1-sol low）
- **環境：** Windows11

### MCPの設定やプロンプトは上記スクリーンショットなど参照
