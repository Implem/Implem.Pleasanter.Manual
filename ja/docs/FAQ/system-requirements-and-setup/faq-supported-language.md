---
title: プリザンターでサポートしている言語とタイムゾーンのパラメータの設定値を知りたい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-supported-language
translationKey: faq-supported-language
shortname: 言語,タイムゾーン
created: 2024-07-03
updated: 2024-07-18
---

## 回答

プリザンターでは、日本語、英語、中国語（簡体）、韓国語、ドイツ語、スペイン語、ベトナム語に対応しています。また、タイムゾーンに関しましては、お使いのOSで有効なタイムゾーン名を使用できます。

---

## 概要

### 1.プリザンターでサポートしている言語

[Service.json](../../setup/parameters/service-json.md)の「DefaultLanguage」に設定します。バージョン1.4.6以降では初回インストール時（CodeDefiner実行時）に指定します。既定値は"en"です。

| 言語       | 値  |
| :--------- | :-- |
| 日本語     | ja  |
| 英語       | en  |
| 中国語     | zh  |
| ドイツ語   | de  |
| 韓国語     | ko  |
| スペイン語 | es  |
| ベトナム語 | vn  |

### 2.タイムゾーン

[Service.json](../../setup/parameters/service-json.md)の「TimeZoneDefault」に設定します。Windows/Linuxで設定内容が異なりますので注意してください。
バージョン1.4.6以降では初回インストール時（CodeDefiner実行時）に指定します。既定値は"UTC"です。以下はタイムゾーンの一例になります。

| 国               | タイムゾーン(Windows)        | タイムゾーン(Linux) |
| :--------------- | :--------------------------- | :------------------ |
| グローバル       | UTC                          | UTC                 |
| 日本             | Tokyo Standard Time          | Asia/Tokyo          |
| アメリカ（東部） | Eastern Standard Time        | America/New_York    |
| 中国             | China Standard Time          | Asia/Shanghai       |
| ドイツ           | Central Europe Standard Time | Europe/Berlin       |
| 韓国             | Korea Standard Time          | Asia/Seoul          |
| スペイン         | Central Europe Standard Time | Europe/Madrid       |
| ベトナム         | SE Asia Standard Time        | Asia/Ho_Chi_Minh    |

そのほかのタイムゾーンは以下のコマンドを実行し適切なタイムゾーンを検索の上設定してください。

=== "Windows"

    ``` ps1
    tzutil /l
    ```

=== "Linux"

    ``` bash
    tzselect
    ```

## 関連情報

-   [プリザンターをAzure App Serviceにサーバレス構成でインストールする](../../setup/installation/install-manually/getting-started-pleasanter-azure.md)
-   [プリザンターをWindowsにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-windows.md)
-   [プリザンターをUbuntuにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-ubuntu.md)
-   [プリザンターをAlmaLinuxにインストールする](../../setup/installation/install-manually/getting-started-pleasanter-almalinux.md)
-   [プリザンターをRed Hat Enterprise Linux 8にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-rhel-8.md)
-   [プリザンターをRed Hat Enterprise Linux 9.7/10.1にインストールする](../../setup/installation/install-manually/getting-started-pleasanter-rhel.md)
-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)
