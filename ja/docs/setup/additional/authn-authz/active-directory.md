---
title: プリザンターとActive Directoryを連携する ― AD連携
category: 追加設定：認証
order: '100'
status: ''
parts: ''
urlstring: active-directory
translationKey: active-directory
shortname: AD連携,LDAP認証,LDAP連携
created: 2019-04-29
updated: 2025-11-14
---

## 注意事項

1. プリザンターでは組織コードをキーとして組織を取り込みます。組織コードが一致している場合、組織名が変わっていても同一の組織として上書きします。そのため、ADのユーザの部署名が変更されると、同期によりプリザンターの組織名が変更されます。
1. ADのセキュリティグループの同期を行うには、マイクロソフト社が提供するライブラリである「DirectoryServices」を使用する必要があります。プリザンターが、このライブラリを使用するには、以下の条件を満たす必要があります。  
   1. プリザンターがWindows環境に構築されている（Linux環境では使用できません）  
   1. Authentication.jsonの DsProviderは「null」に設定されている（"Novell"が設定されている場合には動作しません）
1. プリザンターではADのセキュリティグループのobjectGUIDをキーとしてグループを取り込みます。そのため、グループ名が変わっていても同一のグループとして上書きします。ADのセキュリティグループを削除して、新しいセキュリティグループを同じ名前で作成した場合、objectGUIDが異なるためプリザンター上では別のグループとして新規に登録されます。
1. ADからプリザンターに同期されたユーザは、プリザンターからパスワードの変更を行うことができません。
1. ADと同期した組織、グループ、ユーザをプリザンター側で編集しないでください。プリザンター側で編集しても、再同期の際にAD側の最新情報で上書きされます。

## 概要

プリザンターは**Active Directory**（以降ではADと略します）の**ユーザ**と**セキュリティグループ**を自動的に取り込むことができます。ユーザ情報や組織の情報がADで一元管理され、定期的に更新されている組織では、AD内のユーザ情報、セキュリティグループ情報を取り込むだけで、ユーザ管理を容易に行えます。

### 1. ADのオブジェクトとプリザンターの管理情報の対応

プリザンターのアクセス制御を行う単位に、組織、グループ、ユーザがあります。これらはADから下表のとおり同期されます。

|ADのオブジェクト|同期されるAD情報|プリザンター|
|:--|:--|:--|
|ユーザに含まれる組織の属性情報|組織コード<br>組織名|組織|
|セキュリティグループ|グループ名<br>所属する子グループ<br>所属ユーザ|グループ|
|ユーザ|ログインID<br>名前<br>ユーザコード<br>組織<br>メールアドレス|ユーザ|

ただし、**ADのユーザのパスワードは同期されません**。

### 2. 組織の同期

ADのユーザに含まれる組織の属性情報を使って、プリザンターの組織を作成または更新します。組織を同期するには、ADのドメインコントローラーのサーバ上でADSIエディターを開き、設定ファイル[Authentication.json](../../parameters/authentication-json.md)内のパラメータと下図のように紐づけてください。

![ADSIエディターの属性とAuthentication.jsonのパラメータの対応（組織の同期）](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/84066f86f60249279915dff563c67bf7.png)

ADのユーザオブジェクトには、組織コードに該当する属性がありません。そのため組織コードは使用されていない他の項目に格納されたり、部署の属性に一緒に格納（610 総務部のように）されたりすることがあります。

ADに組織コードが格納されていない場合、**組織名を組織コードとして代用することが可能**です。その場合は"LdapDeptCode"と"LdapDeptName"の両方に"department"を設定してください。

#### 組織コードと組織名が1つの属性に格納されている場合

組織コードと組織名が1つの属性に格納されている場合など、属性の一部を切り出して同期することができます。文字列の一部を切り出す場合、パラメータ値に正規表現パターンを記述してください。

例えば、組織コードと組織名が「610 総務部」のように格納されている場合、1～3桁目を組織コード、空白が1つあり、5桁目以降が組織名というパターンで文字を切り出します。

以下は、変更部分のみの抜粋です。

```
"LdapDeptCodePattern": "^.{0,3}",
"LdapDeptNamePattern": "(?<=^.{4}).+", 
```

### 3. グループの同期

