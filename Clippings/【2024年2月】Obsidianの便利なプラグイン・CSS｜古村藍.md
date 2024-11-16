---
title: "【2024年2月】Obsidianの便利なプラグイン・CSS｜古村藍"
source: "https://note.com/indigo372/n/n0c96bac9a1eb"
author:
  - "[[古村藍]]"
published: 2024-02-25
created: 2024-11-11
description: "現在の私のObsidianの見た目 ぼくがかんがえた最強のObsidian設定&nbsp;という前回の記事がそこそこウケたので、二匹目の泥鰌というわけではないですがあれから色々いじった部分等を徒然話していきたいと思います。  有用なプラグイン  最近台頭してきた優秀なプラグインを紹介していきます。  2Hop Links Plus  Scrapboxであるような二段階バックリンクを実現します。Plusじゃないバージョンの方はバグり散らかしていたのですが、こっちは問題なく動作するため大変便利です。 まるでローカルのScrapbox！ File Indicators  アイコン追加系プラグ"
tags:
  - "clippings"
---
![画像](https://assets.st-note.com/img/1708860562234-6pAocQ4Lpq.png?width=1200)

現在の私のObsidianの見た目

[ぼくがかんがえた最強のObsidian設定](https://note.com/indigo372/n/nae1e72203c5b) という前回の記事がそこそこウケたので、二匹目の泥鰌というわけではないですがあれから色々いじった部分等を徒然話していきたいと思います。

## 有用なプラグイン

最近台頭してきた優秀なプラグインを紹介していきます。

### 2Hop Links Plus

Scrapboxであるような二段階バックリンクを実現します。Plusじゃないバージョンの方はバグり散らかしていたのですが、こっちは問題なく動作するため大変便利です。

![画像](https://assets.st-note.com/img/1708862193690-I9SR3ierCo.png?width=1200)

まるでローカルのScrapbox！

### File Indicators

アイコン追加系プラグインの一種ですが、個人的には**すべてのアイコンプラグインを過去にした**と思っています。なぜか。

- 1\. 軽い

- プラグインフォルダで容量を確認すればわかるが、圧倒的に軽い。90kb以下

- 参考までにobsidian-icon-folderはmain.jsだけで800kb近くある
- 2\. ビジュアル的主張がいい意味で薄い

- 記号と色の情報しかないので、アイコン設定時にも迷う予知が少なく、かつ悪目立ちしない

![画像](https://assets.st-note.com/img/1708860876112-H3FQzXUdqF.png)

これくらいの主張

シンプルゆえに軽量かつバグも少なく大変気に入っております。お試しあれ。

### Custom Frames

- 外部アプリをiframeとしてObsidianのPaneに追加できる
- 素晴らしいのはフレームに対してCSSやJSをカスタムできること。色合いの調和から機能追加までなんでもできる
- Todolist用のテンプレートがあるので自分はとりあえずTodolistを置いている

![画像](https://assets.st-note.com/img/1708860899684-nBfiADyuxr.png)

こちら備え付けになっておりますので

### Floating TOC

常々使いづらいと思っていました、ObsidianのデフォルトTOC。なんといってもペインをひとつ消費しますからね。  
そんな問題を解決してくれる贅沢プラグイン。

きわめて過不足がない、名前通りの機能を果たしてくれる完璧なプラグインです。プラグイン容量も軽いので多分そんなに重くもない。

### その他

- Gemini Assistant

- GoogleのGeminiが利用できる。現在(24/2/21)GeminiのAPIは無料なのでAI系プラグインならこれが一番良いと思います。
- Key-Value List

- 個人的にはテーブル機能の上位互換だと思っています

- なぜテーブルの上位互換か？

- マークダウンテーブルはmarkdownをフォーマットできる環境に依存している。あの形式だと別形式へのコピーペーストがそこそこ面倒。本機能の場合はただのテキストなのでプラグインなしでも骨組みに影響はまったくない
- フォーマット崩れが起きない。markdownテーブルの場合はフォーマットされる前のbare sourceの場合は特にCJK文字だとグチャることが結構ある。本機能の場合はそのリスクがない
- ヘッダーの入力を強制されない。Markdown tableだとヘッダーを強制されるため、書きたい内容の種類によってはここ何書けばええんやってなることが結構ある。

![画像](https://assets.st-note.com/img/1708862384338-x0e20iOGFf.png)

マークダウンビュー

![画像](https://assets.st-note.com/img/1708862496128-XY0zzIt0aL.png)

ソースビュー　Key-Value Listの方が圧倒的に崩れが少なく、見やすい

- Relation Pane

- リンクとバックリンクのペインをひとつにまとめて+アルファで色々つけた感じ
- 単純にペイン数を減らせるので便利かも
- 容量46kb
- Zhongwen-Block

- 中国語勉強してる人特効だけど相当便利
- 中国語処理プラグインの宿命だがそこそこ重いので注意

- Auto file name

- 入力冒頭n文字を参照して自動でタイトルを埋めてくれる
- いろいろ干渉が起きそうなのが恐いが、作動するフォルダを指定できるのでWebClip系フォルダを避けるとかすれば便利かも。

## CSSについて

はい。実は今回の本番はこっちです。前回ほとんど触れませんでしたので。  
ObsidianはプラグインのみならずCSSで輝くところもございます。  
とはいえCSSは見た目を変えるのが主なので、個々人の好みなところはあります。そこで私が申し上げるのはまずひとつ。**以下のショーケースから気に入ったものを片っ端から持っていきなさい。**

上記リポジトリは、質が高いObsidian CSSをちょっと引くくらい大量に格納しています。そのままダウンロードすればObsidian vaultとして開けるショーケースがございますので、どのような効果のCSSかを確認しながら取捨選択し、自分のVaultにコピーするとよろしいと思われます。  
個人的には、「Safari Tabs」と「New Note Button」は見た目のみならず機能性が格段に上がるので追加することをおすすめします。  
Safari Tab CSSの利点は、フォーカスしたタブの横幅を広げてくれるのでObsidianで起こりがちな「タブを多く開くと各タブの視えるタイトル文字数が少なくなりすぎてどのタブがどのノートだったか見失う」現象を抑制できます。  
New Note Button CSSは、地味にボタンひとつでわかりにくい「新規ノート作成」ボタンの見やすさを上げることができます。まぁ普通はCtrl+Nを使うでしょうけど、入れておいて損はないかと。  
あと機能性というよりは見た目の話ですが、Celtic Inline Titleは見た目がかなりカッコよくなるので厨二病の人は入れておくといいかも。

![画像](https://assets.st-note.com/img/1708861520839-iZlzmDE37k.png?width=1200)

Celtic Inline Titleなし

![画像](https://assets.st-note.com/img/1708861503202-esJqTye5lI.png?width=1200)

Celtic Inline Titleあり

ほか、機能的向上が見られるCSSとしては以下のようなものがあるかと思います。私の使っているものから一部抜粋します。

### スクロールバーの太さ変更

```
/* Scrollbar */
/* change width */
::-webkit-scrollbar {
    width: 18px !important;
}
```

ObsidianのデフォルトスクロールバーはWindowsだとどうも細すぎてクリックできないことがあるので。

### ホバープレビューの大きさ変更

```
.hover-popover:has(.markdown-embed.is-loaded) {
    scale: 80% !important;
}
```

最近のバージョンだと抑制されたようですが、マウスオーバーでノートをプレビューする際に他のリンクに覆いかぶさるような形で現れて邪魔なことって結構ありますよね。サイズを小さくしてしまえばそれを抑制できます。

### エクスプローラーに下線を追加

```
div.nav-file-title,
div.nav-folder-title {
    border-bottom: 1px dashed var(--interactive-hover);
}

.oz-nav-file {
    border-bottom: 1px dashed var(--interactive-hover);
}
```

![画像](https://assets.st-note.com/img/1708861755888-HSZQEFhp4G.png)

下線なし

![画像](https://assets.st-note.com/img/1708861733533-XNd8odxQrd.png)

下線あり

エクスプローラーのノート同士の区切りがわかりやすくなります。が、人によっては見た目を損なうのでこれは好みかな。

### サイドドックの色を変更

```
[aria-label*='要素名'] {
    --icon-color: #A899F4; /*などの好きな色*/
    --icon-color-hover: #A899F4;
    --icon-color-active: #A899F4;
    --icon-color-focused: #A899F4;
}
```

![画像](https://assets.st-note.com/img/1708861888557-ZRxu1hIDgC.png)

色変更なし

![画像](https://assets.st-note.com/img/1708861901924-3PZjzanINm.png)

色変更あり

パッと見でどのボタンがどの機能だったかを識別しやすくなります。  
これも人によっては見た目を損なうので選択で。  

以上、Obsidianの有効な設定についてお伝えしました。簡単で効果的なプラグインの導入やアイコンの使用、カスタムフレームの利用など、日常の作業効率を向上させるアイデアが満載です。また、見栄えもスッキリしているのでおすすめです。ぜひ試してみてください。Obsidianの使い方をより上達させるためにも、他の記事やnoteの更新もお見逃しなく！