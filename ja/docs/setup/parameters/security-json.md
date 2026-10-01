---
title: Security.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: security-json
translationKey: security-json
shortname: Security.json
created: 2019-04-30
updated: 2026-08-12
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 制限事項

### IpRestrictionExcludeMembersに設定した組織/グループについて

組織/グループ単位でプリザンターへアクセスを許可している場合、「組織管理機能」/「グループ管理機能」を使用して、該当組織/該当グループの削除/無効化/所属するユーザの削除を行うと、所属ユーザはプリザンターへアクセスできなくなります。テナント管理者等の重要な管理権限をもつユーザがプリザンターへアクセスできなくなった場合、使用機器のIPアドレス変更または「Security.json」の再設定等の作業が必要になる可能性があります。IpRestrictionExcludeMembersに設定した組織/グループの削除/無効化/所属するユーザの削除を行う際は、注意してください。

※AllowIpAddressesでIPアドレスによるアクセス制限を行っていない場合、上記制限事項への考慮は必要ありません。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|AllowIpAddresses|[ "10.10.10.10", "10.10.10.20", "10.10.1.0/24" ]|IPアドレスによりアクセスを制限する場合に利用します。許可したい接続元IPアドレスを指定します。指定方法は、IPアドレスによる表記およびCIDR表記による指定が可能です。nullの場合、IPアドレスによる制限は行いません。|
|IpRestrictionExcludeMembers|[ "User1", "User100", "Dept1", "Group1" ]|AllowIpAddressesにIPアドレスを設定した際に、併せて設定可能です。AllowIpAddressesに設定したIPアドレス以外からのアクセスであっても、本パラメータに指定した条件を満たすユーザについては、アクセスを許可します。詳細は後述の「AllowIpAddresses/IpRestrictionExcludeMembersの組み合わせ」を参照してください。|
|MimeTypeCheckOnApi|false||
|PrivilegedUsers|[ "Administrator", "AdminUser1", "AdminUser2" ]|[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)のログインIDを指定します。[特権ユーザ](../../managers-guide/user-administration/user-management-privileged-users.md)は権限の無いサイトの操作を含め、すべての操作を行うことができます。複数のユーザをカンマ区切りで指定することができます。|
|RevealUserDisabled|false|ユーザが無効化されている事をログイン時にエラーとして表示する場合にはtrueを指定。|
|LockoutCount|10|パスワードを間違った回数が設定回数を超えた場合に自動的にアカウントをロックします。ロックされたアカウントはユーザ管理画面で解除する必要があります。0に設定した場合にはアカウントはロックされません。|
|PasswordExpirationPeriod|90|ローカルユーザのパスワードの有効期間を計算するための日数を指定。0に設定した場合には有効期間無し。|
|JoeAccountCheck|true|同一のログインIDとパスワードを使用することを禁止する場合にはtrueを指定。|
|TokenCheck|false|CSRF（クロスサイトリクエストフォージェリ）対策として、セッション毎にトークンを発行しトークンがリクエストに含まれないPOST要求を不正なリクエストとして拒絶する場合はtrueを指定。[フォーム](../../managers-guide/manage-table/form/index.md)機能を有効化した場合、本パラメータの設定は機能しません（ASP.NET Core標準のCSRF対策を組み込んでいるため、CSRF対策は常に動作します）。|
|SecureCookies|false|SSL/TLS通信を使用する環境でcookieにsecure属性を付与する場合はtrueを指定。|
|DisableMvcResponseHeader|false|レスポンスヘッダに "X-AspNet-Mvc-Version"ヘッダを含めないようにする場合にtrueを設定します。※.NetFramework版のみ有効 |
|DisableDeletingSiteAuthentication|false|サイト削除時に認証情報（ログインID／パスワード）を入力せずに削除を許可する場合はtrueを指定。|
|AccessControlAllowOrigin|["*"]|オリジン間リソース共有 (CORS)の許可するサイトのURLを指定。*の場合には全てを許可。|
|EnforcePasswordHistories|12|過去に設定されたパスワードの履歴を記録する回数を指定します。過去に使用したパスワードの再利用を禁止します。|
|DisableCheckPasswordPolicyIfApi|false|APIでユーザを作成する際にパスワードポリシーを無視する場合にはtrueを指定。LDAP認証の場合などで、作成するユーザのパスワードを指定したくない場合に利用します。|
|PasswordPolicies|設定方法は後述|パスワードポリシーとエラーメッセージを指定します。複数のポリシーを組み合わせて設定できます。|
|PasswordGenerator|true|[ユーザ管理](../../managers-guide/user-administration/index.md)などのパスワード入力欄の右側にパスワード自動生成用のアイコン（鍵アイコン）を表示する場合にtrueを指定。|
|SecondaryAuthentication|設定方法は後述|二段階認証を行う場合はEnabledをtrueに設定します。|
|AspNetCoreDataProtection|設定方法は後述|Microsoft Azure の環境でASP.NET Coreデータ保護の構成を行う際の設定を記述します。|
|HttpStrictTransportSecurity|設定方法は後述|HTTP Strict Transport Security プロトコルを適用して、HTTPSでの通信を強制させます。|
|SecureCacheControl|設定方法は後述|レスポンスヘッダにCache-Controlヘッダを含めるよう設定します。|
|HealthCheck|設定方法は後述|[ヘルスチェック機能](../additional/ops-management/enable-health-check.md)を使用する場合はEnabledをtrueに設定します。|
|ContentSecurityPolicy|設定方法は後述|[コンテンツセキュリティポリシー機能](../additional/security/content-security-policy.md)を使用する場合はEnabledをtrueに設定します。|
|ShowLoginPageOnAuthError|true|プリザンターにログインしていない状態で、プリザンターが解釈可能なURLへアクセスした場合、ログイン画面へ遷移させる場合はtrueに、404ページへ遷移させる場合はfalseに設定します。|
|CaptchaConfig|設定方法は後述|[フォーム](../../managers-guide/manage-table/form/index.md)機能で使用するCAPTCHAを構成します。|
|ForwardedHeaders|設定方法は後述|信頼するリバースプロキシのネットワーク・IPを指定します。[信頼済みリバースプロキシ認証](../additional/authn-authz/trusted-reverse-proxy-auth.md)（[Authentication.json](authentication-json.md)のパラメータTrustedProxyParameters）と組み合わせて使用します。|
|ExcludeCookiePrefixes|["AWSALB", "AWSELB"]|ログアウト時に削除対象外とするCookieのプレフィックスを指定します。|

