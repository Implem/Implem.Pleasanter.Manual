---
title: 一覧
category: ダッシュボード機能
order: '80'
status: ''
parts: ''
urlstring: dashboard-grid
translationKey: dashboard-grid
shortname: ''
created: 2024-02-01
updated: 2024-06-21
---

## 概要

[ダッシュボード](dashboard-add-parts.md)に[一覧](../../managers-guide/manage-table/grid/index.md)を追加します。期限付きテーブルまたは記録テーブルの一覧画面を表示します。

![ダッシュボードに追加した一覧パーツの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/a9b6740548b640418badf4ca3369ade1.png)

## 設定手順

### 全般タブ

![一覧パーツの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/b03bd65292ff4089b65f13d016467104.png)

<a id="record-title"></a>
<a id="record-description"></a>
<a id="base-site"></a>

| 項目名               | 説明                                                                                                                                                                                                                                                   |
| :------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| タイトル             | パーツの名称です。                                                                                                                                                                                                                                     |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                                                                             |
| サイトID             | 表示したいサイトID、サイト名、サイトグループ名をカンマ区切りで入力します。期限付きテーブルまたは記録テーブルのみ指定可能です。複数指定した場合、先頭のサイトが「基準サイト」となり、フィルタタブ、ソータタブおよび一覧タブの選択項目として利用します。 |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「[ダッシュボード機能：パーツの追加](dashboard-add-parts.md)」を参照ください。                                                               |
| CSS                  | タイムラインの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。                                                            |

### 一覧タブ

![一覧パーツの設定画面の一覧タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/c9fd36cd4f374e07af64d660cf868ab5.png)

一覧に表示したい項目を選択します。操作方法については「[テーブルの管理：一覧画面：一覧画面の項目の設定](../../managers-guide/manage-table/grid/table-management-grid-columns.md)」を参照してください。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）に設定されている値がサイトIDで設定した全テーブルのレコードで表示されます。

### フィルタタブ

![一覧パーツの設定画面のフィルタタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/cb6e52fd59034d98ae29b0b415170fc1.png)

タイムラインに出力したいレコードのフィルタ条件を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してフィルタを行います。

### ソータタブ

![一覧パーツの設定画面のソータタブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/4c4f7e0d808e4dbe9664ae6851b31b40.png)

タイムラインに出力したいレコードの並び順を設定します。選択肢は[基準サイト](#base-site)の[表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)となりますが、選択した項目（分類A、数値B等）でサイトIDで設定した全テーブルのレコードに対してソートを行います。未設定の場合は、サイトIDで設定した全テーブルのレコードに対して更新日時の降順でソートします。

### アクセス制御タブ

![一覧パーツの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/bfb41b35878a4fa084eac9f88d5d99b8.png)

タイムラインに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [テーブルの管理：一覧画面](../../managers-guide/manage-table/grid/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：表示名](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-label-text.md)
