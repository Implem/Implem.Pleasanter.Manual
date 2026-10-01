---
title: リッチテキストエディタ
category: 共通機能
order: '1'
status: ''
parts: ''
urlstring: richtexteditor
translationKey: richtexteditor
shortname: リッチテキストエディタ
created: 2025-08-18
updated: 2026-08-12
---

## 概要

[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)と[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)では、**リッチテキストエディタ**を使用できます。リッチテキストエディタを使用すると[マークダウン](markdown.md)よりも柔軟にテキスト、画像、テーブルを扱えます。ワードプロセッサなどから、一定の書式を維持した状態でコピー、貼り付けることもできます。

### 長所と短所

リッチテキストエディタの利用を始める前に、[マークダウン](markdown.md)と比べたときの長所・短所を把握しておきましょう。

| スタイル | 長所 | 短所 |
|:--|:--|:--|
| マークダウン | フィルタやソート機能を問題なく使える | 特殊な記法を覚える必要がある |
| リッチテキストエディタ | 特殊な記法を覚えずに使える | フィルタやソート機能を意図通りに使えなくなる可能性がある |

[マークダウン](markdown.md)との主な違いを下図にまとめます。

![リッチテキストエディタとマークダウンの長所と短所をまとめた図](https://pleasanter.org/files/images/ja/users-guide/common/assets/f726a71088ba41298698d14af13ea276.png)

## 制限事項

1. [内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)や[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)のスタイルとして「リッチテキストエディタ」を選択した場合、各項目の[エディタ](../table/record-authoring/edit-records/table-editor.md)の詳細設定で行える以下の設定が無効となります（無視されます）。

   1. [配置](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-textalign.md)
   2. [最大文字数](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-maxlength.md)
   3. [ビュワー切替](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-change-viewer.md)
   4. [サムネイルサイズ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-thumbnail.md)

1. リッチテキストエディタには、フォントを切り替える機能が含まれますが、この機能で使用できるのはユーザ環境（OS）にインストール済みのフォントに限られます。[詳細ページ](richtexteditor-detail.md)も併せてご覧ください。また、使用するフォントのカスタマイズはオンプレミス環境でのみご利用いただけます。
1. リッチテキストエディタは[一覧編集](../table/record-authoring/edit-records/table-record-editongrid.md)画面での編集に対応していません。

## 前提条件

リッチテキストエディタを有効化するには「[サイトの管理権限](../access-control/access-controls.md)」が必要です。

## いつ内容項目や説明項目のスタイルを決めれば良いか

[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)や[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)のスタイル（ノーマル、ワイド、マークダウン、リッチテキストエディタ）機能は、以下の流れで使用することを想定しています。
**レコード作成後にスタイルを変更した場合、設定した書式は失われます。**

1. テーブルを作成します。
2. 内容項目のスタイルを決定します。
3. 説明項目を使用するかどうかを決定します。
4. 説明項目のスタイルを決定します。
5. レコードを新規作成します。

## 内容項目や説明項目のスタイルの決め方

リッチテキストエディタは[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)や[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)に局所限定的なHTMLを持ち込むことで実現しています。

以下の制約を許容できない場合は、マークダウンなど、ほかのスタイルをご利用ください。

1. フィルタ機能が意図通り機能しないことがあります。
2. ソート機能が意図通り機能しないことがあります。
3. CSVエクスポートや、サイトパッケージのエクスポートもHTML文書として行われます。

## リッチテキストエディタを有効化する

リッチテキストエディタを有効化するには、以下の2つの方法があります。

1. スマートデザインを使う方法
1. テーブルの管理画面のエディタタブを使う方法

### 1. スマートデザインを使う方法

「[スマートデザイン：エディタ：基本項目：内容](../smart-design/editor/smart-design-editor-body.md)」や「[スマートデザイン：エディタ：追加項目：説明](../smart-design/editor/smart-design-editor-description.md)」をご覧ください。

### 2. テーブルの管理画面のエディタタブを使う方法

以下では、[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)でリッチテキストエディタを有効化する手順を紹介します。[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)でも同様の手順でリッチテキストエディタを有効化できます。

なお、[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)が「現在の設定」リストにない場合は、「エディタの項目の設定」を参考に[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)を有効化してください。

1. 対象のテーブルを開いてください。
1. 「管理」メニューから[テーブルの管理](../../managers-guide/manage-table/index.md)をクリックしてください。
1. [エディタ](../table/record-authoring/edit-records/table-editor.md)タブをクリックしてください。
1. 「現在の設定」のリストから対象の[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)を選択し、「詳細設定」ボタンをクリックしてください。
1. [内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)の「詳細設定」画面が開きます。
1. スタイルからリッチテキストエディタを選択してください。
   ![テーブルの管理のエディタタブで、スタイルにリッチテキストエディタを選んだ画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/54304ef4c3594b4e887be5f41a58f272.png)
1. 「変更」ボタンをクリックし、「詳細設定」画面を閉じてください。
1. 「更新」ボタンをクリックしてください。
1.  レコードを新規作成すると[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)にリッチテキストエディタのツールバーが表示されます。

## ツールバー

[内容項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)または[説明項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)の先頭に表示されるツールバーには、次のようなボタンが並んでいます。

![リッチテキストエディタのツールバー](https://pleasanter.org/files/images/ja/users-guide/common/assets/ba96907090bf492f8fb95c8dd3d31967.png)

各ボタンの概要、対応するショートカットは次の通りです。macOSをお使いの場合は、CTRLをCommandと読み替えてください。

| 名前                 | 概要                                                                                                               | ショートカット           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------------------ |
| 元に戻す             | 操作前の状態に戻します。                                                                                           | CTRL＋Z                  |
| 再実行               | 操作後の状態にします。                                                                                             | CTRL＋Y / CTRL＋SHIFT＋Z |
| フォント             | 選択した文字列のフォントを変更します。                                                                             | －                       |
| サイズ               | 選択した文字列の文字サイズを変更します。                                                                           | －                       |
| 段落形式             | カーソルを置いた段落に対して、9種類の段落形式（書式）を設定します。                                                | －                       |
| 太字                 | 選択した文字列を太字にします。                                                                                     | CTRL＋B                  |
| 下線                 | 選択した文字列に下線を追加します。                                                                                 | CTRL＋U                  |
| 斜体                 | 選択した文字列を斜体にします。                                                                                     | CTRL＋I                  |
| 取り消し線           | 選択した文字列に取り消し線を追加します。                                                                           | CTRL＋SHIFT＋S           |
| 下付き               | 選択した文字列を上付きにします。                                                                                   | －                       |
| 上付き               | 選択した文字列を下付きにします。                                                                                   | －                       |
| 文字色               | 選択した文字列に好きな文字色を付けられます。ボタンをクリックすると、カラーパレットが表示されます。                 | －                       |
| 文字の背景色         | 選択した文字列に好きな背景色を付けられます。ボタンをクリックすると、カラーパレットが表示されます。                 | －                       |
| テキストスタイル     | 選択した文字列に3種類のスタイル（書式）を設定します。                                                              | －                       |
| 形式を削除           | 「段落形式」以外の書式を削除します。                                                                               | －                       |
| ブロック表示         | ブロックの可視・不可視を切り替えます。リッチテキストエディタで思うように編集できなくなってしまったときに便利です。 | －                       |
| インデント（左側）   | カーソルを置いた段落を、右へインデントします。ボタンを押すたびに、インデントは深くなります。                       | CTRL＋[                  |
| インデント（右側）   | カーソルを置いた段落を、左へインデントします。ボタンを押すたびに、インデントは浅くなります。                       | CTRL＋]                  |
| ソート               | カーソルを置いた段落の行揃えを変更します。                                                                         | －                       |
| 水平線を挿入         | カーソル位置に横幅いっぱいの水平線を挿入します。                                                                   | －                       |
| リスト               | リスト（箇条書き）の形式（順序なし、順序付き）を選択します。                                                       | －                       |
| 行の高さ             | 選択した行の間隔を選択します。                                                                                     | －                       |
| テーブル             | カーソル位置に最大10行×10列のテーブルを挿入します。                                                               | －                       |
| リンク               | クリックすると、リンクの挿入画面が開き、現在のカーソル位置へリンクを挿入できます。                               | －                       |
| 画像                 | クリックすると、画像の挿入画面が開き、現在のカーソル位置へ画像（**PNG**、**JPEG**、**GIF**）を挿入できます。                                   | －                       |
| 編集モードの切り替え | クリックでON（編集モード）とOFF（閲覧モード）とを切り替えられます。ON（編集モード）のときに、項目を編集できます。  | －                       |

各ボタンの詳細については[共通機能：リッチテキストエディタ：ツールの詳細](richtexteditor-detail.md)を参照してください。

## 対応バージョン

| 対応バージョン | 内容 |
| --- | --- |
| 1.4.20.0以降 | 機能追加 |

## 関連情報

-   [テーブルの管理：項目：内容](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テーブルの管理：項目：説明](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [共通機能：マークダウン](markdown.md)
-   [テーブル機能：レコードのエディタ画面](../table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：配置](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-textalign.md)
-   [テーブルの管理：エディタ：項目の詳細設定：最大文字数](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-maxlength.md)
-   [テーブルの管理：エディタ：項目の詳細設定：ビュワー切替](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-change-viewer.md)
-   [テーブルの管理：エディタ：項目の詳細設定：サムネイルサイズ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-thumbnail.md)
-   [共通機能：リッチテキストエディタ：ツールの詳細](richtexteditor-detail.md)
-   [テーブル機能：レコードの一覧編集](../table/record-authoring/edit-records/table-record-editongrid.md)
-   [アクセス制御の概要](../access-control/access-controls.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)