### AllowIpAddresses/IpRestrictionExcludeMembersの組み合わせ

下記1.～3.のいずれかの組み合わせで、AllowIpAddresses/IpRestrictionExcludeMembersを設定してください。

1. AllowIpAddresses：null / IpRestrictionExcludeMembers：null

    |内容|対象のアクセス|
    |:--|:--|
    |アクセスを許可する接続|すべてのIPアドレスからのアクセス|
    |アクセスを制限する接続|なし|

2. AllowIpAddresses：IPアドレスを設定 / IpRestrictionExcludeMembers：null

    |内容|対象のアクセス|
    |:--|:--|
    |アクセスを許可する接続|AllowIpAddressesに設定したIPアドレスからのアクセス|
    |アクセスを制限する接続|AllowIpAddressesに設定したIPアドレス以外からのアクセス|

3. AllowIpAddresses：IPアドレスを設定 / IpRestrictionExcludeMembers：後述する「IpRestrictionExcludeMembersの設定例」の通りにユーザID/組織ID/グループIDを設定

    |内容|対象のアクセス|
    |:--|:--|
    |アクセスを許可する接続|①AllowIpAddressesに設定したIPアドレスからのアクセス<br/>②AllowIpAddressesに設定したIPアドレス以外からのアクセス、かつ、後述する「IpRestrictionExcludeMembersの設定例」の形式で許可されたユーザのアクセス|
    |アクセスを制限する接続|AllowIpAddressesに設定したIPアドレス以外からのアクセス、かつ、後述する「IpRestrictionExcludeMembersの設定例」の形式で許可されたユーザ以外のアクセス|

