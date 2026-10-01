---
title: エディタ
category: エディタ
order: '100'
status: ''
parts: ''
urlstring: table-management-editor
translationKey: table-management-editor
shortname: エディタ
created: 2019-12-05
updated: 2026-02-10
---

## 概要

[テーブルの管理](../index.md)の[エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブでは、レコード編集画面のデザインを行えます。組織のニーズに合わせ、柔軟にレコード編集画面をデザインできます。

[スマートデザイン](../../../users-guide/smart-design/editor/smart-design-editor.md)を使い、ドラッグ操作でレコードをデザインすることもできます。

## 前提条件

1.  「サイトの管理権限」が必要です。

## 操作方法

1.  任意のテーブルを開いてください。
1.  ナビゲーションメニューの「管理」→[テーブルの管理](../index.md)を選択してください。
1.  [エディタ](../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを選択してください。

## 画面構成

### 1. エディタの設定

![エディタタブの「エディタの設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/21f700f556b74409baa18bcc4776b2b8.png)

[エディタの設定](editor-settings/index.md)では、以下の設定を行えます。詳細は[エディタの設定](editor-settings/index.md)をご覧ください。

1.  どのような[項目](editor-settings/columns/index.md)を
1.  レコード編集画面のどこに
1.  どのような順番で
1.  どのような詳細設定を施して配置するか

### 2. その他の項目の設定

![エディタタブの「その他の項目の設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/510e3aa9158e486b8ba598517f6db04b.png)

[エディタの設定](editor-settings/index.md)で設定できる項目以外の項目（[作成者項目](editor-settings/columns/table-management-creator.md)、[更新者項目](editor-settings/columns/table-management-updator.md)、[作成日時項目](editor-settings/columns/table-management-created-time.md)、[更新日時項目](editor-settings/columns/table-management-updated-time.md)）について、細かい設定を行えます。詳細は[その他の項目の設定](other-columns-settings/index.md)をご覧ください。

### 3. タブの設定

![エディタタブの「タブの設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/03723834f7694d9bb6060c18e0a7c3cd.png)

「タブの設定」では[タブ](tab-settings/index.md)の作成と削除、表示順の変更を行えます。[タブ](tab-settings/index.md)は項目を視覚的に分類・整理するための機能です。詳細は[タブ](tab-settings/index.md)をご覧ください。

### 4. 項目連携の設定

![エディタタブの「項目連携の設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/ba9159ab3a624314b0e9f4999971bfc4.png)

[分類項目](editor-settings/columns/table-management-class.md)に親子関係を設定することができます。親の分類項目を選択した場合に、子の分類項目の選択肢が自動で親の分類項目の選択した値に対応したものに切り替わるように設定することができます。詳細は[項目連携](relating-column-settings/index.md)をご覧ください。

### 5. 多言語ラベル設定

[項目の詳細設定：多言語タブ](editor-settings/advanced-settings/multilingual/index.md)の設定情報を、テーブル単位で、CSVファイルとしてインポートまたはエクスポートします。[項目の詳細設定：多言語タブ](editor-settings/advanced-settings/multilingual/index.md)では項目ごとに設定が必要ですが、「多言語ラベル設定」では一括設定が可能です。

![エディタタブの「多言語ラベル設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/58214ac969754229bb52ea22a9133649.png)

本機能の詳細は「多言語ラベル設定」を確認してください。

### 6. レコード制御関係の設定

![エディタタブの「レコード制御関係の設定」欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/assets/96e18a13b6054a8792174e454fca5b87.png)

レコードに関連する処理の制御に関する設定がまとめられています。

| 設定                                           | 概要                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 自動バージョンアップ                           | プリザンターには自動的にレコードの履歴（バージョン）を保存する機能があります。[自動バージョンアップ](automatic-version-upgrade/index.md)では、どのような更新をバージョンアップと見なすかを制御します。<br>詳細は[自動バージョンアップ](automatic-version-upgrade/index.md)をご覧ください。                                                       |
| 作成後の動作                                   | レコード作成後の動作を制御します。<br>詳細は[作成後の動作](after-create-action/index.md)をご覧ください。                                                                                                                                                                                                                                       |
| 更新後の動作                                   | レコード更新後の動作を制御します。<br>詳細は[更新後の動作](after-update-action/index.md)をご覧ください。                                                                                                                                                                                                                                       |
| コメントの編集を許可                           | 一度登録したコメントの再編集を許可します。<br>詳細は[コメントの編集を許可](allow-editing-comments/index.md)をご覧ください。                                                                                                                                                                                                                       |
| コピーを許可                                   | レコードのコピーを許可するかどうかを制御します。<br>詳細は[コピーを許可](allow-copy/index.md)をご覧ください。                                                                                                                                                                                                                           |
| 参照コピーを許可                               | レコードの参照コピーを許可するかどうかを制御します。参照コピーを行うと、新規作成前の状態でデータがコピーされ、必要な情報を変更した後にレコードを作成することができます。<br>詳細は[参照コピーを許可](allow-reference-copy/index.md)をご覧ください。                                                                                     |
| コピー時に追加する文字                         | レコードをコピーする際、タイトルの末尾へ自動的に追加する文字列を設定します。<br>詳細は[コピー時に追加する文字](characters-to-add-when-copying/index.md)をご覧ください。                                                                                                                                                                       |
| 分割を許可                                     | 期限付きテーブルでは、レコードを最大10個に分割することができます。<br>詳細は[分割を許可](allow-separating-record/index.md)をご覧ください。                                                                                                                                                                                                             |
| テーブルのロックを許可                         | テーブルをロックし、レコードを新規登録、更新、削除できなくします。<br>詳細は[テーブルのロックを許可](allow-lock-table/index.md)をご覧ください。                                                                                                                                                                                               |
| リンクを表示しない                             | 画面下部に表示されるリンクの一覧を表示するかどうかを制御できます。<br>詳細は[リンクを表示しない](hide-link/index.md)をご覧ください。                                                                                                                                                                                                    |
| レコードの遷移にAjaxを使用                     | オンにすると、「＜前」、「次＞」ボタンにより、レコード間の遷移をスムーズに行えるようになります。<br>詳細は[レコードの遷移にAjaxを使用](switch-record-with-ajax/index.md)をご覧ください。                                                                                                                                                          |
| 自動ポストバック時にコマンドボタンを切り替える | [プロセス](../../../users-guide/hands-on/advanced/advanced-operations-process.md)で作成したボタンの切り替えのタイミングおよびサーバスクリプト[elements.DisplayType](../../../developers-guide/server-script/elements/server-script-elements-display-type.md)でボタンの表示状態を切り替える際のタイミングを制御します。<br>詳細は[自動ポストバック時にコマンドボタンを切り替える](switch-command-buttons-during-automatic-postback/index.md)をご覧ください。 |
| 削除時に画像を削除                             | レコードの削除時に画像を削除しないように設定します。<br>詳細は[削除時に画像を削除](delete-image-when-deleting/index.md)をご覧ください。                                                                                                                                                                                                 |

## 対応バージョン

| 対応バージョン | 内容                                                                                                         |
| :------------- | :----------------------------------------------------------------------------------------------------------- |
| 1.4.23.0 以降  | [作成後の動作](after-create-action/index.md)、[更新後の動作](after-update-action/index.md)の機能追加 |
| 1.5.1.0 以降   | [多言語ラベルのインポート／エクスポート](multilingual-label-settings/index.md)を追加              |

## 関連情報

-   [テーブルの管理](../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [スマートデザイン：エディタ：操作方法](../../../users-guide/smart-design/editor/smart-design-editor.md)
-   [テーブルの管理：エディタ：エディタの設定](editor-settings/index.md)
-   [テーブルの管理：項目](editor-settings/columns/index.md)
-   [テーブルの管理：項目：作成者](editor-settings/columns/table-management-creator.md)
-   [テーブルの管理：項目：更新者](editor-settings/columns/table-management-updator.md)
-   [テーブルの管理：項目：作成日時](editor-settings/columns/table-management-created-time.md)
-   [テーブルの管理：項目：更新日時](editor-settings/columns/table-management-updated-time.md)
-   [テーブルの管理：エディタ：その他の項目の設定](other-columns-settings/index.md)
-   [テーブルの管理：エディタ：タブ](tab-settings/index.md)
-   [テーブルの管理：項目：分類](editor-settings/columns/table-management-class.md)
-   [テーブルの管理：エディタ：項目連携](relating-column-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：多言語](editor-settings/advanced-settings/multilingual/index.md)
-   [テーブルの管理：エディタ：自動バージョンアップ](automatic-version-upgrade/index.md)
-   [テーブルの管理：エディタ：作成後の動作](after-create-action/index.md)
-   [テーブルの管理：エディタ：更新後の動作](after-update-action/index.md)
-   [テーブルの管理：エディタ：コメントの編集を許可](allow-editing-comments/index.md)
-   [テーブルの管理：エディタ：コピーを許可](allow-copy/index.md)
-   [テーブルの管理：エディタ：参照コピーを許可](allow-reference-copy/index.md)
-   [テーブルの管理：エディタ：コピー時に追加する文字](characters-to-add-when-copying/index.md)
-   [テーブルの管理：エディタ：分割を許可](allow-separating-record/index.md)
-   [テーブルの管理：エディタ：テーブルのロックを許可](allow-lock-table/index.md)
-   [テーブルの管理：エディタ：リンクを表示しない](hide-link/index.md)
-   [テーブルの管理：エディタ：レコードの遷移にAjaxを使用](switch-record-with-ajax/index.md)
-   [応用編：プロセスと状況による制御](../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [開発者ガイド：サーバスクリプト：elements.DisplayType](../../../developers-guide/server-script/elements/server-script-elements-display-type.md)
-   [テーブルの管理：エディタ：自動ポストバック時にコマンドボタンを切り替える](switch-command-buttons-during-automatic-postback/index.md)
-   [テーブルの管理：エディタ：削除時に画像を削除](delete-image-when-deleting/index.md)
-   [テーブルの管理：エディタ：多言語ラベルのインポート／エクスポート](multilingual-label-settings/index.md)
