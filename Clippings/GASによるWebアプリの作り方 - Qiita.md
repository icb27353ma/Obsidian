---
title: "GASによるWebアプリの作り方 - Qiita"
source: "https://qiita.com/__SATO__/items/fe8900837b09966c3028?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[__SATO__]]"
published: 2024-11-24
created: 2024-11-24
description: "はじめにGoogle Apps Script (GAS) は HTML Service という機能を使って AppsScript関数 を呼び出せる Webアプリ を作ることができます。この記事で…"
tags:
  - "clippings"
---
## はじめに

Google Apps Script (GAS) は HTML Service という機能を使って AppsScript関数 を呼び出せる Webアプリ を作ることができます。

この記事では HTML Service を使ってGASで Webアプリ を作る方法をまとめたものです。

## Webアプリの作り方

## Webアプリを表示する

まずはシンプルなWebページを表示してみましょう。

1. 新規または既存のプロジェクトを開く  
新規または既存のGASのスクリプトプロジェクトを開いてください。
2. サーバサイドの処理を定義  
GASで以下のようなサーバサイドの処理を書きます。

```
function doGet() {
  return HtmlService
    .createTemplateFromFile('index')
    .evaluate();
}
```
3. 表示するページを作る  
続いて、スクリプトエディタで index という名前のHTMLファイルを作成し、内容を以下のように編集してください。

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top"> <!-- ※1 -->
  </head>
  <body>
    <h1>Simple Web App</h1>
  </body>
