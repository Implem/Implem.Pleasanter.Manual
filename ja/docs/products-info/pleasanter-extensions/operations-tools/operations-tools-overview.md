---
title: 機能概要
category: 運用支援ツール
order: '1000'
status: ''
parts: ''
urlstring: operations-tools-overview
translationKey: operations-tools-overview
shortname: Pleasanter Extensions,Operations Tools,機能概要
created: 2025-01-27
updated: 2026-01-14
---

## 概要

本ソフトウェアは、プリザンターの運用者向けに利用状況、性能状況、アクセス権一覧などの確認や監視アラートの設定、不要サイトの削除依頼機能を提供します。各機能はプリザンターの拡張DLLとして設定し、指定のURLにアクセスすることにより動作します。

[https://github.com/Implem/Implem.OperationsTools](https://github.com/Implem/Implem.OperationsTools)

![Operations Tools の画面例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/2013fba2568d4bc690005d65ffc8d22d.png)

## バージョン

1.4.0

## 動作環境

本ソフトウェアは下記の環境で動作します。プリザンターのセットアップが完了していれば、プリザンターの実行環境にOperations Toolsの拡張DLLをセットアップするだけで動作します。セットアップ手順は以下ページを参照してください。

[Operations Tools：セットアップ](operations-tools-setup.md)

### 動作確認済み環境

-   Windows環境：Windows 11 / SQL Server 2022（.NET 10.0）
-   Linux環境：Ubuntu 22.04 / PostgreSQL 18（.NET 10.0）
-   Azure環境：App Service / SQL データベース（.NET 10.0）
-   Docker環境（.NET 10.0）

### 関連情報

FAQ：プリザンターの動作環境や推奨スペックが知りたい | Pleasanter  
[https://pleasanter.org/manual/faq-recommended-specifications](../../../FAQ/system-requirements-and-setup/faq-recommended-specifications.md)

## 制限事項

1.  本ソフトウェアはプリザンターの拡張DLLとして動作します。Pleasanter.netの環境では使用できません。
2.  本ソフトウェアは一部の画面でプリザンターのシステムログが記録されるSysLogsテーブルなどの各テーブルから必要な情報を抽出して画面情報を表示します。動作環境のスペックが低い場合、期待したパフォーマンスが出ない可能性があります。（ver.1.1.0以降では表示データを中間テーブルに保持する仕様になったことでパフォーマンスが向上しています。）

    !!! note
        参考情報として、パフォーマンスの動作確認は以下の環境で行っています。
        
        - Linux環境：SysLogsテーブルが約370万件、CPU: 4 vCPUs、メモリ: 32 GB
        - Azure環境：SysLogsテーブルが約370万件、SQL データベース：200 DTU

3.  [システムログの拡張機能](../../../managers-guide/system-log-administration/syslog-extension.md)を利用していない場合は、API関連などの一部情報が参照できません。

## 前提条件

1.  本ソフトウェアを使用するには、以下のいずれかの条件を満たしている必要があります。

    - 利用環境のプリザンターにEnterprise Edition[^1]が適用されている
    - 利用環境のプリザンターで[Pleasanter Extensionsトライアル](../../../developers-guide/index.md)を実施中である

2.  本ソフトウェアはプリザンターver.1.5.0.0以降で動作します。プリザンターver.1.5.0.0より前のバージョンをご利用中の場合は、プリザンターをバージョンアップしてください。

[^1]: Enterprise Editionについては「プリザンター年間サポートサービス」サービス仕様書を参照してください。申し込んだサポートプランによっては、Enterprise Editionの適用によりプリザンターのユーザ数に制限がかかる場合があります。

## 機能一覧

本ソフトウェアは下記の機能を提供します。

### 運用レポート

| 機能名                                                                              | 概要                                                     |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------- |
| [運用レポート：全体](operations-tools-operation-general.md)（利用状況／性能状況）   | プリザンターの全体的な利用状況や性能状況を確認します     |
| 運用レポート：[性能状況：日別](operations-tools-operation-performance-by-day.md)    | プリザンターの性能状況を日別で確認します                 |
| 運用レポート：[性能状況：時間別](operations-tools-operation-performance-by-time.md) | プリザンターの性能状況を時間別（15分単位）で確認します。 |

### 利用状況詳細

プリザンターの利用状況詳細を確認できる画面です。「月別」「日別」「詳細」を選択することができます。

| 機能名                                                                          | 概要                                                          |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| [利用状況詳細：月別](operations-tools-usage-by-month.md)                        | プリザンターの利用状況詳細を月別で確認します                  |
| [利用状況詳細：日別](operations-tools-usage-by-day.md)                          | プリザンターの利用状況詳細を日別で確認します                  |
| 利用状況詳細：[ログイン履歴](operations-tools-usage-login.md)                   | プリザンターの利用状況詳細としてログイン履歴を確認します      |
| 利用状況詳細：[メール送信履歴](operations-tools-usage-outgoingmails.md)         | プリザンターの利用状況詳細としてメール送信履歴を確認します    |
| 利用状況詳細：[APIリクエスト履歴](operations-tools-usage-api-requests.md)       | プリザンターの利用状況詳細としてAPIリクエスト履歴を確認します |

### 監視アラート

プリザンターの監視アラートとして「データベース」「システムテーブル」「サイト」の単位で現在値の確認やアラートの上限値を設定できる画面です。また、システムテーブルやサイトの明細情報を確認することができます。

| 機能名                                                                         | 概要                                                                                                                         |
| ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| [監視アラート：アラート設定](operations-tools-monitoring-alert-setting.md)     | 「データベース」「システムテーブル」「サイト」に上限値を入力し、更新ボタンをクリックすることでアラートの上限値を設定できます |
| [監視アラート：システムテーブル](operations-tools-monitoring-system-talbes.md) | システムテーブルの明細情報は「システムテーブル名」を指定してフィルタすることができます                                       |
| [監視アラート：サイト](operations-tools-monitoring-sites.md)                   | サイトの明細情報は「サイト名」を指定してフィルタすることができます                                                           |

### サイト情報一覧

| 機能名                                     | 概要                                     |
| ------------------------------------------ | ---------------------------------------- |
| [サイト情報一覧](operations-tools-sites.md) | プリザンターのサイト情報一覧を確認します |

### アクセス権一覧

| 機能名                                            | 概要                                             |
| ------------------------------------------------- | ------------------------------------------------ |
| [アクセス権一覧](operations-tools-permissions.md) | プリザンターのサイトのアクセス権一覧を確認します |

### パラメータ一覧

| 機能名                                           | 概要                                                       |
| ------------------------------------------------ | ---------------------------------------------------------- |
| [パラメータ一覧](operations-tools-parameters.md) | プリザンターのパラメータ一覧と設定値の変更有無を確認します |

### 共通機能

| 機能名                                                           | 概要                     |
| ---------------------------------------------------------------- | ------------------------ |
| [共通機能：サイドメニュー](operations-tools-common-site-menu.md) | サイドメニューの説明です |
| [共通機能：エクスポート](operations-tools-common-export.md)      | エクスポートの説明です   |

![Operations Tools の機能一覧を示す画面例](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/operations-tools/assets/4974e99bdd074fb9819f69390516f8c7.png)

## 関連情報

### Operations Tools

-   [セットアップ](operations-tools-setup.md)
-   [運用レポート：全体（利用状況／性能状況）](operations-tools-operation-general.md)
-   [運用レポート：性能状況：日別](operations-tools-operation-performance-by-day.md)
-   [運用レポート：性能状況：時間別](operations-tools-operation-performance-by-time.md)
-   [利用状況詳細：月別](operations-tools-usage-by-month.md)
-   [利用状況詳細：日別](operations-tools-usage-by-day.md)
-   [利用状況詳細：ログイン履歴](operations-tools-usage-login.md)
-   [利用状況詳細：メール送信履歴](operations-tools-usage-outgoingmails.md)
-   [利用状況詳細：APIリクエスト履歴](operations-tools-usage-api-requests.md)
-   [監視アラート：アラート設定](operations-tools-monitoring-alert-setting.md)
-   [監視アラート：システムテーブル](operations-tools-monitoring-system-talbes.md)
-   [監視アラート：サイト](operations-tools-monitoring-sites.md)
-   [サイト情報一覧](operations-tools-sites.md)
-   [アクセス権一覧](operations-tools-permissions.md)
-   [パラメータ一覧](operations-tools-parameters.md)
-   [共通機能：サイドメニュー](operations-tools-common-site-menu.md)
-   [共通機能：エクスポート](operations-tools-common-export.md)
-   [システムログの拡張機能](../../../managers-guide/system-log-administration/syslog-extension.md)
-   [Pleasanter Extensionsのトライアル](../../../developers-guide/index.md)
