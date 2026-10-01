---
title: Script.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: script-json
translationKey: script-json
shortname: Script.json
created: 2020-12-03
updated: 2025-08-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)をご確認ください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|ServerScript|true|本パラメータをtrueに設定すると「サーバスクリプト」が有効化されます。|
|BackgroundServerScript|false|本パラメータをtrueに設定すると「バックグラウンドサーバスクリプト」が有効化されます。|
|DisableServerScriptHttpClient|false|本パラメータをtrueに設定すると「サーバスクリプト」の「httpClient」を無効化します。|
|ServerScriptTimeOut|2000|「サーバスクリプト」の処理タイムアウト時間をミリ秒で指定します。0を指定すると無制限となります。|
|ServerScriptTimeOutChangeable|false|本パラメータをtrueに設定すると、登録しているサーバスクリプトごとにタイムアウト時間を設定することができるようになります。|
|ServerScriptTimeOutMin|0|タイムアウト時間の下限を設定します。|
|ServerScriptTimeOutMax|86400000|タイムアウト時間の上限を設定します。|
|ServerScriptHttpClientTimeOut|100000|サーバスクリプトの「httpClient」のTimeOutプロパティの初期値をミリ秒単位で指定します。|
|ServerScriptHttpClientTimeOutMin|0|サーバスクリプトの「httpClient」のTimeOutプロパティの設定可能な最小値をミリ秒単位で指定します。|
|ServerScriptHttpClientTimeOutMax|86400000|サーバスクリプトの「httpClient」のTimeOutプロパティの設定可能な最大値をミリ秒単位で指定します。|
|ServerScriptIncludeDepthLimit|10|「サーバスクリプト」の「インクルード」が再帰的に呼び出される深度の上限を指定します。|
|DisableServerScriptFile|true|本パラメータをtrueに設定すると「サーバスクリプト」の「$ps.file」を無効化します。|
|ServerScriptFileSizeMax|1|読み込むファイルサイズの上限(MByte)を指定します。-1を指定すると無制限となります。|
|ServerScriptFilePath|null|読み書きするファイルを格納する基準ディレクトリを指定します。相対パスやルートディレクトリの指定（Windowsでは"C:\\"や"D:\\"、Linuxでは"/"）はエラーとなります。|

## トラブルシューティング

1. 「サーバスクリプト」を設置した「サイト」で「アプリケーションエラー」が発生し「SysLogsテーブル」に「Script execution interrupted by host」と記録される場合には「ServerScriptTimeOut」の時間を増やすことで解決できる場合があります。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|DisableServerScriptFileを追加<br>ServerScriptFileSizeMaxを追加<br>ServerScriptFilePathを追加|
|1.4.19.0 以降|ServerScriptHttpClientTimeOut<br>ServerScriptHttpClientTimeOutMin<br>ServerScriptHttpClientTimeOutMaxを追加|

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)