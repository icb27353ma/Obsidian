---
title: "Emacsの最強GitクライアントMagitの使い方"
source: "https://joppot.info/posts/f2721fb2-0942-4c4e-90e2-0dbdbb329bce"
author:
published:
created: 2024-11-05
description:
tags:
  - "clippings"
---
magitはEmacsのgitクライアントのデファクトスタンダードです。CUIインターフェースにもかかわらず、GUIのgitクライアントに負けないすごい機能を持ち合わせています。

magitの使い方はそれこそ膨大すぎて、全て説明しようとすると１冊本が書けてしまいます。

英語ですが、emacsdocsにmagit専用のドキュメントページがあるので、ここで紹介する以上の情報が欲しい方はそちらを参考にしてください。

こちらが完成したmagitの設定コードです。

```lisp
(use-package magit
  :ensure t
  :bind (("C-x g" . magit-status)
         ("C-x M-g" . magit-dispatch-popup))
  :config
  (defun mu-magit-kill-buffers ()
    "Restore window configuration and kill all Magit buffers."
    (interactive)
    (let ((buffers (magit-mode-get-buffers)))
      (magit-restore-window-configuration)
      (mapc #'kill-buffer buffers)))
  (bind-key "q" #'mu-magit-kill-buffers magit-status-mode-map))
```

## リポジトリの初期化

説明ように適当なリポジトリを作成して、githubにも登録してみます。

```undefined
mkdir html
cd html
touch index.html
git init
```

`index.html`にhtml 5の側だけ用意します。

```lisp
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8"/>
    <title>Document</title>
  </head>
  <body></body>
</html>
```

## githubリポジトリの作成

githubにテスト用のプライベートリポジトリを作ります。 リポジトリ名はなんでも良いので`git-test-repo`とかにします。

Githubに表示されている、こんな感じのリモートの名前は後で使うので、コピっておいてください。

```undefined
git@github.com:yourname/git-test-repo.git
```

## magitの使い方

magitはデフォルトでキーバインドされているコマンドは2つしかありません。 `"C-x g" magit-status)`と`("C-x M-g" magit-dispatch-popup)`です。 magitは他のemacsパッケージとは違って、どちらかというとEmacsというOSを使ってgitのクライアントを動かしているイメージです。magitを使ったgitの操作もEmacsで対話的にやるよりかはMagitクライアントの中で操作します。

magitを起動するコマンドは`"C-x g" magit-status)`です。最初はそれを実行してみましょう。 とてもシンプルなウィンドウが表示されます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/e6b41a58-1c6b-4102-b0f3-2dc4f8944afd/magit-status.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=57b5bbbb70ac1d18fba0acc94aece38a03a41760e8edc8d41bd8f34d20801e74&X-Amz-SignedHeaders=host&x-id=GetObject)

このバッファでは、magitのあらゆるショートカットキーが機能します。 どのコマンドがどれに紐づいているかを暗記するのは大変なので、１つだけ覚えておきましょう。 `h`をタイプするとmagitのヘルプが開きます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/4843472f-60f1-4e87-bed6-be358f7d7c2a/help.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=a8519ce58be800c0ec98388ae4b2fd259e8c0d6f4c55e78f68a3b7e8088ff752&X-Amz-SignedHeaders=host&x-id=GetObject)

青く強調表示されたキーをタイプすると、gitの目的の操作へ移動していきます。

## ステージへ上げる、下ろす

最初に作成した、`index.html`をステージに上げます。 magitのバッファで、カーソルを`index.html`に合わせて、`s`とタイプするとステージされます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/2e678846-f514-4d9f-ad76-bf2d1683119e/stage.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=d3197cfd773437d3ecfb6955dc536e8d3428736dbb457324c813a556b3919141&X-Amz-SignedHeaders=host&x-id=GetObject)

逆に、ステージから下ろす場合は、同じく`index.html`にカーソルを当てて、`u`とタイプします。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/889d9efb-e50f-4640-b390-c02140683d60/unstage.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=50b4ef92c48d7222289cbdda8bb99d8bbf5a354d13c364bd67632f47ef202a74&X-Amz-SignedHeaders=host&x-id=GetObject)

## コミットする

ステージに上げた差分をコミットします。 `c`とタイプするとこのようなコミット操作へのウィンドウが表示されます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/d82d34e0-291f-485b-81f9-85b79206561e/tocommit.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=0caa4a7dddc3693acc6e09ba45aecb6c7b157993cf5dd8d216e4334c149ce91a&X-Amz-SignedHeaders=host&x-id=GetObject)

上の画像を見ると、`c`がコミットへ進むキーになることがわかります。そのまま`c`をタイプすると、コミットログのバッファと差分が表示されます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/949d2e87-9294-42ad-ba45-0931e39222a2/firstcommit.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=62e2b06e8c4b9113d437121c196ab64082f901fe0adc332eb37a4ac1d84dbb82&X-Amz-SignedHeaders=host&x-id=GetObject)

