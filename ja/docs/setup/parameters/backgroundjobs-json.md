---
title: BackgroundJobs.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: backgroundjobs-json
translationKey: backgroundjobs-json
shortname: BackgroundJobs.json
created: 2026-06-26
updated: 2026-09-14
---

[![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/b15923f5b5bb4f5e9b44ada7821f0c74.svg#only-light)![プリザンターの年間サポートサービスのページへのリンクバナー](https://pleasanter.org/files/images/ja/setup/parameters/assets/f6ae3ced07544e1b8ff4ec4e88c16b9e.svg#only-dark)](https://pleasanter.org/support/)

（本機能は[Extensionsトライアル](../../products-info/extensions-trial/index.md)で試用可能です）

## 注意事項

1. パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)をご確認ください。
1. 本ファイルの編集時は、[キューイング](../additional/performance/queuing-manage-jobs.md)を併せて参照してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。

| パラメータ名 | 設定例 | 説明 |
| :-- | :-- | :-- |
| BackgroundQueue | true | キュー方式を有効にするか否かをtrue/falseで指定。デフォルト値はfalse。 |
| BackgroundJobDispatcherInterval | 60 | ジョブを取り出すためにキューを確認する時間間隔（秒）。デフォルト値は60。 |
| BackgroundJobTimeout | 3600 | 「キューの管理画面」で長時間実行している旨の警告メッセージを表示するための閾値。デフォルト値は3600。0を指定すると無効。|
| FallbackLanguage | "ja" | 結果メッセージを表示するための言語。未設定時は[Service.json](service-json.md)のDefaultLanguageの値が使用される。 |
| RecoverAction | "Failed" | 障害などから復旧した際の「実行中」だったジョブの扱いを規定。<br><br>"Failed"（デフォルト値）<br>「実行中」だったジョブを「エラー」にする。<br><br>"Pending"<br>「実行中」だったジョブを「待機」へ戻し、キューの末尾へ再登録する。 |
| OutputFilePath | ・Windowsの場合<br>C:\\\\Output<br><br>・Linuxの場合<br>/var/opt/pleasanter/output| エクスポートの出力ファイルなどジョブに関わるファイルの保存先を設定。パスは環境に応じて適切に設定する必要がある。Windows環境のパス区切り文字\\は\\\\とエスケープすること。なお、対象フォルダへのアクセス権をIIS_IUSRSに付与する必要がある。 |
| InputFilePath | ・Windowsの場合<br>C:\\Input<br><br>・Linuxの場合<br>/var/opt/pleasanter/input| インポートの入力ファイルなどジョブに関わるファイルの保存先を設定。インポートが完了すると対象ファイルは削除される。パスは環境に応じて適切に設定する必要がある。Windows環境のパス区切り文字\\は\\\\とエスケープすること。なお、対象フォルダへのアクセス権をIIS_IUSRSに付与する必要がある。wwwroot配下などの静的ファイル配信が有効な階層を設定しないこと。|

## 対応バージョン

|対応バージョン| 内容|
|:--|:--|
|1.5.6.0 以降|BackgroundJobs.jsonを追加|
| 1.5.7.0 以降 | InputFilePathを追加 |

## 関連情報

-   [パラメータ変更時の確認事項](parameter-edit.md)
-   [Service.json](service-json.md)