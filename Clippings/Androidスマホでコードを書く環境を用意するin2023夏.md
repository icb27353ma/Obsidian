---
title: "Androidスマホでコードを書く環境を用意するin2023夏"
source: "https://zenn.dev/negiboudu/articles/35cf465b683d16"
author:
  - "[[Zenn]]"
published:
created: 2024-11-08
description:
tags:
  - "clippings"
---
## 概要

通勤のときなどにちょっとコードを書いて試したいなと思って試行錯誤した結果、TermuxからGitHub Codespacesに接続するのが一番だという結論に至りました。そのやり方を書きます。

## GitHub Codespacesを用意する

## 費用

無料枠が大きいので、とりあえず作ってみてもお金はかかりません。（2023夏時点）  
接続時間が長かったりストレージの使用量が大きかったりするとお金がかかります。

## 手順

GitHubにログインしたあと、右上の方にある＋マークなどからCodespaceを作成できます。  
![](https://storage.googleapis.com/zenn-user-upload/cb9d717a7ec3-20230729.png)  
リポジトリを選択すればすぐにCodespaceを作成できます。リポジトリはないけれどとりあえず作りたいという場合は、「blank」と入力すれば、`github/codespaces-blank`というものが選択できるので、それで良いです。残りの選択肢はデフォルトのままでOKです。  
![](https://storage.googleapis.com/zenn-user-upload/041d71b253ed-20230729.png)

## スマホにTermuxをインストールする

1. PlayストアにあるTermuxは古くて更新が止まっているので、まず[F-Droid](https://f-droid.org/ja/)をスマホにインストールします。
2. F-droidからTermuxを検索してインストールします。
3. Termuxを起動して、`pkg upgrade`します。途中に表示される選択肢はデフォルトのままEnterでも問題ありません。

## TermuxからCodespaceに接続する準備

1. Gitをインストールします。  
`pkg install git`
2. [GitHub CLIをインストール](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#android)します。  
`pkg install gh`
3. GitHubにログインします。  
`gh auth login`  
選択肢がいくつか表示されるのでお好きなものを選択してください。私は`GitHub.com` `HTTPS` `Login with a web browser` を選択しました。
4. opensshをインストールします。  
`pkg install openssh`
5. Codespaceにsshするときにエラーになってしまうので、もう一度GitHubにログインします。  
`gh auth refresh -h github.com -s codespace`
6. 接続してみます。  
`gh cs ssh`  
接続先のCodespaceを選択すれば接続完了です！

## Codespaceでコードを書くための環境を整える

デフォルトのままだとLanguageServerが使えなかったりして、コードを書くのがなかなか大変なので、私は[mattnさんのvim-lsp-settings](https://github.com/mattn/vim-lsp-settings)をインストールしました。一応私の手順を書きます。

1. まずは[vim-plug](https://github.com/junegunn/vim-plug)をインストールします。[InstallationのUnix](https://github.com/junegunn/vim-plug#unix)に書いてあるcurlコマンドをコピペするだけです。
2. `cd`だけ打ってEnterしてhomeに移動して、`vim .vimrc`してファイルを新規作成します。ファイルの中身は以下のようにします。

.vimrc

```shell
call plug#begin()
call plug#end()
```

3. [vim-lsp-settingsのInstallation](https://github.com/mattn/vim-lsp-settings#installation)に書いてある内容を、先ほど作った.vimrcに書きます。call plug#begin()とcall plug#end()の間に書きます。私は[Auto-complete](https://github.com/mattn/vim-lsp-settings#asyncompletevim)のPlugも併せて書きました。

.vimrc

```shell
call plug#begin()
Plug 'prabirshrestha/vim-lsp'
Plug 'mattn/vim-lsp-settings'
Plug 'prabirshrestha/asyncomplete.vim'
Plug 'prabirshrestha/asyncomplete-lsp.vim'
call plug#end()
```

4. `vim`を起動して、`:PlugInstall`を実行します。
5. 以上で準備完了です。あとはvimでファイルを開いたときに`:LspInstallServer`するように促されますのでその通りに実行すれば、LanguageServerが動くようになります。