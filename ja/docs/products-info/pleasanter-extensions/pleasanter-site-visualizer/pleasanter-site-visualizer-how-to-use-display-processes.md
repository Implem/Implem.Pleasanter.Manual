---
title: プロセス図表示
category: Pleasanter Site Visualizer
order: '0'
status: ''
parts: ''
urlstring: pleasanter-site-visualizer-how-to-use-display-processes
translationKey: pleasanter-site-visualizer-how-to-use-display-processes
shortname: プロセス図表示
created: 2026-04-21
updated: 2026-05-18
---

## 概要

[Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)のプロセス可視化機能について説明します。ログイン中のプリザンターのサイトに設定されたプロセス（状況の遷移・ボタン・データ変更・通知・権限など）を、フロー図とプロセス図の2種類で可視化します。

### Pleasanter Site Visualizerにおけるプロセス可視化

プロセスは、テーブルのエディタ画面に表示されるボタンに関連付けられ、クリック時の状況の変更やデータ変更、通知などを定義する機能です。本画面では以下の2つの表現でプロセス構成を可視化します。

1. **フロー図**:  
   状況を表す四角（ノード）と遷移を表す矢印（エッジ）で、状況の遷移を確認できます。
1. **プロセス図**:  
   遷移元の状況を縦軸、遷移先の状況を横軸としたスイムレーン図のような形式でプロセスを表示します。ボタンの全体像と関係性を確認できます。

画面は「左パネル（プロセス選択）」「フロー図」「プロセス図」の3ブロックで構成されます。フロー図とプロセス図は上下 2 段に並べて表示されます。

![プロセス画面の全体構成。左パネル、フロー図、プロセス図の3ブロックからなる](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/e3dd99586dd141a087f5597b6c4fdd80.png)

各ブロックの役割は以下のとおりです。

