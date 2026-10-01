---
title: Docker環境においてベースURLを変更したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-change-baseurl-docker
translationKey: faq-change-baseurl-docker
shortname: ベースURL
created: 2025-03-06
updated: 2026-07-17
---

## 回答

以下の手順に従って設定変更してください。

---

## 概要

Docker環境において、マニュアルの[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../setup/installation/running-with-docker/change-parameters-at-docker-image.md)手順に従ってプリザンターをインストールすると、URLは以下のように

``` text
http://localhost:50001
```

となりますが、これを

``` text
http://localhost:50001/nakano
```

のようなパス付の「ベースURL」に変更したい場合は以下の手順に従って設定を行ってください。

## 注意事項

1.  稼働中のプリザンターに対して本手順を実行した場合、添付ファイルや説明項目、コメントに貼り付けた画像、サイト画像（アイコン）が表示されなくなります。解消するには再度添付や貼り付けでの対応となります。稼働中にベースURLを変更する際は十分に検討してください。

## 操作手順

ベースURLを変更するには以下の手順で操作を行います。以降の手順ではベースURLを

``` text
http://localhost:50001/nakano
```

とする場合を例に説明します。

1.  Dockerfileの設定
1.  パラメータファイル[Service.json](../../setup/parameters/service-json.md)の設定
1.  コンテナイメージのビルド
1.  プリザンターの起動

!!! tip
    以降の手順で示す各ファイルのパスは[Dockerイメージを使用しパラメータを既定値から変更して起動する](../../setup/installation/running-with-docker/change-parameters-at-docker-image.md)手順に従って操作した場合のものになりますので、ご自身の環境に合わせて適宜読み替えてください。

### 1. Dockerfileの設定

/Pleasanter/Dockerfileに対して以下のようにENTRYPOINTに「"--pathBase", "/nakano"」を追記します。

=== "修正前"

    ``` Dockerfile title="/Pleasanter/Dockerfile"
    ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll" ]
    ```

=== "修正後"

    ``` Dockerfile title="/Pleasanter/Dockerfile"
    ENTRYPOINT [ "dotnet", "Implem.Pleasanter.dll", "--pathBase", "/nakano" ]
    ```

### 2. パラメータファイルService.jsonの設定

[Service.json](../../setup/parameters/service-json.md)の「AbsoluteUri」を以下のように設定します。

``` json
    "AbsoluteUri": "http://localhost:50001/nakano"
```

### 3. コンテナイメージのビルド

以下コマンドを実行します。

``` ps1
docker compose build
```

### 4. プリザンターの起動

コンテナを作成、プリザンターを起動します。

``` ps1
docker compose up -d pleasanter
```

## 関連情報

-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](../../setup/installation/running-with-docker/change-parameters-at-docker-image.md)
-   [パラメータ設定：Service.json](../../setup/parameters/service-json.md)
