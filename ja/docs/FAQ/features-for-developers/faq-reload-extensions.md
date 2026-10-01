---
title: プリザンターを再起動せずにParametersフォルダ配下の情報を再読み込みしたい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-reload-extensions
translationKey: faq-reload-extensions
shortname: ''
created: 2020-07-31
updated: 2025-11-10
---

## 回答

プリザンターを再起動せずにParametersフォルダ配下の情報を再読み込みすることはできません。サーバでのプリザンター再起動の操作を行わずに、WebブラウザからParametersフォルダ配下の情報を再読み込みすることが可能です。[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)にてプリザンターにログインした状態で「http(s)://{ServerName}/admins/reloadparameters」にアクセスしてください。

---

## 概要

プリザンターを再起動せずにParametersフォルダ配下の情報を再読み込みすることはできません。通常はサーバでのプリザンター再起動の操作が必要ですが、特権ユーザに限り、プリザンターにログインした状態で「http(s)://{ServerName}/admins/reloadparameters」にアクセスすることで、Parametersフォルダ配下の情報を再読み込みすることができます。ただしこの方法であってもプリザンターは再起動します。

## 注意事項

1. 本機能を実行した時点でプリザンターが再起動するので、一時的にプリザンターが使用不可になります。またプリザンターでレコード新規登録や更新のタイミングと再起動のタイミングがかぶってしまうとデータの不整合など正常な動作をしない恐れがあります。システム運用中は本機能を実行せず、実行する際は利用者にあらかじめ通知し、一定時間プリザンターの運用を止めてから行う等の十分な注意を行ってください。
1. 本機能の実行はパラメータファイルの再読み込みのみを行い、各種定義情報の再読み込みは行いません。そのため本機能は開発環境でのパラメータ設定確認などの利用にとどめ、本番環境での利用は控えてください。

## 前提条件

1. [特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)でログインしている必要があります。未ログイン状態で本機能を実行した場合はログイン画面が表示します。また[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)以外でログインしている状態で本機能を実行した場合、パラメータは再読み込みされません。

## 操作手順

1. あらかじめ[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)でプリザンターにログインします。
1. パラメータファイルの設定内容を適宜変更し、ファイルを保存してください。
1. ログインした際に使用したブラウザの別タブ（もしくは別ウィンドウ）を開き、URL欄に「http(s)://{ServerName}/admins/reloadparameters」を入力し、Enterキーを押します。Enterキー押下後は画面が真っ白になります。
1. ログイン済みのタブ（もしくはウィンドウ）に戻り、ページを再読み込みしてください。
1. 変更したパラメータ設定内容が反映されていることを確認してください。

## 関連情報

-   [ユーザ管理機能：特権ユーザの設定](../../managers-guide/user-administration/user-management-privileged-users.md)