ADに登録されているセキュリティグループの情報を使って、プリザンターのグループを作成または更新します。組織を同期するには、[Authentication.json](../../parameters/authentication-json.md)のパラメータ"LdapSyncGroupPatterns"に"(&(ObjectCategory=Group))"を設定してください。"LdapSearchRoot"で指定したOU配下のグループの全てが同期されます。

![ADのセキュリティグループがプリザンターのグループへ同期される対応の図](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/3ae9a51d1cee4408adf3be788bb5d440.png)

以下は、変更部分のみの抜粋です。

```
            "LdapSyncGroupPatterns": [
                "(&(ObjectCategory=Group))"
            ],
```

#### グループを絞り込む

LdapSyncGroupPatternsに、検索フィルター構文を指定すると、グループを絞り込めます。検索フィルター構文の文法は、[マイクロソフト社のドキュメント](https://learn.microsoft.com/ja-jp/windows/win32/adsi/search-filter-syntax)を参照してください。

ADからプリザンターに同期されたグループは、「グループの一覧画面」に表示されます。

![ADから同期されたグループが並ぶ、プリザンターのグループの一覧画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/1d7c56fefe474312b82fae591c32f17a.png)

ADからプリザンターに同期されたグループを開くと、下図のように[LDAP同期](active-directory-sync-script.md)のチェックがオンになります。

![グループの編集画面。「LDAP同期」のチェックがオンになっている](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/952d92ff491b443e8aea1f232756e91f.png)

### 4. ユーザの同期

ADに登録されているユーザをプリザンターのユーザとして取り込むことができます。ユーザを同期するには、ADのドメインコントローラーのサーバ上で「Active Directory ユーザとコンピュータ」のツールでユーザのプロパティを開き、「全般」タブと「アカウント」タブ内の情報と、[Authentication.json](../../parameters/authentication-json.md)のパラメータ"LdapParameters"とを、下図のように紐づけます。

![ADのユーザのプロパティとAuthentication.jsonのLdapParametersの対応](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/40c2c94cfa9d485992c4ced9b5c9f81f.png)

ADからプリザンターに同期されたユーザは、下図のようにユーザの一覧画面に表示されます。

![ADから同期されたユーザが並ぶ、プリザンターのユーザの一覧画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/20656315106d45e8ac8b1e086e41ca04.png)

ADからプリザンターに同期されたユーザを開くと、下図のようにユーザの編集画面が表示されます。

![ADから同期されたユーザの編集画面](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/7a98b5a323ba4e07a7abc07549a50862.png)

「メールアドレス」タブを開くと、下図のように同期されたメールが表示されます。

![ユーザの編集画面の「メールアドレス」タブ。同期されたメールアドレスが並ぶ](https://pleasanter.org/files/images/ja/setup/additional/authn-authz/assets/988b2a3bc6024271bd1508b5a3e8dbb2.png)

### 5. 同期の設定

ADの同期は、設定ファイル[BackgroundService.json](../../parameters/background-service-json.md)に設定したスケジュールに従って実行されます。

例えば、昼間の12時と深夜2時の2回実施したい場合には、以下のように設定してください。設定後はプリザンターの再起動が必要です。

```
{

～～ 中略 ～～

    "SyncByLdap": true,
    "SyncByLdapTime": [ "12:00", "02:00" ],

～～ 中略 ～～

}
```

#### 同期をテストする

同期のテストを行う場合は、以下のように実施してください。

1. [Authentication.json](../../parameters/authentication-json.md)を開き、パラメータの値を設定してください。
2. [BackgroundService.json](../../parameters/background-service-json.md)を開き、「SyncByLdapTime」に数分後の時間を設定してください。
3. プリザンターを再起動してください。
4. プリザンターの管理画面（組織、グループ、ユーザ）を開いて確認してください。

## 関連情報

-   [パラメータ設定：Authentication.json](../../parameters/authentication-json.md)
-   [マイクロソフト社のドキュメント](https://learn.microsoft.com/ja-jp/windows/win32/adsi/search-filter-syntax)
-   [プリザンターにActive Directoryのユーザ情報を同期する（外部スクリプト）](active-directory-sync-script.md)
-   [パラメータ設定：BackgroundService.json](../../parameters/background-service-json.md)