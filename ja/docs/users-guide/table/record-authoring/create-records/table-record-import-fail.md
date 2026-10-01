---
title: レコードのインポートがうまくいかない場合の確認事項
category: テーブル機能
order: '205'
status: ''
parts: ''
urlstring: table-record-import-fail
translationKey: table-record-import-fail
shortname: インポート
created: 2020-04-22
updated: 2024-06-07
---

## 概要

プリザンターにデータを[インポート](table-record-import.md)する場合、元データ(CSV)の項目名とプリザンターの表示名を一致させる必要があります。

![CSVの項目名とプリザンターの表示名の対応を示した図](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/209850ae27a84387949fd5e607867593.png)

プリザンター側の表示名は[一覧](../../../../managers-guide/manage-table/grid/index.md)ではなく[エディタ](../edit-records/table-editor.md)で設定してください。

![表示名を設定するエディタの画面](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/0b3e76902f234d68a2efe1fe4cb0e07a.png)

インポートするCSVデータがShift-JISで保存されているか、UTF-8形式か確認し、下記のプリザンターのインポートダイアログに表示される「文字コード」欄にて保存されている形式を選んでください。

![「文字コード」欄があるインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/10497e4ffcdc4d608d89ceb75c574193.png)

## インポートがうまく行かない場合の確認事項

-   データがインポートできない、または一部しかインポートされていない場合。

    インポート時の文字コードが正しく選択されているか確認してください。

    ![インポートのダイアログの「文字コード」の選択欄](https://pleasanter.org/files/images/ja/users-guide/table/record-authoring/create-records/assets/be710d44bb9245d2b56cdddc740bd8c3.png)

    英数字は取り込めて、日本語がうまく取り込めないという場合は文字コードが正しくないケースが考えられますので、うまくいかない場合は、もう一方を試してみてください。

## インポートしたデータがうまくリンクされない場合の確認事項

-   子テーブルのインポートを行う前にマスタテーブルを先にインポートしてください。

    先に子テーブルをインポートしてしまった場合は、マスタテーブルへのデータインポート後に、子テーブルのデータをエクスポートし、そのファイルを「IDが一致するレコードを更新する」にチェックを入れてインポートしてください。  

-   子テーブルのリンク項目名は、親テーブルの項目名ではなく子テーブル側の項目名でインポートしてください。

    期限付きテーブルの場合「完了」項目は値が必須となります。記録テーブルの場合には「完了」項目はありません。
    期限付きテーブルにデータをインポートする場合は「完了」項目には必ず値を入れてください。

## pleasanter.net使用時の制限

1.  pleasanter.netでは一度のインポート処理で取り込めるレコード数が10,000行となっています。10,000行を超える量のデータをインポートする場合は、10,000行ごとに区切ってインポートしてください。

## 関連情報

-   [組織管理機能：インポート](../../../../managers-guide/department-administration/dept-import.md)
-   [テーブルの管理：一覧画面](../../../../managers-guide/manage-table/grid/index.md)
-   [テーブル機能：レコードのエディタ画面](../edit-records/table-editor.md)
