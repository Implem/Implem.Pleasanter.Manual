---
title: 'Edgeでフォームへの入力中、プリザンターの動作がおかしくなる'
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-autofill-problem-ms-edge
translationKey: faq-autofill-problem-ms-edge
shortname: ''
created: 2026-05-15
updated: 2026-06-29
---

## 回答

プリザンターではなくEdgeの自動入力（オートフィル）機能が原因です。  
[General.json](../../setup/parameters/general.json.md)のパラメータDisableAutoCompleteをtrueに設定し、この機能を抑止してください。

---

## 概要

Edgeを使ってWebフォームへ入力していると、「前回使用済み」という選択肢が表示されることがあります。ユーザがこの選択肢を選択すると、関連する別のフォームにも値が自動補完（オートフィル）される場合があります。この補完入力はプリザンターの機能ではなく、Edgeの機能です。

補完される値が意図通りでない場合、下記対策を講じてください。

#### 対策①　プリザンターの設定

[General.json](../../setup/parameters/general.json.md)でパラメータDisableAutoCompleteをtrueに設定してください。

##### General.json

```json
{
    "DisableAutoComplete": true
}
```

フォーム要素にautocomplete="off"が出力され、ブラウザによる自動補完を抑止できます。

なお、Edgeはフォーム要素の指定を遵守しない場合があります。問題が解決しない場合は、下記の対策②と対策③を併用してください。

#### 対策②　ADドメイン環境での一括設定

Active Directoryドメイン環境や、クラウドMDMを利用している場合、Edgeのオートフィル機能を一括無効化できます。詳細は下記ドキュメントを参照してください。

1. オンプレミス（Active Directory + GPO）: [Microsoft Edge ポリシー設定](https://learn.microsoft.com/ja-jp/deployedge/microsoft-edge-policies)
1. クラウド（Intune / Azure AD + MDM）: [Intune での Microsoft Edge 設定](https://learn.microsoft.com/ja-jp/deployedge/configure-edge-with-intune)

#### 対策③　ユーザ側での対応

ユーザ側での対策には下記の方法があります。

1. Edgeの「設定」→「パスワードとオートフィル」からオートフィル機能を無効化する
1. Edgeの「設定」→「プライバシー/検索/サービス」から閲覧データをクリアする

## 対応バージョン

すべてのバージョン

## 関連情報

-   [Microsoft Edge ポリシー設定](https://learn.microsoft.com/ja-jp/deployedge/microsoft-edge-policies)
-   [Intune での Microsoft Edge 設定](https://learn.microsoft.com/ja-jp/deployedge/configure-edge-with-intune)