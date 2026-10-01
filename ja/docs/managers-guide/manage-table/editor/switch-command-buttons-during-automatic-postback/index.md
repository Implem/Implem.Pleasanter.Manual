---
title: 自動ポストバック時にコマンドボタンを切り替える
category: エディタ
order: '24000'
status: ''
parts: ''
urlstring: table-management-change-commandbutton
translationKey: table-management-change-commandbutton
shortname: 自動ポストバック時にコマンドボタンを切り替える
created: 2024-08-26
updated: 2024-09-19
---

## 概要

[プロセス](../../../../users-guide/hands-on/advanced/advanced-operations-process.md)で作成したボタンの切り替えのタイミングおよびサーバスクリプト[elements.DisplayType](../../../../developers-guide/server-script/elements/server-script-elements-display-type.md)でボタンの表示状態を切り替える際のタイミングを制御します。この機能は以下ケースで有効な機能です。

1.  [プロセス](../../../../users-guide/hands-on/advanced/advanced-operations-process.md)を設定した場合の[状況](../editor-settings/columns/table-management-status.md)項目の詳細設定で「自動ポストパック」を設定した場合
1.  [プロセス](../../../../users-guide/hands-on/advanced/advanced-operations-process.md)の[条件](../../../../FAQ/editor/faq-condition-mode-range.md)で設定した項目の詳細設定で「自動ポストパック」を設定した場合
1.  [elements.DisplayType](../../../../developers-guide/server-script/elements/server-script-elements-display-type.md)を制御する際にif文などの条件分岐で利用した項目の詳細設定で「自動ポストパック」を設定した場合

| 設定               | 説明                                                                                                                                                                                                                                             |
| :----------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| チェックなしの場合 | 「作成」や「更新」のタイミングで、対応するプロセス管理のボタンに切り替わります。[elements.DisplayType](../../../../developers-guide/server-script/elements/server-script-elements-display-type.md)の場合は編集画面表示時点のみ実行します。                                                                                                 |
| チェックありの場合 | [自動ポストバック](../editor-settings/advanced-settings/general/table-management-auto-postback.md)を設定した項目の値を変更したタイミングで、対応するプロセス管理のボタンに切り替わります。[elements.DisplayType](../../../../developers-guide/server-script/elements/server-script-elements-display-type.md)の場合はif文などの条件分岐で利用した[自動ポストバック](../editor-settings/advanced-settings/general/table-management-auto-postback.md)を設定した項目の値を変更したタイミングで実行します。 |

## 前提条件

1.  設定を行うには「サイトの管理権限」が必要です。

## 操作手順

1.  対象の[テーブル](../../../../users-guide/table/index.md)を開いてください。
1.  「管理」メニューから[テーブルの管理](../../index.md)をクリックしてください。
1.  [エディタ](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)タブを開いてください。
1.  画面下部にある「自動ポストバック時にコマンドボタンを切り替える」のチェックボックスをオンにしてください。
1.  画面下部の「更新」ボタンをクリックしてください。

### サーバスクリプトelements.DisplayTypeを利用した場合

1.  以下のようなサーバスクリプトを条件：「画面表示の前」で登録します。

    ``` javascript title="JavaScript" linenums="1"
    if (model.ClassA === '更新不可') {
            // 更新ボタンを無効に設定
            elements.DisplayType('UpdateCommand',2);
    }
    ```

1.  分類Aの詳細設定で[自動ポストバック](../editor-settings/advanced-settings/general/table-management-auto-postback.md)にチェックします。

1.2.の設定ですと、編集画面表示時のタイミングのみサーバスクリプトによる制御が有効になりますが、その後分類Aの値を変更しても更新ボタンは変化しませんが、1.2.に加えて「自動ポストバックにコマンドボタンを切り替える」をチェックすることで、分類Aの値の変更内容に伴って更新ボタンの有効／無効が切り替わるようになります。

## 関連情報

-   [応用編：プロセスと状況による制御](../../../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [開発者ガイド：サーバスクリプト：elements.DisplayType](../../../../developers-guide/server-script/elements/server-script-elements-display-type.md)
-   [テーブルの管理：項目：状況](../editor-settings/columns/table-management-status.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../../FAQ/editor/faq-condition-mode-range.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../editor-settings/advanced-settings/general/table-management-auto-postback.md)
-   [テーブル機能](../../../../users-guide/table/index.md)
-   [テーブルの管理](../../index.md)
-   [テーブル機能：レコードのエディタ画面](../../../../users-guide/table/record-authoring/edit-records/table-editor.md)

[プロセス]: ../../../../users-guide/hands-on/advanced/advanced-operations-process.md
[elements.DisplayType]: ../../../../developers-guide/server-script/elements/server-script-elements-display-type.md
[状況]: ../editor-settings/columns/table-management-status.md
[条件]: ../../../../FAQ/editor/faq-condition-mode-range.md
[自動ポストバック]: ../editor-settings/advanced-settings/general/table-management-auto-postback.md
[テーブル]: ../../../../users-guide/table/index.md
[テーブルの管理]: ../../index.md
[エディタ]: ../../../../users-guide/table/record-authoring/edit-records/table-editor.md
