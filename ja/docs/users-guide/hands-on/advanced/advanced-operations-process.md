---
title: プロセスと状況による制御
category: 操作ガイド（応用編）
order: '70'
status: ''
parts: ''
urlstring: advanced-operations-process
translationKey: advanced-operations-process
shortname: プロセス,状況による制御
created: 2023-08-25
updated: 2023-08-25
---

## 概要

「プロセス」機能を使うことで、稟議申請などで用いられる承認ワークフロー機能を実現します。また「[状況による制御](../../../managers-guide/manage-table/control-by-status/index.md)」と組み合わせることで、状況毎に各項目の表示や読取専用などを細かく設定することができます。

## 1. プロセス

「プロセス」機能ではプロセス管理用のボタン設定、入力検証、ステータスごとの条件、ボタン表示有無のアクセス制御、自動採番、ボタン押下時の通知を設定することで、ワークフロー機能を実現します。

### プロセス機能と状況

プロセス機能は[状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を基準に設定します。現在の状況から変更後の状況に変化させる場合の処理内容を設定します。また現在の状況、変更後の状況どちらも"すべての状況"を指定することができ、この指定によりすべての状況で表示するボタンを設置することが可能です。この設定を活用することで標準のボタン（新規作成、更新、削除等）とは別に特定処理を実行するためのボタンを自由に追加することが可能です。

### プロセス機能の設定概要

#### 1. ボタン設定

プロセス処理専用のボタンを追加します。ボタン追加の他に既存の新規作成ボタン／更新ボタンでプロセス処理を実行することも可能です。またボタン押下のアクションを設定することで、任意のスクリプトを実行するためのボタンを設置することが可能です。ボタン設定を活用することで、状況を申請中に進めるボタンや状況を差戻しにするボタンなど承認ワークフローなどで一般的に利用するボタンや、スクリプトやサーバスクリプトを実行するボタンを追加することができます。

##### 設定例

-   状況を"申請待"→"課長承認待"に変化させる"申請"ボタン
-   状況を"経理待"→"完了"に変化させる"支払"ボタン
-   新規登録／更新ボタン押下時に状況は変更しないが、”回答者"欄に操作ユーザを登録する
-   状況が"承認済み"以降で画面を印刷する"印刷"ボタン

#### 2. 入力検証

プロセス処理毎に独自の入力検証処理を設定します。[テーブルの管理](../../../managers-guide/manage-table/index.md)－[エディタ](../../table/record-authoring/edit-records/table-editor.md)で設定した入力必須、入力検証とは別に設定することができ、[エディタ](../../table/record-authoring/edit-records/table-editor.md)で設定した入力検証とのマージや置換を選択できます。

##### 設定例

-   承認ボタン押下時は"回答"欄を入力必須にする

#### 3. 条件

通常は現在の状況で指定した状況の場合にプロセス用ボタンが表示されますが、条件を設定することでボタン表示を詳細に制御できます。

##### 設定例

-   "金額"欄が20万以下の場合、状況を"課長承認待ち"→"経理待"に変化させる"承認"ボタンを表示する
-   "金額"欄が20万を超える場合、状況を"課長承認待ち"→"部長承認待ち"に変化させる"承認"ボタンを表示する

#### 4. アクセス制御

プロセス用ボタンを表示する対象を指定します。ユーザ、組織、グループ毎に指定可能です。条件と組み合わせることでより詳細にボタン表示制御を行うことができます。

##### 設定例

-   経理部に所属するユーザのみ"支払"ボタンを表示する

#### 5. データの変更

プロセス用ボタン押下時に各項目のデータを変更することができます。任意の値の入力や値のコピーなどが可能です。

##### 設定例

-   申請ボタン押下時に"申請日"に操作日を、"申請者"、"申請部門"に操作ユーザの名前および所属する組織を自動で入力する

#### 6. 自動採番

プロセス処理実行のタイミングで自動採番を行います。エディタの項目の詳細設定で設定する自動採番はレコード作成時のタイミングですが、この設定では更新時にも自動採番することが可能です。

##### 設定例

-   承認ボタン押下時に決裁番号を付与する。

#### 7. 通知

プロセス処理実行時のタイミングで通知する内容を設定します。[テーブルの管理](../../../managers-guide/manage-table/index.md)－[通知](advanced-operations-notification.md)とは別処理ですので、組み合わせて使用することが可能です。

##### 設定例

-   状況が"経理待"に変化する"承認"ボタン押下時で経理部メーリングリストにメール通知する。

## 2. 状況による制御

ステータスに応じて、項目ごとに[入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)、[読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)、[非表示](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)の設定やレコード単位で読取専用を設定します。また、設定を有効とする条件やアクセス制御を設定することができます。

##### 設定例

-   状況が"申請待"の場合、承認に関する項目は非表示にする
-   状況が"課長承認待"の場合、社員グループに所属するユーザはレコードを読取専用とする
-   状況が"経理待"で"金額"が100万円を超える場合、全ての項目を読取専用で表示する

## 関連情報

-   [テーブルの管理：項目：状況](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)
-   [テーブルの管理](../../../managers-guide/manage-table/index.md)
-   [テーブル機能：レコードのエディタ画面](../../table/record-authoring/edit-records/table-editor.md)
-   [応用編：通知、リマインダー](advanced-operations-notification.md)
-   [テーブルの管理：エディタ：項目の詳細設定：入力必須](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-required.md)
-   [テーブルの管理：エディタ：項目の詳細設定：読取専用](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-readonly.md)
-   [テーブルの管理：エディタ：項目の詳細設定：非表示](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/table-management-hide.md)
