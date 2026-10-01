---
title: 自動採番
category: プロセス
order: '700'
status: ''
parts: ''
urlstring: process-autonumber
translationKey: process-autonumber
shortname: ''
created: 2025-06-19
updated: 2026-02-24
---

## 概要

プロセス実行時のタイミングで、指定した文字列を扱える項目（タイトル、内容、分類、説明）に番号を自動入力する機能です。プロセスの詳細設定の[自動採番](../editor/editor-settings/advanced-settings/auto-numbering/index.md)タブの対象項目を設定し、書式欄に採番のフォーマットを記述することで有効化されます。

## 制限事項

-   プロセスの一括処理を実行する際に採番順序は指定できません。

## 操作手順

1.  自動採番タブをクリックします。
1.  「新規作成」ボタンをクリックします。
1.  対象となる項目を選択をします。
1.  必要な項目を設定します。
1.  「変更」ボタンをクリックします。
1.  プロセス管理の「更新」ボタンをクリックします。

## 設定項目

![プロセスの自動採番の設定画面。項目や書式、リセット種別などを設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/646f8090f4c840df8d71008286927b2c.png)

| 項目名       | 説明                                     | 設定例                     |
| :----------- | :--------------------------------------- | :------------------------- |
| 項目         | 自動採番の対象となる項目を選択           |                            |
| 書式         | 自動採番の書式を指定                     | [yyyyMMdd]-[分類A]-[NNNN]  |
| リセット種別 | 自動採番のカウントをゼロに戻す種別を指定 | 年、月、日、文字列から選択 |
| 既定値       | 自動採番を開始する値を指定               | 1                          |
| ステップ     | 自動採番の間隔を指定                     | 1                          |

自動採番の設定方法は、[エディタの項目の詳細設定](../editor/editor-settings/advanced-settings/index.md)の[自動採番](../editor/editor-settings/advanced-settings/auto-numbering/index.md)と同様になりますので、詳細は下記ページをご覧ください。

[テーブルの管理：エディタ：項目の詳細設定：自動採番](../editor/editor-settings/advanced-settings/auto-numbering/index.md)

## Tips

-   プロセスの条件タブやアクセス制御タブと組み合わせて任意のタイミングで実行できます。
-   全般タブの実行種別を「作成または更新」に設定することで、標準の更新ボタンでレコードを更新したタイミングで実行できます。
-   [エディタの項目の詳細設定](../editor/editor-settings/advanced-settings/index.md)の[自動採番](../editor/editor-settings/advanced-settings/auto-numbering/index.md)はレコード作成時に実行できますが、プロセスの自動採番タブはレコード更新時にも利用できます。
-   自動採番を設定した項目に対して入力内容をクリアした場合は自動採番が再度実行されます。
-   採番済みの入力内容に対する変更を許可しない場合は読取専用としてください。

## 対応バージョン

| 対応バージョン | 内容                                                                             |
| :------------- | :------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | 変更種別に値の関数操作を追加<br>メール通知の宛先にCc、Bccを追加                  |
| 1.4.11.0 以降  | 実行種別に追加したボタン／作成・更新を追加<br>共通設定・全般タブにアイコンを追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：自動採番](../editor/editor-settings/advanced-settings/auto-numbering/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定](../editor/editor-settings/advanced-settings/index.md)
