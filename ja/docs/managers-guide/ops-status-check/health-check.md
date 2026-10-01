---
title: ヘルスチェック機能
category: その他
order: '0'
status: ''
parts: ''
urlstring: health-check
translationKey: health-check
shortname: ヘルスチェック機能
created: 2024-09-06
updated: 2026-08-12
---

## 概要

プリザンターの稼働状況を確認するための機能です。

## 前提条件

ヘルスチェック機能を有効化するには、[Security.json](../../setup/parameters/security-json.md)の"HealthCheck": {"Enabled"}パラメータの値をtrueに設定してください。

詳細は[プリザンターのヘルスチェック機能を有効化する](../../setup/additional/ops-management/enable-health-check.md)を参照してください。

## エンドポイント

ヘルスチェック機能のエンドポイントは /healthzです。http\://localhostの場合、アクセスすべきURLはhttp\://localhost/healthzです。

## データベース稼働状況の監視

データベース稼働状況の監視も同時に実施可能です。

データベース稼働状況監視を有効化するには、[Security.json](../../setup/parameters/security-json.md)の"HealthCheck": {"EnableDatabaseCheck"}パラメータの値をtrueに設定してください。

## 監視元の制限

監視を行うホスト（監視元）を制限できます。[Security.json](../../setup/parameters/security-json.md)の"HealthCheck": {"RequireHosts"}パラメータに指定したホスト（監視元）からのみ、エンドポイントへアクセスできるようになります。

## システムログへの記録について

エンドポイントへのアクセスはシステムログへ記録されません。

## レスポンス例

### デフォルト

以下は[Security.json](../../setup/parameters/security-json.md)で"HealthCheck": {"Enabled": true}と設定した場合のレスポンス例です。

#### 正常時

<details markdown="1">
<summary>ブラウザ上でのhttpアクセス結果</summary>

