---
title: SQLServer環境で漢数字のゼロを含む検索結果が正しくない
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-sqlserver-kanji-zero
translationKey: faq-sqlserver-kanji-zero
shortname: ''
created: 2022-12-07
updated: 2024-04-29
---

## 回答

SQL Serverの仕様です。

---

## 概要

SQLServerの環境では、漢数字の〇（ゼロ）を含む値の検索が想定した結果にならない場合があります。検索時、漢数字の〇（ゼロ）は空文字と判断されます。例えば、likeの検索条件で"三〇一"を検索すると、"三〇一"だけではなく"三一"や"三〇〇一"のデータも検索結果に含まれて出力されます。また、漢数字の〇（ゼロ）のみ入力された項目は未設定（空）と判断されます。

この事象はSQL Serverの動作仕様となります。

## 関連情報

[SQL Server の辞書順照合順序を使用している環境で、漢数字の〇 (ゼロ) を含む検索が正しい結果を返さない - Microsoft サポート](https://support.microsoft.com/ja-jp/topic/sql-server-%E3%81%AE%E8%BE%9E%E6%9B%B8%E9%A0%86%E7%85%A7%E5%90%88%E9%A0%86%E5%BA%8F%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E7%92%B0%E5%A2%83%E3%81%A7-%E6%BC%A2%E6%95%B0%E5%AD%97%E3%81%AE%E3%80%87-%E3%82%BC%E3%83%AD-%E3%82%92%E5%90%AB%E3%82%80%E6%A4%9C%E7%B4%A2%E3%81%8C%E6%AD%A3%E3%81%97%E3%81%84%E7%B5%90%E6%9E%9C%E3%82%92%E8%BF%94%E3%81%95%E3%81%AA%E3%81%84-23374a9c-32e7-e026-52cb-d54aff0db8f9)
