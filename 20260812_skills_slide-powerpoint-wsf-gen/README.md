# [Agent Skills] スライドの生成

`汎用` `Agent Skills`

## 📋 概要
- コーディングエージェント活用によるスライド（pptx）作成の検討が煮詰まって（手詰まって）きたので一旦まとめる
- 現状のコンセプトは次のスライドの通り

![concept](concept.png)

---

## 🎬 生成させてみた例

- 使用資材は後述
- 手順は、
  - プロンプト１でスライド設計をドキュメント化
  - プロンプト２でAgent Skillsを使いながらwsfやsvgを作成
  - PowerPointで真っ白スライドをアクティブにした状態でwsfを実行
  - レビューしつつ、レイアウト崩れなどを手直し
- 最後のレビューと手直しは必須。一発で納得のいく結果は得られない

→ [生成例1](codex-plugins.pdf)

→ [生成例2](cowork.pdf)

---

## 🛠️ 再現手順

### 前提環境
- **使用ツール：** OpenAI Codex CLI（gpt-5.6-sol medium）
- **環境：** wslc

### 資材説明（エージェント実行時のプロジェクトフォルダに配置）

- [.agents](.agents)フォルダ
  - 手順の中で利用されるAgent Skillsを含む
- [design_template](design_template)フォルダ
  - スライド設計をドキュメント化する際のテンプレートを含む
- [prompts](prompts)フォルダ
  - 手順で使用する2つのプロンプトのひな形を含む
- material-design-icons-wght300-48pxフォルダ
  - プロジェクトフォルダ直下にフォルダを作成し、[Material Symbol のSVGファイル](material-design-icons-wght300-48px/README.md)を格納する
- illust8フォルダ
  - プロジェクトフォルダ直下にフォルダを作成し、[イラストエイトの画像ファイル](illust8/README.md)を格納する
