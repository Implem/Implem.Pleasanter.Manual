---
title: 入力検証
category: プロセス
order: '300'
status: ''
parts: ''
urlstring: process-data-validation
translationKey: process-data-validation
shortname: ''
created: 2025-06-19
updated: 2026-08-17
---

## 概要

プロセス処理時の入力検証内容を設定します。

![プロセスの入力検証タブ。入力検証種別を設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/cd19f42b437147a3bb203b328cf5492e.png)

### 操作手順

## 入力検証種別

プロセス機能で追加されたボタンの入力検証種別を設定します。

| 選択肢 | 説明                                                                                                                                                                                                                                                                         |
| :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| マージ | 「エディタの項目の設定」の[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)とプロセスの[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)を行います。             |
| 置換   | 「エディタの項目の設定」の[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)を行わず、プロセスの[入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)のみを行います。 |
| 無し   | [入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)を行いません。                                                                                                                                                        |

既定値は「マージ」になっています。

## 入力検証の新規作成

項目・検証内容ごとに、入力検証を作成します。

1.  入力検証タブをクリックします。
1.  「新規作成」ボタンをクリックします。
1.  検証条件を設定をします。
1.  「追加」ボタンをクリックします。
1.  入力検証タブの「変更」ボタンをクリックします。
1.  プロセス管理の「更新」ボタンをクリックします。

![プロセスの入力検証の新規作成画面。項目ごとに検証条件を設定する](https://pleasanter.org/files/images/ja/managers-guide/manage-table/process/assets/9a8cdc3d5f8b48508b249885a91fac2f.png)

## 入力検証の設定項目

| 項目名               | 説明                                                                           |
| :------------------- | :----------------------------------------------------------------------------- |
| 項目                 | 検証対象とする項目を選択。                                                     |
| 入力必須             | 入力必須とする場合に設定。                                                     |
| クライアント正規表現 | 入力後に、項目からフォーカスが移ったタイミングで検証する内容を正規表現で設定。 |
| サーバ正規表現       | レコードの作成・更新のタイミングで検証する内容を正規表現で設定。               |
| エラーメッセージ     | 検証エラー時に表示するメッセージを設定。                                       |

## 対応バージョン

| 対応バージョン | 内容                                                                             |
| :------------- | :------------------------------------------------------------------------------- |
| 1.4.10.0 以降  | 変更種別に値の関数操作を追加<br>メール通知の宛先にCc、Bccを追加                  |
| 1.4.11.0 以降  | 実行種別に追加したボタン／作成・更新を追加<br>共通設定・全般タブにアイコンを追加 |

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：入力検証](../editor/editor-settings/advanced-settings/input-validation/index.md)
