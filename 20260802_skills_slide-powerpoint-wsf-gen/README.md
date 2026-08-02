# [Agent Skills] スライドの生成

`汎用` `Agent Skills`

## 📋 概要
- SVG生成と同様に、VBScriptによるスライドレイアウトのコーディングもAgent Skills化してみる実験

---

## 🎬 生成させてみた例

Codex CLIでgrill-meっぽくチャットすることでスライドの設計書を作成

プロンプト：
`````
スライド作成の要件を整理したいです。
作業中は一貫して`.agents/skills/slide-powerpoint-wsf-gen/references/slide-guideline.md`および`.agents/skills/slide-svg-gen/references/svg-design-guideline.md`内容を念頭に置いてください。
スライドを生成する上で必要となる方針について共通理解に達するまで徹底的に質問してください。
決定ツリーの各枝をたどり、決定事項間の依存関係を一つずつ解決していきましょう。
それぞれの質問に対して、あなたの推奨する回答を提示してください。
一度に複数の質問をすると、混乱を招く可能性があります。
質問は一つずつ行い、それぞれの質問に対する回答を待ってから次の質問に進んでください。
参照可能な情報を調べることで分かる事実であれば、私に尋ねるのではなく、自分で調べてください。
ただし、最終的な決定権は私にあります。一つ一つ私に尋ねて、私の回答をお待ちください。
議論した内容を各タイミングでドキュメント化することを依頼します。それまではドキュメントの編集などは行わないでください。

スライドのテーマ：
```
進化する生成AIと脅威

下記2つの記事は、OpenAIおよびAnthropicの最新モデルによって実社会で引き起こされたセキュリティインシデントを報じています。
これらの記事から、目覚ましい速度で進化する生成AIによって引き起こされる、いままでにない社会へのリスクが懸念されます。
これらを啓蒙するためのスライドです。
https://ledge.ai/articles/openai_hugging_face_security_incident
https://ledge.ai/articles/anthropic_claude_cybersecurity_eval_incidents
```
`````
　　↓

[slide-spec.md](slide-spec.md)

同じCodex CLIセッションで引き続きSVGとWSFを生成

プロンプト：
`````
SVGとWSFを順次作成して
`````

　　↓

5スライド分のwsfとsvgが作成される。  
5枚の真っ白なスライドをPowerPointで開いた状態で、wsfを実行すると、スライドにレイアウトが反映される  
※wsfに記述されているファイルPATHをWindows環境でのPATHに手直しする必要あり

　　↓

[result.pptx](result.pptx)

　　↓

予期しない折り返しでレイアウトがくずれたりが若干あるため、PowerPoint上で補正したり、SVGをInkscapeで補正したりで、スライドを使える状態にする。

　　↓

[result_improved.pptx](result_improved.pptx)

### スライドを生成させてみた所感

- 所要時間
  - AIとの質疑応答でスライド設計を作成するのに40分程度
  - そこからsvgとwsfを生成するのに20分程度
  - 手直しに10分程度
  - 思ったほど短時間ではないけど、質疑応答は考えながらやっているので、仕方がない
- 微妙なところ
  - 表紙の図解が意味不明
  - なぜかSVG描写の上からPowerPointのテキストボックスを配置している → 図解を作成するならテキストもSVGとするようにするほうがよいかも

---

## 🛠️ 再現手順
### 前提環境
- **使用ツール：** OpenAI Codex CLI（gpt-5.6-sol low）
- **環境：** wslc
### 手順
- [.agents](.agents)フォルダをプロジェクトフォルダに配置（2つのAgent Skills定義を含む）
- プロジェクトフォルダ直下に [material-design-icons-wght300-48px](material-design-icons-wght300-48px) というフォルダを作成し、[Material Symbol のSVGファイル](material-design-icons-wght300-48px/README.md)を格納する
- Codexがスキルを認識していることを確認し、プロンプトを実行