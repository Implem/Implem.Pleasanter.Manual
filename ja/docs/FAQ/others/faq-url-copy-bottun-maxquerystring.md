---
title: フィルタ条件を多数選択した複雑なビューの場合は、URLコピーボタンでコピーしたURLが開けないケースがある
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: FAQ-url-copy-bottun-maxquerystring
translationKey: FAQ-url-copy-bottun-maxquerystring
shortname: ''
created: 2025-09-18
updated: 2026-06-16
---

## 回答

IISの設定ファイル「web.config」を編集します。変更を保存したタイミングでIISが再起動されます。

---

## 概要

フィルタ条件を多数選択した複雑なビューの場合は、パンくずリストの左側の「URLコピーボタン」でコピーしたURLが開けないケースがあります。原因の1つとして、IISがクエリとして受付可能な文字列の上限に達している可能性があります。IISがクエリとして受付可能な文字列の上限は、IISの設定ファイル「web.config」内のパラメータmaxQueryStringで設定され、そのデフォルト値は2048です。この値を変更することでURLを開けるようにします。

web.configはマニュアル通りにセットアップした場合、C:\web\pleasanter\Implem.Pleasanter\web.configにあります。

## 注意事項

1. 編集したweb.configを保存したタイミングでIISが再起動されます。本手順の実施にあたってはサービス停止可能時間に行ってください。
1. web.configファイルは、プリザンターのバージョンアップ時に上書きされるため、再度設定が必要です。

## 操作手順

1. メモ帳などのテキストエディタでweb.configを開きます。
2. requestFilteringなどの文字列で検索し、編集箇所を探します。見つけたら、次のように変更してください。  
   変更前（抜粋）
   ```
   <requestFiltering>
       <requestLimits maxAllowedContentLength="2147483647" />
   </requestFiltering>
   ```
   変更後（抜粋）
   ```
   <requestFiltering>
       <requestLimits maxAllowedContentLength="2147483647" maxQueryString="4096" />
   </requestFiltering>
   ```
3. 変更を保存すると、IISが再起動します。
4. URLコピーボタンの動作を確認してください。