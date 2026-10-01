---
title: オリジナルのテンプレートを追加したい（ver.1.3.5.0以前）
category: FAQ：システム管理の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-original-template
translationKey: faq-original-template
shortname: ''
created: 2020-03-11
updated: 2025-01-30
---

## 回答

プリザンターのフォルダ内¥App_Data¥Definitionsのdefinition_Template.xlsmにオリジナルテンプレートの情報を編集し、プリザンターを再起動してください。

---

## 注意事項

本FAQはプリザンターのバージョン1.3.5.0以前の内容です。バージョン1.3.6.0以降をご利用の場合は以下FAQを参照ください。  
[FAQ：オリジナルのテンプレートを追加したい](faq-original-template-json.md)

## 制限条件

1. マクロ付Excelファイルを編集するため、Microsoft ExcelをインストールしたPCが必要です。

## 概要

テーブルの新規作成で選択できるテンプレートとして独自に作成したオリジナルテンプレートを登録することができます。

## 操作手順

1.  テンプレートとして登録したい構成の通常のテーブルとして新規作成します。作成後、そのサイトIDを記録しておいてください。
1.  SQLServer Management Studioなどを使ってImplem.Pleasanterのdbo.sitesテーブルを開きます。SiteIdが手順1で記録したサイトIDと一致するレコードを選択し、SiteSettingsカラムの内容をコピーしてください。この内容がオリジナルテンプレートの構成になります。

    ![SQL Server Management Studio で dbo.sites の SiteSettings をコピーするところ](https://pleasanter.org/files/images/ja/FAQ/system-administration-operations-and-settings/assets/cdb98aff949d4f6495ab71c72ca57785.png)

1.  プリザンターのフォルダ内¥App_Data¥Definitionsの「definition_Template.xlsm」を開いて編集します。例として、Template14の下に行を挿入し、その行にオリジナルテンプレートを定義します。
    -   Id列には他のテンプレートと重複しない任意の値を入力してください。
    -   SiteSettingsTemplate列には先程コピーしたSiteSettingsの内容を貼り付けてください。
    -   Language列にはja、Title列にはオリジナルのテンプレート名を入力します。例としてオリジナルテンプレと入力してください。
    -   Project列には、11と入れてください。これは「プロジェクト」タブの11番目に表示するという意味です。Tagsよりも右側の列が新規作成時のタブになりますので、登録したいタグの列に数値を入力してください。

    ![definition_Template.xlsm にオリジナルテンプレートの行を追加したところ](https://pleasanter.org/files/images/ja/FAQ/system-administration-operations-and-settings/assets/b1c4016b48dd4d6b89f3410e1a2d305b.png)

1.  プリザンターを再起動してください。新規作成時、指定したタブに追加したテンプレートが追加されていることを確認してください。

    ![新規作成の画面。指定したタブに追加したテンプレートが表示されている](https://pleasanter.org/files/images/ja/FAQ/system-administration-operations-and-settings/assets/3211db6cf1d644a7ab8d9d7fa130cd93.png)
