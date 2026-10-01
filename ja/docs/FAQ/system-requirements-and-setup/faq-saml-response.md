---
title: SAML認証設定でAuthentication.json に設定するSAMLレスポンスの属性名を確認したい
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-saml-response
translationKey: faq-saml-response
shortname: ''
created: 2020-03-23
updated: 2024-04-29
---

## 回答

Webブラウザの開発者ツールを使用します。

---

## 概要

[SAML](../../setup/additional/authn-authz/saml.md)認証設定で[Authentication.json](../../setup/parameters/authentication-json.md)の"SamlParamters.Attributes"に指定するSAMLレスポンスの属性名を確認する方法を以下に記載します。

!!! tip
    以下はWebブラウザにGoogle Chromeを利用した場合の手順です。別のWebブラウザを利用している場合は、適宜読み替えて実施してください。

1.  下記マニュアルの手順に従い、SAML認証機能追加の設定を行います（その際、[Authentication.json](../../setup/parameters/authentication-json.md)の"SamlParamters.Attributes"の設定はスキップして構いません）。
1.  プリザンターのログイン画面を表示後、++f12++キーで開発者ツールを開きます。
1.  「SSOログイン」ボタンでSAML認証を開始し、IDプロバイダからプリザンターの画面に戻ったところで以下を実施します。
    -   開発者ツールで「Network」タブを選択
    -   左側の「Name」で「ASC」を選択
    -   中央の「Headers」タブを選択、表示される内容をスクロールしてForm Dataを探す
    -   SAML Responseの内容をコピー

    ![開発者ツールのNetworkタブ。Form Data に SAML Response が表示されている](https://pleasanter.org/files/images/ja/FAQ/system-requirements-and-setup/assets/690beafc65b8494a9f16158487734a80.png)

1.  コピーした内容を以下のスクリプトの$base64SamlResponseに設定します。

    ``` ps1 title="SAML Response（Base64）をデコードし、XMLファイルとして保存するPowerShellスクリプト" linenums="1" hl_lines="1"
    $base64SamlResponse =  "ここにSAMLResponseを貼り付け"
    $outputFile = ".\samlResponse.xml"
    $xml = [xml]([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($base64SamlResponse)));
    $xmlwriter= New-Object System.Xml.XmlTextWriter($outputFile, [System.Text.Encoding]::UTF8);
    $xmlwriter.Formatting = [System.Xml.Formatting]::Indented;
    $xml.Save($xmlwriter);
    $xmlwriter.Close();
    ```

1.  上記スクリプトをテキストエディタ等に貼り付け、拡張子"*.ps1"で保存します。
1.  保存したスクリプトファイルを右クリックし、「PowerShellで実行」で実行すると、スクリプトファイル（.ps1）と同じフォルダにsamlResponse.xmlが出力されます。
1.  出力されたXMLファイルを開き、`<AttributeStatement>`で定義されている属性を確認してください。

## 関連情報

-   [SAML認証を利用する](../../setup/additional/authn-authz/saml.md)
