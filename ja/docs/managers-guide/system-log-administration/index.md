---
title: システムログ管理機能
category: システムログ管理機能
order: '100'
status: ''
parts: ''
urlstring: syslog
translationKey: syslog
shortname: syslog,システムログの管理,システムログ
created: 2022-10-19
updated: 2024-06-21
---

## システムログの管理

以下の操作でシステムログを参照することが可能です。

## 制限事項

1.  [特権ユーザ](../user-administration/user-management-privileged-users.md)のみ利用できます。
1.  レコードの更新はできません。
1.  表示するカラムは変更できません。
1.  作成日時の降順で表示され、任意でのソートはできません。
1.  必ず[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)の条件を1つ以上指定してください。条件指定がない場合は[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンをクリックしてもシステムログは表示しません。
1.  エクスポート時の書式は変更できません。
1.  エクスポートは[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンクリック後に表示したレコードで指定した条件に合致したログがエクスポートされます。

## システムログの表示

1.  「管理」メニューを開き「システムログの管理」をクリックしてください。

    ![「管理」メニューを開いたナビゲーションメニュー。「システムログの管理」が並ぶ](https://pleasanter.org/files/images/ja/managers-guide/system-log-administration/assets/1042869d8c734672be23e61103260d03.png)

1.  参照条件を入力し、[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)ボタンをクリックしてください。

    ![参照条件とフィルタボタンが並ぶシステムログの一覧画面](https://pleasanter.org/files/images/ja/managers-guide/system-log-administration/assets/bf4df4e45c554f66b7e6c48b92ca154a.png)

    [システムログの拡張機能](syslog-extension.md)を利用する場合は追加カラムの情報も表示されます。（API、サイトID、参照ID、参照種別、状況、説明）

    ![拡張機能の追加カラムも表示されたシステムログの一覧画面](https://pleasanter.org/files/images/ja/managers-guide/system-log-administration/assets/5ac88739a2c2433f89fb1ff49cc44e5e.png)

## エクスポート

1.  上記の「システムログの表示」の手順でエクスポートしたいシステムログを表示してください。
1.  [エクスポート](../../developers-guide/api/table-operations/api-export.md)をクリックしてください。
1.  表示されたダイアログで文字コードを選択してください。

## 関連情報

-   [パラメータ設定：Rds.json](../../setup/parameters/rds-json.md)
-   [システムログの拡張機能](syslog-extension.md)
