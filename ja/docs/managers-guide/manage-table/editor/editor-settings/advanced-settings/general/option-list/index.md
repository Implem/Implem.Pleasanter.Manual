---
title: 選択肢一覧
category: エディタ
order: '7500'
status: ''
parts: ''
urlstring: table-management-choices-text
translationKey: table-management-choices-text
shortname: 選択肢一覧
created: 2021-05-02
updated: 2025-11-27
---

## 概要

[分類項目](../../../columns/table-management-class.md)を「セレクトボックス」で表示する際の選択肢を指定します。選択肢は改行区切りで指定します。また、選択肢一覧には、リンクしたテーブルから値を転記する[ルックアップ](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)機能の設定や、[ソート・フィルタ・表示フォーマット](table-management-choice-json.md)を使った選択肢の制御が可能です。

### 「選択肢一覧」カテゴリのマニュアル

<div class="grid cards" markdown>

-   [リンク](table-management-choices-text-link.md)
-   [組織](table-management-choices-text-depts.md)
-   [グループ](table-management-choices-text-groups.md)
-   [ユーザ](table-management-choices-text-users.md)
-   [フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [フィルタ（選択肢一覧を他の項目の値で絞り込む）](table-management-choice-json-column-filter-expressions.md)
-   [ルックアップ](table-management-lookup.md)
-   [コピー時に子レコードを同時にコピーする](table-management-copy-with-links.md)
-   [削除時に子レコードを同時に削除する](table-management-delete-with-links.md)
-   [親レコードからの子レコード作成時に特定の項目にのみ親レコードの値を設定する](table-management-select-new-link.md)
-   [ログインユーザ設定ボタン](table-management-choices-text-own-user.md)
-   [所属組織設定ボタン](table-management-choices-text-own-dept.md)

</div>

## 制限事項

1. [状況項目](../../../columns/table-management-status.md)、[担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)、[分類項目](../../../columns/table-management-class.md)以外では使用できません。
1. [状況項目](../../../columns/table-management-status.md)では「保存する値」に数値を使用する必要があります。
1. [担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)では「ユーザ一覧」以外は使用できません。
1. 「値」が同じものは設定しても表示されません。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 記述例

#### 記述例1

最も単純な文字列の選択肢を表示する記述例です。[分類項目](../../../columns/table-management-class.md)でのみ使用可能です。

```text title="選択肢一覧" linenums="1"
要件定義
設計
構築
テスト
リリース・展開
初期サポート
運用
```

#### 記述例2

「保存する値」と「画面上の表示」を区別する場合の記述例です。「保存する値」と「画面上の表示」の順にカンマ区切りで指定します。「保存する値」の文字列をそのままに「画面上の表示」の文字列を変更するとレコードを編集せずに「画面上の表示」を変更することができます。この記述例は[状況項目](../../../columns/table-management-status.md)、[担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)では使用できません。

```text title="選択肢一覧" linenums="1"
AC7459,製品A
UW9336,製品B
PX1223,製品C
```

!!! tip "画面上の表示にカンマ（,）を含めるには"
    画面上の表示にカンマ（,）を含めたい場合は、**バックスラッシュでエスケープ**してください。

    ```text title="選択肢一覧" linenums="1"
    1\,000円まで
    2\,000円まで
    3\,000円まで
    ```

#### 記述例3

記述例2に加え、「画面上の短い表示名」、「スタイルシートのクラス名」を指定する場合の記述例です。記述例2と同様にカンマ区切りで指定します。「画面上の短い表示名」は[一覧画面](../../../../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)の表示幅を節約するために有効です。「スタイルシートのクラス名」は指定したクラス名のスタイル（背景色、文字色など）を適用することができます。**クラス名は"status-"で始まる必要があります。** オリジナルのスタイルは[テーブルの管理](../../../../../index.md)の[スタイル](../../../../../../../developers-guide/style/index.md)で別途設定する必要があります。この記述例は[担当者項目](../../../columns/table-management-owner.md)、[管理者項目](../../../columns/table-management-manager.md)では使用できません。

```text title="選択肢一覧" linenums="1"
100,未着手,未,status-new
150,準備,準,status-preparation
200,実施中,実,status-inprogress
300,レビュー,レ,status-review
900,完了,完,status-closed
910,保留,留,status-rejected
```

#### その他の記述例

その他、選択肢には[組織の選択肢一覧](table-management-choices-text-depts.md)、[グループの選択肢一覧](table-management-choices-text-groups.md)、[ユーザの選択肢一覧](table-management-choices-text-users.md)、[リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)などが使用できます。また[選択肢一覧のフィルタ、ソート、表示フォーマット](table-management-choice-json.md)が使用できます。詳しくは関連情報を参照してください。

## 関連情報

-   [テーブルの管理：項目：分類](../../../columns/table-management-class.md)
-   [応用編：リンク](../../../../../../../users-guide/hands-on/advanced/advanced-operations-link.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：フィルタ、ソート、表示フォーマット](table-management-choice-json.md)
-   [テーブルの管理：項目：状況](../../../columns/table-management-status.md)
-   [テーブルの管理：項目：担当者](../../../columns/table-management-owner.md)
-   [テーブルの管理：項目：管理者](../../../columns/table-management-manager.md)
-   [テーブル機能：レコードの一覧画面](../../../../../../../users-guide/table/record-authoring/data-analysis/table-grid.md)
-   [テーブルの管理](../../../../../index.md)
-   [開発者ガイド：スタイル](../../../../../../../developers-guide/style/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：グループ](table-management-choices-text-groups.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](table-management-choices-text-users.md)