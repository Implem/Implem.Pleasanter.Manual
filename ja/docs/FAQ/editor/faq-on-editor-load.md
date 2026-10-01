---
title: 編集画面で更新ボタンの押下後にスクリプトが実行されない
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-on-editor-load
translationKey: faq-on-editor-load
shortname: ''
created: 2021-02-12
updated: 2024-04-29
---

## 回答

[$p.events.on_editor_load](../../developers-guide/script/events/script-events-on-editor-load.md)を利用してください。

---

## 概要

編集画面で更新ボタンを押下した際に、自動で画面全体がリフレッシュされる仕様に変更されました。  
それにより、編集画面で実行されていたスクリプトが、更新ボタン押下後に意図した動作をしないケースが発生します。  

## 対処方法

### on_editor_loadを使う  

対象：Pleasanter.net、オープンソース版    

出力先で編集を選択し、on_editor_load配下にスクリプトを配置することで、リフレッシュ時の編集画面読み込み時にスクリプトが実行されます。  

##### JavaScript

```
$p.events.on_editor_load = function () {
    //既存の処理
}
```    

[開発者ガイド：スクリプト機能：$p.events.on_editor_load](../../developers-guide/script/events/script-events-on-editor-load.md)  

### General.jsonで設定を変更する  

対象：オープンソース版  

General.jsonのUpdateResponseTypeを0から1に変更します。Jsonファイルの変更時は再読み込みが必要となりますので、以下の注意事項のリンクを確認してください。  
※設定変更後は、サーバスクリプト機能で、項目の読取専用を行う機能などが動作しなくなります。  

[パラメータ設定：General.json](../../setup/parameters/general.json.md)

## 注意事項

パラメータ変更時の注意事項などについては以下を参照してください。  
[パラメータ変更について](../../setup/parameters/parameter-edit.md)
