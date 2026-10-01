---
title: pg_dumpコマンドでバックアップを取得しようとすると「テーブル"Binaries"の内容のダンプに失敗」というエラーが発生する
category: FAQ：バックアップ、リストア
order: '0'
status: ''
parts: ''
urlstring: faq-backup-pgdump-error
translationKey: faq-backup-pgdump-error
shortname: ''
created: 2025-09-19
updated: 2025-09-22
---

## 回答

レコードに大容量ファイルが添付され、添付ファイルがPostgreSQLデータベース内に保存されることで、メモリ不足に陥った可能性があります。添付されている大容量ファイルの数が多くなければ、添付ファイルを個別にダウンロードしてバックアップし、データベースから添付ファイルを取り除くことで、pg_dumpを実行できる可能性があります。

---

## 概要

前提条件を確認後、操作手順を実施してください。

## 前提条件

1.  以下は、大容量添付ファイルの数が多くなく、設定ファイル[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)のProviderの値がRdsであるときの対処方法です。
1.  Providerの値がRdsの場合、添付ファイルはPostgreSQL内のBinariesテーブル、およびBinaries_deletedテーブルに格納されます。
1.  Binariesテーブル内の添付ファイルは、プリザンターの画面操作で削除可能です。
1.  Binaries_deletedテーブルには削除済みの添付ファイルが（復元や履歴からの参照に備える目的で）格納されています。
1.  添付ファイルは、BASE64でエンコードされ、文字列としてデータベース内に格納されます。
1.  大容量ファイルの目安は、エンコード後のファイルサイズで1Gバイトです。
1.  BASE64エンコードによりファイルサイズは約30％増加します。

## 操作手順

1.  データベースのBinariesテーブルのSize列でファイルサイズを確認することで、対象ファイルと対象レコードを特定します。
1.  プリザンターで対象レコードの編集画面を開き、大容量の添付ファイルを個別にダウンロードして、検証、保存します。
1.  プリザンターで添付ファイルを削除します。
1.  Binaries_deletedテーブルにもBinariesテーブルと同じレイアウトでSize列が存在します。Size列の値が大きいレコードを特定し、DELTEEクエリで削除します。
1.  pg_dumpコマンドを実行し、データベースを移行します。
1.  データベースの移行後、ダウンロードしておいたファイルを対象のレコードに対して個別にアップロードします。

## 関連情報

-   [パラメータ設定：BinaryStorage.json](../../setup/parameters/binary-storage-json.md)
