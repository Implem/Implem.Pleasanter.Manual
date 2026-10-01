---
title: URLやUNCパスを入力して外部にリンクしたい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-url-and-unc
translationKey: faq-url-and-unc
shortname: ''
created: 2020-01-20
updated: 2024-04-29
---

## 回答

内容、説明項目、コメントにURLやUNCパスを記述すると自動的にリンクを設定します。

---

## 制限事項

1. 分類項目に記述しても自動的にリンクが設定されません。
1. UNCパス※で指定されたリソースへのアクセスは、ローカルネットワークへのアクセスとなるためセキュリティ上、それぞれのブラウザごとに設定が必要となります。  

※UNCパス：主にWindowsネットワーク上のファイルなどのリソースの位置を表記するための記法です。  
  [Windowsシステムのファイルパス](https://docs.microsoft.com/ja-jp/dotnet/standard/io/file-path-formats#unc-paths)

## 概要

1. プリザンターではURLやUNCパスを内容、説明項目、コメントに直接記述すると自動的にその文字列にリンクを設定します。  
  https://implem.co.jp/test.jpg  
  ftp://implem.co.jp/test.jpg  
  Notes://implem/files/test.jpg  
  ¥¥implem¥files¥test.jpg  

1. リンクを設定する際に表示名を利用したい場合は、[表示名] (URL)という記法を用いてリンクを設定することが可能です。
  `[株式会社インプリム](https://implem.co.jp)`
  ※htmlで言うと`<a href ="https://implem.co.jp">株式会社インプリム</a>`という記述と同じ結果となります。

1. 表示名を使ったリンクを設定する場合、リンク名に半角閉じカッコ")"が含まれているとリンクが正しく設定されないケースがあります。
`[テスト画像1](https://implem.cojp/test(01).jpg)
[テスト画像2](¥¥server¥folder¥test(01).jpg)`

1. マークダウン形式で入力（[md]を先頭に記載）することでURLの場合のみ半角閉じカッコがあっても正しくリンクさせることができます。
`[md]
[テスト画像1](https://implem.cojp/test(01).jpg)`
