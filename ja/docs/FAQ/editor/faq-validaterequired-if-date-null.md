---
title: 日付が未入力の場合に別の分類項目を入力必須にしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-validaterequired-if-date-null
translationKey: faq-validaterequired-if-date-null
shortname: ''
created: 2024-05-29
updated: 2024-05-29
---

## 回答

以下対応で実現できます。

1.  日付項目に対して[日付フィルタのモード選択](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-date-filter-mode.md)で[範囲指定](faq-condition-mode-range.md)を設定
1.  [状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)の「全般」タブにて分類項目を[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)とし、[条件](faq-condition-mode-range.md)タブにて日付項目で「未設定」を選択
1.  [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)で日付項目の詳細設定で[自動ポストバック](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)にチェック

---

## 概要

『日付Aが未入力の場合に分類Aを入力必須にしたい』などの条件によって入力必須を制御したい場合は、[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)と[自動ポストバック](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)で実現できます。また[日付項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)に対して未入力であることを条件にしたい場合は条件タブにて日付項目で「未設定」を選択します。

## 操作手順

1.  [テーブルの管理](../../managers-guide/manage-table/index.md)－[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)タブより「日付A」を選択し、「詳細設定」ボタンをクリック。詳細設定ダイアログにて「モード選択」を「既定」に設定します。

    ![日付Aの詳細設定ダイアログ。モード選択を「既定」にする](https://pleasanter.org/files/images/ja/FAQ/editor/assets/3f475dcdfe814c44bf1e82b4fad7ca7e.png)

1.  [テーブルの管理](../../managers-guide/manage-table/index.md)－[状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)タブにて以下内容で制御内容を登録します。
    1.  全般タブを開き、「項目の制御」にて「分類A」を選択後、[入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)ボタンをクリックします。

        ![状況による制御の全般タブ。分類Aに入力必須を設定する](https://pleasanter.org/files/images/ja/FAQ/editor/assets/aef7bd18085d45dd9628b2ac39da3505.png)

    1.  条件タブを開き、日付Aを追加、条件として「未設定」にチェックします。

        ![状況による制御の条件タブ。日付Aの条件に「未設定」を指定する](https://pleasanter.org/files/images/ja/FAQ/editor/assets/e69d35be0f2d4800ac0459dedfbc0874.png)

1.  [テーブルの管理](../../managers-guide/manage-table/index.md)－[エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)タブにて分類A、日付Aを有効化し、日付Aの詳細設定にて[自動ポストバック](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)にチェックします。

    ![日付Aの詳細設定で自動ポストバックにチェックした状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/9bf2d8d379bb4ac89cec89ebc8f19dab.png)

### 設定後の動作

-   日付Aが未入力の場合、分類Aが入力必須

    ![日付Aが未入力のとき、分類Aが入力必須になっている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/904fe8d9f5f44597954a26a57dd739d8.png)

-   日付Aに値を入力すると、分類Aの入力必須は解除される

    ![日付Aに値を入力し、分類Aの入力必須が解除された状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/ee9cf2c1893d489aa39b007536eba49f.png)

## 関連項目

-   [テーブルの管理：フィルタ：日付項目フィルタのモード選択](../../managers-guide/manage-table/filter/filter-settings/table-management-filter-date-filter-mode.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](faq-condition-mode-range.md)
-   [応用編：プロセスと状況による制御](../../users-guide/hands-on/advanced/advanced-operations-process.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：自動ポストバック](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-auto-postback.md)
-   [テーブルの管理：項目：日付](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-date.md)
-   [テーブルの管理](../../managers-guide/manage-table/index.md)
-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
