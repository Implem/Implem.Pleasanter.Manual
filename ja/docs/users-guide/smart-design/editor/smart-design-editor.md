---
title: 操作方法
category: スマートデザイン：エディタ
order: '2000'
status: ''
parts: ''
urlstring: smart-design-editor
translationKey: smart-design-editor
shortname: スマートデザイン
created: 2025-03-28
updated: 2026-04-14
---

## 概要

スマートデザインではエディタ画面のレイアウトをドラッグ＆ドロップで簡単に編集することができます。
また、各項目の表示に関するオプションをダイアログで個別に変更することも可能です。

![スマートデザインのエディタ画面全体](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/2378f81e295c4c5f81d663e606fdfc22.png)

## 制限事項

1. バージョン1.5.2.0以前では「全般」タブのみを編集できます。 [追加したタブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)に配置した項目は編集できませんのでご注意ください。
1. [コメント](../../common/comment.md)はスマートデザインのエディタから編集できません。必要な場合は[テーブルの管理](../../../managers-guide/manage-table/index.md)から設定してください。
1. [エディタの設定](../../../managers-guide/manage-table/editor/editor-settings/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)で表示されるA～Zで終わる項目は、スマートデザインから呼び出されると、設定内容がリセットされます。ご注意ください。
1. [エディタの設定](../../../managers-guide/manage-table/editor/editor-settings/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)で表示されるA～Zで終わる項目をエディタのレイアウトから削除すると、設定内容がリセットされます。ご注意ください。
1. 「スマートデザイン：概要」の制限事項も確認してください。

## 画面の説明

### ドラッガブルエリア

![ドラッガブルエリア。左の項目一覧と右のレイアウトエリアに番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/e49b0147624348a7933bbad301422e82.png)

<span class="pl-callout">**➊**</span>**エディタの項目一覧**

エディタの項目一覧の項目を選択し、右のレイアウトエリアにドラッグ＆ドロップすることでエディタに配置できます。

エディタの項目一覧には、「項目グループ名」が表示されます。項目グループ名をクリックすると、レイアウトエリアに配置可能な項目が表示されます。

各項目グループの詳細は以下の通りです。

|項目グループ名|説明|
|:--|:--|
|基本項目|サイトを構成する基本的な項目です。 |
|追加項目|分類/数値/日付/説明/チェック/添付ファイルなどA～Zで終わる項目です。|
|リンクテーブル|サイトにリンクが紐づけられている場合にリンクのテーブルを配置できます。|
|その他|[見出し](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-section.md)と項目の設定『[回り込みしない](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-no-wrap.md)』を改行として配置できます。|

<span class="pl-callout">**➋**</span>**レイアウトエリア**

画面右側にアプリのエディタ画面に配置されている項目がカード型のユニットでレイアウトされます。 
配置済みの項目カードはドラッグ＆ドロップで自由に並び替えることが可能です。

バージョン1.5.3.0以降では、レイアウトエリアで[タブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)を編集できるようになりました。  
詳細は「スマートデザイン：エディタ：タブ」を確認してください。

## 各種項目カード

![各種の項目カードと、カード上の構成要素に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/5228b53b86e04297bdeda79ec6a4a4b3.png)
配置済みの項目カードの表示構成です。

|No|タグ|説明|
|:--:|:--|:--|
|1|表示名|配置された項目の表示名です。|
|2|編集ボタン|項目の設定を変更する編集ダイアログを表示するボタンです。|
|3|タグ|一部の設定のオプション値を表示します。詳しくは下記のタグ一覧を確認してください。|

#### タグ一覧

|タグ|説明|
|:--|:--|
|入力必須|[入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)がチェックされている場合に表示|
|読取専用|[読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)がチェックされている場合に表示|
|項目グループ|画面右側の一覧に属しているグループ名|
|カラム名|項目のオリジナルのカラム名。[タイトル]や[分類A]など。|
|コントロール種別|分類項目（ドロップダウンリスト / ラジオボタン）と数値項目（スピナー）のコントロール種別の値|
|マークダウン|説明項目のスタイルが[マークダウン](../../common/markdown.md)の場合に表示|
|リッチテキストエディタ|説明項目のスタイルが[リッチテキストエディタ](../../common/richtexteditor.md)の場合に表示|
|日付の書式|日付項目のエディタの書式の値|
|リンク先サイトID|リンクテーブルに紐づいているリンク先のサイトID|
|リンク元サイトID|リンクテーブルに紐づいているリンク元のサイトID|

