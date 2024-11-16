---
title: "これだけはできてほしいgitとGitHub - Qiita"
source: "https://qiita.com/tomoswifty/items/be3ff39ab3361a8e9c47?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[tomoswifty]]"
published: 2024-11-16
created: 2024-11-17
description: "これだけはできてほしいGitとGitHubはじめにこれができればチーム開発に参加できます！最低限のGitとGitHubの使い方を学ぶことができます．私が普段使うコマンドをまとめて説明します．…"
tags:
  - "clippings"
---
## これだけはできてほしいGitとGitHub

## はじめに

これができればチーム開発に参加できます！  
最低限のGitとGitHubの使い方を学ぶことができます．私が普段使うコマンドをまとめて説明します．  
基本的に，コピペで実行できます．エラーがあればissueに書いてください．

## 目次

1. クローン
2. git管理
3. sshでのGitHub
4. GitHubへ保存する
5. 変更をGitHubへ反映する
6. 他の人の変更を取り込む
7. ブランチを使って開発する
8. gitignore

## 環境

- Host: MacBook Pro 14 inch
- OS: macOS Sequoia 15.1
- Shell: zsh 5.9

linuxでも同様にできます．Windowsの場合はGit Bashを使ってください．  
Git Bashのインストール方法は次の記事を参考にしてください．  
[WindowsにGit Bashをインストールする](https://qiita.com/suke_masa/items/404f06309bb32ca6c9c5)

## 1\. クローン

### 1-1. リポジトリのクローン

これができれば天才の開発したコードを使うことができます．  
まずは，このリポジトリをクローンしてみましょう．  
以下のコマンドをターミナルに入力してください．

```
git clone https://github.com/tomoswifty/learn-git.git
```

すると，今いる場所に`learn-git`というフォルダが追加されています．

### 1-2. ブランチを指定してクローン

公開されているコードには，ブランチで分けられている場合があり自分の環境に合わせたバージョンのコードになっている必要があります．  
そこで，複数のバージョンを公開する場合によく用いられる方法として複数のブランチが公開されています．

```
git clone -b dev https://github.com/tomoswifty/learn-git.git
```

これで，指定したブランチのリポジトリをクローンできます．先ほどのmainブランチではなく，`dev`ブランチが追加されています．

ブランチの確認は以下のようにすると，存在を確認できます．

```
git branch
### 実行結果
* dev
  main
```

特にこのリポジトリは必要ありませんので，削除して構いません．

## 2\. git管理

### 2-1. ファイルの作成

まずはgit管理したいファイルを作成します．  
`learn-git`というフォルダを作成して，その中に`test.txt`というファイルを作成しましょう．

```
mkdir learn-git
cd learn-git/
touch test.txt
```

`text.txt`に`Hello, World!`と記入しましょう．

#### nanoエディタの使い方

`ctrl + x`→`y`→`Enter`で保存して終了です．

[![nano1](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F038fce26-9ec4-24a7-76cc-c0bb0e35578f.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=be81cd64ca2e056eb26809f4a7dc004e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F038fce26-9ec4-24a7-76cc-c0bb0e35578f.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=be81cd64ca2e056eb26809f4a7dc004e) [![nano2](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F6558f238-3509-e919-bffe-2d14a94acccf.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4002d16bf31002eb4977b29b4df9911b)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F6558f238-3509-e919-bffe-2d14a94acccf.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4002d16bf31002eb4977b29b4df9911b) [![nano3](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fc3781de6-ada2-dfd3-0df4-28cfb813b528.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=10609e87174e7aeff73bee55d6111430)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fc3781de6-ada2-dfd3-0df4-28cfb813b528.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=10609e87174e7aeff73bee55d6111430)

> \[!NOTE\]  
> nanoが使えない場合  
> `nano`が使えない場合はインストールしましょう．
> 
> もしくは`vim`など他のエディタを使ってください．

ここで，ファイルを確認しましょう．

このように表示されているはずです．

次にファイルの中身を変更しましょう．

このように表示されていれば成功です．

### 2-2. git管理に追加

これでgit管理されます．  
以下のように表示されれば成功です．

```
$ git init
Initialized empty Git repository in /Users/{YOUR USERNAME}/learn-git/.git/
```

### 2-3. 変更のステージ

コミット前に必要なおまじないです．

### 2-4. 変更をコミット

```
git commit -m "first commit"
```

これがコミットです．  
変更が保存されます．

## 3\. sshでのGitHub

sshでGitHubにアクセスする方法を紹介します．

### 3-1. sshキーを生成

このとき，`.ssh`がなければ作成します．

ssh鍵を生成します．

作成できたか確認します．

このように,`id_rsa`と`id_rsa.pub`が表示されていれば成功です．

```
$ ls -a
.		id_rsa
..		id_rsa.pub
```

公開鍵を確認します．

この中身をコピーします．

### 3-2. GitHubにsshキーを登録

GitHubにsshキーを登録します．

GitHubにログインし，右上のアイコンから「Settings」を選択します．

[![GitHubでsshキーを登録](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F36cefb40-72f2-f2e7-5b45-636ed572036e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2ac4ed9b279fab1884731cd0e5e2f84a)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F36cefb40-72f2-f2e7-5b45-636ed572036e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2ac4ed9b279fab1884731cd0e5e2f84a)

左のメニューから「SSH and GPG keys」を選択します．

[![GitHubでsshキーを登録](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F9a8cf752-515d-7b16-3ffc-0cee314d408d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=99492ab79c1aa60f959092f1491a1a47)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F9a8cf752-515d-7b16-3ffc-0cee314d408d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=99492ab79c1aa60f959092f1491a1a47)

「New SSH key」をクリックします．

[![GitHubでsshキーを登録](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F7cf66a7f-b0c9-1274-71b1-af31bf2422c0.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4e67c90e7c8d9862d7258509a7b8f292)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F7cf66a7f-b0c9-1274-71b1-af31bf2422c0.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4e67c90e7c8d9862d7258509a7b8f292)

「Title」に任意の名前を入力し，「Key」に先ほどコピーした公開鍵を貼り付けます．

「Add SSH key」をクリックして登録完了です．

[![GitHubでsshキーを登録](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fc7fc8ce4-3505-4e8b-5820-0ab6057a99b2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ce3d7ce73080ede6abe4143733bb66c2)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fc7fc8ce4-3505-4e8b-5820-0ab6057a99b2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ce3d7ce73080ede6abe4143733bb66c2)

これで，sshキーの登録は完了です．

## 4\. GitHubへ保存する

### 4-1. GitHubにリポジトリを作成

GitHubにリポジトリを作成します．  
ブラウザからGitHubにアクセスしてサインインします．  
この画像のように，緑色の「Create repository」ボタンをクリックしてリポジトリを作成します．

[![GitHubでリポジトリを作成](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F1eba1747-9a6b-0465-3e58-6a3e93147156.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f6c6404a12b84f77f4535db2d8bc8e81)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F1eba1747-9a6b-0465-3e58-6a3e93147156.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f6c6404a12b84f77f4535db2d8bc8e81)

リポジトリ名は「learn-git」とします．  
「Public」を選択し，「Add a README file」のチェックは外します．

[![GitHubでリポジトリを作成](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F934917c8-885d-8c4a-1450-e9f722f6f9d3.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5453019bee4b858362816a3294c39e2b)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F934917c8-885d-8c4a-1450-e9f722f6f9d3.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5453019bee4b858362816a3294c39e2b)

作成したら，以下のような画面が表示されます．

[![GitHubでリポジトリを作成](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F61ce85b7-a832-8fb7-d77b-38c426fd29b8.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f275e9801d2c5d5865b38e6cc9af48b2)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F61ce85b7-a832-8fb7-d77b-38c426fd29b8.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f275e9801d2c5d5865b38e6cc9af48b2)

ここのQuick setupのSSHをクリックします．  
以下のような画面が表示されます．  
前章で作成したsshキーを使ってこのリポジトリにアクセスします．

[![GitHubでリポジトリを作成](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F17c17374-cabe-d3d0-120c-6f192ca5f7aa.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=68a823f04380e770214e2c2cf35231d1)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F17c17374-cabe-d3d0-120c-6f192ca5f7aa.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=68a823f04380e770214e2c2cf35231d1)

この画像にあるコマンドを次章で実行します．

### 4-2. remoteにリポジトリを追加

ターミナルへ戻ります．

commitまでは完了していますので，次はリモートリポジトリを追加します．  
その前に，おまじないです．

これは，ブランチ名をmainに変更するコマンドで，昔はmasterという名前でした．転換期に必要なコマンドでしたが最新版のgitではデフォルトでmainになっているので不要ですが，念のため実行しておきます．

そして，リモートリポジトリを追加します．

```
git remote add origin git@github.com:YOUR_GITHUB_USERNAME/learn-git.git
```

ここで，`git@github.com:YOUR_GITHUB_USERNAME/learn-git.git`の部分は，先ほどGitHubで作成した自身のリポジトリのURLに変更してください．

### 4-3. GitHubへpush

これでGitHubへpushできました．

```
$ git push -u origin main                                      
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 228 bytes | 228.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:YOUR_GITHUB_USERNAM/learn-git.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

GitHubのページをリロードして，リポジトリが更新されていることを確認してみましょう．

[![GitHubでリポジトリを作成](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F59d6da84-afe1-4381-bf16-1b373b96172a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=65abd403a3a3023e0f57db3f0d4885dd)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F59d6da84-afe1-4381-bf16-1b373b96172a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=65abd403a3a3023e0f57db3f0d4885dd)

## 5\. 変更をGitHubへ反映する

### 5-1. ファイルを変更する

### 5-2. ローカルでコミットする

```
git add -u
git commit -m "add a comment"
```

### 5-3. GitHubへpush

4章と同様に，GitHubのページをリロードして，リポジトリが更新されていることを確認してみましょう．  
変更が反映されていれば成功です．  
コミットメッセージも変更されているはずです．

## 6\. 他の人の変更を取り込む

### 6-1. ファイルの変更

GitHubのページで変更を加えます．  
GitHubのページで「Add a README」をクリックします．  
[![github_commit1.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fa4ed0b50-2771-d76d-5a87-d428ba24879d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=365cec7d923804758af655564ea72b66)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2Fa4ed0b50-2771-d76d-5a87-d428ba24879d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=365cec7d923804758af655564ea72b66)

タイトルを記入して「Commit changes」をクリックします  
[![GitHubで変更を加える](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F02bef14a-c55f-8a7c-845e-104d9162d4b9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1770ec872dbdefa3b836991ee83ee7af)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F02bef14a-c55f-8a7c-845e-104d9162d4b9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1770ec872dbdefa3b836991ee83ee7af)

コミットメッセージを確認して，「Commit」をクリックします．

[![github_commit3](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F9fae4c3a-922b-e313-a776-734217fe3db9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=830eda7883683c08f848df748cd9e592)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F9fae4c3a-922b-e313-a776-734217fe3db9.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=830eda7883683c08f848df748cd9e592)

これで，GitHub上で変更が加えられました．  
[![GitHubで変更を加える](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F3879168e-8a44-846c-6f7e-23ee1f229640.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=074794dc8737bc99e546beccd831895a)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3374774%2F3879168e-8a44-846c-6f7e-23ee1f229640.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=074794dc8737bc99e546beccd831895a)

### 6-2. ローカルへpull

となって変更を取り込むことができました．

## 7\. ブランチを使って開発する

### 7-1. ブランチを作成する

### 7-2. ブランチをpushする

## 8\. gitignore

いらないファイルをgit管理から除外することができます．

git管理から外すファイルを作成してみます．

macOSでは`.DS_Store`がたびたび作成されます．  
わざわざpushする必要はないので，`.gitignore`に追加しましょう．

これでpushしてみましょう．  
すると，リモートリポジトリにはdummyfile.txtが反映されていないはずです．

## おわりに

これでひととおりGitとGitHubを使うことができるようになったと思います．

## 参考文献

- [GitHubでssh接続する手順~公開鍵・秘密鍵の生成から~](https://qiita.com/shizuma/items/2b2f873a0034839e47ce)
- [\[Git\]これだけ押さえる！gitconfigの基本](https://qiita.com/C_HERO/items/c35e679f0b03a5f06469)