| No | ブロック | 役割 |
| :-: | --- | --- |
| 1 | 左パネル（プロセス選択） | 設定されたプロセスの一覧から、表示対象を切り替えます。（詳細は[2-1](#pr21)参照） |
| 2 | フロー図（上段） | 状況を表す四角と遷移を表す矢印で、状況間の遷移方向や遷移条件を確認できます。（詳細は[2-2](#pr22)参照） |
| 3 | プロセス図（下段） | 遷移元の状況を縦軸、遷移先の状況を横軸としたスイムレーン図のような形式でプロセスを表示し、ボタンの全体像と関係性を確認できます。（詳細は[2-2](#pr22)参照） |

左パネルでは、各プロセスが「プロセスパネル」と呼ぶカード形式で一覧表示されます。プロセスパネルの表示例と、各要素の意味は以下のとおりです。

![左パネルに並ぶプロセスパネルの表示例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/e7898f9fcb1142edb1552c0e1cee26db.png)

| No | 要素 | 説明 |
| :-: | --- | --- |
| 1 | プロセス名 | プロセスの表示名（未設定時は名称、いずれも未設定時はID）を表示します。 |
| 2 | チェックボックス | プロセスをフロー図・プロセス図に表示するかを切り替えます。 |
| 3 | 遷移元 → 遷移先 | プロセスの「現在の状況」→「変更後の状況」を表示します。括弧内は状況値（ID）です。 |
| 4 | 通知アイコン | プロセスに通知設定がある場合に表示されます。右側の数字は件数で、ツールチップで内容を確認できます。 |
| 5 | 権限アイコン | プロセスにアクセス制御（グループ／組織／ユーザ）設定がある場合に表示されます。右側の数字は件数です。 |
| 6 | ⓘアイコン | クリックするとプロセスの詳細モーダルが開きます（[3-1](#pr31)参照）。 |

## 制限事項

1. フロー図とプロセス図はテーブル内の情報に基づき自動描画されます。そのため、ユーザがオブジェクトや矢印の描画位置を制御することはできません。
1. プロセス図において前進処理と後退処理を同時に描画させた場合、表示項目数が増え、情報の把握が困難になる場合があります。目的に応じて表示範囲を絞り込んでください。

## 前提条件

1. 「サイトの管理権限」が必要です。

## 1. 操作手順（ポップアップ表示）

1. サイトの管理者権限のあるユーザでログインします。
1. プロセスを確認したいサイトに移動します。
1. [Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)ブラウザ拡張アイコンをクリックします。

    | アイコン状態 | 説明 |
    |--|--|
    | ![操作可能なことを示す青色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/e5e085f9031e414fa4834ec4b0f61242.png)| 青色アイコン時は操作が可能です。 |
    | ![操作できないことを示す灰色の Pleasanter Site Visualizer 拡張アイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/d98808bc72d94ab09ea5b3ed2c440f79.png)| 灰色アイコン時は操作が不可能です。（ログインしていない、またはサイト管理が開けないページを開いている場合にこの状態となります。） |

1. [Pleasanter Site Visualizer](pleasanter-site-visualizer-how-to-use-sites.md)の操作画面が表示されます。

    ![Pleasanter Site Visualizer の操作画面](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/a2961ee3d2d54b0ebf2634e36252405a.png)

## 2. 操作手順（画面を表示）

1. 「プロセスのワークフローを確認する」の「画面を表示」をクリックします。

    ![操作画面の「プロセスのワークフローを確認する」にある「画面を表示」ボタン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/b8e0136142024fb79b9b2daa544e91c0.png)
1. 「プロセス画面」が開きます。画面上部のドロップダウンリストで[テーブル](../../../users-guide/table/index.md)を切り替えて表示できます。

    ![開いたプロセス画面。上部にテーブルを切り替えるドロップダウンリストがある](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/f71a6894b3cb4ff4a2b0fdb69d8e12e0.png)

<a id="pr21"></a>

### 2-1. 左パネル（プロセス選択）

設定されたプロセスの一覧が表示されます。プロセスパネルのチェックをオン・オフすることで、プロセス図への表示・非表示を切り替えられます。

![プロセス画面の左パネル。プロセス一覧と絞り込み・選択のボタンが並ぶ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/d457eacb76b745b5b51ba8ddd539fdc8.png)

| 要素 | 機能 |
|---|---|
| 「キーワードで絞り込み」テキストボックス | プロセス名でプロセスを絞り込みます。 |
| 「すべて選択」ボタン | 全プロセスを表示対象にします。 |
| 「すべて解除」ボタン | 全プロセスを非表示にします。 |
| 「初期状態に戻す」ボタン | 前進遷移のみ選択した初期状態に戻します。 |

#### デフォルトのプロセス選択状態について

変更後の状況の値が変更前の状況の値より大きいプロセス（前進遷移）だけが選択されています。後退遷移・自己遷移は未選択です。

<a id="pr22"></a>

### 2-2. フロー図・プロセス図

画面右側にはフロー図とプロセス図が上下2段で表示されます。

- **上段: フロー図（通常表示）** — 状況と遷移の矢印で遷移関係を表示します。矢印の向きで遷移方向を表し、前進遷移は**青い実線**、後退遷移・自己遷移は**赤い破線**で表示されます。左パネルで選択中のプロセスが24件を超えた場合、同じ遷移元・遷移先の組み合わせをもつ複数の矢印が1本に集約され、ラベルが「N件」と表示されます。なお 24 件のしきい値は本機能内の固定値で、変更はできません。

    ![上段のフロー図。状況を表す四角と遷移を表す矢印で構成される](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/f597cc22050b4b5f919182028559bb41.png)

- **下段: プロセス図** — 遷移元の状況を縦軸、遷移先の状況を横軸としたスイムレーン図のような形式でプロセスを表示します。

    ![下段のプロセス図。遷移元を縦軸、遷移先を横軸に並べた形式](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/35b3a16ec67a4842a131b46642b789ff.png)

各図に配置されているボタンについての説明は、下記の表のとおりです。

| アイコン | ボタン名 | 配置 | 機能 |
|:--|:--|:--|:--|
| ![「全体表示」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/28614728702243bf8a711168ab85bc31.png) | 全体表示 | 上段 | フロー図を「全体表示モーダル」で拡大表示します（[下記](#full-view)参照）。 |
| ![「フロー図MMD保存」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/01a9d335518d49aa9e467b460402b56b.png) | フロー図MMD保存 | 上段 | フロー図を Mermaid 形式（.mmd）のテキストファイルとしてダウンロードします（[下記](#mmd-output)参照）。 |
| ![「フロー図PNG保存」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/0914144d264d4f39b8208897db57d95e.png) | フロー図PNG保存 | 上段 | フロー図を PNG 画像としてダウンロードします（[下記](#png-output)参照）。 |
| ![「プロセス図PNG保存」ボタンのアイコン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/0914144d264d4f39b8208897db57d95e.png) | プロセス図PNG保存 | 下段 | プロセス図を PNG 画像としてダウンロードします（[下記](#png-output)参照）。 |

<a id="full-view"></a>

### 「全体表示モーダル」

フロー図の「全体表示」アイコンをクリックすると、フロー図全体表示モーダルが開きます。全体表示モーダルでは集約なしにすべての矢印が個別に表示されます。

![フロー図の全体表示モーダル。すべての矢印が個別に表示される](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/d9c874d6fe3d4dbabbe2f13457c6c3f6.png)

<a id="mmd-output"></a>

### 「MMDテキスト出力」ダイアログ

「フロー図MMD保存」ボタンをクリックすると、MMDテキスト出力ダイアログが開きます。

![フロー図の「MMDテキスト出力」ダイアログ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/6ecf9e31ecd74f56b0288ec597bb096c.png)

| オプション | 効果 |
|---|---|
| 図全体を出力する | プロセスが24件を超える場合でも、すべての矢印を含む .mmd ファイルを出力します。 |

ダウンロードした.mmdファイルは、[Mermaid Live Editor](https://mermaid.live/) などでプレビューできるほか、Markdown ドキュメントにコードブロックとして埋め込むなどして活用できます。

<a id="png-output"></a>

### 「PNG画像出力」ダイアログ

「フロー図PNG保存」および「プロセス図PNG保存」ボタンをクリックすると、PNG画像出力ダイアログが開きます。

![プロセス画面の「PNG画像出力」ダイアログ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/1468a1f897324d35b9ab844ee2d9850c.png)

このダイアログでは、出力する PNG 画像の縦横サイズを指定できます。

| オプション | 効果 |
|---|---|
| 「幅(px)」「高さ(px)」 | 出力サイズを指定します。数字以外の値や空欄を入力した場合は初期値が適用されます。 |
| 「アスペクト比を維持」にチェック | 縦横比を保持して片方を変更するともう一方が自動計算されます。 |
| 「図全体を出力する」にチェック（フロー図のみ） | プロセスが24件を超える場合でも、すべての矢印を含む .png ファイルを出力します。 |

サイズが極端に大きい場合はエラーメッセージが表示され、画像生成は実行されません。

![出力サイズが大きすぎるときに表示されるエラーメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/87e5daf642c742439503a942b66968f2.png)

## 3. 操作手順（詳細表示）

プロセスの詳細情報をモーダルで表示できます。

<a id="pr31"></a>

### 3-1. 詳細表示のトリガー

以下のいずれかの操作で詳細モーダルが開きます。

1. プロセス図上のプロセスボタンをクリック
1. 左パネルのプロセス名の ⓘ アイコンをクリック

### 3-2. 詳細モーダルの内容

詳細モーダルはプロセスの設定内容に基づき、以下のセクションを表示します。

![プロセスの詳細モーダル](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/31a8913baea040c08193f5a7c09d5f9a.png)

| セクション | 内容 |
|---|---|
| 全般 | プロセス基本情報（ID / 名称 / 表示名 / 画面種別 / 現在の状況 / 変更後の状況 / 説明 / ツールチップ / アイコン / 確認メッセージ / 成功メッセージ / クリック時の動作 / 実行種別 / アクション種別 / 状態変更後の動作 / 一括処理を許可） |
| 入力検証 | プロセス実行時の入力検証ルール |
| 条件 | プロセス実行条件（未完了 / 自分 / 期限が近い / 遅延 / 期限超過 / 検索 / 項目一覧） |
| データの変更 | プロセス実行時のデータ変更ルール（変更種別 / コピー元 / 値 / 計算式 / 基準日時 / 期間 など） |
| 自動採番 | 自動採番設定（書式 / リセット種別 / 既定値 / ステップ） |
| 通知 | 通知設定（通知種別 / 件名 / アドレス / Cc / Bcc / トークン / 内容） |
| アクセス制御 | 権限設定（グループ / 組織 / ユーザ） |

設定値は日本語のラベルに変換されて表示されます（例: 画面種別は「編集」、通知種別は「メール」のように表示）。

## 4. 複数サイトの切り替え

ポップアップ画面の「オプション項目」で「サイトID」に複数の ID を指定、または「サイトグループ名」にサイトグループ名を指定した状態で「画面を表示」を実行すると、画面上部のサイトセレクタ（ドロップダウン）から表示対象のサイトを切り替えられます。

![プロセス画面上部のサイトセレクタのドロップダウン](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/55e81e2cfdad47e2ab5b7ffe934fafca.png)

![サイトセレクタで表示対象のサイトを切り替えた状態](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-site-visualizer/assets/a3d4f2fe66e14360b7a6bf0d628afa9c.png)

- 記録テーブル・期限付きテーブル以外のテーブル（Wiki など）はセレクタに表示されません。
- 「サイトの管理権限」がない場合には、ドロップダウンメニューに表示されません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|プリザンター1.5.4.0以降|新規作成|

## 関連情報

-   [Pleasanter Site Visualizer：使い方：サイト設定表示](pleasanter-site-visualizer-how-to-use-sites.md)
-   [テーブル機能](../../../users-guide/table/index.md)
-   [Mermaid Live Editor](https://mermaid.live/)
