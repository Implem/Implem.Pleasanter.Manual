---
title: カンバン
category: ダッシュボード機能
order: '70'
status: ''
parts: ''
urlstring: dashboard-kanban
translationKey: dashboard-kanban
shortname: ''
created: 2024-01-10
updated: 2024-06-21
---

## 概要

[ダッシュボード](dashboard-add-parts.md)に[カンバン](../table/record-authoring/data-visualize/table-kanban-chart.md)を追加します。選択したサイトのレコードをカンバン形式で表示します。

![ダッシュボードに追加したカンバンパーツの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/efdd6d4fb4f64c25b48bde535ea3ae29.png)

## 設定手順

### 全般タブ

![カンバンパーツの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/138bfd009d0e453b8438d2a8eac8f88b.png)

<a id="record-title"></a>
<a id="record-description"></a>
<a id="base-site"></a>

| 項目名               | 説明                                                                                                                                                                                                                         |
| -------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| タイトル             | パーツの名称です。                                                                                                                                                                                                           |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                                                   |
| サイトID             | 表示したいサイトID、サイト名、サイトグループ名をカンマ区切りで入力します。期限付きテーブルまたは記録テーブルのみ指定可能です。複数指定した場合、先頭のサイトが「基準サイト」となり、フィルタタブの選択項目として利用します。 |
| 列の分類             | カンバンの「列の分類」を指定します。「列の分類」については「テーブル機能：レコードのカンバン表示」を確認してください。                                                                                                         |
| 行の分類             | カンバンの「行の分類」を指定します。「行の分類」については「テーブル機能：レコードのカンバン表示」を確認してください。                                                                                                         |
| 集計種別             | カンバンの「集計種別」を指定します。「集計種別」については「テーブル機能：レコードのカンバン表示」を確認してください。                                                                                                         |
| 集計対象             | （「集計種別」が「件数」以外の場合のみ有効）カンバンの「集計対象」を指定します。「集計対象」については「テーブル機能：レコードのカンバン表示」を確認してください。                                                             |
| 最大列数             | カンバンの「最大列数」を指定します。「最大列数」を超えた場合、カンバンは分割されて多段表示となります。                                                                                                                       |
| 集計表示             | 「集計表示」のON/OFFを切り替えます。「集計表示」については「テーブル機能：レコードのカンバン表示」を確認してください。                                                                                                         |
| 状況を表示           | 「状況を表示」のON/OFFを切り替えます。チェックボックスにチェックを付けた場合、各レコードの状況を表すアイコンが表示されます。                                                                                                 |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「ダッシュボード機能：パーツの追加」を確認してください。                                   |
| CSS                  | タイムラインの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。                                  |

### フィルタタブ

![カンバンパーツの設定画面のフィルタタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/8ae7dcfbf1f74226a5aceb240532f7fa.png)
カンバンに出力したいレコードのフィルタ条件を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してフィルタを行います。

### アクセス制御タブ

![カンバンパーツの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/44a41d00219b4cf0a8edc7da1454019f.png)

カンバンに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 制限事項

サイトIDに複数のサイトを指定し、複数サイトのレコードを同時に表示している場合、ドラッグ操作によるレコードの移動はできません。

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [テーブル機能：レコードのカンバン表示](../table/record-authoring/data-visualize/table-kanban-chart.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
