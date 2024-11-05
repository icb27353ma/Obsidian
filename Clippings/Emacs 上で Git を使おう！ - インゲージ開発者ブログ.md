---
title: "Emacs 上で Git を使おう！ - インゲージ開発者ブログ"
source: "https://blog.ingage.jp/entry/2019/11/11/114716"
author:
  - "[[https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023351.png]]"
published: 2019-11-11
created: 2024-11-05
description: "こんにちは、masm11 です。 皆さん、Git 使ってますか? 使ってますよね? Git を使っている人はもう Emacs 人口を超えているのでは、と思っています。 一方で、Emacs ってご存知ですか? 高機能なエディタです。 ですが、最近はあまり人気がないらしいですね。 出来の良い IDE の登場によるのでしょうか。 でも私はそんなことはお構いなく、Emacs を使っています。 さて、今回はそんな Emacs 上で Git が使える Magitの使い方をご紹介したいと思います。 インストール Emacs で M-x package-list-packages してしばらく待つと、magi…"
tags:
  - "clippings"
---
こんにちは、masm11 です。

皆さん、Git 使ってますか? 使ってますよね? Git を使っている人はもう Emacs 人口を超えているのでは、と思っています。

一方で、Emacs ってご存知ですか? 高機能なエディタです。 ですが、最近はあまり人気がないらしいですね。 出来の良い IDE の登場によるのでしょうか。 でも私はそんなことはお構いなく、Emacs を使っています。

さて、今回はそんな Emacs 上で Git が使える [Magit](https://magit.vc/)の使い方をご紹介したいと思います。

### インストール

Emacs で `M-x package-list-packages` してしばらく待つと、magit が現れます (しばらく待たないと現れないと思います)。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023351.png)

`magit` で Enter を押して、`Install` で Enter を押すと、インストールできます。 ![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023439.png)

そして少し設定します。私は `~/.emacs` で以下のようにしています。

```
(defalias 'magit 'magit-status)
(global-set-key "\C-xg" 'magit-status)

(setenv "GIT_EDITOR" "emacsclient")
(add-hook 'shell-mode-hook 'with-editor-export-git-editor)
```

### 使ってみる

- 起動

`C-x g` と入力すると、Magit が起動します。 カレントディレクトリが git 管理されているなら、そのディレクトリが対象になります。 そうでない場合は、ディレクトリを尋ねられますので入力してください。 もし、カレントディレクトリが git 管理されているけど違うディレクトリを対象にしたい 場合は、代わりに `C-u C-x g` と入力すれば、必ずディレクトリを尋ねてくれます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023513.png)

これで Magit が起動しました。`magit: <ディレクトリ名>` というバッファが開いています。ここには、現在の状態が表示されています。Magit はこのバッファで操作します。

まずはファイルを編集してください。普通に Magit とは関係なく編集します。 その後、Magit のバッファに戻ってください。戻り方は `C-x b` でもいいですし、 `C-x g` でもう一度起動しても構いません。`C-x b` で戻った場合は、バッファの内容を 更新するために一度 `g` を押してください。

編集したファイルが Unstaged changes という項目に表示されています。 新規ファイルの場合は Untracked files に表示されています。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023549.png)
- stage

Unstaged changes または Untracked files の該当ファイル名で `s` を押すと、 そのファイルを `git add` (stage) することができます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023638.png)
- stage をキャンセル

Staged changes の該当ファイル名で `u` を押すと、unstage できます。
- diff

Staged changes で `d d` と入力してみてください。今 stage した差分が表示 されます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023705.png)

Unstaged changes がまだあるなら、そちらで `d d` すれば、まだ stage して いない差分が表示されます。

Untracked files はファイル名でそのまま Enter を押すとファイルの内容が表示 されます。
- commit

Staged changes で `c c` と入力すると、stage しておいた差分を commit することができます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023727.png)

commit message を入力して、`C-c C-c` で commit できます。キャンセルしたい場合は `C-c C-k` でできます。
- log

`l l` と入力すると、ログがグラフ付きで表示されます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023750.png)

ログの各行で Enter すると、その commit の詳細が表示されます。
- push

`P u` と入力すると、 push できます。

現在のブランチを初めて push する場合は、push 先を尋ねられますので、入力してください。この時、補完を活用すると便利です。2回め以降の場合は最初と同じ場所に push されます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191029/20191029203540.png)

2箇所それぞれに push したいこともあります(あまりないと思いますが…)。 その場合、2箇所めは代わりに `P p` と入力すればできます。使い方は `P u` と似ているのですが、push 先はブランチでなく remote のみで指定します。ブランチ名は手元と同じになります。

`u` の場合と `p` の場合でそれぞれに push 先を覚えてくれます。 push 先が心配になった場合は、`P` まで入力すると以下のバッファが必ず開きますので、 ここで確認できます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023838.png)

この画面のとおり、実は3箇所めもあって、`P e` です。これは push 先を覚えてくれません。稀にしか使わない remote ブランチに使うと良いでしょう。
- pull

pull したい時は `F u`, `F p`, `F e` です。`u`, `p`, `e` は push の場合と同じです。

この時、マージの commit message を求められますので、そのまま `C-c C-c` で commit します。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023023925.png)

通常は vim 等が呼び出されてしまうのですが、冒頭に紹介した設定の↓この部分により、代わりに Emacs に投げることができているわけです。

```
(setenv "GIT_EDITOR" "emacsclient")
(add-hook 'shell-mode-hook 'with-editor-export-git-editor)
```

- コンフリクトの解消

pull するとコンフリクトすることがありますね。

この時、Magit バッファには `unmerged` と表示されています。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191110/20191110005646.png)

このファイルを開いて `====` などで検索すると、コンフリクトしている箇所が見つかり、 色分けされているので一目瞭然です。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191110/20191110005717.png)

コンフリクトを解決してファイルを保存してください。

Magit バッファに戻ると、既に stage されています。全てのコンフリクトが解消したら、 `c c` で commit してください。

以上で基本的な操作は一通りできると思います。

### 更に便利な操作

更に、もう少し便利な操作を説明します。

- ファイル中の一部の変更のみ stage

Unstaged changes で `d d` すると、stage していない差分が表示されるわけですが、 この中から特定の hunk のみを stage できます。 その hunk に合わせて `s` を押すだけです。

…ところで、hunk とは何でしょうか? 差分の表示は `@@ -0,0 +1,2 @@` のような `@@` の行で区切られていますね? この区切られた一つひとつを hunk と呼んでいます。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023024002.png)

この hunk ごとに stage できるわけです。しかも手軽に。
- ファイル中の一部の変更のみ unstage する

Staged changes の差分表示中に `u` を押すと、その hunk のみを unstage することができます。
- ファイル中の一部の変更のみ元に戻す

Unstaged changes の差分表示中に `k` を押すと、その hunk をキャンセルして元に戻すことができます。

差分を見ながら、「この hunk を stage」「この hunk はやっぱり変更キャンセル」などが 手軽にできるのは、とても便利です。

### まとめ

私がよく使う Magit の操作を紹介してみました。 他にもいろいろな操作ができます。 Magit バッファで `?` と入力すると、どのキーでどんな操作ができるのかがわかります。

![](https://cdn-ak.f.st-hatena.com/images/fotolife/m/masm11/20191023/20191023024035.png)

今回はこれらのうち極一部しか説明しませんでした。いろいろ試してみると良いでしょう。

ではまた。