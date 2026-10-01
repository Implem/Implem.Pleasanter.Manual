---
title: パラメータ変更時の確認事項
category: パラメータ設定
order: '1'
status: ''
parts: ''
urlstring: parameter-edit
translationKey: parameter-edit
shortname: パラメータ変更時の確認事項
created: 2019-06-30
updated: 2026-08-14
---

## パラメータの設定

プリザンターの各種基本設定のパラメータファイルはJSON形式で構成されています。

## パラメータファイルの格納場所

標準構成の場合、パラメータファイルは下記のディレクトリに格納されています。

=== ":fontawesome-brands-windows: Windows"

    ``` text
    C:\web\pleasanter\Implem.Pleasanter\App_Data\Parameters
    ```

=== ":fontawesome-brands-linux: Linux"

    ``` text
    /web/pleasanter/Implem.Pleasanter/App_Data/Parameters
    ```

=== ":material-microsoft-azure: Azure [^1]"

    ``` text
    C:\home\site\wwwroot\App_Data\Parameters
    ```

[^1]: ユーザによっては`D:\home\site`となる場合があります。その場合は適宜読み替えてください。

!!! note "Dockerの場合"
    Dockerの場合は[Dockerイメージを使用しパラメータを既定値から変更して起動する](../installation/running-with-docker/change-parameters-at-docker-image.md)を参照してください。

## 注意事項

1.  パラメータの変更を反映するにはプリザンターの再起動が必要です。再起動時にはサービスが停止しますので注意してください。
1.  パラメータファイルを変更する前に、オリジナルのバックアップを作成してください。

## 設定変更の反映

=== ":fontawesome-brands-windows: Windows"

    IISを再起動してください。

=== ":fontawesome-brands-linux: Linux"

    プリザンターのサービスを再起動してください。

    ``` bash
    sudo systemctl restart pleasanter
    ```

=== ":material-microsoft-azure: Azure"

    Azure App Serviceを再起動してください。

## トラブルシューティング  

設定が正しく反映できない場合には、[JSON形式のチェック](../../FAQ/features-for-developers/faq-json-format.md)を確認してください。

## 関連情報

-   [Dockerイメージを使用しパラメータを既定値から変更して起動する](../installation/running-with-docker/change-parameters-at-docker-image.md)
-   [FAQ：変更後の設定ファイルやAPIリクエスト(JSON形式)が正しく認識されない場合の確認事項](../../FAQ/features-for-developers/faq-json-format.md)
