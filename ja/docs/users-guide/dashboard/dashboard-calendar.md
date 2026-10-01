---
title: カレンダー
category: ダッシュボード機能
order: '60'
status: ''
parts: ''
urlstring: dashboard-calendar
translationKey: dashboard-calendar
shortname: ダッシュボード,パーツ,カレンダー
created: 2023-11-14
updated: 2026-04-14
---

## 概要

[ダッシュボード](dashboard-add-parts.md)に「カレンダー」を追加します。選択したサイトのレコードを任意の条件、並び順で表示します。

2種類のカレンダーをパーツとして追加できます。

1.  [カレンダータイプ：FullCalendar](../table/record-authoring/data-visualize/table-calendar-type-fullcalendar.md)
1.  [カレンダータイプ：標準](../table/record-authoring/data-visualize/table-calendar-type-standard.md)

以下の図で、上側が[カレンダータイプ：FullCalendar](../table/record-authoring/data-visualize/table-calendar-type-fullcalendar.md)、下側が[カレンダータイプ：標準](../table/record-authoring/data-visualize/table-calendar-type-standard.md)です。

![上がFullCalendar、下が標準のカレンダータイプの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/5c243e9d28e64fad88e823f02c236a74.png)

## 設定手順

### 全般タブ

![カレンダーパーツの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/58e7585704f6498b832ae931379c9fbd.png)

<a id="record-title"></a>
<a id="record-description"></a>
<a id="base-site"></a>

| 項目名               | 説明                                                                                                                                                                                                                                                                                                                                                         |
| :------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| タイトル             | パーツの名称です。                                                                                                                                                                                                                                                                                                                                           |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                                                                                                                                                                                   |
| サイトID             | 表示したいサイトID、サイト名、サイトグループ名をカンマ区切りで入力します。期限付きテーブルまたは記録テーブルのみ指定可能です。複数指定した場合、先頭のサイトが「基準サイト」となり、フィルタタブの選択項目として利用します。                                                                                                                                 |
| カレンダータイプ     | カレンダーの種類を「標準」と「FullCalendar」から選択します。                                                                                                                                                                                                                                                                                                 |
| 分類                 | （カレンダータイプが「標準」の場合のみ有効）カレンダーの[分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)を指定します。カレンダーの[分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)については「テーブル機能：レコードのカレンダー表示」を確認してください。 |
| 期間                 | （カレンダータイプが「標準」の場合のみ有効）カレンダーの「期間」を指定します。カレンダーの「期間」については「テーブル機能：レコードのカレンダー表示」を確認してください。                                                                                                                                                                                     |
| 項目                 | カレンダーの[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)を指定します。カレンダーの[項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)については「テーブル機能：レコードのカレンダー表示」を確認してください。                             |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「ダッシュボード機能：パーツの追加」を確認してください。                                                                                                                                                                   |
| CSS                  | タイムラインの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。                                                                                                                                                                  |

### フィルタタブ

![カレンダーパーツの設定画面のフィルタタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/86f7bab0877a4a4e89100b917daab977.png)

カレンダーに出力したいレコードのフィルタ条件を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してフィルタを行います。

### アクセス制御タブ

![カレンダーパーツの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/6cd37c0f7c274af597a200ac743f828f.png)

カレンダーに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [テーブル機能：レコードのカレンダー表示：FullCalendar](../table/record-authoring/data-visualize/table-calendar-type-fullcalendar.md)
-   [テーブル機能：レコードのカレンダー表示：標準](../table/record-authoring/data-visualize/table-calendar-type-standard.md)
-   [テーブルの管理：項目：分類](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目](../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
