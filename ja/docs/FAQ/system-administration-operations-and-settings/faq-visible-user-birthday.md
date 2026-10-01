---
title: ユーザの管理で生年月日と性別を表示したい
category: FAQ：システム管理の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-visible-user-birthday
translationKey: faq-visible-user-birthday
shortname: ''
created: 2024-05-07
updated: 2024-05-14
---

## 回答

CustomDefinitionsフォルダを作成し、Column.jsonを作成後にプリザンターを再起動してください。

---

## 概要

ver.1.4.4より[ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)の管理から「生年月日」と「性別」が非表示になりましたが、以下の手順で再度表示することができます。

## 操作方法

1.  `.\pleasanter\Implem.Pleasanter\App_Data¥Parameters\`に、「CustomDefinitions」フォルダを作成します。
1.  手順1で作成した「CustomDefinitions」フォルダ配下に以下サンプルコードのファイルを作成し、「Column.json」というファイル名で保存します。
1.  プリザンターを再起動します。
1.  [ユーザの管理](../../managers-guide/user-administration/index.md)を開き、生年月日と性別が表示されていることを確認します。

## サンプルコード

``` json linenums="1"
{
    "Users_Birthday": {
        "ReadAccessControl": "ManageTenant",
        "CreateAccessControl": "ManageTenant",
        "UpdateAccessControl": "ManageTenant"
    },
    "Users_Gender": {
        "ReadAccessControl": "ManageTenant",
        "CreateAccessControl": "ManageTenant",
        "UpdateAccessControl": "ManageTenant"
    }
}
```

## 関連情報

-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