![デフォルトのヘルスチェックで正常時のレスポンスをブラウザに表示した結果](https://pleasanter.org/files/images/ja/managers-guide/ops-status-check/assets/c2dc2aa887054b1899ca66ae7f8c952a.png)

</details>

<details markdown="1">
<summary>curlコマンド実行結果</summary>

``` bash
> curl -v http://localhost:59802/healthz
* Host localhost:59802 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
*   Trying [::1]:59802...
* Connected to localhost (::1) port 59802
> GET /healthz HTTP/1.1
> Host: localhost:59802
> User-Agent: curl/8.8.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK   
< Cache-Control: no-cache,no-store
< Pragma: no-cache
< Transfer-Encoding: chunked
< Content-Type: text/plain
< Expires: -1
< Server: Microsoft-IIS/10.0
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
< X-Content-Type-Options: nosniff
< Set-Cookie: .AspNetCore.Session=CfDJ8BhRE%2F1n6gFEg%2FFi5QpkmjYBXzH3hLQuPSWT3%2FWSicn0%2FoTkvL0gQxL0PhIpEllpSThoIScuxLx%2BBkzflF7s6QtQ0KQbEZHNj6GFer1zDY31zIheRbyVqmuE%2FFCy3jFYe0YyRRwZCVcEDIngCpWN7ShO5eDwpYHh0rSTSwTqNrbg; path=/; samesite=lax; httponly
< Date: Fri, 30 Aug 2024 07:46:49 GMT
<
Healthy* Connection #0 to host localhost left intact
```

</details>

#### 異常時

<details markdown="1">
<summary>ブラウザ上でのhttpアクセス結果</summary>

![デフォルトのヘルスチェックで異常時のレスポンスをブラウザに表示した結果](https://pleasanter.org/files/images/ja/managers-guide/ops-status-check/assets/ac92726ff9f84eaa9e7c4b95fe535f70.png)

</details>

<details markdown="1">
<summary>curlコマンド実行結果</summary>

``` bash
> curl -v http://localhost:59802/healthz
* Host localhost:59802 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
*   Trying [::1]:59802...
* Connected to localhost (::1) port 59802
> GET /healthz HTTP/1.1
> Host: localhost:59802
> User-Agent: curl/8.8.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 503 Service Unavailable
< Cache-Control: no-cache,no-store
< Pragma: no-cache
< Transfer-Encoding: chunked
< Content-Type: text/plain
< Expires: -1
< Server: Microsoft-IIS/10.0
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
< X-Content-Type-Options: nosniff
< Set-Cookie: .AspNetCore.Session=CfDJ8BhRE%2F1n6gFEg%2FFi5QpkmjbLLy0X9bkXSSPBceSDvwq0hxTGGAn%2BvIlQvdTzLl1MXvJdDKZ1pIIzHiRPLyQXvrbfMPZ%2FuRDj%2BY9yC60FDJ6X0s2nDzb%2B5cA234mlFzZCFd5lhEe6aO0u3V8T0OBdm1d5WOVj1QDxTX6iMSTLykpd; path=/; samesite=lax; httponly
< Date: Fri, 30 Aug 2024 09:31:56 GMT
<
Unhealthy* Connection #0 to host localhost left intact
```

</details>

### 詳細なレスポンス

以下は、上記に加え、[Security.json](../../setup/parameters/security-json.md)の"HealthCheck": {"EnableDetailedResponse": true}と設定した場合のレスポンス例です。以下のパラメータを含む、詳細なレスポンスが返却されます。

#### EnableDetailedResponse

| パラメータ名  | 説明                                                                                            |
| :------------ | :---------------------------------------------------------------------------------------------- |
| status        | すべての正常性チェックの集計状態を示します。                                                    |
| totalDuration | ヘルスチェックにかかった時間を示します。                                                        |
| entries       | 各正常性チェックの結果を示します。結果の各パラメータについては後述のentriesを確認してください。 |

#### entries

| パラメータ名 | 説明                                                             |
| :----------- | :--------------------------------------------------------------- |
| data         | コンポーネントの正常性を説明する追加のキーと値のペアを示します。 |
| description  | チェック対象のコンポーネントの状態を示します。                   |
| duration     | 正常性チェックの実行時間を示します。                             |
| exception    | 状態をチェックするときにスローされた例外を示します。             |
| status       | チェック対象のコンポーネントの正常性状態を示します。             |
| tags         | 正常性チェックに関連付けられているタグを示します。               |

上記のパラメータ（プロパティ）の詳細は、Microsoft社の公式ドキュメントを確認してください。

1.  [ASP.NET Core のルーティング > RequireHost とルートが一致するホスト](https://learn.microsoft.com/ja-jp/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#host-matching-in-routes-with-requirehost)
1.  [HealthReport クラス (Microsoft.Extensions.Diagnostics.HealthChecks)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreport?view=net-8.0)
1.  [HealthReportEntry 構造体 (Microsoft.Extensions.Diagnostics.HealthChecks)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreportentry?view=net-8.0)

以下はパラメータを有効化した際のレスポンス例となります。

#### 正常時

<details markdown="1">
<summary>ブラウザ上でのhttpアクセス結果</summary>

![詳細なレスポンスで正常時のヘルスチェック結果をブラウザに表示した結果](https://pleasanter.org/files/images/ja/managers-guide/ops-status-check/assets/a9122324b0f64a9da63fcea9537b1a87.png)

</details>

<details markdown="1">
<summary>curlコマンド実行結果</summary>

``` bash
> curl -v http://localhost:59802/healthz
* Host localhost:59802 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
*   Trying [::1]:59802...
* Connected to localhost (::1) port 59802
> GET /healthz HTTP/1.1
> Host: localhost:59802
> User-Agent: curl/8.8.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Cache-Control: no-cache,no-store
< Pragma: no-cache
< Transfer-Encoding: chunked
< Content-Type: application/json
< Expires: -1
< Server: Microsoft-IIS/10.0
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
< X-Content-Type-Options: nosniff
< Set-Cookie: .AspNetCore.Session=CfDJ8BhRE%2F1n6gFEg%2FFi5QpkmjaiitMqPqEs7TbYFEEFcn15Jp4YlUELnyMVYVOWv8Gxm9ulRUliba3n9iqP2LUPxXyjkAtR64tjpiU6KI6d8uvYTYwSuMQltVPqREVq0aIYJdZJz7MpPzwcgd%2FZfr49Vr20ivKL5xDaVY8UHGUNjapU; path=/; samesite=lax; httponly
< Date: Fri, 06 Sep 2024 04:33:53 GMT
<
{"status":"Healthy","totalDuration":"00:00:00.0034430","entries":{"sqlserver":{"data":{},"duration":"00:00:00.0032497","status":"Healthy","tags":[]}}}* Connection #0 to host localhost left intact
```

</details>

#### 異常時

<details markdown="1">
<summary>ブラウザ上でのhttpアクセス結果</summary>

![詳細なレスポンスで異常時のヘルスチェック結果をブラウザに表示した結果](https://pleasanter.org/files/images/ja/managers-guide/ops-status-check/assets/3aaee80215104ce5b4e72ddb5554aee8.png)

</details>

<details markdown="1">
<summary>curlコマンド実行結果</summary>

``` bash
> curl -v http://localhost:59802/healthz
* Host localhost:59802 was resolved.
* IPv6: ::1
* IPv4: 127.0.0.1
*   Trying [::1]:59802...
* Connected to localhost (::1) port 59802
> GET /healthz HTTP/1.1
> Host: localhost:59802
> User-Agent: curl/8.8.0
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 503 Service Unavailable
< Cache-Control: no-cache,no-store
< Pragma: no-cache
< Transfer-Encoding: chunked
< Content-Type: application/json
< Expires: -1
< Server: Microsoft-IIS/10.0
< X-Frame-Options: SAMEORIGIN
< X-Xss-Protection: 1; mode=block
< X-Content-Type-Options: nosniff
< Set-Cookie: .AspNetCore.Session=CfDJ8BhRE%2F1n6gFEg%2FFi5QpkmjbdJ%2BduGBq4Z0W3jus8FOO73FKVvJnG3%2FLl7BY6xMs78%2BnhDKEqvQIPgzAzlQK0pmILAQNNw8nMUfSjdkW1QtGKMx%2Fklg95mZEo44NtHfsgKX5a7ikO%2BSpAe%2Bqqe7DuxAsNeDHxXdgFT8rOIur7ELB7; path=/; samesite=lax; httponly
< Date: Fri, 06 Sep 2024 04:31:31 GMT
<
{"status":"Unhealthy","totalDuration":"00:00:00.0096425","entries":{"sqlserver":{"data":{},"description":"サーバーとの接続を正常に確立しましたが、ログイン中にエラーが発生しました。 (provider: SSL プロバイダー, error: 0 - 信頼されていない機関によって証 明書チェーンが発行されました。)","duration":"00:00:00.0081609","exception":"サーバーとの接続を正常に確立しましたが、ログイン中にエラーが発生しました。 (provider: SSL プロバイダー, error: 0 - 信頼されていない機関によって証明書チェーンが発行されました。)","status":"Unhealthy","tags":[]}}}* Connection #0 to host localhost left intact
```

</details>

## 対応バージョン

| 対応バージョン | 内容     |
| :------------- | :------- |
| 1.4.8.0 以降   | 機能追加 |

## 関連情報

-   [パラメータ設定：Security.json](../../setup/parameters/security-json.md)
-   [プリザンターのヘルスチェック機能を有効化する](../../setup/additional/ops-management/enable-health-check.md)
-   [ASP.NET Core のルーティング > RequireHost とルートが一致するホスト](https://learn.microsoft.com/ja-jp/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#host-matching-in-routes-with-requirehost)
-   [HealthReport クラス (Microsoft.Extensions.Diagnostics.HealthChecks)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreport?view=net-8.0)
-   [HealthReportEntry 構造体 (Microsoft.Extensions.Diagnostics.HealthChecks)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreportentry?view=net-8.0)
