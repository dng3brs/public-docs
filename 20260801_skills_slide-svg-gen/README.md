# [Agent Skills] スライド向け図解SVGの生成

`汎用` `Agent Skills`

## 📋 概要
- スライドに載せる図解などをAIで生成するのはSVG形式がよさそう
- デザインガイドやMaterial Symbolsなどを含めてAgent Skills化することで、品質や再現性の向上に期待する実験

---

## 🎬 生成させてみた例

Agent SkillsをセットアップしたCodex CLIで指示

プロンプト：
`````
skill $slide-svg-gen を適用し、SVGを作成する。
出力はプロジェクトフォルダに`pdca_diagram.svg`で出力する。
skillの手順やガイドが不十分と感じる点があれば報告する。

作成するSVGの内容：
```
一般的なPDCAサイクルの概念を日本語表記で図式化
```
`````
　↓

![pdca_diagram.svg](pdca_diagram.svg)


---

## 🛠️ 再現手順
### 前提環境
- **使用ツール：** OpenAI Codex CLI（gpt-5.6-sol low）
- **環境：** wslc
### 手順
- [.agents](.agents)フォルダをプロジェクトフォルダに配置（Agent Skills定義を含む）
- プロジェクトフォルダ直下に [material-design-icons-wght300-48px](material-design-icons-wght300-48px) というフォルダを作成し、[Material Symbol のSVGファイル](material-design-icons-wght300-48px/README.md)を格納する
- Codexがスキルを認識していることを確認し、プロンプトを実行