#### IpRestrictionExcludeMembersの設定例

|設定例|結果|
|:--|:--|
|["User1"]|ユーザID:1のユーザのアクセスを許可します。|
|["Dept1"]|組織ID:1に所属するユーザのアクセスを許可します。|
|["Group1"]|グループID:1に所属するユーザ/「グループID:1に所属する組織」に所属するユーザのアクセスを許可します。|

["User1","Dept1","Group1"]のようにカンマ区切りで複数のIDをIpRestrictionExcludeMembersに指定すると、いずれかと一致するユーザのアクセスを許可します。

### PasswordPoliciesの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|このポリシーを利用するかどうかをtrue/falseで設定します。|
|Regex|設定方法は後述|パスワードに含む必要のある文字列を正規表現で設定します。|
|Languages|任意のエラーメッセージ|エラーメッセージを対応する言語毎に設定します。|

### Regexに設定する正規表現の例

|正規表現|説明|
|:--|:--|
|".{8,}"|パスワードの長さは8文字以上必要です。|
|"[a-z]+"|アルファベット小文字が1文字以上必要です。|
|"[A-Z]+"|アルファベット大文字が1文字以上必要です。|
|"[0-9]+"|数字が1文字以上必要です。|
|"[^a-zA-Z0-9]+"|アルファベットと数字以外の文字(記号)が1文字以上必要です。|

### SecondaryAuthenticationの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|~~Enabled~~|~~true~~|~~このポリシーを利用するかどうかをtrue/falseで設定します。~~　※１|
|Mode|"None"|2段階認証機能の利用を設定します。|
|NotificationType|"Mail"|認証方式を設定します。"Mail"または"Totp"が設定可能です。※2|
|CountTolerances|1|TOTP認証時、有効とする確認コードの世代数を指定します。※2|
|NotificationMailBcc|true|認証コードをSupportFromのアドレスにBCCで送付するかどうかをtrue/falseで設定します。|
|AuthenticationCodeCharacterType|"Number"|認証コードの文字種を設定します。（Number: 数字のみ、Letter: 英字のみ、NumberAndLetter: 数字と英字）|
|AuthenticationCodeLength|128|文字数を設定します。|
|AuthenticationCodeExpirationPeriod|300|認証コードの有効時間を秒単位で設定します。|

※１ プリザンター 1.3.2.0 以降、プリザンター .NET Framework版 0.51.2 以降のバージョンより廃止となりました。代替パラメータとして、Modeをご利用ください。

※2 各認証方式についての詳細は、下記マニュアルを確認してください。
[メールによる二段階認証を有効にする](../additional/authn-authz/secondary-authentication.md)
[TOTP（Time-based One-Time Password）による二段階認証を有効にする](../additional/authn-authz/totp-authentication.md)

###  Modeの設定

|設定値|説明|
|:--|:--|
|None|2段階認証機能を無効にします。|
|DefaultEnable|2段階認証機能を有効にし、既定設定として全てのユーザに対して2段階認証を有効化します。[ユーザ管理](../../managers-guide/user-administration/index.md)から、任意のユーザに対し2段階認証を無効化する設定ができます。|
|DefaultDisable|2段階認証機能を有効にし、既定設定として全てのユーザに対して2段階認証を無効化します。[ユーザ管理](../../managers-guide/user-administration/index.md)から、任意のユーザに対し2段階認証を有効化する設定ができます。|

### AspNetCoreDataProtectionの設定

#### データ保護キーを永続化する場所について