コミットログバッファに`first commit`と入力し、これがコミットメッセージになります。

コミットを確定するには`C-c C-c`を入力します。 magitを利用したコミットができました。

## リモートを追加

Githubのリモートを追加します。 `"C-x g" magit-status)`でmagitバッファを開いて、とりあえず`h`でヘルプを見ます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/4843472f-60f1-4e87-bed6-be358f7d7c2a/help.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=a8519ce58be800c0ec98388ae4b2fd259e8c0d6f4c55e78f68a3b7e8088ff752&X-Amz-SignedHeaders=host&x-id=GetObject)

リモート関連は`M`とあるので、それをタイプします。 リモートを加えるは`Add`なので`a`をタイプします。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/09175e0d-d18f-418c-9fd9-b5d64a3801e4/add.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=711f8f60fb27caf898d5f6cb8f38a16be5ef475877bec7fdf8440d0eb85d5a9a&X-Amz-SignedHeaders=host&x-id=GetObject)

エコーエリアに`Remote name:`が表示されるので、`origin`とタイプしてエンターを押します。 `Remote url:`と出るので、上の方でコピーした`git@github.com:yourname/git-test-repo.git`みたいなものを貼り付けてエンターを押します。詳しくは自分で作成したGithubのリポジトリページをみてください。 `Set remote.pushDefault' to "origin"? (y or n)`はデフォルトのプッシュ先として設定して良いかを聞かれるので、`y`をタイプする。

これでリモート設定が完了しました。

## Gitプッシュする

`"C-x g" magit-status)`でmagitバッファを開いて、`h`でヘルプを見ます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/4843472f-60f1-4e87-bed6-be358f7d7c2a/help.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=a8519ce58be800c0ec98388ae4b2fd259e8c0d6f4c55e78f68a3b7e8088ff752&X-Amz-SignedHeaders=host&x-id=GetObject)

Push関連は`P`なのでそれをタイプします。今の設定では`origin/main`がリモート先です。そこに向けてプッシュしたいので`p`をタイプします。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/af3b2ec5-2fbc-4987-95b4-16eb4aa0db5a/push.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=849d5cf3f3079ced11c6fa11dc1aca8fbc20773abefdba9af936772304647861&X-Amz-SignedHeaders=host&x-id=GetObject)

エコーエリアに`Git finished`が表示されればプッシュが成功しています。

## Gitログを表示

`"C-x g" magit-status)`でmagitバッファを開いて、`h`でヘルプを見ます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/4843472f-60f1-4e87-bed6-be358f7d7c2a/help.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=a8519ce58be800c0ec98388ae4b2fd259e8c0d6f4c55e78f68a3b7e8088ff752&X-Amz-SignedHeaders=host&x-id=GetObject)

ログ表示は`l`でそれをタイプします。次のウィンドウではいくつかのログの表示オプションが提示されます。一番無難なのはローカルのブランチも、リモートのブランチも表示する`b`です。リモートの表示が不必要な場合は`l`がおすすめです。ここではリモートもチェックしたいので`b`をタイプします。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/d878a0e5-3369-492a-8fb7-d6fb8420cd63/log.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=23b03c60f69e47ff5fba45a5ea86aefeab1b047a3167ca5ff2e665752a029d43&X-Amz-SignedHeaders=host&x-id=GetObject)

このようにログが表示されます。

![article image](https://prod-files-secure.s3.us-west-2.amazonaws.com/a3d79190-572a-4604-a045-8b27c534a5b2/49aa2c17-ddf3-4bf5-add7-9fee2c27dcd6/tree.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45GO43JXI4%2F20241105%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20241105T005256Z&X-Amz-Expires=3600&X-Amz-Signature=681694a2569eca3e1d16a8d78e56bece90204d86f716e78a60602f7a9e72de92&X-Amz-SignedHeaders=host&x-id=GetObject)

## magitの終了

Gitの操作が終わったら、magitアプリケーションを終了します。 magitはコミット操作が終わってもデフォルトでは３つのバッファを放置したままにします。

```undefined
magit-process: html. %*-  171      Magit Process
magit-diff: html     %%-  169      Magit Diff
magit: html          %%-  233      Magit
```

そのままだと邪魔なので、`mu-magit-kill-buffers`でmagitを終了時に削除しています。 このコードはこちらの方を参考にさせてもらいました。

```lisp
(defun mu-magit-kill-buffers ()
    "Restore window configuration and kill all Magit buffers."
    (interactive)
    (let ((buffers (magit-mode-get-buffers)))
      (magit-restore-window-configuration)
      (mapc #'kill-buffer buffers)))
  (bind-key "q" #'mu-magit-kill-buffers magit-status-mode-map)
```

magitのバッファで`q`をタイプし終了します。

## その他の操作とまとめ

magitはここで紹介したもの以外でも、amend、rebase、pull、force pushなどにももちろん対応しています。 どうやって操作し良いかわからなくもてヘルプを開いて、そこから目的の操作までキーをタイプして挑戦してみてください。