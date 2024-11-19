---
title: "初心者・子どもでも簡単！markdown AIの新機能使ってみた！ - Qiita"
source: "https://qiita.com/phibi-soon/items/4046d66a8e866258faa4?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[phibi-soon]]"
published: 2024-11-17
created: 2024-11-19
description: "導入こんにちは、もんすんです！「Webサイト制作のハードルを下げたい」そんな思いを持つ方にぜひお勧めしたいmarkdown AIの紹介です！markdown AIは、非エンジニアや初心者でも…"
tags:
  - "clippings"
---
## 導入

こんにちは、もんすんです！

**「Webサイト制作のハードルを下げたい」**  
そんな思いを持つ方にぜひお勧めしたい`markdown AI`の紹介です！  
`markdown AI`は、非エンジニアや初心者でも手軽にWebサイトを作成・公開できる革新的なツールです。  
この記事では、前回の記事で紹介した基本機能に加えて、`markdown AI`の新たな可能性を引き出す「AIモデル生成機能」について詳しく解説します。

前回の記事はこちらからご覧ください。

## markdownAIについて

## 概要

前回記事とほとんど同じですが、  
`markdown AI`は、誰でも簡単にWebサイトを作成・公開できるツールです。  
特に子どもや非エンジニアに優しい設計がされています。

`markdown AI`を利用しない場合、Webサイトを作成・公開するには、

1. Webサイトのデザインの作成
2. Webサイトのドメイン取得とサーバーの確保
3. HTML/CSS/JavaScriptによるWebサイトのページの作成
4. 公開

という手順を踏む必要があります。

これらの手順のうち、特に「HTML/CSS/JavaScriptによるWebサイトのページの作成」においてはプログラミングの技術が必要になるため、子どもや非エンジニアにとって障壁があるように感じます。  
一方で、`markdown AI`を使うとこういった手順が不要になります。

また、公式のサイトには以下の記載があります。

> You need to rent a server to create a website, but with markdown AI you can publish it as is.

> Publishing is easy and you can get your site's URL with just a few clicks of a button.

**日本語訳**  
Webサイト制作にはサーバーを借りる必要がありますが、`markdown AI`ならそのままサイトを公開できます。

公開は簡単で、ボタンを数回クリックするだけでサイトのURLを取得することができます。

上記からも、サーバーに関する知識などやプログラミング経験がなくても、Webサイトを作成することが可能ということが伺えます。

こういった部分が`markdown AI`の強みなんでしょうね！

## 新機能について

前回記事から、5ヶ月ほど経ちましたが、`markdown AI`にログインした先には、新しいボタンが追加されていました。

[![スクリーンショット 2024-11-02 22.20.04.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fe838d8fe-78b9-dc45-201e-ae22219c8f8b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=678c302d4d03d3d8c471ea32aa957f81)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fe838d8fe-78b9-dc45-201e-ae22219c8f8b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=678c302d4d03d3d8c471ea32aa957f81)

ロボットのアイコンのボタンです。

この機能はAIモデル生成機能のようです。  
こちらでは、`markdown AI`で作成したWebサイトなどを基にAI モデルを作成することができ、さらにそれを自分で作成した`markdown AI`のWebサイトに、生成したのAIモデルを利用するための機能を設置することができます。

## AIモデル生成

上述のロボットのボタンをクリックしましょう！  
すると以下の画面が現れます。

[![スクリーンショット 2024-11-04 21.00.10.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F472a1e93-c041-fc63-421f-64b5f0a55884.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=33cc58ffd0224cd655021c9329ece366)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F472a1e93-c041-fc63-421f-64b5f0a55884.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=33cc58ffd0224cd655021c9329ece366)

画面は2段構成になっています。  
まず、1段目は、上記の画像と同じですが、作成するAIモデルの基本情報を設定すル部分です。

