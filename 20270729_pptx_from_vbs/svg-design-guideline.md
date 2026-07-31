# SVG デザインガイドライン

---

# デザイン基本方針

LLMが生成するSVG図解の品質を一貫させることを目的とする。
美しさは目的ではない。
**最も短時間で、最も正確に情報を伝えること**を目的とする。
理解しやすさを最優先する。
装飾より構造を優先する。
独創性より一貫性を重視する。
余白はデザインの一部である。
1枚の図では1つのメッセージのみを伝える。

---

# デザイン構成

## Canvas

作成する前にどちらのサイズを使用するかを質問すること
また、差し込み用途のため、任意のサイズも使用可能とする

### ワイド

| Token | Value |
|--------|------|
| canvas.width | 1600 |
| canvas.height | 900 |
| canvas.margin | 80 |

### 正方形

| Token | Value |
|--------|------|
| canvas.width | 900 |
| canvas.height | 900 |
| canvas.margin | 80 |

---

## Grid

すべての座標・サイズは8pxグリッドに揃える。

| Token | Value |
|--------|------|
| grid.base | 8 |

---

## Spacing

| Token | Value |
|--------|------:|
| space.1 | 8 |
| space.2 | 16 |
| space.3 | 24 |
| space.4 | 32 |
| space.5 | 48 |
| space.6 | 64 |

---

## Radius

| Token | Value |
|--------|------:|
| radius.sm | 4 |
| radius.md | 8 |
| radius.lg | 12 |

---

## Stroke

| Token | Value |
|--------|------:|
| stroke.light | 1 |
| stroke.normal | 2 |
| stroke.bold | 3 |

---

# タイポグラフィ

## Font Family

```css
font-family:
"Noto Sans CJK JP",
Arial,
sans-serif;
```

---

## Font Sizes

フォントサイズは最小16とする

| Token | Size |
|--------|-----:|
| font.title | 32 |
| font.section | 24 |
| font.heading | 20 |
| font.body | 18 |
| font.caption | 16 |

---

## Font Weight

| Usage | Weight |
|--------|-------:|
| Title | 700 |
| Heading | 600 |
| Body | 400–500 |

---

## Rules

### MUST

- 左揃えを基本とする
- タイトルのみ中央揃え可
- 行間は1.3〜1.5
- 縦書き禁止
- 回転文字禁止
- ボックス内は3〜5行以内
- 1行20〜25文字程度を目安とする

---

# 配色

## ブランドカラー

| Name | Value |
|------|------|
| Primary | **#6485C1** |

---

## Semantic Colors

| Purpose | Color |
|---------|-------|
| Success | #5FA56D |
| Warning | #E3A64A |
| Danger | #D96A6A |
| Highlight | #8A6CCF |

---

## Neutral Palette

| Token | Value |
|--------|------|
| Gray900 | #2F343B |
| Gray700 | #5B6470 |
| Gray500 | #8E97A3 |
| Gray300 | #D5DAE2 |
| Gray100 | #F4F6F9 |

---

## Background

| Usage | Color |
|-------|------|
| Canvas | #FFFFFF |
| Section | #F8FAFC |
| Neutral Area | #F4F6F9 |

---

## AS-IS / TO-BE

### AS-IS

- Background: #F4F6F9
- Border: #D5DAE2
- Text: #5B6470

### TO-BE

- Background: #EAF2FF
- Border: #6485C1
- Text: #2F343B

---

## 配色ルール

### MUST

- ブランドカラーを主色とする
- 色は意味を持つ
- 同じ意味には同じ色を使用する
- 色数は最小限
- グラデーションは使用しない
- 彩度の高い原色は使用しない

---

# Shape

## Standard Shape

角丸長方形を標準とする。

- Radius: radius.md

90%以上の要素はこの形状を使用する。

---

## Decision

菱形

用途：

- Yes / No
- 分岐

---

## Container

```
fill: Gray100
stroke: Gray300
```

---

## Stroke

