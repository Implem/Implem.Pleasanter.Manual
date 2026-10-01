---
title: カスタムHTML
category: ダッシュボード機能
order: '50'
status: ''
parts: ''
urlstring: dashboard-customhtml
translationKey: dashboard-customhtml
shortname: ダッシュボード,パーツ,カスタムHTML
created: 2023-07-11
updated: 2025-02-12
---

## 概要

[ダッシュボード](dashboard-add-parts.md)に「カスタムHTML」を追加します。動画やBIツールで作成したグラフの埋め込みの他、[スクリプト](../../managers-guide/manage-table/scripts/index.md)、[スタイル](../../developers-guide/style/index.md)と組み合わせることで、様々な用途に拡張可能です。

## 設定手順

### 全般タブ

![カスタムHTMLの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/011d5ee0791e4faea966943fb3a324cb.png)

| 項目名               | 説明                                                                                                                                                                                        |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| タイトル             | パーツの名称です。                                                                                                                                                                          |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                  |
| 内容                 | 表示したい内容をHTML形式で入力します。                                                                                                                                                      |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については「[ダッシュボード機能：パーツの追加](dashboard-add-parts.md)」を参照ください。    |
| CSS                  | カスタムHTMLの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。 |

### アクセス制御タブ

![カスタムHTMLの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/e047de2714124ab28d60d4078fde61ec.png)

カスタムHTMLに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

## 表示内容

=== "例：動画の表示"

    ![カスタムHTMLで動画を表示した例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/e15243d731f841c4a6a7de2ae7ac8989.gif)

=== "例：BIツールで作成したグラフの表示"

    ![カスタムHTMLでBIツールのグラフを表示した例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/eb2e124527e0468bb90a97bed49a4d29.png)

## コードエディタの使用

第2世代[ユーザインターフェースのテーマ](../../managers-guide/user-administration/user-management-theme.md)の場合は、ハイライトやコードヒント・タブキーでのインデント入力などをサポートする便利なコードエディタ機能がご利用いただけます。

![ハイライトやコードヒントが使えるコードエディタで内容を入力する画面](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/a085f04d78914a82a350f2fe7eb570ec.png)

!!! tip "コードエディタを使うには"
    [General.json](../../setup/parameters/general.json.md)の"EnableCodeEditor"を有効化することで利用可能です。

## 対応バージョン

| 対応バージョン | 内容                   |
| :------------- | :--------------------- |
| 1.4.13.0 以降  | コードエディタ機能追加 |

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../../managers-guide/user-administration/user-management-theme.md)
-   [パラメータ設定：General.json](../../setup/parameters/general.json.md)
