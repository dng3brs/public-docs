---
name: slide-powerpoint-wsf-gen
description: 指定された要件に従ってPowerPointスライド編集VBScriptスクリプト生成し、指定された .wsf ファイル名で保存します。エージェントがスライドの作成を依頼する場合に使用します。生成するスライドはskillに含まれるスライド作成ガイドラインに則ります。
---

# Slide PowerPoint wsf Generator

ユーザーコンテンツ、レイアウト、サイズ、およびファイル名の要件に基づき、PowerPointスライド編集VBScriptスクリプト(wsfファイル)を作成する。

---

## wsf(vbscript)実装方針

### テンプレート

出力するwsfファイルは下記形式に厳密に則る。

```
<?xml version="1.0" encoding="utf-8" ?>
<package>
<job>
<runtime></runtime>
<script language="VBScript">
<![CDATA[
{ここにvbscriptコードを記述}
]]>
</script>
</job>
</package>
```

### スライド編集後の画像エクスポート処理の実装

VBScriptの最後（スライド編集完了後）に、対象スライドをPNGにエクスポートする。
ファイル名はwsfファイルの拡張子をpngに変更したものとする。

### VBScriptのコーディング規約

下記ルールを厳守する。

1. `CreateObject`の使用は禁止。
2. `GetObject`は起動済PowerPointのオブジェクト取得のみ許可。
   - コード内での使用は、必ず1度だけ`Set ppt = GetObject(, "PowerPoint.Application")`を使用する。
3. 下記に該当するコードは禁止。
   - WScript.Shell
   - Execute
   - ShellExecute
   - Shell.Application
   - Scripting.FileSystemObject
   - ADODB.Stream
   - ExecuteGlobal
   - Eval
   - Application.Run
   - ppt.Run
   - VBE
   - VBProject
   - VBComponents
   - CodeModule
   - CommandBars
4. 外部（インターネットやLAN内の他の環境）へアクセスする処理は禁止。
5. `Loop`,`While`,`For`によるループ処理は禁止。
6. アクティブウィンドウのアクティブスライドに対する編集のみ許可。
   - コード内での使用は、必ず1度だけ`Set slide = ppt.ActiveWindow.View.Slide`を使用する。
   - アクティブスライド以外のスライドを参照する処理は禁止。
   - アクティブスライドの編集操作のみ許可。
   - ファイルの保存やプレゼンテーションなど、編集操作以外の処理は禁止。
7. スライドへの画像の追加は`AddPicture`を使用し、これ以外の外部ファイルへの参照は不可。
8. スライド上にハイパーリングを追加する処理は禁止。
9. `On Error`などエラーハンドリングの処理は実装しない。

---

## 作業手順

1. SVGの設計や作成を行う前に、[スライド作成ガイドライン](references/slide-guideline.md) をすべて読み、スライド作成作業全般に適用する
2. リクエストおよび関連するプロジェクトファイルから、必要なメッセージ、ラベル、関係性、サイズ、ファイル名、出力先ファイルPATHを抽出する。
3. 高確度に推測できない情報は質問する：
   - 指定がない限りスライドのサイズは1920x1080を適用する。
   - 出力先ファイルPATH（ディレクトリ、ファイル名）が不明な場合は、質問する。
   - 出力先ディレクトリが指定されていない場合は、現在のワークスペースに保存する。
4. 描写する内容を検討する
   - 伝えたいメッセージを特定する
   - タイトル、セクション、内容などの構成を検討する
   - レイアウトを決める
5. 指定されたファイル名で直接wsfを書き出す。
   - `.wsf` 拡張子で作成する。
   - ユーザーから要望がない限り、追加の成果物を作成しない。
6. 完了を報告する前に、結果を検証してください：
   - 指定されたパスにファイルが存在することを確認する。
   - `wsf(vbscript)実装方針`に厳密に従っているかを確認する。従っていない点が検出された場合、その内容を報告し、出力ファイル名の拡張子を`.wsf`から`.wsf.txt`に変更する。

---

## 完了報告

生成されたwsfへのファイルPATHを返す。
