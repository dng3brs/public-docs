# [環境] WSL コンテナ（wslc）を利用した Dev Container

`Dev Container` `開発`

## 📋 概要
- [wslc]() を利用して Dev Container 環境を構築する

---

## 🛠️ 再現手順
### 前提環境
- **使用ツール：** VSCode, WSL
- **環境：** Windows

### wslc のインストール

[wslc]() を参照

### Dev Container 拡張機能のインストール

- VSCode で拡張機能の [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) をインストールする
- インストール後、`pre-release`版にアップデートする

### Dev Containers が使用する docker コマンドを wslc に変更

- VSCodeのコマンドパレット `Ctrl + Shift + P` で `Preferences: Open User Settings`を実行し、`dev.containers.dockerPath` の設定値を `docker` から `wslc` に変更する

### プロジェクトフォルダを作成

### プロジェクトフォルダに `.devcontainer` フォルダを作成し、`Dockerfile` と `devcontainer.json` を格納する

### VSCode で プロジェクトフォルダを Dev Containerで開く
- VSCodeでプロジェクトフォルダを開く
- `Reopen in Container` を実行する → コンテナがビルドされ、コンテナ環境でVSCodeが操作可能となる