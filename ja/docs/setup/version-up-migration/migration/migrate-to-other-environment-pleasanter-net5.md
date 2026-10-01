---
title: 異なる環境にプリザンターのデータベース(SQL Server)を移行する手順
category: 移行
order: '700'
status: ''
parts: ''
urlstring: migrate-to-other-environment-pleasanter-net5
translationKey: migrate-to-other-environment-pleasanter-net5
shortname: ''
created: 2022-02-07
updated: 2026-01-13
---

## 注意事項

1. 本手順は、OSがWindows Server 2019、DBがSQL Serverの環境を想定したものとなります。

## 移行元からのデータバックアップ

1. 移行元の環境にログインします。
1. SQL Server Management Studioを起動しログインします。
1. 「データベース」→「Implem.Pleasanter」を右クリックし「タスク」→「データ層アプリケーションのエクスポート」と操作します。
1. 「ローカルディスクに保存」の「参照」ボタンをクリックしファイル名を入力し「次へ」をクリックします。
1. 「完了」をクリックします。
1. エクスポートが完了すると拡張子がbacpacのファイルが出力されるので確認します。

## 移行先へのデータ移行

1. 移行先の環境にログインします。
1. bacpacファイルを移行元のコンピュータから移行先のコンピュータにコピーします。
1. 移行先の環境にプリザンターをインストールします。
   - インストール手順は[こちら](../../installation/install-manually/getting-started-pleasanter-windows-server2019.md)です。
1. SQL Server Management Studioを起動しログインします。
1. 「データベース」→「Implem.Pleasanter」を右クリックし[削除](../../../users-guide/table/record-authoring/edit-records/table-record-delete.md)をクリックします。
1. ダイアログが表示されるので「接続」欄を確認し、対象のサーバで間違いが無いかチェックします。  
   - **間違った環境で本操作を行うと意図しないデータを消失する可能性がありますので、ご注意ください。**  
1. 「既存の接続を閉じる」にチェックを入れ「OK」をクリックします。
1. 「データベース」を右クリックし「データ層アプリケーションのインポート」をクリックします。
1. 「ローカルディスクからインポート」の「参照」ボタンをクリックしbacpacファイルを選択します。
1. 「次へ」ボタンをクリックします。
1. 「新しいデータベース名」に「Implem.Pleasanter」を指定し「次へ」をクリックします。
1. 「完了」をクリックします。
1. データの移行が完了したら、移行元と移行先のParametersをWinMerge等で差分を確認します。
1. 移行元のParametersの設定を移行先のParametersへマージし、IISを再起動します。  
  - **Enterprise Editionをご契約いただいてるお客様はライセンスファイルも合わせて移行いただきますようお願いいたします。**  
1. プリザンターにログインし、データが移行できた事を確認します。
