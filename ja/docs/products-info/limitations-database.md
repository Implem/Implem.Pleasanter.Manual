---
title: データベースによる制限事項
category: もっと活用するために
order: '0'
status: ''
parts: ''
urlstring: enterprise-edition-restriction-database
translationKey: enterprise-edition-restriction-database
shortname: Enterprise Edition,制限事項
created: 2025-01-24
updated: 2025-02-14
---

## 概要

年間サポートサービス契約者が利用できるEnterprise Edition、Pleasanter Extensionsにおいて、セットアップ時に選択するデータベース（SQL Server、PostgreSQL、MySQL）の違いによって発生する制限事項について説明します。

## 項目拡張で追加する項目の上限

Community Editionでは[分類項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)、[数値項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)、[日付項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)、[説明項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)、[チェック項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)、[添付ファイル項目](../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)の各項種別毎に26個、計156項目が利用できますが、Enterprise Editionでは項目を追加することができます。ただしセットアップ時に選択するデータベース毎に追加できる項目の上限が異なります。

| DB         | Enterprise Editionで追加できる項目の上限                                                                              |
| :--------- | :-------------------------------------------------------------------------------------------------------------------- |
| SQL Server | 6つの項目種別の合計で**最大744項目**まで<br>（Community Editionで利用可能な156項目との合計で**900項目まで拡張可能**） |
| PostgreSQL | 6つの項目種別の合計で**最大744項目**まで<br>（Community Editionで利用可能な156項目との合計で**900項目まで拡張可能**） |
| MySQL      | 6つの項目種別の合計で**最大100項目**まで<br>（Community Editionで利用可能な156項目との合計で**256項目まで拡張可能**） |

## Pleasanter Extensionsの制限

セットアップ時に選択するデータベース毎に、利用可能なPleasanter Extensionsのラインナップが異なります。

| DB         | Development Tools | Operations Tools |
| ---------- | ----------------- | ---------------- |
| SQL Server | 利用可            | 利用可           |
| PostgreSQL | 利用可            | 利用可           |
| MySQL      | 利用不可          | 利用不可         |

## 関連情報

-   [テーブルの管理：項目：分類](../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [テーブルの管理：項目：数値](../managers-guide/manage-table/editor/editor-settings/columns/table-management-num.md)
-   [テーブルの管理：項目：日付](../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理：項目：説明](../managers-guide/manage-table/editor/editor-settings/columns/table-management-description.md)
-   [テーブルの管理：項目：チェック](../managers-guide/manage-table/editor/editor-settings/columns/table-management-check.md)
-   [テーブルの管理：項目：添付ファイル](../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
