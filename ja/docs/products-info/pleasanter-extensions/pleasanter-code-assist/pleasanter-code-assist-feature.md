---
title: コマンドおよび設定項目
category: Pleasanter Code Assist
order: '5000'
status: ''
parts: ''
urlstring: pleasanter-code-assist-feature
translationKey: pleasanter-code-assist-feature
shortname: Pleasanter Code Assist,PCA Feature,コマンド,設定項目
created: 2025-02-26
updated: 2026-03-12
---

## 1. コマンド一覧

[Pleasanter Code Assist](pleasanter-code-assist-create-workfolder.md)で使用できるコマンドを説明します。

### PCA: Toggle Enable/Disable processing on save

ファイル保存時に実行される自動処理の有効/無効を切り替えるコマンドです。開発作業の状況に応じて柔軟に制御でき、ステータスバーでも状態を制御／確認できます。状態は、ワークスペース設定ファイルに保存され、再起動後も維持されます。

関連 :material-arrow-right: [設定項目：pleasanter-code-assist.enabled](#pleasanter-code-assistenabled)

### PCA: Insert Metadata or Extension Settings

現在の編集コンテキストに基づいて、適切なメタデータや設定情報を挿入するコマンドです。コードの構造化と標準化をサポートします。

| プラットフォーム | ショートカットキー |
| :--------------- | :----------------- |
| Windows/Linux    | ++ctrl+alt+i++     |
| macOS            | ++command+alt+i++  |

### PCA: Toggle Omit/Not Omit API Response Data Output

APIからの応答データの出力レベルを制御するコマンドです。開発やデバッグの状況に応じて、詳細なログと簡潔なログを切り替えることができます。状態は、ワークスペース設定ファイルに保存され、再起動後も維持されます。

関連 :material-arrow-right: [設定項目：omitApiResponseDataOutput](#pleasanter-code-assistomitapiresponsedataoutput)

### PCA: Create Pleasanter Code Assist Directories

開発に必要な標準的なディレクトリ構造を自動生成するコマンドです。プロジェクトの初期設定を効率化し、一貫した開発環境を構築します。

!!! tip "利用手順"
    以下のページを参照してください。  
    [Pleasanter Code Assist：コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)

### PCA: Save and Sync

<!-- meta version="1.3.0" -->

Pleasanter Code Assist 1.2.0以前は、ファイルの保存操作がPleasanterへのファイル同期と連動していました。

Pleasanter Code Assist 1.3.0以降では、意図しない同期が発生するケースへの対応として、保存と同期を独立したコマンドに分離しました。「PCA: Save and Sync」コマンドを実行した場合、またはショートカットキー ++ctrl+s++ / ++command+s++ を押下した場合のみ、保存と自動同期が行われます。

以下の表を参照してください。

=== "Pleasanter Code Assist 1.3.0以降"

    | 操作                        | 動作                     |
    | :-------------------------- | :----------------------- |
    | ++ctrl+s++ / ++command+s++  | 保存＋自動同期           |
    | VS Codeのメニューから保存   | 保存のみ（同期されない） |
    | VS Codeの自動保存による保存 | 保存のみ（同期されない） |

=== "Pleasanter Code Assist 1.2.0以前"

    保存に関わるすべての操作が、プリザンターとの同期を伴います。

    | 操作                        | 動作           |
    | :-------------------------- | :------------- |
    | ++ctrl+s++ / ++command+s++  | 保存＋自動同期 |
    | VS Codeのメニューから保存   | 保存＋自動同期 |
    | VS Codeの自動保存による保存 | 保存＋自動同期 |

## 2. 設定項目

Pleasanter Code Assistの設定項目を説明します。

-   `settings.json`に記載することで、拡張機能の動作をカスタマイズできます。
-   `settings.json`をGUIで操作する場合には、名前の表記が異なりますのでご注意ください。

    !!! tip "pleasanter-code-assist.omitApiResponseDataOutputの場合の例"
        「Pleasanter-code-assist: Omit Api Response Data Output」と表記されます。

### pleasanter-code-assist.autoClearOutput

出力パネルの自動クリア機能を制御する設定です。長時間の開発セッションでログを整理し、重要な情報を見やすく保つために使用します。

<!-- meta default="false" -->

### pleasanter-code-assist.autoShowOutputPanel

出力パネルの表示タイミングを制御する設定です。作業の種類や好みに応じて、適切な表示モードを選択できます。

| 選択可能な値 | 説明             |
| :----------- | :--------------- |
| never        | 表示しない       |
| always       | 常に表示         |
| error        | エラー時のみ表示 |

<!-- meta default="always" -->

### pleasanter-code-assist.caPaths

信頼されたルートCA証明書を含むPEMファイルへのパスを指定します。（使用ファイルはBasic Constraints: CA:TRUEのものを使用してください。）

<!-- meta version="1.2.0" default_none -->

### pleasanter-code-assist.enabled

ファイル保存時の動作を制御する設定です。メタ情報の入力および保存を行うなど、特定の作業フェーズで拡張機能の機能を一時的に無効にしたい場合に使用します。

<!-- meta default="true" -->

### pleasanter-code-assist.fileExtensionMappings.css

CSSファイルとして認識する拡張子を定義します。複数の拡張子を指定できます。

<!-- meta default="[css]" -->

### pleasanter-code-assist.fileExtensionMappings.html

HTMLファイルとして認識する拡張子を定義します。複数の拡張子を指定できます。

<!-- meta default="[html]" -->

### pleasanter-code-assist.fileExtensionMappings.js

JavaScriptファイルとして認識する拡張子を定義します。複数の拡張子を指定できます。

<!-- meta default="[js]" -->

### pleasanter-code-assist.fileExtensionMappings.sql

SQLファイルとして認識する拡張子を定義します。複数の拡張子を指定できます。

<!-- meta default="[sql]" -->

### pleasanter-code-assist.omitApiResponseDataOutput

既存データの確認時におけるAPI応答データの出力を制御する設定です。通常の開発時はログを簡潔に保ち、必要に応じて詳細なデータを確認できるようにします。

<!-- meta default="true" -->

### pleasanter-code-assist.showAxiosErrorResponseJson

通信に用いてるAxiosのエラーが発生した場合、レスポンスJSON（利用可能な場合）を拡張機能の出力パネルに表示します。

<!-- meta version="1.2.0" default="false" -->

### pleasanter-code-assist.showMessage

情報メッセージやエラーメッセージの表示方法を制御する設定です。通知の頻度を作業スタイルに合わせて最適化できます。

| 選択可能な値 | 説明             |
| :----------- | :--------------- |
| never        | 表示しない       |
| always       | 常に表示         |
| error        | エラー時のみ表示 |

<!-- meta default="always" -->

### pleasanter-code-assist.strictSSL

SSL/TLS証明書の検証を行うかどうかを制御します。Node.jsで証明書を検証できない場合（例：自己署名証明書や信頼されていない証明書を使用する開発環境など）にのみ`false`に設定してください。この設定を`false`にすると証明書検証が無効化されるため、本番環境では使用しないでください。また、プロキシを用いた接続においても、Pleasanter Code Assistでは`http.proxyStrictSSL`は参照せず、こちらの設定のみを用います。

<!-- meta version="1.2.0" default="true" -->

## 3. 設定項目（Visual Studio Code標準）

Pleasanter Code Assistで参照しているVisual Studio Code標準の設定項目を概説します。

-   settings.jsonに記載することで、拡張機能の動作をカスタマイズできます。
-   settings.jsonをGUIで操作する場合には、名前の表記が異なりますのでご注意ください。

    !!! tip "「http.proxy」の場合の例"
        「Http: Proxy」と表記されます。

### http.noProxy

HTTP/HTTPSリクエストにおいてプロキシ設定を無視するドメイン名を指定します。

<!-- meta version="1.2.0" default_none -->

### http.proxy

使用するプロキシを設定してください。

<!-- meta version="1.2.0" default_none -->

### http.proxyAuthorization

すべてのネットワークリクエストに送信するProxy-Authorizationヘッダーの値を設定します。

<!-- meta version="1.2.0" default_none -->

### http.systemCertificates

OSからCA証明書を読み込むかどうかを制御します。

<!-- meta version="1.2.0" default="true" -->

## 対応バージョン

| 対応バージョン       | 内容                                                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| バージョン1.2.0 以降 | 以下の設定項目を追加<br>・pleasanter-code-assist.caPaths<br>・pleasanter-code-assist.showAxiosErrorResponseJson<br>・pleasanter-code-assist.strictSSL<br>・http.noProxy<br>・http.proxy<br>・http.proxyAuthorization<br>・http.systemCertificates |
| バージョン1.3.0 以降 | PCA: Save and Syncコマンドを追加                                                                                                                                                                                                                  |

## 関連情報

-   [Pleasanter Code Assist：コマンドによる作業フォルダ作成](pleasanter-code-assist-create-workfolder.md)
