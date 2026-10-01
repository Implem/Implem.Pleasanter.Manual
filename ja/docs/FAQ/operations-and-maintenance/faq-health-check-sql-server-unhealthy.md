---
title: ヘルスチェック機能でデータベース(SQLServer)の接続確認が"UnHealthy"となる
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-health-check-sql-server-unhealthy
translationKey: faq-health-check-sql-server-unhealthy
shortname: ''
created: 2024-08-27
updated: 2024-09-10
---

## 回答

[Rds.json](../../setup/parameters/rds-json.md)のUserConnectionStringパラメータの設定を編集してください。

---

## 概要

以下のようなヘルスチェックのレスポンスの場合、Rds.jsonのUserConnectionStringパラメータの設定値に「Encrypt=false;」を追記することで、正常なレスポンス(Healthy)となる可能性があります。

### レスポンス

```json
{
    "status": "Unhealthy",
    "totalDuration": "00:00:00.2663513",
    "entries": {
        "sqlserver": {
            "data": {},
            "description": "サーバーとの接続を正常に確立しましたが、ログイン中にエラーが発生しました。 (provider: SSL プロバイダー, error: 0 - 信頼されていない機関によって証明書チェーンが発行されました。)",
            "duration": "00:00:00.1871996",
            "exception": "サーバーとの接続を正常に確立しましたが、ログイン中にエラーが発生しました。 (provider: SSL プロバイダー, error: 0 - 信頼されていない機関によって証明書チェーンが発行されました。)",
            "status": "Unhealthy",
            "tags": []
        }
    }
}
```

### UserConnectionString

#### 編集前

```
"UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD;Connection Timeout=30;"
```

#### 編集後

```
"UserConnectionString": "Server=(local);Database=#ServiceName#;UID=#ServiceName#_User;PWD=SetUsersPWD;Connection Timeout=30;Encrypt=false;"
```

## 設定手順

1. App_Data/Parameters/Rds.jsonを開きます。
2. UserConnectionStringパラメータの設定値を編集します。
3. プリザンターを再起動します。
4. ヘルスチェックのエンドポイントへアクセスします。

## 関連情報

- [プリザンターのヘルスチェック機能を有効化する](../../managers-guide/ops-status-check/health-check.md)
- [パラメータ設定：Rds\.json](../../setup/parameters/rds-json.md)
- [パラメータ設定：Security\.json](../../setup/parameters/security-json.md)