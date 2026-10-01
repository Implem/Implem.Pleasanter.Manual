---
title: Linux環境においてベースURLを変更したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-change-baseurl-linux
translationKey: faq-change-baseurl-linux
shortname: ベースURL
created: 2025-03-06
updated: 2025-03-13
---

## 回答

以下の手順に従って設定変更してください。

---

## 概要

Linux環境やDocker環境において、マニュアルの[Linuxにインストール](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)する手順に従ってプリザンターをインストールすると、URLは以下のように

``` text
http://localhost
```

となります[^1]が、これを

``` text
http://localhost/nakano
```

のようなパス付の[ベースURL](faq-change-baseurl-docker.md)に変更したい場合は以下の手順に従って設定を行ってください。

[^1]: Docker環境の場合は`http://localhost:50001`となります。

## 注意事項

1.  稼働中のプリザンターに対して本手順を実行した場合、添付ファイルや説明項目、コメントに貼り付けた画像、サイト画像（アイコン）が表示されなくなります。解消するには再度添付や貼り付けでの対応となります。稼働中にベースURLを変更する際は十分に検討してください。

## 操作手順

ベースURLを変更するには以下の手順で操作を行います。以降の手順ではベースURLを

``` text
http://localhost/nakano
```

とする場合を例に説明します。

1.  Pleasanterの起動設定
1.  nginxのproxy設定
1.  パラメータファイル[Service.json](../../setup/parameters/service-json.md)の設定
1.  Pleasanter、nginxの再起動

!!! tip
    以降の手順で示す各ファイルのパスは[Linuxにインストール](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)する手順に従ってインストールした場合のものになりますので、ご自身の環境に合わせて適宜読み替えてください。

### 1. Pleasanterの起動設定

Pleasanterサービス用スクリプト（`/etc/systemd/system/pleasanter.service`）に対して、以下のようにExecStartの末尾に「--pathBase=/nakano」をパラメータとして付与します。

=== "修正前"

    ``` env
      [Service]
      ExecStart = /root/dotnet/dotnet Implem.Pleasanter.dll
    ```

=== "修正後"

    ``` env
      [Service]
      ExecStart = /root/dotnet/dotnet Implem.Pleasanter.dll --pathBase=/nakano
    ```

### 2. nginxのproxy設定

リバースプロキシの設定ファイル（`/etc/nginx/conf.d/pleasanter.conf`）に対して以下のように2か所にパスを追記します。

=== "修正前"

    ``` conf
        location / {
            proxy_pass         http://localhost:5000;
    ```

=== "修正後"

    ``` conf
        location /nakano {
            proxy_pass         http://localhost:5000/nakano;
    ```

### 3. パラメータファイルService.jsonの設定

[Service.json](../../setup/parameters/service-json.md)の「AbsoluteUri」を以下のように設定します。

``` json
    "AbsoluteUri": "http://localhost/nakano"
```

### 4. pleasanter、nginxの再起動

以下手順でプリザンターとnginxを再起動します。

``` bash
sudo systemctl restart nginx
sudo systemctl restart pleasanter
```

## 関連情報

-   [インストーラでプリザンターをAlmaLinuxにインストールする](../../setup/installation/install-with-installer/getting-started-installer-pleasanter-almalinux.md)
-   [FAQ：Docker環境においてベースURLを変更したい](faq-change-baseurl-docker.md)
-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)