BlobContainerUriとKeyIdentifierを両方指定した場合は、BlobContainerUriで指定したURL上に永続化します。BlobContainerUriとKeyIdentifierのどちらかまたは両方nullで、KeyValueStoreConnectionStringを指定した場合は、KeyValueStoreConnectionStringで指定したKVS（Redis）上に永続化します。いずれにも当てはまらない場合は、DBに永続化します。KVSへの永続化の詳細は「[ASP.NET Coreデータ保護キーを外部保存する](../additional/ready-for-clustering/data-protection-key-store.md)」を参照してください。

#### Asp.NET Coreのデータ保護について

Asp.NET Coreのデータ保護の詳細や設定方法につきましては、Microsoft社の公式ドキュメントを確認してください。
[ASP.NET Core データ保護の構成](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/overview)
[ASP.NET Core でのデータ保護のキー管理と有効期間](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/default-settings)
[ASP.NET Core でのキー ストレージ プロバイダー](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/implementation/key-storage-providers)

#### パラメータ一覧

|パラメータ名|設定例|説明|
|:--|:--|:--|
|BlobContainerUri|"https://stragename.blob.core.<br>windows.net/containername"|データ保護キーを永続化するBlobコンテナのURLを指定します。システム環境変数に登録可能。|
|KeyIdentifier|"https://keyvalult-name.vault.<br>azure.net/keys/key-name/...."|データ保護キーを保護するための暗号化キーを管理するAzure Key Vaultのキー識別子を指定します。システム環境変数に登録可能。|
|KeyFileName|"keys.xml"|Blobコンテナに永続化されるデータ保護キーのファイル名を指定します。|
|XmlAesKey|"a0b1c2..."|データ保護キーを保護するための暗号化キーを生成するための文字列を指定します。nullの場合は内部で自動的に文字列を指定します。ロードバランサーによる負荷分散構成で複数のプリザンターがある場合でかつこのパラメータで文字列を指定する場合は、全てのプリザンターで同じ文字列を指定してください。システム環境変数に登録可能。|
|KeyValueStoreConnectionString|"localhost:6379,<br>abortConnect=false"|データ保護キーを永続化するKVS（Redis）の接続文字列を指定します。BlobContainerUriとKeyIdentifierを両方指定した場合は、そちらが優先されます。システム環境変数に登録可能。|
|KeyValueStoreKeyName|"Pleasanter:DataProtection-Keys"|KVSに永続化するデータ保護キーのキー名を指定します。nullの場合は「（[Service.json](service-json.md)の「Name」）:DataProtection-Keys」を使用します。システム環境変数に登録可能。|

### HttpStrictTransportSecurityの設定

#### HTTP Strict Transport Security (HSTS)について

HTTP Strict Transport Security (HSTS) は、応答ヘッダーを使って Web アプリによって指定されるオプトイン セキュリティ拡張機能です。HSTS をサポートするブラウザーがこのヘッダーを受け取ると、次のようになります。

-   ブラウザーに、HTTP 経由の通信を送信できないようにするドメインの構成が保存されます。 ブラウザーでは、すべての通信が強制的に HTTPS 経由で実行されます。
-   ブラウザーによって、ユーザーが信頼されていない証明書や無効な証明書を使えなくなります。 ユーザーがそのような証明書を一時的に信頼できるようにするプロンプトがブラウザーで無効になります。

