---
title: 便利なオススメ機能のご紹介
category: 新機能サマリ
order: '0'
status: ''
parts: ''
urlstring: useful-function
translationKey: useful-function
shortname: ''
created: 2021-06-30
updated: 2024-10-31
---

## 概要

便利に使えるオススメ機能をご紹介します。

1. [稟議申請などのワークフローを実現できるプロセス機能](#process)
2. [様々な書式に対応可能な自動採番機能](#auto-numbering)
3. [エクセルのVLOOKUP関数のように使えるルックアップ機能](#lookup)
4. [メール通知機能で宛先を動的に変更する](#notification)
5. [ナビゲーションメニューのカスタマイズ](#navigation-menu)
6. [分類項目の複数選択](#multiple-selections)
7. [選択肢にビューを指定することで並び替えやフィルタを実行](#choice-json)
8. [画面のカラーテーマをカスタマイズ](#theme)

## 1. 稟議申請などのワークフローを実現できるプロセス機能 {#process}

稟議申請などで用いられる承認ワークフロー機能を、プロセス機能を用いて実現します。簡単なマウス操作だけで様々な承認ルートや条件などを設定することができます。

![稟議申請などのワークフローを実現できるプロセス機能](https://pleasanter.org/files/images/ja/users-guide/assets/dd0402b0daaf480c92d0be72c21c3976.png)

FAQ▶ [稟議申請などのワークフロー（承認プロセス）をプロセス機能で実現する](../FAQ/sample-codes/faq-process-workflow.md)

## 2. 様々な書式に対応可能な自動採番機能 {#auto-numbering}

自動採番機能は、文字列を扱える項目（タイトル、内容、分類、説明）で使用できます。様々な書式を指定して採番することが可能です。

| 登録順 | 連番               | 説明                                                      |
| :----: | :----------------- | :-------------------------------------------------------- |
|   1    | 202203東京支店-001 | 202203東京支店、という文字列でグルーピングし1からカウント |
|   2    | 202203東京支店-002 | 同じ文字列なのでカウントアップ                            |
|   3    | 202203横浜支店-001 | 横浜支店に変わったので1からカウント                       |
|   4    | 202203東京支店-003 | 東京支店に戻ったので3からカウント                         |
|   5    | 202204東京支店-001 | 月が変わったので1からカウント                             |

ユーザマニュアル▶ [自動採番](../managers-guide/manage-table/editor/editor-settings/advanced-settings/auto-numbering/index.md)

## 3. エクセルのVLOOKUP関数のように使える待望のルックアップ機能 {#lookup}

「[リンク](hands-on/advanced/advanced-operations-link.md)」された「[項目](../managers-guide/manage-table/editor/editor-settings/columns/index.md)」を選択した際に、リンク先の「[テーブル](table/index.md)」の「[項目](../managers-guide/manage-table/editor/editor-settings/columns/index.md)」を転記できます。  
例えば商談テーブルから顧客テーブルをリンクしている際に、顧客テーブルの住所項目、電話番号項目などを商談テーブルに転記できます。  
今まではスクリプト機能を使わなければできませんでしたが、ルックアップ機能により、非常に簡単な記述方法で実現することができます。

![リンク先のテーブルの項目を転記するルックアップの設定画面](https://pleasanter.org/files/images/ja/users-guide/assets/b81b0a7b043c4e89b6326aaaccc6c8a6.png)

ブログ記事▶ [Excelのように使える新機能ルックアップのご紹介](https://pleasanter.org/blogs/function-guide-lookup)
ユーザマニュアル▶ [ルックアップ](../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-lookup.md)

## 4. メール通知で宛先を動的に変更する {#notification}

直接アドレスを指定するだけではなく、指定した項目で入力・選択されたメールアドレスにもメール通知を送信できるようになりました。プロセス管理など数多くの業務で通知機能が活用できるようになりました。

![項目で入力・選択されたメールアドレスを宛先に指定した通知の設定画面](https://pleasanter.org/files/images/ja/users-guide/assets/031a4bfde89b44c7b067b68706b82ed6.png)

ユーザマニュアル▶ [通知](../managers-guide/manage-table/notifications/table-management-notification.md)

## 5. ナビゲーションメニューのカスタマイズ {#navigation-menu}

画面左側に並ぶナビゲーションメニューをカスタマイズできるようになりました。  
あまり使わないメニューを削除することはもちろん、新たなメニュー項目を追加することも可能です。

![項目を足したり消したりしてカスタマイズしたナビゲーションメニュー](https://pleasanter.org/files/images/ja/users-guide/assets/2e1a26c32afa40a0a51d58bc572fe84f.png)

ユーザマニュアル▶ [NavigationMenus.json](../setup/parameters/navigation-menus-json.md)

## 6. 分類項目の複数選択 {#multiple-selections}

分類項目で複数の選択肢を選択できるようになりました。今までは複数の分類やチェックを配置する必要があった要件も、この機能追加で効率的に実装できます。

![分類項目で複数の選択肢を選んだ状態](https://pleasanter.org/files/images/ja/users-guide/assets/8e46fb3c9f3d4df4a8ee38fe322d87a1.png)

ユーザマニュアル▶ [分類項目の複数選択](../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-multiple-selections.md)

## 7. 選択肢にビューを指定することで並び替えやフィルタを実行 {#choice-json}

分類項目で表示される選択肢の並び替えやフィルタリングなど、JSON形式で記述することでカスタマイズした選択肢が使用可能になりました。

![JSON形式で並び替えやフィルタを指定した選択肢の例](https://pleasanter.org/files/images/ja/users-guide/assets/8bb9f8e34fb24f3eb62545d0b155820d.png)

ユーザマニュアル▶ [フィルタ、ソート、表示フォーマット](../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choice-json.md)

## 8. 画面のカラーテーマをカスタマイズ {#theme}

### 第2世代ユーザーインターフェースのテーマ

第2世代では全4種類のテーマからユーザ毎に自分好みのカラーバリエーションを設定することができます。

<table>
   <tr>
      <td style="width:50%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/26cerulean.png" alt="第2世代のテーマ「cerulean」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:50%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/27green-tea.png" alt="第2世代のテーマ「green-tea」を適用した画面" style="margin: 0 !important;"></td>
   </tr>
   <tr>
      <td style="width:50%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/28mandarin.png" alt="第2世代のテーマ「mandarin」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:50%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/29midnight.png" alt="第2世代のテーマ「midnight」を適用した画面" style="margin: 0 !important;"></td>
   </tr>
</table>

### 第1世代ユーザーインターフェースのテーマ

第1世代では全25種類のテーマからお選びいただけます。

<table>
   <tr>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/10hot-sneaks.png" alt="第1世代のライトテーマ「hot-sneaks」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/24ui-lightness.png" alt="第1世代のライトテーマ「ui-lightness」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/12le-frog.png" alt="第1世代のダークテーマ「le-frog」を適用した画面" style="margin: 0 !important;"></td>
   </tr>
   <tr>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/13mint-choc.png" alt="第1世代のダークテーマ「mint-choc」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/19start.png" alt="第1世代のライトテーマ「start」を適用した画面" style="margin: 0 !important;"></td>
      <td style="width:33%; text-align:center;"><img src="https://pleasanter.org/files/images/ja/users-guide/assets/03blitzer.png" alt="第1世代のライトテーマ「blitzer」を適用した画面" style="margin: 0 !important;"></td>
   </tr>
</table>

ユーザマニュアル▶ [ユーザインターフェースのテーマをカスタマイズ](../managers-guide/user-administration/user-management-theme.md)
