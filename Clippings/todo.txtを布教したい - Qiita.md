---
title: "todo.txtを布教したい - Qiita"
source: "https://qiita.com/maedana/items/713390ce590b92fee97f?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[maedana]]"
published: 2024-12-02
created: 2024-12-06
description: "この記事はソニックガーデン プログラマ アドベントカレンダーの6日目の記事です。はじめにこんにちは。株式会社ソニックガーデンのmaedanaです。今回は(自分の知る限り)マイナーなTodo管理…"
tags:
  - "clippings"
---
この記事は[ソニックガーデン プログラマ アドベントカレンダー](https://qiita.com/advent-calendar/2024/sonicgarden)の6日目の記事です。

---

## はじめに

こんにちは。株式会社ソニックガーデンのmaedanaです。

今回は(自分の知る限り)マイナーな[Todo管理用のテキストファイル(todo.txt)](https://github.com/todotxt/todo.txt)及び、このテキストファイルを利用するためのクライアントツールについて書きます。なお今回の話の前提として**個人のTodo管理**を想定しており、チームのTodo管理は想定していません。

[todo.txt](https://github.com/todotxt/todo.txt)は、todo管理のためのテキストファイルのフォーマットの仕様が書かれたドキュメントです。さて、いきなりですが[todo.txt](https://github.com/todotxt/todo.txt) には冒頭で以下のように書かれています。

> The first and most important rule of todo.txt:  
> A single line in your todo.txt text file represents a single task.

つまり、1行1タスクです。例えば以下のようなシンプルな中身のテキストファイルです。

基本的にはこれだけです。

## なぜテキストファイルなのか

[todo.txt](https://github.com/todotxt/todo.txt)をもう少し読み進めると以下のように書かれています。

> Plain text is software and operating system agnostic. It's searchable, portable, lightweight, and easily manipulated.

(ただのテキストファイルなので)`OS依存しない/検索可能/ポータブル/軽量/操作しやすい`という当たり前だけど、とても重要なことが書かれています。個人的嗜好としても

- マウス操作よりキーボード操作が好き
- GUIよりCUI/TUIが好き
- シンプルなものが好き
- 普段使うエディタはNeoVim

ということがあるので、**単なるテキストファイル**というのはとても相性がいいのです。この**単なるテキストファイル**をクラウドに自動同期されるようにし、様々なクライアントツールを利用すればPC/スマホなど様々なデバイスで利用することも簡単です。

## [todo.txt](https://github.com/todotxt/todo.txt)の細かな形式について

[todo.txt](https://github.com/todotxt/todo.txt)にとても詳しく書かれていますが、全ては以下の画像に集約されます。

[![todo.txtのフォーマットルール](https://qiita-user-contents.imgix.net/https%3A%2F%2Fraw.githubusercontent.com%2Ftodotxt%2Ftodo.txt%2Frefs%2Fheads%2Fmaster%2Fdescription.svg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a0022bbd80c02b49be678082c4d016fd)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fraw.githubusercontent.com%2Ftodotxt%2Ftodo.txt%2Frefs%2Fheads%2Fmaster%2Fdescription.svg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a0022bbd80c02b49be678082c4d016fd)

見る人が見ればわかりますが、これは[GTD(Getting Things Done)](https://en.wikipedia.org/wiki/Getting_Things_Done)に沿った運用ができる、ということです。今回はGTDについては説明しませんので、気になる方は調べてみるといいと思います。検索すれば日本語の情報や書籍等も豊富に見つかります。なお、[拡張仕様](https://github.com/todotxt/todo.txt?tab=readme-ov-file#additional-file-format-definitions)を定義することも可能なので、自分好みに拡張することもできます。

## [todo.txt](https://github.com/todotxt/todo.txt)のクライアントツール紹介

- todo.txt-cli
- [https://github.com/todotxt/todo.txt-cli](https://github.com/todotxt/todo.txt-cli)
- todotxtでホスティングしているので公式?のCUIクライント。これで満足できるならきっとこれが一番いいのだと思います。僕の場合は複数プロジェクトを俯瞰してみたいというのがあってこれだけでは流石に運用が難しかったです。
- topydo
- [https://github.com/topydo/topydo](https://github.com/topydo/topydo)
- 当初愛用していたツールです。CUI(というか正確にはTUI?)でここまで表現できるのかという驚きがありました。ただ、僕の場合結構大きめの粒度のタスク登録をして、その詳細は別のテキストファイルに書きたい、というのがあってその点で後述の自作ツール作成に繋がりました。
- 完全に余談ですけど、TUIで何か自作するなら例えばRustの [https://github.com/ratatui/ratatui](https://github.com/ratatui/ratatui) など使うと色々出来て楽しいんじゃないかなと思います。
- tokaido
- [https://github.com/maedana/tokaido](https://github.com/maedana/tokaido)
- 自作のビューワーです。当初TUIで作りたかったんですけど、なかなか思うようにいかず、日頃から慣れているRailsでローカルで動かす前提のWebアプリとして実装しました。NeoVimと連動させないとほぼ意味がないので、その場合はtopydoがいいかなと思います。各Todoの詳細を別テキストファイルで管理したくて作りましたが、自分さえ使えればいいと思っているのであまりちゃんと作り込んでないです。そろそろ作り直したい気持ちはちょっとあります。
- 詳しく言及しませんが、[https://github.com/neovim/neovim-ruby](https://github.com/neovim/neovim-ruby) を使うことでRubyからNeoVim操作できるので工夫すればもっと色々できそうです。

## 個人的な運用方法について

- [tokaido](https://github.com/maedana/tokaido)をビューワーとして利用
- [todo.txt](https://github.com/todotxt/todo.txt)の編集はNeoVim
- [tokaido](https://github.com/maedana/tokaido)とNeoVimの連動で個別Todoの詳細をさらに別のテキストファイルで編集
- [todo.txt](https://github.com/todotxt/todo.txt)と個別TodoのテキストファイルをGitリポジトリで管理
- Priorityは使わない。エディタで行単位の並び替えをするだけで十分
- Contextは使わない。主に仕事のみでの利用なので切り替える必要性を感じない。
- Projectは凄く使う。複数プロジェクト掛け持ちなのでプロジェクトごとの進行中のタスクを管理したいので。
- 期限付きタスクはdue: をセット(しつつ、リマインド目的で必要に応じて別のリマインダーツールに登録)

このように運用することで

- 移動中など最悪ネット環境がなくてもタスク管理できる
- すべてテキストなのでタスクの詳細テキスト含めて[ripgrep](https://github.com/BurntSushi/ripgrep)等で素早く探せる
- タスクの詳細テキストをMarkdownで書くようにしているので、例えばチームへの共有用にgithub issueに内容を転記したいなどの場合でもコピペで済む

など日々の仕事の進める上でとても便利です。

## まとめ

[Todo管理用のテキストファイル(todo.txt)](https://github.com/todotxt/todo.txt)について紹介しました。自作にこだわりはないので、もっとこれが流行ってもっと使い勝手のよいクライアントができてほしいなーと思ってます。

---

[ソニックガーデン プログラマ アドベントカレンダー](https://qiita.com/advent-calendar/2024/sonicgarden) 7日目は [@LuckOfWise](https://qiita.com/LuckOfWise) です。お楽しみに！