詳細は下記ドキュメントを参照ください。
[HTTP Strict Transport Security プロトコル (HSTS)|Microsoft Learn](https://learn.microsoft.com/ja-jp/aspnet/core/security/enforcing-ssl#http-strict-transport-security-protocol-hsts)

#### パラメータ一覧

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|HSTS機能を有効にします|
|Preload|false|Strict-Transport-Security ヘッダーのプリロード パラメーターを設定します。 プリロードは RFC HSTS 仕様の一部ではありませんが、Web ブラウザーでは、新規インストール時に HSTS サイトのプリロードを行うことがサポートされています。 |
|IncludeSubDomains|false|includeSubDomain を有効にします。これにより、HSTS ポリシーがホスト サブドメインに適用されます。|
|MaxAge|30.00:00:00|Strict-Transport-Security ヘッダーの max-age パラメーターを設定します。設定しない場合、既定値は 30 日です。次のフォーマットに従って値を設定します。 "{日数}.{時間}:{分}:{秒}"|
|ExcludeHosts|["abc.example.com", "xyx.example.com"]|除外するホスト名を配列形式で指定します。|

### SecureCacheControlの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|NoCache|false|Cache-Controlヘッダにno-cacheパラメータを付与します。|
|NoStore|false|Cache-Controlヘッダにno-storeパラメータを付与します。|
|Private|false|Cache-Controlヘッダにprivateパラメータを付与します。|
|MustRevalidate|false|Cache-Controlヘッダにmust-revalidateパラメータを付与します。|
|PragmaNoCache|false|Pragma:no-cache ヘッダをレスポンスに含めます。|

※NoCache,NoStore,Private,MustRevalidateの何れかをtrueとした場合にCache-Controlヘッダがレスポンスに付加されます。

※各パラメータの詳細については下記ドキュメントを確認してください
[Cache-Control|MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control)
[Pragma|MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Pragma)

### HealthCheckの設定

#### パラメータ一覧

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|true|ヘルスチェック機能を有効にします。|
|EnableDatabaseCheck|true|ヘルスチェック機能でデータベースの接続確認を有効にします。※|
|HealthQuery|"select 1;"|データベースの接続確認で使用するSQLを指定します。|
|RequireHosts|["192.168.1.100"]|指定したホストからのみヘルスチェックが行えるよう制約を適用する場合に指定します。|
|EnableDetailedResponse|false|ヘルスチェックで詳細なレスポンスを返却する場合に有効にします。|

※[Rds.json](rds-json.md)のUserConnectionStringに設定された接続文字列をもとにデータベースの接続確認を行います。

##### EnableDetailedResponse

|パラメータ名|説明|
|:--|:--|
|status|すべての正常性チェックの集計状態を示します。|
|totalDuration|ヘルスチェックにかかった時間を示します。|
|entries|各正常性チェックの結果を示します。結果の各パラメータについては後述の entries を確認してください。|

##### entries

|パラメータ名|説明|
|:--|:--|
|data|コンポーネントの正常性を説明する追加のキーと値のペアを示します。|
|description|チェック対象のコンポーネントの状態を示します。|
|duration|正常性チェックの実行時間を示します。|
|exception|状態をチェックするときにスローされた例外を示します。|
|status|チェック対象のコンポーネントの正常性状態を示します。|
|tags|正常性チェックに関連付けられているタグを示します。|

##### 参考情報

上記のパラメータ(プロパティ)についての詳細につきましては、Microsoft社の公式ドキュメントを確認してください。
   [ASP\.NET Core のルーティング > RequireHost とルートが一致するホスト](https://learn.microsoft.com/ja-jp/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#host-matching-in-routes-with-requirehost)  
   [HealthReport クラス \(Microsoft\.Extensions\.Diagnostics\.HealthChecks\)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreport?view=net-8.0)  
   [HealthReportEntry 構造体 \(Microsoft\.Extensions\.Diagnostics\.HealthChecks\)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreportentry?view=net-8.0)  

### ContentSecurityPolicyの設定

#### パラメータ一覧

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Enabled|false|コンテンツセキュリティポリシー機能を利用するかどうかをtrue/falseで設定します。※3 ※5 ※6|
|ReportOnlyEnabled|true|コンテンツセキュリティポリシーレポートオンリー機能を利用するかどうかをtrue/falseで設定します。※4 ※5|
|Values|設定方法は後述|コンテンツセキュリティポリシー機能に適用する設定を指定します。|

※3 trueを設定した状態でポリシー違反が検出された場合はブラウザのコンソールログに違反レポート出力され違反対象となったリソースの読み込みがブロックされます。
※4 trueを設定した状態でポリシー違反が検出された場合はブラウザのコンソールログに違反レポート出力されます。
※5 report-uriが指定されている場合は違反レポートを送信します。
※6 Enabledをtrueに設定する場合はReportOnlyEnabledをtrueに設定した状態でプリザンターの動作に影響がないことを確認後に設定してください。

#### Values

|パラメータ名|設定例|説明|
|:--|:--|:--|
|default-src|'self'|デフォルトのリソースの読み込み元を指定します。|
|script-src|'self' 'strict-dynamic'|スクリプトの読み込み元を指定します。|
|script-src-attr|'self' 'unsafe-inline'|属性内スクリプトの許可元を指定します。|
|script-src-elem|－|&lt;script&gt;要素として読み込まれるスクリプトの読み込み元を指定します。|
|style-src|'self'|スタイルシートの読み込み元を指定します。|
|style-src-attr|'self' 'unsafe-inline'|属性内スタイルの許可元を指定します。|
|style-src-elem|'self' 'unsafe-inline'|style要素の許可元を指定します。|
|img-src|'self' data:|画像の読み込み元を指定します。|
|font-src|'self' data:|フォントの読み込み元を指定します。|
|object-src|'none'|オブジェクトの読み込み元を指定します。|
|connect-src|'self'|外部通信先のURLを指定します。|
|frame-src|'none'|フレームで読み込み元を指定します。|
|manifest-src|－|マニフェストファイルの読み込み元を指定します。|
|media-src|－|&lt;audio&gt;、&lt;video&gt;などメディア要素の読み込み元を指定します。|
|worker-src|－|Worker、SharedWorker、ServiceWorkerスクリプトの読み込み元を指定します。|
|base-uri|'self'|baseタグの許可元を指定します。|
|form-action|'self'|フォーム送信先を指定します。|
|frame-ancestors|－|&lt;frame&gt;、&lt;iframe&gt;、&lt;object&gt;、&lt;embed&gt;などのフレーム読み込み元を指定します。|
|report-uri|/CspReport/Report|違反レポートの送信先を指定します。|
|report-to|－|違反レポートの送信先エンドポイントを指定します。|
|sandbox|－|スクリプト禁止、フォーム送信禁止などのページ操作に適用するサンドボックス制限を指定します。|
|upgrade-insecure-requests|false|HTTPリソース要求を自動的にHTTPSに書き換えて安全にロードを行うかを指定します。|

各パラメータの設定値については[MDN Web Docs: Content Security Policy (CSP)](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Content-Security-Policy#directives) を参照してください。
パラメータの設定値を変更した場合はReportOnlyEnabledをtrueに設定した状態でプリザンターの動作に影響がないことを確認してください。

### CaptchaConfigの設定

|パラメータ名|設定例|説明|
|:--|:--|:--|
|Type|None|使用するCAPTCHAサービス名を設定します。|
|SiteKey|－|CAPRCHAサービスプロバイダが発行するサイトキーを設定します。|
|SecretKey|－|CAPRCHAサービスプロバイダが発行するシークレットキーを設定します。|
|RecaptchaV3|{"DefaultScoreThreshold": "0.7"}|Google社のreCAPTCHA v3スコアの閾値を設定します。|

### ForwardedHeaders

このパラメータには、リバースプロキシとして信頼するネットワーク・IPアドレスを指定します。以下の2つの用途に使用されます。それぞれ独立した効果があります。

1. 信頼済みプロキシ認証の送信元制限（[Authentication.json](authentication-json.md)のTrustedProxyParametersを参照）  
   設定されている場合、送信元IPがKnownNetworks/KnownProxiesのいずれかに一致したリクエストのみを自動ログイン対象とします。  
   両方が空の場合、1.5.7.0以降は信頼済みプロキシ認証による自動ログインを行いません。1.5.6.x以前は送信元IPの検証がスキップされます（すべての送信元が対象になります）。
1. Forwarded Headers Middlewareの警告ログ抑止
   .NET 8系の環境では、Pleasanterをクラスタリング構成で実行する際、以下のような警告ログが表示されることがあります。

   ```
   pleasanter-1  | warn: Microsoft.AspNetCore.HttpOverrides.ForwardedHeadersMiddleware[1]
   pleasanter-1  |       Unknown proxy: [::ffff:172.18.0.4]:45988
   ```

   これは、ASP.NET CoreのForwarded Headers Middlewareが、リクエスト元のプロキシIPアドレスを信頼できないものとして認識しているために発生します。Docker環境では、コンテナ間通信に使用される内部IPアドレスが動的に割り当てられるため、この警告が表示されることがあります。本パラメータを正しく設定することで、この警告ログを抑止できます。

|パラメータ名|設定例|説明|
|:--|:--|:--|
|KnownNetworks|["172.17.0.0/16", "172.18.0.0/16", "172.19.0.0/16"]|信頼するネットワーク範囲（CIDR形式）を指定します。|
|KnownProxies|["10.0.0.5"]|信頼する特定のIPアドレスを指定します。|

**信頼済みプロキシ認証を使用する場合は、KnownNetworksまたはKnownProxiesを必ず設定してください。1.5.7.0以降は、両方が空の場合は自動ログインを行いません。1.5.6.x以前は、両方が空の場合、任意の送信元からのリクエストが自動ログイン対象となるため、なりすましの危険があります。**

## システム環境変数への登録方法

BlobContainerUri、KeyIdentifier、XmlAesKey、KeyValueStoreConnectionString、KeyValueStoreKeyNameは[システム環境変数に登録](credentials-in-environment-variables.md)できます。システム環境変数への登録については以下ページも参照ください。  
[パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)

### 1. 命名規則

システム環境変数の命名規則は以下の通りです。
```
（サービス名）_Security_AspNetCoreDataProtection_BlobContainerUri
（サービス名）_Security_AspNetCoreDataProtection_KeyIdentifier
（サービス名）_Security_AspNetCoreDataProtection_XmlAesKey
（サービス名）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString
（サービス名）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName
```

|項目|必須|説明|
|---|---|---|
|サービス名|○|[Service.json](service-json.md)の「EnvironmentName」または「Name」を指定|

#### 設定例

|変数|設定例|
|:--|:--|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_BlobContainerUri|https://stragename.blob.core.windows.net/containername|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyIdentifier|https://keyvalult-name.vault.azure.net/keys/key-name/....|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_XmlAesKey|a0b1c2...|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString|localhost:6379,abortConnect=false|
|Implem.Pleasanter_Security_AspNetCoreDataProtection_KeyValueStoreKeyName|Pleasanter:DataProtection-Keys|

### 2. 優先順

本パラメータファイルとシステム環境の両方に設定した場合や省略形で設定した場合の優先順位は以下のとおりです。

#### 1. BlobContainerUriの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「BlobContainerUri」|
|2|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_BlobContainerUri」|
|3|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_BlobContainerUri」|

#### 2. KeyIdentifierの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「KeyIdentifier」|
|2|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyIdentifier」|
|3|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyIdentifier」|

#### 3. XmlAesKeyの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「XmlAesKey」|
|2|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_XmlAesKey」|
|3|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_XmlAesKey」|
|4|[Service.json](service-json.md)の「Name」（1～3のいずれも設定されていない場合）|

#### 4. KeyValueStoreConnectionStringの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「KeyValueStoreConnectionString」|
|2|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString」|
|3|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyValueStoreConnectionString」|

#### 5. KeyValueStoreKeyNameの優先順

|優先順|設定値|
|:--|:--|
|1|本パラメータファイルの「KeyValueStoreKeyName」|
|2|環境変数の「（サービス名：EnvironmentName）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName」|
|3|環境変数の「（サービス名：Name）_Security_AspNetCoreDataProtection_KeyValueStoreKeyName」|

### 3. システム環境変数に登録する際の注意点

「2. 優先順」に記載の通りパラメータファイルに設定した値が最優先となるため、システム環境変数に登録する場合はパラメータファイルでは「null」を指定してください。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.8.0 以降|HealthCheckパラメータ追加|
|1.4.19.0 以降|ContentSecurityPolicyパラメータ追加|
|1.4.23.0 以降|ContentSecurityPolicyパラメータに以下を追加<br>・script-src-elem<br>・manifest-src<br>・media-src<br>・worker-src<br>・frame-ancestors<br>・report-to<br>・sandbox<br>・upgrade-insecure-requests<br><br>ShowLoginPageOnAuthErrorパラメータ追加|
|1.5.2.0 以降|ForwardedHeadersパラメータ追加<br>ExcludeCookiePrefixesパラメータ追加|
|1.5.7.0 以降|信頼済みプロキシ認証で、KnownNetworks・KnownProxiesが両方空の場合は自動ログインを行わないよう変更<br>AspNetCoreDataProtectionにKeyValueStoreConnectionString・KeyValueStoreKeyNameパラメータ追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
-   [ユーザ管理機能：特権ユーザの設定](../../managers-guide/user-administration/user-management-privileged-users.md)
-   [テーブルの管理：フォーム](../../managers-guide/manage-table/form/index.md)
-   [ユーザ管理機能](../../managers-guide/user-administration/index.md)
-   [プリザンターのヘルスチェック機能を有効化する](../additional/ops-management/enable-health-check.md)
-   [コンテンツセキュリティポリシー機能](../additional/security/content-security-policy.md)
-   [信頼済みリバースプロキシ認証](../additional/authn-authz/trusted-reverse-proxy-auth.md)
-   [パラメータ設定：Authentication.json](authentication-json.md)
-   [メールによる二段階認証を有効にする](../additional/authn-authz/secondary-authentication.md)
-   [TOTP（Time-based One-Time Password）による二段階認証を有効にする](../additional/authn-authz/totp-authentication.md)
-   [ASP.NET Core データ保護の構成](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/overview)
-   [ASP.NET Core でのデータ保護のキー管理と有効期間](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/configuration/default-settings)
-   [ASP.NET Core でのキー ストレージ プロバイダー](https://docs.microsoft.com/ja-jp/aspnet/core/security/data-protection/implementation/key-storage-providers)
-   [HTTP Strict Transport Security プロトコル (HSTS)|Microsoft Learn](https://learn.microsoft.com/ja-jp/aspnet/core/security/enforcing-ssl#http-strict-transport-security-protocol-hsts)
-   [Cache-Control|MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control)
-   [Pragma|MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Pragma)
-   [パラメータ設定：Rds.json](rds-json.md)
-   [ASP\.NET Core のルーティング > RequireHost とルートが一致するホスト](https://learn.microsoft.com/ja-jp/aspnet/core/fundamentals/routing?view=aspnetcore-8.0#host-matching-in-routes-with-requirehost)
-   [HealthReport クラス \(Microsoft\.Extensions\.Diagnostics\.HealthChecks\)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreport?view=net-8.0)
-   [HealthReportEntry 構造体 \(Microsoft\.Extensions\.Diagnostics\.HealthChecks\)](https://learn.microsoft.com/ja-jp/dotnet/api/microsoft.extensions.diagnostics.healthchecks.healthreportentry?view=net-8.0)
-   [MDN Web Docs: Content Security Policy (CSP)](https://developer.mozilla.org/ja/docs/Web/HTTP/Reference/Headers/Content-Security-Policy#directives)
-   [パラメータ設定：資格情報をシステム環境変数に登録する](credentials-in-environment-variables.md)
-   [パラメータ設定：Service.json](service-json.md)
-   [ASP.NET Coreデータ保護キーを外部保存する](../additional/ready-for-clustering/data-protection-key-store.md)