### 項目編集ダイアログ

項目カードの (2) の編集ボタンから編集ダイアログを呼び出し、設定の変更や、配置した項目を削除することができます。
![項目編集ダイアログ。各部に番号を振った図](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/d0e9d734990b4ef5b6616fa56d1f3b09.png)
以下は項目編集ダイアログの表示構成です。

|No|タグ|説明|
|:--:|:--|:--|
|1|ヘッダ|項目のオリジナルのカラム名を表示。|
|2|設定エリア|項目の設定を編集できます。|
|3|簡易プレビュー|編集した内容で入力フォームのUIをリアルタイムでプレビューできます。|
|4|閉じるボタン|編集ダイアログを閉じます|
|5|更新ボタン|編集した内容で項目カードを更新します。|
|6|削除ボタン|選択した項目カードをレイアウトから削除します。|

## 操作方法

### 項目の配置・並び替え

スマートデザイン起動時に現在のテーブル管理 > [エディタ](../../table/record-authoring/edit-records/table-editor.md)の構成を表示します。
![スマートデザイン起動時に表示される現在のエディタの構成](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/077f6423f9be4c26b6ae6bbda9d7712b.png)
画面左の項目一覧から必要な項目をドロップ操作で任意のタブの、任意の位置に配置することができ、 配置済みの項目も自由に並び替えられるので直感的にエディタ画面のレイアウトを設計することが可能です。 
未選択のタブへドラッグ＆ドロップすると、そのタブの最後の項目の後ろに配置されます。

#### 追加項目の配置についての注意事項

以前に設定を変更した追加項目をレイアウトエリアに配置すると変更内容がリセットされますのでご注意ください。

### 項目の別のタブへの移動

1. 任意の項目カードをドラッグし移動先のタブへ重ねてください。
1. 移動先のタブの背景色が濃くなったタイミングでドロップすると、別のタブへ移動できます。

たとえば、下図は「全般」タブの[内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)項目を「タブ2」へ移動している画面です。

![「全般」タブの内容項目を「タブ2」へドラッグして移動している画面](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/fcecf1ac61724bca87f79eaf66c11182.png)

#### 追加項目の配置についての注意事項

以前に設定を変更した追加項目をレイアウトエリアに配置すると変更内容がリセットされますのでご注意ください。

### 項目の編集

配置した項目カードの編集ボタンから項目編集ダイアログを呼び出すことができます。
![項目カードの編集ボタンから開いた項目編集ダイアログ](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/c963e9c9cd114092b3bc4cdc77155cd5.png)
ダイアログ内では簡易的なプレビューを確認しながら設定を変更することが可能です。
変更した内容は「更新ボタン」を押下すると項目カードに反映します。

### 項目をレイアウトから削除

