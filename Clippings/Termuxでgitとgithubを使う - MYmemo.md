---
title: "Termuxでgitとgithubを使う - MYmemo"
source: "https://mymemo8.hatenablog.com/entry/2023/10/01/151054"
author:
  - "[[https://cdn-ak.f.st-hatena.com/images/fotolife/M/MYmemo/20220502/20220502111504.jpg]]"
published: 2023-10-01
created: 2024-11-08
description: "Termuxで書いたコードをgithubにpushするまでの一連の流れを勉強がてらメモしたので、記事にもしてみました。Termuxで、と題してはみたものの、Termuxだからといって特別なことはほぼ無い、と思います。 環境条件 私用のスマホPixcel6aにTermuxをインストールしています(Termuxへのgitのインストールは以下のみ。Termuxではsudoも不要です。インストール時のメモはこちら。 mymemo8.hatenablog.com apt install git あとpush先のgithub側の設定もお忘れなく。 Termux特有？エラー回避 これがTermuxのみで発生…"
tags:
  - "clippings"
---
![](https://cdn-ak.f.st-hatena.com/images/fotolife/M/MYmemo/20220502/20220502111504.jpg)

Termuxで書いたコードを[github](https://d.hatena.ne.jp/keyword/github)にpushするまでの一連の流れを勉強がてらメモしたので、記事にもしてみました。Termuxで、と題してはみたものの、Termuxだからといって特別なことはほぼ無い、と思います。

## 環境条件

私用の[スマホ](https://d.hatena.ne.jp/keyword/%A5%B9%A5%DE%A5%DB)Pixcel6aにTermuxをインストールしています(Termuxへのgitのインストールは以下のみ。Termuxではsudoも不要です。インストール時のメモはこちら。

[mymemo8.hatenablog.com](https://mymemo8.hatenablog.com/entry/2022/05/04/235236)

```
apt install git
```

あとpush先の[github](https://d.hatena.ne.jp/keyword/github)側の設定もお忘れなく。

これがTermuxのみで発生する内容なのか分からないのですが、もし以下のようなメッセージで次に進まない場合は....

```
fatal: detected dubious ownership in repository  
```

  
これを試してみてください。 `project`までの部分は[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)のパスなので、もちろんご自身の環境条件下でのパスを指定してください。ここで留意点なのですが、[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)までのパスを例え誤入力してもエラーになりません。コマンドがエラーにならないのに再度引っかかる場合はパスの部分で誤打がないか確認してください。

```
git config --global --add safe.directory /storage/emulated/0/project
```

## 一連の流れを順にやってみる

例えば以下のような作業フォルダがあったとします。「project」というフォルダ内に3つファイルが入っているだけの単純なものです。

```
project
├── main.py  
├── sub.py
└── readme.md
```

まずはprojectフォルダを[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)にするために`git init`を実行する。

```
$ git init  
Initialized empty Git repository in /project/.git/
```

うまく行っていれば、`.git`ができているハズ

```
project
├── main.py  
├── sub.py
├── readme.md
└── .git
```

これでとりあえず[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)ができたことになる。続いて、ブランチも作ってみる。 ブランチ名は別にmainじゃなくても良い。`git branch`だけを実行するとブランチ一覧が表示される。

```
$ git branch -M main
$ git branch  
* main
```

  
ついでに[github](https://d.hatena.ne.jp/keyword/github)へのpushの準備もしておく。username/projectのところは適宜変更ください。

```
$ git remote add origin https://github.com/username/project.git
```

  
上記の中で、`origin`はリモー[トリポジ](https://d.hatena.ne.jp/keyword/%A5%C8%A5%EA%A5%DD%A5%B8)トリ名称で、別になんでもいい。この状態ではまだ何も`add`していないので`git status`を実行すると。以下のようになるハズ。

```
$ git status  

On branch main  

No commits yet    

Untracked files:  
 main.py
 sub.py
 readme.py
```

すべてのファイルが`Untracked files`に位置づけられている。ではまず、readme.mdのみをaddしてみます。

```
$ git add readme.md  
$ git status

On branch main

No commits yet

Changes to be committed:
 new file:   readme.md

Untracked files:
 main.py
 sub.py
```

  
`Changes to be committed`のところに新規ファイルとしてreadme.mdが移動してきているのがわかります。普通はやらないとは思いますが、一旦readmeだけでコミットしてみます。

```
git commit -m "First commit"                 
[main (root-commit) 6c0e5a4] First commit
 1 file changed, 3 insertions(+)
 create mode 100644 readme.md
```

  
この状態でステータスを見てみましょう。

```
$ git status
On branch master

Untracked files:
 main.py
 sub.py
```

  
readme.mdが消えました。コミット済のファイル一覧は`git show`で確認できる。

```
$ git show --name-only
commit d9ab44ca591cc729edbe62c2045cdfa651c04ac5 (HEAD -> main)  
Author: username
 <xxxxxxxxx@yahoo.co.jp>
Date:   Sat Sep 30 12:10:00 2023 +0900

First commit

readme.md
```

  
最後に[github](https://d.hatena.ne.jp/keyword/github)の[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)に押し込んでみます。ユーザー名称とパスワードは事前に確認しておくこと。

```
$ git push -u origin main                    
Username for 'https://github.com': username
Password for 'https://username@github.com':
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 249 bytes | 31.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/username/project.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

Statusを確認するとこんな感じになると思います。[github](https://d.hatena.ne.jp/keyword/github)の[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)とローカルの[リポジトリ](https://d.hatena.ne.jp/keyword/%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA)が`up to date`だそうです。

```
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
 main.py
 sub.py

nothing added to commit but untracked files present (use "git add" to track)
```

  
さすがにコミットされているのがreadmeだけだとあまりにもさみしいので、main.pyもプッシュまで持っていきましよう。まずは`add`します。

```
$ git add main.py
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
 new file:   main.py

Untracked files:
 sub.py
```

  
コミットします。

```
$ git commit -m "2nd commit"
[main dd81e33] upload main
 1 file changed, 39 insertions(+)
 create mode 100644 main.py
```

  
んで、プッシュします。

```
$ git push -u origin main
Username for 'https://github.com': username
Password for 'https://username@github.com':
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 690 bytes | 345.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/username/project.git
   6c0e5a4..dd81e33  main -> main
branch 'main' set up to track 'origin/main'.
```