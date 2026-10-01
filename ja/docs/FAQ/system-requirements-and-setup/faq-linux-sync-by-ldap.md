---
title: .NET Core版（Linux）プリザンターにActive Directoryのユーザ情報を定期的に同期したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-linux-sync-by-ldap
translationKey: faq-linux-sync-by-ldap
shortname: ''
created: 2020-07-10
updated: 2024-04-29
---

**プリザンターのバージョン1.3.19.0以降では、設定ファイル[BackgroundService.json](../../setup/parameters/background-service-json.md)のSyncByLdapをtrueにすることで、毎日定時にLDAP同期処理を行う設定が可能となりました。本FAQは1.3.18以前のプリザンターの内容となります。**

## 回答

Toolsフォルダ内の「SyncByLdap.py」をcronで定期実行してください。

---

## 概要

LDAP同期処理を定期実行したい場合は、Toolsフォルダ内の「SyncByLdap.py」をcronで定期実行してください。

## 操作手順

1.  以下を事前に設定してください。
    1.  「プリザンターとActiveDirectoryを連携する。」を参照の上、パラメータ設定を行ってください。
    1.  python3をインストールしてください。
1.  プリザンターをマニュアルの手順に従ってインストールした場合は、/web/pleasanter/Toolsフォルダ配下に「SyncByLdap.py」が配置済みですので、手順6に進んでください。
1.  上記ファイルが存在しない場合は、以下手順4,5を実施してください。
1.  プリザンターをダウンロードします。
1.  ダウンロードしたzipファイル内にある「Tools/SyncByLdap.py」を任意のディレクトリにコピーします。
1.  「SyncByLdap.py」をエディタで開き、URLを指定する部分の`[http://localhost/pleasanter]`はご利用の環境に合わせて修正してください。
1.  cron設定を行ってください。以下は、LDAP同期処理を午前2時に実行するようにrootユーザのcronに設定するサンプルです。

    ``` cron
    # crontab -e
    0 2 * * * python3 /web/pleasanter/Tools/SyncByLdap.py
    ```