項目カードをレイアウトから削除したい場合は編集ダイアログの下の削除ボタンから操作可能です。
![項目編集ダイアログの下部にある削除ボタン](https://pleasanter.org/files/images/ja/users-guide/smart-design/editor/assets/19385df1188b40f2826f899ed7f307bd.png)
「基本項目 / リンクテーブル」の項目は設定内容を保持したまま項目一覧に返却、「追加項目 / その他」の項目の設定内容はリセットされます。

#### 追加項目の配置についての注意事項

リンクに紐づいた分類項目を削除するとリンクテーブルも削除されますのでご注意ください。

## 設定できる項目の種類

|名称|概要|備考|
|:---|:---|:---|
|ID|「レコード」の一意なIDを格納する項目。読取専用|期限付きテーブル、記録テーブルでデフォルト設定|
|バージョン|「レコード」のバージョン番号を格納する項目。読取専用|期限付きテーブル、記録テーブルでデフォルト設定|
|タイトル|「レコード」を識別するための[タイトル](../../../managers-guide/tenant-administration/tenant-logo.md)を格納する「入力項目」|期限付きテーブル、記録テーブルでデフォルト設定|
|内容|「レコード」の内容をフリーテキストで文字列を入力可能な「入力項目」。[マークダウン](../../common/markdown.md)や[リッチテキストエディタ](../../common/richtexteditor.md)を利用した入力や[画像](../../table/record-authoring/edit-records/table-record-upload-picture.md)の登録が可能|期限付きテーブル、記録テーブルでデフォルト設定|
|開始|「レコード」の「開始日時」を格納する「入力項目」|期限付きテーブルでデフォルト設定、記録テーブルでは設定不可|
|完了|「レコード」の期限を示す「完了日時」を格納する「入力項目」|期限付きテーブルでデフォルト設定、記録テーブルでは設定不可|
|作業量|「レコード」の「作業量」を格納する「入力項目」|期限付きテーブルでデフォルト設定、記録テーブルでは設定不可|
|進捗率|「レコード」の[進捗率](../../table/record-authoring/edit-records/table-record-progression-rate.md)を0～100%のパーセンテージで格納する「入力項目」|期限付きテーブルでデフォルト設定、記録テーブルでは設定不可|
|残作業量|「レコード」の「作業量」と[進捗率](../../table/record-authoring/edit-records/table-record-progression-rate.md)から「残作業量」を自動計算する項目。読取専用|期限付きテーブルでデフォルト設定、記録テーブルでは設定不可|
|状況|「レコード」の状況（ステータス）を格納する「入力項目」|期限付きテーブル、記録テーブルでデフォルト設定|
|管理者|「レコード」の「管理者」を格納する「入力項目」|期限付きテーブル、記録テーブルでデフォルト設定|
|担当者|「レコード」の「担当者」を格納する「入力項目」|期限付きテーブル、記録テーブルでデフォルト設定|
|ロック|[レコードのロック](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)を行うための「入力項目」|期限付きテーブル、記録テーブルでデフォルト設定|
|分類|[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)からの選択形式、またはフリーテキスト形式の「入力項目」||
|数値|フリーテキストで数値を入力可能な「入力項目」||
|日付|フリーテキストまたはカレンダーから日付と時刻を入力可能な「入力項目」||
|説明|フリーテキストで文字列を入力可能な「入力項目」。[マークダウン](../../common/markdown.md)や[リッチテキストエディタ](../../common/richtexteditor.md)を利用した入力や[画像](../../table/record-authoring/edit-records/table-record-upload-picture.md)の登録が可能||
|チェック|チェックボックスの「入力項目」||
|添付ファイル|[添付ファイル](../../table/record-authoring/edit-records/table-record-attachment-delete.md)をアップロード/ダウンロード可能な「入力項目」||
|リンクテーブル|サイトに紐づいたリンクのテーブル。|リンクが設定されてない場合は非表示|
|見出し|エディタのレイアウトを整理する見出し項目|詳細モーダルで編集可能|
|改行|詳細設定『[回り込みしない](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-no-wrap.md)』を改行として項目化||

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.15.0以降|機能追加|
|1.4.20.0以降|[リッチテキストエディタ](../../common/richtexteditor.md)を追加|
|1.5.3.0以降|エディタのタブ編集機能を追加|

## 関連情報

-   [追加したタブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)
-   [共通機能：コメントを追加](../../common/comment.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブルの管理：エディタ：エディタの設定](../../../managers-guide/manage-table/editor/editor-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：エディタ：見出し](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-section.md)
-   [テーブルの管理：エディタ：項目の詳細設定：回り込みしない](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-no-wrap.md)
-   [テーブルの管理：エディタ：タブ](../../../managers-guide/manage-table/editor/tab-settings/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)
-   [共通機能：マークダウン](../../common/markdown.md)
-   [共通機能：リッチテキストエディタ](../../common/richtexteditor.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：項目：内容](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-body.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../../managers-guide/tenant-administration/tenant-logo.md)
-   [テーブル機能：レコードに画像を登録](../../table/record-authoring/edit-records/table-record-upload-picture.md)
-   [テーブル機能：レコードの進捗率表示](../../table/record-authoring/edit-records/table-record-progression-rate.md)
-   [テーブルの管理：エディタ：レコードのロックを許可](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-record-lock.md)
-   [テーブル機能：レコードの添付ファイルの削除](../../table/record-authoring/edit-records/table-record-attachment-delete.md)