- **Model List**  
既に作成したAIモデルが記録されるエリアになります。  
AIモデル名をクリックすると、選択したAIモデルの設定情報が確認できます。  
私の場合、既に\[test\]と\[new\]という名前のAIモデルを作成していたため、上の画像ではModel Listに2つの項目が表示されています。
- **Select Model**  
これは、これから利用するAIモデルの基になるモデルを選択できるセレクトボックスです。  
Gemini/Claude/gpt-4o-mini/Perplexityといったモデルを選択できます。それぞれのモデルの特徴は以下の記事から確認が可能です。  
[MarkdownAIの誰でもわかる使い方#【AIモデルの説明】](https://qiita.com/mdown_ai_jpn/items/d3e281565c876a0bd64f#ai%E3%83%A2%E3%83%87%E3%83%AB%E3%81%AE%E8%AA%AC%E6%98%8E)
- **Model Name**  
自分で作成する(した)AIモデルの名前です。自分がどれがどのAIモデルだったかわからなくならないように忘れない名前をつけるのが良さそうです。
- **Prompt**  
極めて重要な項目です。作成するAIに何をしてほしいかを指示するためのエリアです。`markdown AI`では「5つのR」というプロンプトの書き方を推奨しているとのことでした。  
[MarkdownAIの誰でもわかる使い方#プロンプトとは](https://qiita.com/mdown_ai_jpn/items/d3e281565c876a0bd64f#%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88%E3%81%A8%E3%81%AF)  
私も先日プロンプトエンジニアリングの「7R」について記事を書きましたので、参考にしていただけたらと思います。

試しにPrompt欄に「アヒル口調にしてください」と入れて、AIに「こんにちは」と送ると、「こんにちは、アヒルだよ〜！クワック！今日はどんなことをお話しするのかな〜？🐥✨」とAIから返信が返ってきました。間違いなくアヒルですね。  
この場合、7Rのうちの「**Role(役割)**」に分類されるかと思います。

次は2段目の内容です。

[![スクリーンショット 2024-11-04 21.00.17.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F8bf7b992-287c-f3f1-725d-7623ef928b33.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f0e9501dd5a4b43b79141f9bccf0e6ca)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F8bf7b992-287c-f3f1-725d-7623ef928b33.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f0e9501dd5a4b43b79141f9bccf0e6ca)

- **Knowledge**  
AIに事前に教えておきたい情報を共有することができます。  
これは、おそらく`RAG(Retrieval Augmented Generation：検索拡張生成)`という機構が利用されていると思われます。`RAG`は、事前にAIに教えておいた情報をデータベースに保持しておき、それに関連する質問が来た際にデータベースから情報を取りに行くというものです。つまり、この**事前に共有したデータを基に回答を生成してくれる**ようになります。  
さて、この`Knowledge`ですが、以下の3種類の方法で、事前情報を提供しておくことができるようです。
- markdown
- 既に`markdown AI`で作成したページを共有できます。
- \[View\]ボタンから、そのページをマークダウンではなく、HTMLで確認することが可能です。
- file
- HTML・PDF形式のファイルを共有できます。
- 自分が作成しているHPの情報をファイルで共有したり、資料をPDFで共有したりすることができるようです。
- link
- WebサイトのURLを共有できます。
- 自分のHPの情報や会社の情報などが記載されたWebサイトがある場合に利用できます。

`Knowledge`は\[Upload\]ボタンを押すことで、アップロードが完了します。

- **Comments**  
作成するAIに対するメモのようなもののようです。特に作成するAIモデルには影響しません。
- **Create/Updateボタン**  
このボタンで、設定を保存します。  
これでこれまでAIを使ったことがない方でもすぐにAIモデル作成が完了です！！

## markdown AIのページへのAIモデルの適用

AIモデルを`markdown AI`のページへ埋め込む方法は極めて簡単です！  
まず、作成画面に進み、以下の「Insert」ボタンをクリックします。  
[![スクリーンショット 2024-11-04 23.31.35.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F651da915-b44d-e07a-ca59-2d1dd0f3fba1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0a40e364789dd23e3cfe7d7c92afa5f6)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F651da915-b44d-e07a-ca59-2d1dd0f3fba1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0a40e364789dd23e3cfe7d7c92afa5f6)

次に「Script」を選択し、適用したいAIモデルを選択した上で、「Insert」をクリックします。  
[![スクリーンショット 2024-11-04 23.31.42.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F4c5c1beb-aa82-a361-dcbf-fffcff35b733.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=416fbc6922543de490be07636e195c55)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F4c5c1beb-aa82-a361-dcbf-fffcff35b733.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=416fbc6922543de490be07636e195c55)

[![スクリーンショット 2024-11-04 23.32.43.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fad997433-4693-ed34-c3f2-282de15d89e9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c1679ced7857a86f3eecd53e4893ebea)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fad997433-4693-ed34-c3f2-282de15d89e9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c1679ced7857a86f3eecd53e4893ebea)

すると、以下のように作成中のページに以下のようにスクリプトが埋め込まれます。  
[![スクリーンショット 2024-11-04 23.32.58.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fdb3d4e53-8285-f29d-2eb0-719f74f577fc.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c83185e61d58548e915168df50ca4891)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fdb3d4e53-8285-f29d-2eb0-719f74f577fc.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c83185e61d58548e915168df50ca4891)

これは、markdownではなく、少々プログラミングの知識が必要になる領域ではありますが、小難しいことは一旦割愛します。  
ここで、さらに上にある「View」ボタンをクリックしてみましょう。  
すると、以下のように「Run AI」というボタンが現れると思います。

[![スクリーンショット 2024-11-04 23.42.49.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fb324708f-5db1-c15f-fe07-2c9d07ce01db.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8f7e605e600f9a7c1b78f64c388bedd4)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2Fb324708f-5db1-c15f-fe07-2c9d07ce01db.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8f7e605e600f9a7c1b78f64c388bedd4)

さらにこのボタンをクリックすると、...

[![スクリーンショット 2024-11-04 23.42.57.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F817210d7-2b68-d8d0-7896-f0e22c5418a7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=b225f48d03cfa8ea3baf2b91e293dbb8)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F817210d7-2b68-d8d0-7896-f0e22c5418a7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=b225f48d03cfa8ea3baf2b91e293dbb8)

メッセージが表示されました！！  
これは、AIからの返信を表示しており、ボタンをクリックする度、表示されるメッセージは変化していきます。

これで、AIの埋め込みは完了です！  
ようこそ、AIの世界へ！！！![:robot:](https://cdn.qiita.com/emoji/twemoji/unicode/1f916.png ":robot:")

## markdown AIとAIモデル機能の使い道を考えてみた！

さて、ここからはどのようにこの機能を活かしていくか考えてみたので紹介していきます。

## 社会人向け

2024年11月時点で`Knowledge`を追加するとサーバーエラーとなるため、一旦ここでは活用方法の提案のみとなります。

私は、過去に製造業で仕事をしていたことがあります。

その工場には長い歴史があり、作業フローが極めて複雑になっておりました。  
そのため、そのフローをWordで作成し、印刷し、作業者が閲覧できるようにファイリングして棚に収納していました。  
安全管理のためのフローだったこともあり、全部で**数百**ありました。

このように手順書をWordなどで作成し、紙で保存している、、という会社はいまだに多いのではないかと思います。

### Phase1: 作業フロー書をmarkdown AIで共有する

まずPhase1として、Wordで作成していた作業フロー書をmarkdown AIで書き起こしていきます。  
以下のようにマークダウンの見出しに基準を決めておくと、良いでしょう。

```
見出しの基準(例)

# タイトル(例: コンテナへのAA粉の投入手順)

## 手順番号(例: Step1)

### 手順小番号(例: Step1-2)
```

以下のようにマークダウンを入力した後は、「Save」を選択し、入力した内容を保存し、さらに「View」を選択し、閲覧モードに切り替えます。

[![スクリーンショット 2024-11-14 0.30.55.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F213b4051-d65c-78fd-787d-434dccd0dd93.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=994db52d390ad03e4d27ac2019f532de)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F213b4051-d65c-78fd-787d-434dccd0dd93.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=994db52d390ad03e4d27ac2019f532de)

そうすると、以下のように編集モードから閲覧モードになるので、次は「URL」を選択します。

[![スクリーンショット 2024-11-14 0.37.03.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F81ad1096-272b-71bc-71b4-3a17f51d2a25.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ef340219e36127772c6e32ad374e43c7)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F81ad1096-272b-71bc-71b4-3a17f51d2a25.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ef340219e36127772c6e32ad374e43c7)

以下のようなモーダルが表されるので、指示の通り「Publish」を選択しましょう。

[![スクリーンショット 2024-11-14 0.31.28.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F1c2c2e2f-878b-80be-76ec-f5eb23bac1c8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f2df8cee87afa006be7a383116343897)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F1c2c2e2f-878b-80be-76ec-f5eb23bac1c8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f2df8cee87afa006be7a383116343897)

すると、最後にURLが表示されるので、これで、1ページ手順書の作成が完了します。

[![スクリーンショット 2024-11-14 0.31.35.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F43a81340-5c1b-7105-0eee-aa07494b07f8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8d3a9e22b2f9f22fab569d1f4c44db4a)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F43a81340-5c1b-7105-0eee-aa07494b07f8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8d3a9e22b2f9f22fab569d1f4c44db4a)

### Phase2: AIモデルの`Knowledge`に作業フロー書を読み込ませて、チャットBotにする

さて、Phase1で、作業フロー書は、紙面からデジタルに変換することができました。

## 子ども向け

子どもは某論破王の方(の真似をするの)が好きよく聞きます。  
子どもに興味を持ってもらうために、その方を模した相手とディベートをできるチャットを作成してみました。

### AIモデル作成

ここでは、`markdown AI`で推奨している「5つのR」というプロンプトの書き方を利用しました。

[MarkdownAIの誰でもわかる使い方#プロンプトとは](https://qiita.com/mdown_ai_jpn/items/d3e281565c876a0bd64f#%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88%E3%81%A8%E3%81%AF)

```
Request: 私とディベートしてください。上から目線の敬語で回答してください。
Role: あなたは大人で、議題に関するの専門家です。
Rule: あなたの一人称は「おいら」です。
Recommend: 私が個人的な感想を述べた場合、「それってあなたの感想ですよね？」と高圧的に返答する。感想ではなかった場合は、それに対して反対意見を述べる。「だって、〇〇って△△じゃないですか？」や「〇〇ですよね？」という表現を多用してください。日本語で200文字以内で返答してください。
```

こちらを\[![:robot:](https://cdn.qiita.com/emoji/twemoji/unicode/1f916.png ":robot:")ボタン\]から開いた「Create Model」の画面の「Prompt」に入力します。

そのほかの設定は以下の通り、

- Select Model: 自由に好みなものを選択
- Memory: チェックをオンにします。✅
- Model Name: 自由に自分がわからなくならないように設定します。
- Knowledge: 何も設定しません。  
設定が完了したら、下にある「Create」ボタンを押します。

\[参考\]  
[![スクリーンショット 2024-11-16 23.56.04.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F72f8bda0-b849-f214-8497-153497093149.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=91b258b003feeba5d24e08a42d044d17)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F72f8bda0-b849-f214-8497-153497093149.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=91b258b003feeba5d24e08a42d044d17)

## AIモデルの埋め込み

次にmarkdown AIのサイト作成ページにAIモデルを埋め込んでいきます。  
基本的な作業としては、上の「markdown AIのページへのAIモデルの適用」で紹介しているので、そちらを参考にしてください。

ここで、追加された処理の中に以下のソースコードがあります。  
この中で、\[`**********`\]と書いた部分には、ランダムな文字列が書かれていると思います。  
これは次の「画面の修正」のところで使うので、メモ帳とかにコピペしておきましょう。

```
const answer = await serverAi.getAnswerText('**********', '', message);
```

## 画面の修正

上記で、AIモデルを埋め込んだあと、注意書きにある\[`**********`\]をコピーしたら、一旦エディタをまっさらにします。

その後、以下のソースコードを埋め込みます。  
少々難易度が高めですが、ほとんど、コピペで使えますし、子どもは柔軟なので、おかしなことがあってもすぐに対処できる...と信じています。

```
# 論破王とディベート対決！

## ディベート設定
<div style="display: inline-block;">
  テーマ: <input type="text" id="theme">についてディベートします。論破王は、
  <select id="opinion">
    <option>賛成</option>
    <option>反対</option>
  </select>
の立場をとります。
</div>
<br>
<br>
<button id="start-btn">ディベート開始</button>
<button id="reset-btn">リセット(テーマ変更)</button>

## 議論
<div id="chat-area">
  <div id="chat-container">
  </div>
  <div id="input-container">
    <input type="text" id="message-input" placeholder="論破王に返信">
    <button id="send-btn" disabled>送信</button>
  </div>
</div>

<script>
(() => {
  // 以下の[**********]をコピーした値に置き換える
  const serverAiId = '**********';
  // ↑↑↑ ここだけ修正 ↑↑↑
  let messageId = 0;
  const serverAi = new ServerAI();
  const startButton = document.getElementById('start-btn');
  const sendButton = document.getElementById('send-btn');
  const resetButton = document.getElementById('reset-btn');
  const theme = document.getElementById('theme');
  const opinion = document.getElementById('opinion');
  const input = document.getElementById('message-input');
  const chatContainer = document.getElementById('chat-container');
  startButton.addEventListener('click', async event => {
      startButton.disabled = true;
    if (theme.value.trim() !== "") {
      theme.disabled = true;
      opinion.disabled = true;
      const themeMsg = \`##テーマ## ${theme.value} \n##botの立場## ${opinion.value}\`;
      await getAiAnswer(themeMsg).catch((e) => {
        console.error(e);
        startButton.disabled = false;
        theme.disabled = false;
        opinion.disabled = false;
      });
      sendButton.disabled = false;
    } else {
      startButton.disabled = false;
    }
  });

  sendButton.addEventListener('click', async event => {
    sendButton.disabled = true;

    if (input.value.trim() !== "") {
      // Add new message
      const messageDiv = document.createElement('div');
      messageDiv.className = 'user';
      messageDiv.id = \`message-${messageId}\`;
      messageDiv.textContent = input.value;

      chatContainer.appendChild(messageDiv);
      chatContainer.scrollTop = chatContainer.scrollHeight;
      messageId++;
      const msg = \`私の意見に対しての回答のみしてください。\n\n##テーマ## ${theme.value} \n##botの立場## ${opinion.value}\n##私の立場## ${opinion.value}ではない\n\n##私の意見## ${input.value}\`;
      await getAiAnswer(msg);
      input.value = '';
    }
    sendButton.disabled = false;
  });

  resetButton.addEventListener('click', async event => {
    chatContainer.innerHTML = '';
    sendButton.disabled = true;
    startButton.disabled = false;
    theme.disabled = false;
    opinion.disabled = false;
  });

  const getAiAnswer = async (message) => {
      const answer = await serverAi.getAnswerText(serverAiId, '', message);
      const messageDiv = document.createElement('div');
      messageDiv.className = 'ai-response';
      messageDiv.id = \`message-${messageId}\`;
      messageDiv.textContent = answer;

      chatContainer.appendChild(messageDiv);
      chatContainer.scrollTop = chatContainer.scrollHeight;
      messageId++;
  }
})();
</script>

<style>
  button {
    margin-left: 10px;
    padding: 10px 20px;
    font-size: 16px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  button:disabled{
    filter:brightness(0.8);
    cursor:not-allowed;
  }
  #chat-area {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    height: 50vh;
  }
  #chat-container {
    flex: 1;
    padding: 20px;
    overflow-y: auto;
    background-color: #f5f5f5;
  }
  .user, .ai-response {
    margin: 10px 0;
    padding: 10px;
    border-radius: 10px;
    max-width: 60%;
  }
  .user {
    background-color: #d1e7ff;
    align-self: flex-start;
  }
  .ai-response {
    background-color: #f1c40f;
    align-self: flex-end;
  }
  #input-container {
    display: flex;
    padding: 10px;
    background-color: #fff;
  }
  #input-container input {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  #input-container button:hover {
    background-color: #0056b3;
  }
</style>
```

上記の\[\*\*\*\*\*\*\*\*\*\*\]の部分を、上のステップでコピーした値に置き換えます。  
念の為、修正箇所だけを抽出したものを以下に示します。

```
// 以下の[**********]をコピーした値に置き換える
const serverAiId = '**********';
// ↑↑↑ ここだけ修正 ↑↑↑
```

以上の設定を終えると、このような画面が表示されるかと思います。  
[![スクリーンショット 2024-11-17 0.27.41.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F3a126356-0f42-1581-6568-7dc545f765c3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=685c1ce76939941816e439ac17a6b2f0)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F3a126356-0f42-1581-6568-7dc545f765c3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=685c1ce76939941816e439ac17a6b2f0)

テーマを入力して、賛成反対を選択し、「ディベート開始」を押すと、「議論」のエリアでチャットが可能になります。

[![スクリーンショット 2024-11-17 0.34.42.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F9e39b507-535c-cd68-60db-b275cc539a5d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=dc52b6fd94c13a4c4c420e3fbc7d1fdf)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F1655179%2F9e39b507-535c-cd68-60db-b275cc539a5d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=dc52b6fd94c13a4c4c420e3fbc7d1fdf)

## 公開URL

こちらから遊ぶことが可能です。

## 終わりに

今回は、`markdown AI`の概要とAIモデル生成機能を紹介しました。  
`markdown AI`はプログラミングの知識がなくてもWebサイトを簡単に作成できるツールで、特に非エンジニアにとって手軽に利用できる点が魅力です。

また、AIモデル生成機能により、自作したサイトにAIを組み込むことができ、ユーザー体験を大幅に向上させる可能性を秘めています。

`markdown AI`は今後、さらに使いやすいツールとして進化していって欲しいと思いました。

もしWebサイト作成やAI導入に興味がある方は、この記事を参考にぜひ`markdown AI`を試してみてください。