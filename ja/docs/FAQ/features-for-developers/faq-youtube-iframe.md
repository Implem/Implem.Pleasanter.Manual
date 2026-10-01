---
title: 編集画面でYouTubeの動画を表示したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-youtube-iframe
translationKey: faq-youtube-iframe
shortname: ''
created: 2019-07-06
updated: 2024-04-29
---

## 回答

あらかじめ準備したYouTubeの埋め込みタグを[スクリプト](../../managers-guide/manage-table/scripts/index.md)にて表示します。

---

## 概要

編集画面にてYouTubeの埋め込みタグによる動画の表示と再生を行う方法を説明します。

## 事前準備

(1) 対象となるテーブルを開きの「管理」メニューから[テーブルの管理](../../managers-guide/manage-table/index.md)を開きます。  
(2). エディタタブで分類Aを追加します。名称を「埋め込みタグ」等に変更します。  
(3). スクリプトタブを開き「新規作成」ボタンをクリックし、[タイトル](../../managers-guide/tenant-administration/tenant-logo.md)に任意のタイトルを入力し、[スクリプト](../../managers-guide/manage-table/scripts/index.md)に以下のスクリプトを入力します。  

##### JavaScript

```
// 動画のiframeをセット
showMovie = function () {
    // 分類Aに入力された埋め込みタグを取得
    var html = $p.getControl('ClassA').val();
    // 埋め込みタグを内容欄にセット
    $p.getControl('Body').parent().html(html);
}
// ページが表示されたら動画を表示
   showMovie(); 
// 分類Aが変更されたら動画を変更
$p.on('change', 'ClassA', function () {
   showMovie(); 
});
```
(4) 「出力先」を「編集」のみに設定します。  
(5) 「変更」ボタンをクリックしダイアログを閉じます。  
(6) 画面下部の「更新」ボタンをクリックします。  
(7) 任意のレコードを開き「埋め込みタグ」の欄にYoutubeの埋め込みタグを入力します。  

YouTubeの埋め込み用のタグの取得方法は下記のヘルプの手順を参照してください。  
https://support.google.com/youtube/answer/171780?hl=ja
