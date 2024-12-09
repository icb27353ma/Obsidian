---
title: "Google Apps Scriptでslackに通知を送ってみよう - Qiita"
source: "https://qiita.com/sy_k/items/90ca663ea64aef19097c?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[sy_k]]"
published: 2024-12-02
created: 2024-12-08
description: "はじめに参画中のプロジェクトで、Google Apps Script（GAS）を使用したslack通知機能を作成したので、その手順を紹介します。今回は、画面のボタンを押すと通知を送る仕様で作りた…"
tags:
  - "clippings"
---
## はじめに

参画中のプロジェクトで、Google Apps Script（GAS）を使用したslack通知機能を作成したので、その手順を紹介します。  
今回は、画面のボタンを押すと通知を送る仕様で作りたいと思います。

## slack側の設定

1\. Incoming WebHooksのアプリを追加

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F83ddfdad-916a-11c8-8112-333ae8605369.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1098b9c1fa924728bb6cbd6fda19f538)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F83ddfdad-916a-11c8-8112-333ae8605369.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1098b9c1fa924728bb6cbd6fda19f538)

2\. Incoming WebHooksのページがブラウザで開かれるので、  
通知を送信したいチャンネルを選択して、「Incoming WebHooks インテグレーションの追加」をクリックする。

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F753ebc53-c29c-35ef-799f-7f2efaf53fc7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=450c59f5196e411516cd3c4aebe0fbec)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F753ebc53-c29c-35ef-799f-7f2efaf53fc7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=450c59f5196e411516cd3c4aebe0fbec)

3\. WebHook URLが発行されるので、控えておく。

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F7ebde65e-a3a3-e472-6c28-04be5d6d3c73.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6d35b9deb0bcbdd3eef38e53cae29611)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F7ebde65e-a3a3-e472-6c28-04be5d6d3c73.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6d35b9deb0bcbdd3eef38e53cae29611)

## GASプロジェクトの作成

※既にプロジェクト作成済みの場合は省略してください。

1\. ブラウザでgoogledriveを開く

2\. 任意のフォルダ内で右クリック

3\. 「その他」→「Google Apps Script」を選択

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F0add354e-a926-2d9f-7d65-6f28fcbc4f78.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0785f5414af53be859a3d10f4f3001be)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F0add354e-a926-2d9f-7d65-6f28fcbc4f78.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0785f5414af53be859a3d10f4f3001be)

## コード

gasは下記の通り。  
`notifySlack()`の`url`には、先ほど発行したWebHook URLを記載します。

common.gs

```
function doGet(e) {
  const template = HtmlService.createTemplateFromFile('index');
  template.deployURL = ScriptApp.getService().getUrl();
  const htmlOutput = template.evaluate();
  return htmlOutput;
}

function doPost(e) {
  notifySlack();
  const template = HtmlService.createTemplateFromFile('index');
  template.deployURL = ScriptApp.getService().getUrl();
  const htmlOutput = template.evaluate();
  return htmlOutput;
}

function notifySlack() { 
  const url = "XXXXXXX"                                  // WebHook URL
  let userName = "slack通知"                             // 通知アプリの名前
  let icon = ":christmas_tree:"                          // アプリのアイコン 
  let message = "<!channel>\n\n\` + \`通知を送りました！\`"  // メッセージ文言

  let jsonData = {
    "username": userName,
    "icon_emoji": icon,
    "text": message
  }

  let payload = JSON.stringify(jsonData)

  let options =
  {
    "method": "post",
    "contentType": "application/json",
    "payload": payload
  };

  // 通知を送信
  UrlFetchApp.fetch(url, options);
}
```

画面のhtmlは下記の通り。

index.html

```
<!DOCTYPE html>
<html>

<head>
  <base target="_top">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
</head>

<body>
  <div class="text-center m-4">
    <form class="mb-5" method="POST" action="<?= deployURL ?>">
      <p>ボタンを押すとslack通知を送信します &#128276;</p>
      <button type="submit" class="btn btn-primary" name="notify" value="true">通知</button>
    </form>
  </div>
</body>

</html>
```

## 実際に通知を送る

コードを記載したら、実際に通知を送信してみます。

1\. GASプロジェクト右上部にあるデプロイボタンを押した後、「デプロイをテスト」をクリックします。  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F40cf0f40-df8e-f27c-abef-fd708db5a49e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c79a5299aed5a21661bc4efe9f0b090e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F40cf0f40-df8e-f27c-abef-fd708db5a49e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c79a5299aed5a21661bc4efe9f0b090e)

2\. 表示されたウェブアプリのURLをクリックします。  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2Fbe5b18dd-49d3-e729-dc06-3a8f2ac28197.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=eca1a04101d7343bfcbf6771d3138c74)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2Fbe5b18dd-49d3-e729-dc06-3a8f2ac28197.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=eca1a04101d7343bfcbf6771d3138c74)

3\. 先ほどのhtml画面が表示されますので、通知ボタンを押す。  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2Fd92faf65-efdd-caa7-dca1-f64d78b0e3a2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d74f92547564cafd8ffdcb15baaf6025)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2Fd92faf65-efdd-caa7-dca1-f64d78b0e3a2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d74f92547564cafd8ffdcb15baaf6025)

チャンネルに送信されました！  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F0c50df42-b207-3bdd-02b7-3258bf799177.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ea6bddbcca3576935b9cf512526f91a1)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3917357%2F0c50df42-b207-3bdd-02b7-3258bf799177.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ea6bddbcca3576935b9cf512526f91a1)

## 通知メッセージについて

最後に、＠channelなどのメンションやアイコンの記載方法を紹介します。

- メンション

| メンション | 記載方法 | メンション対象 |
| --- | --- | --- |
| ＠channel | `<!channel>` | チャンネルに参加していて、送信時に「アクティブなステータス」のメンバー |
| ＠here | `<!here>` | チャンネル内のメンバー全員（ログイン状態は関係しない） |
| ＠everyone | `<!everyone>` | ゲストを除く#general 内のメンバー全員（ログイン状態は関係しない、#generalでのみ使用可） |

- アイコン  
先ほどのgasコード内の`let icon = ":christmas_tree:" `で、好きな絵文字を通知アプリのアイコンにすることができます。  
絵文字のコードは、下記のサイトを参考にしました。

## おわりに

思ったより簡単に作成することができました。  
GASを使う際は参考になったら嬉しいです！