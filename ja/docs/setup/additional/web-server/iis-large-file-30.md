---
title: IISで30MB以上のファイルをアップロードする場合の事前設定
category: 追加設定：Webサーバ
order: '100'
status: ''
parts: ''
urlstring: iis-large-file-30
translationKey: iis-large-file-30
shortname: アップロード
created: 2019-05-02
updated: 2023-04-12
---

## IISによるファイルサイズの制限について

プリザンターは動作環境として「Microsoft IIS」を利用しています。「Microsoft IIS」の標準設定は、30MB以上のファイルをアップロードできないよう制限されています。30MB以上のファイルを登録またはインポートする際には以下の手順を実施してください。また、100MB以上のファイルを登録またはインポートする際には、[大きなファイルを登録する場合の設定（100MB以上）](iis-large-file-100.md)の手順も実施してください。

## 設定手順

1.  「コンピューターの管理」を起動します。++win+r++と操作し、ファイル名を指定して実行ダイアログを表示し「compmgmt.msc」を実行してください。

1.  左ペインにて、「コンピューターの管理(ローカル)」-「サービスとアプリケーション」-「インターネットインフォメーションサービス」を選択し、中央ペインにてサイト-「Default Web Site」-「pleasanter」をクリックしてください。

    ![コンピューターの管理の画面。「Default Web Site」の下の「pleasanter」を選んだ状態](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/ffd95bab6ff34d7fad7dfa28d5dc666c.png)

1.  「要求フィルター」をクリックしてください。

    ![コンピューターの管理の画面。「要求フィルター」を選ぶところ](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/acd51e2c7d3e499c85292ca27d0e9bcf.png)

1.  右ペインにて「機能設定の編集」をクリックしてください。

    ![要求フィルターの画面。右ペインに「機能設定の編集」がある](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/74c556cc6b124451a0fa1ef51bb82ee0.png)

1.  「許可されたコンテンツ最大長(バイト)(C)」にインポートを行うファイルの最大サイズを入力し、「OK」ボタンをクリックしてください。

    ![「許可されたコンテンツ最大長(バイト)(C)」に最大サイズを入力するダイアログ](https://pleasanter.org/files/images/ja/setup/additional/web-server/assets/ad99de0be6f144a3a9c3a58f23a9ef0d.png)

## 関連情報

-   [大きなファイルを登録する場合の設定（100MB以上）](iis-large-file-100.md)
