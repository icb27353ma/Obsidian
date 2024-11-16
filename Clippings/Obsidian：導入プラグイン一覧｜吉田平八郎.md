---
title: "Obsidian：導入プラグイン一覧｜吉田平八郎"
source: "https://note.com/yoshida_he8ro/n/nfffe1c85b467"
author:
  - "[[吉田平八郎]]"
published: 2023-10-01
created: 2024-11-11
description: "はじめに  メモ／ノート管理アプリ「Obsidian」の何が魅力かといえば、一番はプラグインの豊富さかもしれない。 デフォルト（バニラ）の状態でも十分使いでのあるアプリだが、プラグインをいくつか入れてしまえば、サラの状態に戻すのに苦痛を伴うだろう(笑)  Minecraft や Cities:Skylines でもMOD沼にハマった私だが、Obsidianにおいても案の定プラグイン探しに日々明け暮れた。  [Obsidian] コミュニティプラグイン全集 改訂版Obsidianには標準で用意されたコアプラグインとコミュニティプラグイン（いわゆるサードパーティプラグイン）が存"
tags:
  - "clippings"
---
## はじめに

**メモ／ノート管理アプリ「Obsidian」**の何が魅力かといえば、一番はプラグインの豊富さかもしれない。  
デフォルト（バニラ）の状態でも十分使いでのあるアプリだが、プラグインをいくつか入れてしまえば、サラの状態に戻すのに苦痛を伴うだろう(笑)

Minecraft や Cities:Skylines でもMOD沼にハマった私だが、Obsidianにおいても案の定プラグイン探しに日々明け暮れた。

数々の有益な情報を載せているWebの中でも、特にプラグイン選びの指標となった上記サイトに敬意を表しつつ、現在の私の環境下にあるプラグインを一覧してみる。

★は個人的なオススメの指標だが、私が使いこなせてないものは★無しの場合も。各分類内の順番はアルファベット順。  
説明や使用方法が明後日の方向に間違ってる場合は、Twiitterでやさしくご指摘意くだされ。

**【注意】**Obsidianを初めたばかりという方にとっては、このプラグイン紹介記事を一瞥した段階で「こんな数のプラグイン紹介をみて判断できるか！ふざけんな！」って思うかもしれません。  
でも使い始めて半年経った頃に振り返ってみてください。たぶんその時にはあなたもこれぐらいのプラグインを導入してますから（笑）

## 目次

## 記事投稿後の動き（'24/10/29）

前回更新分は各項目に再配置しました。

### Lazy Plugin Loader　★