| Usage | Width |
|--------|------:|
| Standard | 2 |
| Secondary | 1 |
| Bold | 3 |

---

## Arrow

- Round linecap
- Round linejoin
- Small arrowhead

---

## Rules

### MUST

- 接続線は交差させない
- 不要な線を描かない
- 影は原則使用しない

---

# アイコン

## Library

Google **Material Symbols Outlined**

```css
font-variation-settings:
'FILL' 0,
'wght' 300,
'GRAD' 0,
'opsz' 24;
```

---

## Size

| Usage | Size |
|--------|-----:|
| Standard | 24 |
| Large | 32 |
| Small | 20 |

16px以下は禁止。

---

## Color

標準

Gray700

強調

Primary

---

## Rules

### MUST

- アイコンは積極的に使用
- アイコンは意味を持つ
- Material Symbols Outlinedのみ使用、独自でアイコンを作成しない

---

# 6. Component Library

## Standard Components

- Title
- Section Header
- Card
- Container
- Badge
- Callout
- Legend
- Divider
- Arrow
- Note

---

# Information Architecture

## MUST

- 主題は1つ
- ボックス1つにつき概念1つ
- 階層は3段まで
- 関係性は「近さ」で表現する
- 矢印は最小限

---

# Layout System

## Flow

- 流れは左→右、上→下の順で配置
- キャンバスの15〜30%は余白として残す。
- 視覚的重心が偏らないよう配置する。

---

# Diagram Pattern Library

推奨パターン

- Process
- Flowchart
- Timeline
- Comparison
- Matrix
- Hierarchy
- Cycle
- Hub & Spoke
- Swimlane
- Architecture
- Before / After
- AS-IS / TO-BE
- Pyramid
- Funnel
- Roadmap

---

# SVG Implementation Rules

### MUST

- viewBoxを設定
- SVG 1.1互換を優先
- グループ化する
- 命名規則を統一する
- text要素は水平配置
- 不要なfilterは使用しない
- 可能な限りシンプルな構造にする

---

# Generation Workflow

SVG生成前に必ず実施する。

## Step 1

伝えたいメッセージを1つ決める。

---

## Step 2

情報を整理する。

- Title
- Section
- Content

---

## Step 3

適切なDiagram Patternを選択する。

---

## Step 4

Layoutを決める。

---

## Step 5

SVGを生成する。

---

## Step 6

Quality Checklistで確認する。

---

# Quality Checklist

## Information

- 主題は1つか
- 階層は3段以内か
- ボックス1つにつき概念1つか

---

## Layout

- 8pxグリッドか
- 余白は十分か
- 線は交差していないか
- 視線誘導は自然か

---

## Typography

- サイズ体系を守っているか
- 左揃えか
- 長文になっていないか

---

## Color

- ブランドカラーを使用しているか
- 色の意味は統一されているか
- 色数は最小限か

---

## Icons

- Material Symbols Outlinedか
- FILL=0か
- Weight=300か

---

## SVG

- viewBoxがあるか
- 不要な要素がないか
- 重なりがないか

---

# 13. NEVER Rules

- 複数の主題を混在させない
- 色だけで意味を伝えない
- 長文をボックスへ入れない
- グラデーションを使用しない
- 接続線を交差させない
- 過剰な装飾をしない
- シャドウを多用しない
- アイコンを装飾目的で使用しない
- 8pxグリッドを崩さない
- 不均一な余白を作らない
- 視線の流れを妨げない

---

# Appendix A – Recommended Material Symbols

推奨カテゴリ

- AI
- Analytics
- Architecture
- Business
- Cloud
- Data
- Database
- Document
- Network
- People
- Process
- Security
- Server
- Settings
- Success
- Timeline
- Warning
- Workflow

---

# Appendix B – SVG Starter Template

```xml
<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 1600 900"
  width="1600"
  height="900">

  <defs>
    <!-- symbols -->
    <!-- markers -->
  </defs>

  <rect
    width="1600"
    height="900"
    fill="#FFFFFF"/>

</svg>
```

