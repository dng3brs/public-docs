# 開発環境 (Dev Container on wslc)

このプロジェクトは VSCode の Dev Containers を利用して開発環境を構築します。

## 構成

下記内容があらかじめ設定されています。必要に応じて変更を加えてください。

- **ベース OS**: Debian 13 (Trixie) slim版
- **言語**: nodejs, python, java, rust
- **VSCode 機能拡張**:
  - ESLint
  - Prettier

## セットアップ手順 (WSLのインストール）

コンテナ実行環境はwslcを想定しています。バージョンは3.0.1以降が必要です。ディストリビューションは不要です。

```powershell
# WSLのバージョン確認
wsl --version

# 未インストールの場合
wsl --install --no-distribution

# バージョンを更新する場合
wsl --update
```

## セットアップ手順 (コンテナイメージのビルド）

開発環境として使用するコンテナイメージをビルドします。wslc環境でビルド済であればこの手順は不要です。

```powershell
cd .devcontainer\base
wslc build -t base-for-devcontainer:latest .
```
上記とは別に個人固有のセットアップを盛り込んだコンテナイメージをビルドします。wslc環境でビルド済であればこの手順は不要です。

```powershell
# 必ずDockerfileを編集してから実行する
cd .devcontainer\custom
wslc build -t base-for-devcontainer:custom .
```

## セットアップ手順 (Dev Containers拡張機能）

VSCodeですでにセットアップ済の場合は不要です。拡張機能が古い場合はアップデートしたほうがよいです。

1. VSCode Extensions で Dev Containers (ms-vscode-remote.remote-containers) をインストールします。
2. User Settings から `Docker Path` を検索し、設定値を `wslc` に変更します。

## セットアップ手順 (WindowsフォルダをDev Container化する）

1. このテンプレートフォルダをコピーして新しいワークスペースフォルダを作成するか、既存のワークスペースフォルダに`.devcontainer`フォルダをコピーします。
2. `devcontainer.json`に記述されたプロジェクト名（2箇所）を変更してプロジェクト名を付けます。
3. VSCode でワークスペースフォルダを開きます。
4. コマンドパレット (Ctrl+Shift+P) から `Dev Containers: Reopen in Container` を選択します。

## セットアップ手順（追加オプション）

Codex CLIのインストール手順です。

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

コンテナ環境ではbubblewrapが機能しないため、コンテナ自体をサンドボックスとみなしてbubblewrapは無効にします。そのため`~/.codex/config.toml`に下記設定を追記します。


```bash
sandbox_mode = "danger-full-access"
approval_policy = "on-request"
```

## Tips 1

VSCodeのターミナルよりWindowsターミナルの方が挙動が自然です。下記コマンドでWindowsターミナル（PowerShell）からコンテナのシェルに入る方法です。

```PowerShell
wslc exec -it <プロジェクト名(コンテナ名)> bash
```

## Tips 2

wslcもwslと同様にストレージがvhdxファイルとして管理されていて、しばらく運用すると肥大化します。wslcコマンドでセッションを強制終了させたうえで、`%USERPROFILE%\AppData\Local\wslc\sessions\`の配下のフォルダを削除することで、リセットすることができます。ただし、ビルドしたコンテナイメージや使用していたコンテナも削除されるため、再作成の必要があります。

```PowerShell
wslc system session terminate
```

