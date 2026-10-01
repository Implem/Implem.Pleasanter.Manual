---
title: タイムライン
category: ダッシュボード機能
order: '30'
status: ''
parts: ''
urlstring: dashboard-timeline
translationKey: dashboard-timeline
shortname: ダッシュボード,パーツ,タイムライン
created: 2023-07-11
updated: 2024-06-21
---

## 概要

[ダッシュボード](dashboard-add-parts.md)に「タイムライン」を追加します。選択したサイトのレコードを任意の条件、並び順で表示します。

## 設定手順

### 全般タブ

![タイムラインの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/dfb4bfaedcf04167bb6efa20df3c0ca3.png)

<a id="record-title"></a>
<a id="record-description"></a>
<a id="base-site"></a>

| 項目名               | 説明                                                                                                                                                                                                                                         |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| タイトル             | パーツの名称です。                                                                                                                                                                                                                           |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                                                                   |
| サイトID             | 表示したいサイトID、サイト名、サイトグループ名をカンマ区切りで入力します。期限付きテーブルまたは記録テーブルのみ指定可能です。複数指定した場合、先頭のサイトが「基準サイト」となり、フィルタタブおよびソータタブの選択項目として利用します。 |
| レコードのタイトル   | タイムライン上に表示する際のタイトルを指定します。角括弧([])囲いで[基準サイト](#base-site)の項目名を指定することで、動的に値を設定することができます。                                                                                       |
| レコードの内容       | タイムライン上に表示する際の内容を指定します。角括弧([])囲いで[基準サイト](#base-site)の項目名を指定することで、動的に値を設定することができます。                                                                                           |
| 表示タイプ           | タイムラインに表示するレコードの表示タイプを選択します。                                                                                                                                                                                     |
| 表示件数             | タイムライン上に表示するレコードの件数を指定します。                                                                                                                                                                                         |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「[ダッシュボード機能：パーツの追加](dashboard-add-parts.md)」を参照ください。                                                     |
| CSS                  | タイムラインの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。                                                  |

### フィルタタブ

![タイムラインの設定画面のフィルタタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/ef96b1ddbb754c1fb9c1944d58f7123b.png)

タイムラインに出力したいレコードのフィルタ条件を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してフィルタを行います。

### ソータタブ

![タイムラインの設定画面のソータタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/485b81e872d949d2aaa6a8bca290a72e.png)

タイムラインに出力したいレコードの並び順を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してソートを行います。未設定の場合は、サイトIDで設定した全テーブルのレコードに対して更新日時の降順でソートします。

### アクセス制御タブ

![タイムラインの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/4b3de68ebb634eba96d24060e9a3e3ed.png)

タイムラインに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 表示内容

### 表示タイプ

表示タイプの設定に応じて下記の通り表示します。

| 表示タイプ | 表示内容                                                                                                                                           |
| :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| 簡易       | 初期表示は[レコードのタイトル](#record-title)を表示します。マウスカーソルを乗せるとテーブル名、[レコードの内容](#record-description)を表示します。 |
| 標準       | 初期表示はテーブル名、[レコードのタイトル](#record-title)を表示します。マウスカーソルを乗せると[レコードの内容](#record-description)を表示します。 |
| 詳細       | 初期表示の時点でテーブル名、[レコードのタイトル](#record-title)、[レコードの内容](#record-description)を表示します。                               |

=== "表示タイプ：簡易"

    ![表示タイプが「簡易」のタイムラインの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/981563def6a74a4fb073f4da9a37b38c.gif)

=== "表示タイプ：標準"

    ![表示タイプが「標準」のタイムラインの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/35bf9bc82cd24c8da9c8f9654a730390.gif)

=== "表示タイプ：詳細"

    ![表示タイプが「詳細」のタイムラインの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/e2dbf48560ee4cf8ae6e00ab26ab9eb7.gif)

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
