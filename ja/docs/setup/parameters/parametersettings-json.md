---
title: ParameterSetting.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: parametersettings-json
translationKey: parametersettings-json
shortname: ParameterSetting.json
created: 2026-05-29
updated: 2026-06-09
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。

| パラメータ名 | 設定例 | 説明                                                                                                                                                                                            |
| --- | --- | --- |
| EnableScreenManagement | false  | true<br>画面からパラメータを編集する機能を有効化します。ナビゲーションメニューに「パラメータの管理」が表示されます。<br><br>false（既定値）<br>画面からパラメータを編集する機能を無効化します。<br><br>詳細は以下のマニュアルを確認してください。<br>・「パラメータ管理機能」 |
| EnableRestart | false  | true<br>「パラメータ管理」画面に「再起動」ボタンが表示されます。<br><br>false（既定値）<br>「再起動」ボタンは表示されません。<br><br>詳細は以下のマニュアルを確認してください。<br>・「パラメータ管理機能：画面からの再起動」<br>・「パラメータ管理機能：環境別の自動再起動設定」 |
| RestartCheckIntervalSeconds | 120 |再起動予定時刻を決定するためのDB参照を一定間隔（秒数）内に抑制します。既定値は120（秒）です。<br><br>0またはnullの場合<br>再起動しません。<br><br>詳細は「パラメータ管理機能：冗長化構成におけるパラメータ設定の連係」を参照してください。|

## 対応バージョン

| 対応バージョン | 内容 |
| -------------- | ---- |
| 1.5.5.0 以降 | ParameterSetting.jsonを追加 |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