</html>
```

※ GASでWebアプリ作る場合、headerタグ内には上記のようなbaseタグが必要になります。
4. Webアプリをデプロイする  
スクリプトとHTMLが用意できたら「デプロイ」→「新しいデプロイ」と順に選択し、以下の設定でデプロイを実施してください。

- デプロイの種類：ウェブアプリ
- 次のユーザとして実行：自分
- アクセスできるユーザ：自分のみ
5. Webアプリの動作を確認する  
デプロイが完了したらwebアプリのURLにアクセスし、Webページが表示できるかを確認しましょう。

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3939665%2F1636aff4-be22-131e-621a-52bddf84c466.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=cc5babf956be638c6e79a4eac5b91d12)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3939665%2F1636aff4-be22-131e-621a-52bddf84c466.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=cc5babf956be638c6e79a4eac5b91d12)

## スクリプトレットの利用

GASにはHTML内にAppsScriptのコードを埋め込む スクリプトレット と呼ばれる機能があります。

### Standard Scriptlets (標準スクリプトレット)

Standard Scriptlets (標準スクリプトレット) は if構文 などのページに直接出力されない要素を AppsScriptサーバ の処理で埋め込むスクリプトレットです。

以下は標準スクリプトレットのサンプルです。

```
function doGet() {
  return HtmlService
    .createTemplateFromFile('index')
    .evaluate()
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <? if (true) { ?>
      <p>この要素は常に表示されます</p>
    <? } else  { ?>
      <p>この要素は表示されません</p>
    <? } ?>
  </body>
</html>
```

※ evalute()：AppsScriptサーバがスクリプトレットを評価する関数

### Printing Scriptlets (出力スクリプトレット)

Printing Scriptlets (出力スクリプトレット) は AppsScriptサーバ から戻される値をページに書き込むスクリプトレットです。

```
function doGet() {
  return HtmlService
    .createTemplateFromFile('index')
    .evaluate()
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    現在は <?= new Date() ?> です。
  </body>
</html>
```

  

### Force-printing Scriptlets (強制出力スクリプトレット)

Force-printing Scriptlets (強制出力スクリプトレット) は Printing Scriptlets (出力スクリプトレット) だとブロックされてしまう出力内容を強制的にページに書き出すスクリプトレットです。

ただし、強制出力スクリプトレットは特殊な場合を除き出力スクリプトレットと同じ動きをするので、特に必要でない場合は出力スクリプトレットを使用しましょう。

```
function doGet() {
    return HtmlService
        .createTemplateFromFile('index')
        .evaluate();
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    Hello! The time is <?!= new Date() ?>. <!-- ※1 -->
  </body>
</html>
```

### AppsScript関数の利用

スクリプトレット内はAppsScriptサーバ環境なので、スクリプトレット内では通常のGASと同じコードを書くことができます。

以下はスクリプトレット内でスプレッドシートの内容を取得してHTMLページに埋め込んでいます。

```
function doGet() {
  return HtmlService
    .createTemplateFromFile('index')
    .evaluate();
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <? let data = SpreadsheetApp
        .openById('スプレッドシートID')
        .getActiveSheet()
        .getDataRange()
        .getValues(); ?>
    <table>
      <? for (let i = 0; i < data.length; i++) { ?>
        <tr>
          <? for (let j = 0; j < data[i].length; j++) { ?>
            <td><?= data[i][j] ?></td>
          <? } ?>
        </tr>
      <? } ?>
    </table>
  </body>
</html>
```

### 変数のプッシュ

doGet や doPost の中ではHTMLサービスで作成したHTMLオブジェクトに直接属性を追加できます。

以下の例では doGet の中でスプレッドシートのデータを取得し、HTMLオブジェクトにプッシュしてスクリプトれ都内で直接利用できるようにしています。

```
function doGet() {
  let t = HtmlService.createTemplateFromFile('index');
  t.data = getSpreadsheetData();
  return t.evaluate();
}

function getSpreadsheetData(){
  return SpreadsheetApp
    .openById('スプレッドシートID')
    .getActiveSheet()
    .getDataRange()
    .getValues();
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <table>
      <? for (let i = 0; i < data.length; i++) { ?> <!-- ※1 -->
        <tr>
          <? for (let j = 0; j < data[i].length; j++) { ?>
            <td><?= data[i][j] ?></td>
          <? } ?>
        </tr>
      <? } ?>
    </table>
  </body>
</html>
```

### パラメータの処理

doGet や doPost ではユーザ入力のパラメータを処理することができます。

以下のサンプルでは、doGet でユーザに入力フォームを表示し、doPost でフォームから受け取った値を表示しています。

```
function doGet() {
  return HtmlService
    .createTemplateFromFile('form')
    .evaluate();
}

function doPost(e){
  let name = e.parameter.name; // ※1
  let age = e.parameter.age;
  return HtmlService.createHtmlOutput(\`
    <div>name: ${name}</div>
    <div>age: ${age}</div>
  \`);
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
    </script>
  </head>
  <body>
    <form 
      action=<?= ScriptApp.getService().getUrl() ?>
      method="post"
    >
      <label>name: </label>
      <input name="name" type="text"><br/>
      <label>age: </label>
      <input name="name" type="text"><br/>
      <input type="submit">
    </form>
  </body>
</html>
```

※ ScriptApp.getService().getUrl()：WebアプリがデプロイされたURLを取得

### HTMLサービスのベストプラクティス

- HTML/CSS/JavaScriptの分離  
HTMLサービスでHTML/CSS/JavaScriptを別ファイルに分けて管理したい場合はスクリプトレットを使ってstyleタグやscriptタグをHTMLの一部として読み込む方法が推奨されています。

```
function doGet(request) {
  return HtmlService.createTemplateFromFile('Page')
    .evaluate();
}

function include(filename) { // スクリプトレットでstyleタグやscriptタグを取得するのに使用
  return HtmlService.createHtmlOutputFromFile(filename)
    .getContent();
} 
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <?!= include('styles'); ?>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>Please enjoy this helpful script.</p>
    <?!= include('scripts'); ?>
  </body>
</html>
```

```
<style>
    h1{font-size: 18px;}
    p {color: green;}
</style>
```

```
<script>
  window.addEventListener('load', function() {
    console.log('Page is loaded');
  });
</script>
```
- 遅延ロード  
HTMLサービスはAppsScriptサーバ側でスクリプトレットを評価してからユーザにページを返すので、スクリプトレットに重たい処理が使われているとページが表示されるまでに時間がかかることがあります。  
ページ表示を高速化するには、時間のかかる処理はスクリプトレットで書くのではなくクライアント側で google.script.run メソッドを呼び出してAppsScriptサーバの応答を非同期的に処理しましょう。

```
    function doGet() {
  return HtmlService
    .createTemplateFromFile('index')
    .evaluate();
}

function getData(){
  return SpreadsheetApp
    .openById('スプレッドシートID')
    .getActiveSheet()
    .getDataRange()
    .getValues();
}
```

```
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <h2>Contents of Spreadsheet</h2>
    <table id="target">
      Loading...
    </table>
    <script>
      function showTable(data) {
        let table = document.createElement("table");
        table.textContent = "";
        for (let i = 0; i < data.length; i++) {
          let tr = document.createElement("tr");
          for (let j = 0; j < data[i].length; j++){
            let td = document.createElement("td");
            td.textContent = data[i][j];
            tr.appendChild(td);
          }
          table.appendChild(tr);
        }
      }
      google.script.run
        .withSuccessHandler(showTable)
        .getData();
    </script>
  </body>
</html>
```