[https://github.com/alangrainger/obsidian-lazy-plugins](https://github.com/alangrainger/obsidian-lazy-plugins)

- '24/10/28 install
- プラグインの起動順位を設定できるプラグイン。
- 結果としてObsidian起動時の速さを調整できる。
- 導入している全プラグインを個別に「無効・起動時反映・少し遅れて反映・だいぶ遅れて反映」が設定可能。
- あまりやりすぎるとレイアウト崩れたりするので、様子見しながら変更。

### Multiple Notes Outline　★

[https://github.com/iiz00/obsidian-multiple-notes-outline](https://github.com/iiz00/obsidian-multiple-notes-outline)

- '24/9/10 install
- サブパネルにノートのリンク、バックリンクのアウトラインなどを表示する。当該ノートに関連するノートを把握しやすい。
- 表示スペースが大きい 2-hop link の代わりとしてお試し中。
- 表示項目や表示順番がカスタマイズできるとありがたいのだけど。

### Book Search Plugin

[https://github.com/anpigon/obsidian-book-search-plugin](https://github.com/anpigon/obsidian-book-search-plugin)

- '24/7/29 install
- 書籍名から書籍情報をネットから拾い上げ、テンプレートに反映できる。
- 気が向いたので書籍の感想をノートに残そうと思い立った。
- とりあえず書籍テンプレートを用意しておけば、あとで別途Dataview一覧などの活用もできるだろう。

## デイリーノート

### Calendar　★★★

[https://github.com/liamcain/obsidian-calendar-plugin](https://github.com/liamcain/obsidian-calendar-plugin)

- もうバニラ搭載でも良いんジャマイカと思うカレンダー。
- 日付からその日のデイリーノート作成／未作成、文章量が視覚的に把握できるの良き。
- これとTemplaterがあればデイリーノートの最低限が揃うよね。

### Periodic Notes

[https://github.com/liamcain/obsidian-periodic-notes](https://github.com/liamcain/obsidian-periodic-notes)

- 日次・週次・月次・四半期次・年次毎のノートを管理できるようになるプラグイン。
- ~~けっきょく私は日次レベルで持て余してるので、ほぼ意味を成してない orz~~
- 自分なりの週次と月次テンプレートを使いだしたので、一応現役。  
ただこのプラグインはカレンダー日曜始まりを優遇してるかも？

## ノート：外部URL処理

### Auto Card Link　★★

[https://github.com/nekoshita/obsidian-auto-card-link](https://github.com/nekoshita/obsidian-auto-card-link)

- ブログで言うところのブログカードの形でURLリンクする。
- サムネイルとタイトル、見出し部分、ドメインを一瞥できて見た目も良い。
- 右クリックサブメニューに追加すると便利。

### Auto Link Title　★★★

[https://github.com/zolrath/obsidian-auto-link-title](https://github.com/zolrath/obsidian-auto-link-title)

- URL先のタイトルを取得して、タイトル付きリンクする。
- 上記の場所を取るCard Linkと使い分けしてる。
- 右クリックサブメニューに追加すると便利。

### Consistent Attachments and Links

[https://github.com/dy-sh/obsidian-consistent-attachments-and-links](https://github.com/dy-sh/obsidian-consistent-attachments-and-links)

- Obsidian内のリンクをマークダウン形式の相対パスに変換し、外部アプリとの互換性を高める、らしい。
- バニラ機能の代わりにファイル移動の内部リンク自動更新等を行う。
- なぜ入れてるのかイマイチ覚えてないのだが、特に問題なく動いてるのでいいか。

### Local Images　★★

[https://github.com/aleksey-rezvov/obsidian-local-images](https://github.com/aleksey-rezvov/obsidian-local-images)

- ノート内の外部リンク画像をすべてローカル保存する。
- ReadItLater などでWebサイトをノート化した際に外部リンク画像のままだったりするので、続けて実行することが多いコマンド。

### ReadItLater　★★

[https://github.com/DominikPieper/obsidian-ReadItLater](https://github.com/DominikPieper/obsidian-ReadItLater)

- ブラウザプラグインで言うところのWebClipper。クリップボードに格納されてるURL先のWebページをノートに変換して保存する強つよプラグイン。

## ノート：データ処理

### Dataview　★★

[https://github.com/blacksmithgu/obsidian-dataview](https://github.com/blacksmithgu/obsidian-dataview)

- Obsidianを照会可能なデータベースとして扱うプラグイン。
- 要は条件に適合したノートを一覧表示させたり、要素でソートできる。
- ノートに埋め込まれた要素（旧：フロントマター、現：プロパティ）の扱いを得意としてるっぽい。
- 私は「特定タイトルやタグを含むノートを一覧させてMOC（索引）化」「特定フォルダ内のノート一覧」「今日作ったノート一覧」といった利用がせいぜい。
- Dataviewで内部リンク一覧表示（検索結果表示）させても、そのDataview記述を書いたノートとリンク先のノートは実際にはリンクされてないので、グラフビューのリンクには反映されないのが何気に落とし穴。

### Tasks　★★★

[https://github.com/obsidian-tasks-group/obsidian-tasks](https://github.com/obsidian-tasks-group/obsidian-tasks)

- 全ノートに渡ってタスク（チェックボックス）を検索し一覧表示するプラグイン。
- 完了／未完了、特定日付より前後、タグ、キーワードに合致するものなど条件でふるい分けできる。
- 私はこれでネタ帳・タスク・欲しい物リストを管理してて重宝してます。

## ノート：閲覧補助

### Creases　★

[https://github.com/liamcain/obsidian-creases](https://github.com/liamcain/obsidian-creases)

- ノート内の見出しレベル(H1～H6)をまとめて折り畳んだり、開いたりできる。
- 長くなったノートをアウトラインと使い分けで編集・閲覧しやすくする。

### Embedded Code Title

[https://github.com/tadashi-aikawa/obsidian-embedded-code-title](https://github.com/tadashi-aikawa/obsidian-embedded-code-title)

- '24/4/6 install
- コードブロックにタイトルを埋め込めるプラグイン
- 閲覧モードのときに表示される。編集モードではない。

### Furigana

[https://github.com/uonr/obsidian-furigana](https://github.com/uonr/obsidian-furigana)

- '24/2/22 install
- 漢字や外国語などにルビをふることができる。
- 地味に重宝する人は重宝しそう。

### Limelight

[https://github.com/smikula/obsidian-limelight](https://github.com/smikula/obsidian-limelight)

- '23/3/18 install
- アクティブなパネル以外を暗くして、視認性を高める補助系プラグイン。

### Mind Map

[https://github.com/lynchjames/obsidian-mind-map](https://github.com/lynchjames/obsidian-mind-map)

- '24/1/4 install
- きれいなマインドマップを簡単に作れるプラグイン。
- といいつつ、マインドマップをあまり使わない。

### Old Note Admonitor

[https://github.com/tadashi-aikawa/obsidian-old-note-admonitor](https://github.com/tadashi-aikawa/obsidian-old-note-admonitor)

- 例えば365日など、設定した日付以上に更新されてないノートを開くと、注意を促す表示がでる。

### Quiet Outline　★★

[https://github.com/guopenghui/obsidian-quiet-outline](https://github.com/guopenghui/obsidian-quiet-outline)

- 見出し(H1～H6)の階層構造をアウトラインとしてサブメニューに表示し、かつ見出しレベルを選んでワンクリックで開け閉じを簡単にできる。
- 長いノートを見渡すのに便利な気がする。

### Reading Time

[https://github.com/avr/obsidian-reading-time](https://github.com/avr/obsidian-reading-time)

- ブログでよくある「この記事は◯分で読めます」をノートのステータス欄で確認できる。

## ノート：編集補助

### Date Inserter　★★

[https://github.com/namikaze-40p/obsidian-date-inserter](https://github.com/namikaze-40p/obsidian-date-inserter)

- '24/2/25 install
- ホットキーを押すと、カレンダーを呼び出して、選択した日付をオプションで設定したフォーマットにて出力する。
- GUIから選んで表示できる点がとても便利。

### Fleeting Notes Sync　★★

[https://github.com/fleetingnotes/fleeting-notes-obsidian](https://github.com/fleetingnotes/fleeting-notes-obsidian)

- '23/10/4 in
- スマホアプリ「Fleeting Notes」のObsdian側同期プラグイン。
- 想像していたような同期ではなく、帯に短し襷に長し。でもありがたい。
- 私はスマホから一時的なメモを放り込む、に特化した使い方をしている。

### Linter

[https://github.com/platers/obsidian-linter](https://github.com/platers/obsidian-linter)

- ノートのフォーマットやスタイルを色々できるプラグイン。
- 色々出来すぎて全く把握してない。俺たちは気分でプラグインを入れてる。
- たぶん新しいノートを保存した際に自動的にプロパティの一部を追加するために利用してる模様（失念）。

### Outliner

[https://github.com/vslinko/obsidian-outliner](https://github.com/vslinko/obsidian-outliner)

- 構造化されたリストを自由に入れ替えられるようになる。
- 使うときは使いそうだけど、いつもでは無いなぁ。

### Quick Preview

[https://github.com/RyotaUshio/obsidian-quick-preview](https://github.com/RyotaUshio/obsidian-quick-preview)

- '23/12/12 install
- マークダウンリンクを貼る際に選択肢のノート名から選ぶわけですが、「これ、本当にリンク貼りたいと思ってるノートかな？」とためらうこともありますよね。
- このプラグインを導入して、リンクの選択肢が出たところで Alt(Windows)／Option(Mac)を押し続けると、ノートのプレビュー画面を表示してくれます。

### Rendered Block Link Suggestions　★

[https://github.com/RyotaUshio/obsidian-rendered-block-link-suggestions](https://github.com/RyotaUshio/obsidian-rendered-block-link-suggestions)

- '23/12/12 install
- Obsidianならではといえるリンクで最も使いづらいブロックリンクを使いやすくしてくれる。
- 通常、リンク先の文章ブロックにこれまた付けづらいIDをつけてから、リンク元からリンクを貼るという仕組みなのだが、このプラグインによってリンクを貼るタイミングでノート先のブロックを選べば勝手にIDをつけてくれるという神仕様。

### Select current line

[https://github.com/gokulk16/select-current-line-plugin](https://github.com/gokulk16/select-current-line-plugin)

- '23/11/16 in
- ESCキーを押すと、マークダウン記号を含む現在行を選択できるプラグイン。
- ショートカットキーの変更は可能だが、確かにESCぐらいでいいかも。

### Templater　★★★

[https://github.com/SilentVoid13/Templater](https://github.com/SilentVoid13/Templater)

- 用途に応じたテンプレートを作成できる。
- テンプレート内に変数や関数結果、データビュータグ等も含められる。
- ほぼ必須といっても良いのではなかろうか。

### Various Complements　★★★★

[https://github.com/tadashi-aikawa/obsidian-various-complements-plugin#auto-complete-from-custom-dictionaries](https://github.com/tadashi-aikawa/obsidian-various-complements-plugin#auto-complete-from-custom-dictionaries)

- '23/12/17 install
- 日本語入力(IME)のように、入力しながらその単語あるいは英語綴り、リンクノート先といったものを候補として表示する神プラグイン。満点★３つのところ★４つ！
- 最初はそんな便利な動きはきっと重いに違いないと試しもしないで判断したのを、ものすごく後悔しました。まずはお試しを。

## 外観・装飾

### Highlightr　★

[https://github.com/chetachiezikeuzor/Highlightr-Plugin](https://github.com/chetachiezikeuzor/Highlightr-Plugin)

- ノートに色とりどりなハイライトを追加できる。
- あればあったで便利かな。

### Iconize　★★★

[https://github.com/FlorianWoelki/obsidian-iconize](https://github.com/FlorianWoelki/obsidian-iconize)

- フォルダーにアイコンを追加できる。視認性大事。

### Minimal Theme Settings

[https://github.com/kepano/obsidian-minimal-settings](https://github.com/kepano/obsidian-minimal-settings)

- 外観テーマで「Minimal」をインストールしているので、そのセッティング用プラグイン。
- 外観テーマは好きずきなので好みのテーマを見つけよう。

### Style Settings

[https://github.com/mgmeyers/obsidian-style-settings](https://github.com/mgmeyers/obsidian-style-settings)

- 導入しているスニペット、テーマ、プラグインの各CSSをまとめて表示し、編集をしやすくするプラグイン。
- 逆に多すぎて、どこもいじらないままメニューを閉じることしばしば。

## タグ関連

### Colored Tags　★★★

[https://github.com/pfrankov/obsidian-colored-tags](https://github.com/pfrankov/obsidian-colored-tags)

- タグを名称ごとに自動色分けする。視認性が全然違うのでオススメ。
- カラーバリエーションも渋い選択が揃ってる。

### TagFolder　★

[https://github.com/vrtmrz/obsidian-tagfolder](https://github.com/vrtmrz/obsidian-tagfolder)

- '23/12/5 in
- ノート内に含まれるタグを元に、Valut全体からタグをフォルダ扱いにした参照ができるようになる。
- 以前は重たいという話だったが、アップグレードで解消されてる模様。
- 自分の環境はタグを意識してなかったノート側の問題で、まだ本領発揮されていない。

### Tag Wrangler　★

[https://github.com/pjeby/tag-wrangler](https://github.com/pjeby/tag-wrangler)

- '24/3/4 re-install
- タグ系の他のプラグインがあるのでいらないかな？と思って一度アンインストールしたけど、タグをリネームしたりマージできる機能は超便利。

## 画像関連

### Clearing Unused Images　★★

[https://github.com/ozntel/oz-clear-unused-images-obsidian](https://github.com/ozntel/oz-clear-unused-images-obsidian)

- 使っていない画像をObsidianフォルダ内から削除する。
- 案外ノート削除したり、画像差し替えたりで未リンク画像は増えるもの。

### Image Converter　★★★

[https://github.com/xryul/obsidian-image-converter](https://github.com/xryul/obsidian-image-converter)

- '23/12/7 in
- Paste image Png to Jpegの後継。
- ドロップ／ペーストした画像を、WebP、JPG、PNGのいずれかに自動的に変換してくれる。画像のファイルサイズ削減やサイズ変更も。
- 何かと面倒なWebPを変換してくれるので非常に助かる。
- ただ自動ファイル名変換は「ファイル名-タイムスタンプ」式だったため、プラグインのmain.jsを少し変更した。日本語ファイル名にしたくないので。

プラグインフォルダのmain.jsを「NewName」で検索。J.basenameがファイル名。"Pasted-image-タイムスタンプ.拡張子"となるよう変更した。

### Image Layouts　★★★

[https://github.com/vertis/obsidian-image-layouts](https://github.com/vertis/obsidian-image-layouts)

- '23/10/28 in
- ようやく見つけた、複数画像のレイアウトを簡単にするプラグイン！  
そう、こういうのでいいんだよ、こういうので。
- !\[\](local-imagefile)式に対応してなかったが、Git配布先のIssuesにスクリプト変更例が掲載されてて助かった。

### Image Toolkit　★★★

[https://github.com/sissilab/obsidian-image-toolkit](https://github.com/sissilab/obsidian-image-toolkit)

- ノート内の画像をプレビュー表示させて拡大・縮小やノート内の画像を順に表示できるなど、画像操作系プラグイン。
- 単純に拡大縮小できるだけも便利。

## 機能追加

### Advanced URI

[https://github.com/Vinzent03/obsidian-advanced-uri](https://github.com/Vinzent03/obsidian-advanced-uri)

- URIを開くだけで設定された動作を行えるプラグイン。
- 前々から導入はしていたが、上手く使いこなせていない。

### Beautitab　★

[https://github.com/andrewmcgivery/obsidian-beautitab](https://github.com/andrewmcgivery/obsidian-beautitab)

- '24/3/3 install
- 新しいタブを開いた時に表示される画面に、見やすい時計、きれいな壁紙、検索フォーム、ランダム引用文を表示する。
- デフォルト運用で十分満足だけど、壁紙と引用文をカスタマイズ可能なので、沼る人は沼りそう。

### Commander　★★

[https://github.com/phibr0/obsidian-commander](https://github.com/phibr0/obsidian-commander)

- '23/11/9 in
- 画面の色んなところにボタン式の新しいコマンドボタンを追加したり、あるいは既存のコマンドを削除／非表示／並び替えできる。
- ノートタブの右上に「前・後ファイルに移動する」「このノートを別の場所に移動する」ボタンをつけたりしてます。

### Hover Editor

[https://github.com/nothingislost/obsidian-hover-editor](https://github.com/nothingislost/obsidian-hover-editor)

- 内部リンクの簡易表示（ページプレビュー）を強化する。
- 簡易表示を閉じずにそのままホバー表示させ続けたり、直接編集可能に。

### Projects

[https://github.com/marcusolsson/obsidian-projects](https://github.com/marcusolsson/obsidian-projects)

- '24/1/25 install
- プロジェクト管理したいノート群をテーブル一覧表示、カレンダー日付管理、サムネタイル一覧といった見やすい形にまとめる。
- 書籍管理といった使い方もでき、アイデア次第で利用シーンは広がりそう。

### QuickAdd　★★★★

[https://github.com/chhoumann/quickadd](https://github.com/chhoumann/quickadd)

- 私がもっとも有用と感じてるので唯一の★４つです！
- ただし機能はけっこう奥深い。テンプレート拡張、どこからでも入力プロンプトを呼び出してノート追記できるキャプチャー、複数のコマンドかJavaScriptを実行するマクロの3つを適宜設定できる。
- 具体例はいつか記事を書いてみたいが、「別のノート開いてるときに思いついたメモやタスクをそれぞれ専用ノートあるいデイリーノートに記述」といったキャプチャー運用が便利すぎる。

### Slash Commander　★★

[https://github.com/alephpiece/obsidian-slash-commander](https://github.com/alephpiece/obsidian-slash-commander)

- '24/4/5 install
- 「/」スラッシュから呼び出すコマンドの選択肢が表示され、含まれる文字から絞り込みが可能。
- 選択肢をカスタマイズできるため、自分好みに頻度の高いコマンドを追加できるのは便利。
- コマンドをまとめるグループ機能が今後実装予定の模様。

### Vertical Tabs View　★

[https://github.com/hdykokd/obsidian-vertical-tabs-view](https://github.com/hdykokd/obsidian-vertical-tabs-view)

- '24/3/3 install
- 開いているノート一覧をサブパネルに表示する。
- ノート沢山開いてしまう症候群の人は重宝しそう。

## 検索・置換・辞書索引

### Another Quick Switcher　★★

[https://github.com/tadashi-aikawa/obsidian-another-quick-switcher](https://github.com/tadashi-aikawa/obsidian-another-quick-switcher)

- '24/4/6 install
- 存在は以前から知っていたが、プラグインの多機能さに圧倒されて未導入だったのを今さら後悔したプラグインの１つ。
- 標準搭載のクイックスイッチャーから今すぐにでも乗り換えたほうがよい！　こっちのほうが検索も早いという驚異のプラグイン。

### Core Search Assistant　★★

[https://github.com/qawatake/obsidian-core-search-assistant-plugin](https://github.com/qawatake/obsidian-core-search-assistant-plugin)

- '23/10/4 in
- 検索結果をサムネイル付きカードスタイルで表示する。
- たしかに標準の検索結果は見づらいので、ありがたい強化。

### Keyboard Analyzer

[https://github.com/cogscides/obsidian-keyboard-analyzer](https://github.com/cogscides/obsidian-keyboard-analyzer)

- キーボード画像上でホットキーの割当具合を確認、検索できる。
- 増え続けるプラグインとホットキーの割当で頭がパンクしそうになるのを抑えてくれるはず。

### Quick Explorer

[https://github.com/pjeby/quick-explorer](https://github.com/pjeby/quick-explorer)

- Obsidian内のファイル検索や移動・閲覧を補助する。
- あんまり意識して使ってない。フォルダ構造を複雑化してると使い勝手ありそう。逆に一つのフォルダに大量にノートを入れる管理方式だと向いてないかも？
- フォルダ内の前後ファイルに移動するコマンドボタンをノートタブにつければ、デイリーノート内にリンクを貼る必要もなく、前後の日付に飛べるから便利になりました。

### Regex Find/Replace

[https://github.com/Gru80/obsidian-regex-replace](https://github.com/Gru80/obsidian-regex-replace)

- 正規表現で検索・置換する機能を追加する。たぶん活躍する機会があるはず。

## 動作変更

### Hider　★

[https://github.com/kepano/obsidian-hider](https://github.com/kepano/obsidian-hider)

- Obsidianメニューや各種表示を適宜非表示にできる。
- プラグイン増量とともにアプリ内の表示が増えるので、使わないと判断したものは非表示のほうが迷わない。

### No Dupe Leaves　★

[https://github.com/scambier/obsidian-no-dupe-leaves](https://github.com/scambier/obsidian-no-dupe-leaves)

- バニラは同じノートを複数開くので、新規に開くのではなく、既存の開いてるノートにフォーカスを切り替える。
- カレンダー？からか、たまに有効にならず複数開いちゃうこともある。

### Open In New Tab

[https://github.com/patleeman/obsidian-open-in-new-tab](https://github.com/patleeman/obsidian-open-in-new-tab)

- サイドメニューのフォルダや内部リンクからノートを開く場合、現在開いてるノートのタブではなく、新規タブに開く。
- そのノートが既存のタブで開かれている場合は、そちらをアクティブにする。
- タブの挙動はどちらか一方となっても微妙に悩ましい。

## ファイル処理

### Auto Note Mover

[https://github.com/farux/obsidian-auto-note-mover](https://github.com/farux/obsidian-auto-note-mover)

- 設定した条件に従って、ノートを自動移動する。
- Evernoteから引越し時に振り分けで使ってた。
- まぁ無くても手動でコツコツ整理するのが間違いなさそう。

### Find orphaned files and broken links ★

[https://github.com/Vinzent03/find-unlinked-files](https://github.com/Vinzent03/find-unlinked-files)

- Obsidianの全ノートを検索して、リンクの壊れてるノートや孤立ファイルを一覧で示す。
- Evernoteからの引越し時に大いに助けられた。インポートしたノートのリンクが壊れまくってたので。
- たぶん普段使いではお世話にならなさそう。

### Importer　★★★

[https://github.com/obsidianmd/obsidian-importer](https://github.com/obsidianmd/obsidian-importer)

- 他のアプリやファイル形式からObsidianにインポートするプラグイン。
- 大多数のユーザが最初にお世話になっただろうなぁ。

### Trash Explorer　★

[https://github.com/proog/obsidian-trash-explorer](https://github.com/proog/obsidian-trash-explorer)

- Obsidianの各ノートは実際にローカルPCに作成されるmd形式のファイルだが、Obsidian上で削除すると、実ファイルも即座にPCのゴミ箱に入れられてしまう。そこでObsidian上の仮想ゴミ箱にワンクッションさせるためのプラグイン。

## キャンバス関連

### Simple Canvasearch

[https://github.com/ddalexb/obsidian-simple-canvasearch](https://github.com/ddalexb/obsidian-simple-canvasearch)

- '24/3/11 install
- キャンバス補助プラグイン。開いているキャンバス内だけを検索できる。

### Canvas Connections

[https://github.com/felixchenier/obsidian-optimize-canvas-connections](https://github.com/felixchenier/obsidian-optimize-canvas-connections)

- '24/3/11 install
- キャンバス補助プラグイン。カードのコネクトラインをつなぎ直せる。コマンドで呼び出す。

### Canvas Send to Back

[https://github.com/Zachatoo/obsidian-canvas-send-to-back](https://github.com/Zachatoo/obsidian-canvas-send-to-back)

- '24/3/11 install
- キャンバス補助プラグイン。カードの前後順を右クリックで指定できる。

## ベースプラグイン系

### BRAT (Beta Reviewers Auto-update Tester)

[https://github.com/TfTHacker/obsidian42-brat](https://github.com/TfTHacker/obsidian42-brat)

- Obsidianはオプションメニュー「コミュニティプラグイン」からプラグインを選んで導入できるが、そこに登録されてないプライベートプラグイン（あえて公式登録してない等）の導入・アップデートを補助するプラグインとなる。

## 残念ながらアンインストールしたプラグイン

### 2Hop Links plus　★★

[https://github.com/L7Cy/obsidian-2hop-links-plus](https://github.com/L7Cy/obsidian-2hop-links-plus)

- '23/10/21 in → ’24/10/28 out：Multiple Notes Outlineに機能代用
- 人によっては重宝しそうなScrapboxみたく関連ノートを簡単に確認できるプラグイン。
- ~~ノートが充実してくると活きてきそう。~~
- ノート作成時に、上位ノートにとりあえずリンクを貼っておけば、上位ノートが索引ノート（MOC）になってノート関係性の構築が楽になるような気がしてる。
- ノート下部に場所を取りすぎ、閲覧性が低い

### Customizable Menu　★★★

[https://github.com/kzhovn/obsidian-customizable-menu](https://github.com/kzhovn/obsidian-customizable-menu)

- 右クリックのサブメニューにコマンドを追加または非表示する。
- コマンドごとにアイコンも設定できる。細かい配慮。
- 右手マウス族には嬉しいプラグイン。
- ’24/10/24 out：Commanderが上位互換プラグインのため、そちらに集約

### Daily Notes Viewer　★

[https://github.com/Johnson0907/obsidian-daily-notes-viewer](https://github.com/Johnson0907/obsidian-daily-notes-viewer)

- デイリーノートを一定数まとめて表示できる。
- ウィークリー、マンスリーノートを作るまでもないな（たぶん使いこなせないし）、という日記に向いていない派にいいかも。

### Plugin Groups

[https://github.com/Mocca101/obsidian-plugin-groups](https://github.com/Mocca101/obsidian-plugin-groups)

- '23/10/4 in → '24/10/28 out：後継のLazyに乗り換え
- プラグインをグループ分けして一括有効/無効化、遅延読み込みなど動作変更できる。
- 起動に時間のかかるプラグイン等を遅延させるのが良いっぽい。
- とりあえず起動時に即必要っぽくないプラグインを放り込み様子見。私の環境下では起動が早くなってる印象はない。

### Recent Files　★

[https://github.com/tgrosinger/recent-files-obsidian](https://github.com/tgrosinger/recent-files-obsidian)

- 最近開いたノートの一覧をサイドバーに表示する、バニラに標準搭載されて然るべきなプラグイン。
- デイリーノートや画像は除くなど、除外設定ができるのも便利。
- '24/4/7 out：Another Quick Switcherで最近のファイルを確認できるため不要とした。

### Remember cursor position

[https://github.com/dy-sh/obsidian-remember-cursor-position](https://github.com/dy-sh/obsidian-remember-cursor-position)

- 各ノートのカーソル位置、スクロール位置を記憶していて、ノート間の移動やアプリ起動時に前回状態が保存されてるなど、作業効率をアップする、はず。
- ノートの容量（行数や貼ってる画像数など）が増えてくるとオンマウスでガクガク動く現象が発生したりするが、落ち着くまでしばらく様子見しましょう。
- '24/3/3 uninstall　機能はすばらしいが、ガクガクがあまりに気になるので。

とりあえず今導入しているプラグインをほぼ全て書き出してみた。  
幾つか用途不明で説明できないものを省いた。  
一覧に挙げてみたものの、ほぼ使った覚えのないプラグインもあり、こういうときのためにメモを残す習慣をつけないとな、と反省する。

Obsidianについての初めての記事がこれとなったが、機会があれば他の記事も書いてみよう。