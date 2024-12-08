---
title: "【2024最新版】Pythonの仮想環境ベストプラクティス - Qiita"
source: "https://qiita.com/KeiJei/items/c2d25daf34bfe9a21ba9?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[KeiJei]]"
published: 2024-12-08
created: 2024-12-08
description: "弊社Nucoでは、他にも様々なお役立ち記事を公開しています。よかったら、Organizationのページも覗いてみてください。また、Nucoでは一緒に働く仲間も募集しています！興味をお持ちいただ…"
tags:
  - "clippings"
---
弊社Nucoでは、他にも様々なお役立ち記事を公開しています。よかったら、Organizationのページも覗いてみてください。  
また、Nucoでは一緒に働く仲間も募集しています！興味をお持ちいただける方は、[こちら](https://www.recruit.nuco.co.jp/?qiita_item_id=c2d25daf34bfe9a21ba9)まで。

## 序章: はじめに

Pythonプロジェクトには仮想環境の設定が不可欠です。

特に、最近はPoetryがデファクトスタンダードとして定着しつつあり、仮想環境の管理と依存関係の整理においても強力なツールとして注目されています。本記事では、Poetryを活用した仮想環境のベストプラクティスについて解説します。  
[![スクリーンショット 2024-11-19 15.13.11.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3864803%2F63014b75-69d1-3390-3db2-2dafe9857af4.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=930d76ed17acf5a4820791b1773769e8)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3864803%2F63014b75-69d1-3390-3db2-2dafe9857af4.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=930d76ed17acf5a4820791b1773769e8)  
※出典: Googleトレンド, [https://trends.google.co.jp/trends/](https://trends.google.co.jp/trends/), 2024年11月19日取得

多くのエンジニアがPoetryを利用し始めたものの、チーム環境での共有において思わぬトラブルが生じるケースも少なくありません。

例えば、poetry.lockファイルが不整合を起こしたり、プロジェクトの初期設定が原因で、同一の環境が再現されないといった課題が挙がっています。

本記事では、こうした失敗例に基づき、確実に環境を再現できる手順と設定方法をわかりやすく説明します。

**特に第5章**では、実際のプロジェクトでのトラブルシューティングに役立つ具体的な事例を交えて、チーム開発におけるPoetryの使い方を深掘りします。

## 第1章: 仮想環境の基本

**既に知っている方は読み飛ばして[2章](https://qiita.com/KeiJei/private/245b6cfe3e375bfea42e#%E7%AC%AC2%E7%AB%A0-pyenv%E3%81%A8poetry%E3%81%A7%E3%81%AE%E7%92%B0%E5%A2%83%E8%A8%AD%E5%AE%9A)へ!**

仮想環境とは、Pythonプロジェクトごとに依存ライブラリやバージョンを管理し、他プロジェクトと隔離された環境を提供する技術です。Python開発において、異なるプロジェクトでライブラリのバージョンが競合するのを防ぎ、動作環境を安定させるための基盤として、仮想環境は重要な役割を果たします。

仮想環境を利用することで、以下のような利点があります：

- **依存関係の競合を回避**:  
複数のプロジェクトで異なるバージョンのライブラリを使用する場合、仮想環境を使えば互いに干渉しません。
- **環境の再現性を確保**:  
他の開発者やサーバーに環境を簡単に再現できます。
- **クリーンな環境の維持**:  
システム全体にパッケージをインストールせず、プロジェクトごとに管理できます。

本章では、以下の代表的な仮想環境ツールについて、それぞれの特徴と利点・欠点を簡単に解説します。

---

### 1\. venv

venvは、Python標準ライブラリで提供される仮想環境作成ツールです。  
追加インストールなしで使用できます。

- **利点**:
- Pythonに標準で含まれているため、追加インストールが不要。  
シンプルで軽量な仮想環境の作成が可能。
- **欠点**:
- 依存ライブラリのバージョン管理を手動で行う必要がある
- プロジェクト管理ツールとしての機能はない。

---

### 2\. virtualenv

`virtualenv`は、Pythonの仮想環境を作成するためのツールで、軽量かつシンプルです。

- **利点**:
- プロジェクトごとの環境を手軽に作成可能。
- **欠点**:
- プロジェクト管理ツールではないため、依存ライブラリの記録や管理は手動で行う必要がある。
- 現代的なツールと比較すると、利便性が劣る。

---

### 3\. Poetry

`Poetry`は、仮想環境の作成だけでなく、依存ライブラリやプロジェクト管理も簡単に行えるツールです。

- **利点**:
- `pyproject.toml`にプロジェクト構成を一元管理。
- 仮想環境作成と依存関係管理がシームレスに統合されている。
- チーム開発に適した`.lock`ファイルを生成し、再現性の高い環境構築が可能。
- **欠点**:
- 初心者にとって設定が複雑に感じる場合がある。
- 特定のPythonバージョンで仮想環境を構築する際に、`pyenv`との併用が必要。

---

### 4\. pyenv

`pyenv`は、異なるPythonバージョンを切り替えられるツールで、仮想環境管理ツールではありませんが、`venv`や`Poetry`と併用することで強力な開発環境を構築できます。

- **利点**:
- Pythonのバージョンをプロジェクトごとに切り替え可能。
- ローカルやグローバルでのバージョン指定が簡単。
- **欠点**:
- 仮想環境の作成は直接サポートされておらず、`venv`や`Poetry`と組み合わせて使用する必要がある。

## 第2章: pyenvとPoetryでの環境設定

もうお気づきかと思いますが、

Poetry自体には直接Pythonのバージョンを切り替える機能はありません！

そのためPoetryはpyenvとセットで使用されることが多いです。　そこで本章では、パッケージ管理および仮想環境の設定を行う`Poetry`と、Pythonのバージョン管理を担当する`pyenv`のインストールから基本設定までの手順を詳しく紹介します。

- **Poetryのインストール**:  
公式ドキュメントを参考にしたインストール手順を示し、環境変数の設定方法も解説します。  
インストール方法は以下のリンクがわかりやすいです。  
[https://www.cfxlog.com/python\_poetry/#rtoc-6](https://www.cfxlog.com/python_poetry/#rtoc-6)

terminalから下記のコマンドを実行しましょう

terminal

```
curl -sSL https://install.python-poetry.org | python3 -
```

すると以下のように表示されます  
※usernameは実行環境に応じて変化します

terminal

```
Retrieving Poetry metadata

# Welcome to Poetry!

This will download and install the latest version of Poetry,
a dependency and package manager for Python.

It will add the \`poetry\` command to Poetry's bin directory, located at:

/Users/username/.local/bin

You can uninstall at any time by executing this script with the --uninstall option,
and these changes will be reverted.

Installing Poetry (1.8.4): Done

Poetry (1.8.4) is installed now. Great!

To get started you need Poetry's bin directory (/Users/username/.local/bin) in your \`PATH\`
environment variable.

Add \`export PATH="/Users/username/.local/bin:$PATH"\` to your shell configuration file.

Alternatively, you can call Poetry explicitly with \`/Users/username/.local/bin/poetry\`.

You can test that everything is set up by executing:

\`poetry --version\`
```

以下のコマンドを実行します

実行した後に.zshrcに以下を記載します。  
`i`を押すと挿入モードに切り替わり追記ができます。

.zshrc

```
export PATH="/Users/username/.local/bin:$PATH"
```

記入した後は`Esc`キーを押してから以下いずれかを実行します。

| key | 内容 |
| --- | --- |
| ZZ | 上書き保存し、viを終了 |
| :w | 内容を保存 |
| :q! | 間違えたため、保存せずに終了 |

source コマンドで設定を恒久化します。

terminal

```
# zsh の場合
source ~/.zshrc
```

ここで一旦ターミナルを再起動します。  
再度立ち上がったら以下のコマンドを実行して

バージョンが出ると成功です。

- **pyenvのインストール**:  
Homebrewを使用したインストール方法を説明します。  
まずは[公式HP](https://brew.sh/ja/)を参考にHomebrewをインストールします。

terminal

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

そうすると

terminal

```
Press RETURN/ENTER to continue or any other key to abort:
```

と表示されるのでENTERを押してしばし待ちましょう。

terminal

```
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
   (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/username/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
- Run brew help to get started
- Further documentation:
   https://docs.brew.sh
```

この指示が出たらPoetryと同様の手順で.zshrcにパスを追加しましょう。  
これでHomeBrewの準備は完了です。  
あとは

を実行し、お決まりの

からの

```
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```

を.zshrcに追加したら完了です。

## 第3章: Poetryの高度な設定

本章では、Poetryを使ったプロジェクト管理をさらに柔軟に行うための設定方法や便利なコマンドを紹介します。特に、複数のプロジェクトを一つのディレクトリ内で管理する場合の具体的な手順を解説します。

以下のようなモノレポ構成を想定します。

モノレポ（モノリポジトリ）とは、複数のプロジェクトを1つのリポジトリで管理する手法です。コード共有や依存関係の統一が容易になる一方で、大規模になると管理が複雑化することがあります。

- 大きなディレクトリ（例: `Big_project`）内に複数のプロジェクトディレクトリ（例: `project_task1`, `project_task2`, `project_task3`）が存在する。
- 各プロジェクトごとに独立した仮想環境を作成し、それぞれ異なる依存関係を管理したい。

```
Big_project/
├── project_task1/
├── project_task2/
└── project_task3/
```

通常の設定では、1つの仮想環境が`Big_project`全体に反映されてしまう可能性がありますが、`poetry config --local virtualenvs.in-project true`を使用することでプロジェクト単位での管理が可能になります。

---

### 実際の手順

#### 1\. ディレクトリの準備

まず、プロジェクト用のディレクトリ構造を作成します。

terminal

```
mkdir -p ~/main_directory/project1
mkdir -p ~/main_directory/project2
mkdir -p ~/main_directory/project3
```

#### 2\. VS Codeでディレクトリを開く

VS Codeを起動します。  
ディレクトリ`~/main_directory`を選択して開きます。

#### 3\. 各プロジェクトごとのPoetry設定

それぞれのプロジェクトディレクトリに移動してPoetryを設定します。

terminal

```
cd ~/main_directory/project1
poetry init  # pyproject.tomlを作成
poetry config --local virtualenvs.in-project true  # 仮想環境をプロジェクト内に作成
poetry install  # 仮想環境を構築
```

他のプロジェクト（project2, project3）でも同様に以下を実行します。

#### 4\. 依存関係の管理

各プロジェクトごとに必要なライブラリをインストールできます。  
以下では参考にdjangoとflaskを別々の環境にインストールしています。

terminal

```
cd ~/main_directory/project1
poetry add django@3.2
```

terminal

```
cd ~/main_directory/project2
poetry add flask@2.0
```

#### 5\. VS Codeでの操作

VS CodeのTerminalを使用して、各プロジェクト専用の仮想環境をアクティブにします。

Project1の仮想環境をアクティブ化

terminal

```
cd ~/main_directory/project1
poetry shell
```

また仮想環境を切り替える場合は、以下コマンドで一旦現状の環境から出て

他のディレクトリに移動してアクティブ化を再実行します。

#### 6\. よく使うコマンド

| **番号** | **用途** | **コマンド** | **補足** |
| --- | --- | --- | --- |
| 1 | 設定の確認（全体設定） | `poetry config --list` | 全体の設定を一覧表示 |
| 2 | 設定の確認（ディレクトリごと） | `poetry config --local --list` | 現在のプロジェクトでの設定を表示 |
| 3 | 仮想環境の情報確認 | `poetry env info` | 仮想環境のパスや状態を確認 |
| 4 | 仮想環境の削除 | `poetry env remove <env_name>` | `<env_name>`に削除する仮想環境の名前を指定 |
| 5 | 依存関係のグループ管理 | `poetry add pytest --group test` | testやdocsなど、自作のグループごとにライブラリを管理する（詳細は[公式ドキュメント](https://python-poetry.org/docs/managing-dependencies/)参照） |

## 第4章: .lockファイルの理解

Poetryが生成する`.lock`ファイルは、依存関係を固定し、環境の一貫性を保つために重要な役割を果たします。  
lockファイルは自動で作成、更新されていくため、なんとなく使用してうまく動いている方もいらっしゃるかと思いますが、チームで環境を共有する際に問題が起きるかもしれません。この章では、`.lock`ファイルの役割や重要性を詳しく解説します。

---

### 1\. `pyproject.toml`と`.lock`ファイルの違い

- **`pyproject.toml`**  
プロジェクトの依存関係を記述するファイル。依存ライブラリの「希望するバージョン範囲」が記載されています。また自作モジュールの管理も可能ですが、ここについては**5章**で解説いたします。
- **`.lock`ファイル**  
依存ライブラリのバージョンを厳密に固定した情報を記録します。このファイルにより、同じ環境を再現することが可能になります。

例:

pyproject.toml

```
[tool.poetry.dependencies]
numpy = "^1.20"
pandas = "^1.3"
```

poetry.lock

```
[[package]]
name = "numpy"
version = "1.20.3"
...

[[package]]
name = "pandas"
version = "1.3.5"
...
```

pyproject.tomlでは依存ライブラリの「範囲」(例: ^1.20)が記載される一方、.lockファイルにはインストールされた具体的なバージョン(例: 1.20.3)が記録されます。

### 2\. 重要性

環境を誰かと共有する際はpyproject.tomlだけでは不十分で、pyproject.tomlに記載された条件は満たすが別のバージョンをインストールしてしまう場合があります。  
結論としましては、**環境をチームで共有する際はtomlに加えて、lockファイルも一緒に渡しましょう。**

## 第5章: チーム開発におけるベストプラクティス

4章までの内容でとりあえず仮想環境を動かすことができますが、実際に使用する中でいくつかの問題に直面すると思います。またこの部分についてまとめられた記事は少なく、私も苦戦いたしました。。。  
そこで本章では、チームでPoetryを利用する際のベストプラクティスを具体的な事例と共に紹介します。

### トラブル事例と解決策

#### 1\. **ライブラリ名の色分け問題**

- 共有されたpyproject.tomlをもとに

を実行し、必要なライブラリをインストールして

でライブラリを確認した際に、ライブラリ名が赤文字と青文字で混在することがあります。

**赤文字のライブラリはインストールできておりません！**

色の意味は以下の通りです。

**赤いライブラリ名**  
ライブラリが現在インストールされていない場合を示します

**青いライブラリ名**  
ライブラリがインストールされている場合を示します

全てが青いライブラリ名になっていれば正常ですが、赤いライブラリが混在している場合は何かしらの問題でうまく環境が構築できていないことを示しています。toml、lockファイルを再度確認して問題がないか確認しましょう。  
必要に応じて

```
poetry remove パッケージ名
poetry add パッケージ名
```

再インストールすることで問題が解決する場合もあります。  
ただし同じライブラリを再インストールしてもlockファイルは更新されますので注意が必要です。

---

#### 2\. **`poetry.lock`と`pyproject.toml`の不整合**

Poetryを使用しているプロジェクトで、`poetry.lock`と`pyproject.toml`間の依存関係の不整合が原因でエラーが発生する場合、以下の手順で問題を解決できます。

---

`Run poetry lock [--no-update] to fix it`  
これは`poetry.lock`と`pyproject.toml`の間に互換性の問題があることを示します

**修正手順**  
1.**現在の状態の確認**

次のコマンドを使用して、依存関係の状態が正しいか確認します：

terminal

```
poetry check
poetry check --lock
```

問題なければ`All set!`、ある場合は詳細が表示されます。

2.**ロックファイルを再生成**  
依存関係を再解決し、poetry.lockを更新するには以下を実行します：

オプション：`--no-update`  
\--no-updateを使用することで、既存の依存関係のバージョンを変更せずにpoetry.lockを更新できます：

3.**依存関係を更新する場合**

すべての依存関係を最新のバージョンに更新しつつ、poetry.lockを生成したい場合は以下を実行します：

特定の依存関係のみを更新する場合：

terminal

```
poetry update <package_name>
    
例：poetry update requests toml
```

---

#### 3\. **`pyproject.toml`内の設定管理**

- `name`や`version`フィールドなど、チームで共通設定を共有する方法について解説します。  
まずpyproject.tomlは以下のようの形式をしています。

---

pyproject.toml

```
[tool.poetry]
name = "test"
version = "0.1.0"
description = "A short description of the package."
authors = [
    "Your Name <you@example.com>"
]
license = "MIT"
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.11"

[tool.poetry]
packages = [
    { include = "my_package" },
    { include = "lib/extra_package", from = "lib" }
]

[tool.poetry.group.test.dependencies]
pytest = "^8.3.3"

[tool.poetry.group.demo.dependencies]
matplotlib = "^3.9.2"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

- `name`にはプロジェクト名や、環境を共有するグループの名前をつけましょう。この仮想環境の用途がわかりやすいとGoodです。ただし詳細は`description`に記入できるため、名前に詰め込みすぎる必要はありません
- 仮想環境をバージョン管理する際は`version`が便利ですが、初期の`version 0.0.0`から一向に変化させなくても動作には全く問題ありません
- `license`には`MIT`や`Apache-2.0`があります
- `author`には作成者の名前とメールアドレスを記入します
- `readme`や`documentation`にプロジェクトの概要がわかり資料をつけておくと便利です！

```
[tool.poetry.group.test.dependencies]
pytest = "^8.3.3"

[tool.poetry.group.demo.dependencies]
matplotlib = "^3.9.2"
```

この部分では`poetry add pytest --group test`などでテスト時にしか使わないライブラリなどを分けてインストールした場合に自動で追記されます。  
（詳細は公式ドキュメント参照）

この機能を利用して、開発中、テスト、実運用、別々にライブラリを管理することができます！

## 第6章: Jupyter NotebookとPoetryの統合

データサイエンスや分析プロジェクトでは、Jupyter Notebookを利用するケースが多くあります。

ただしPoetry環境で開発していると、デフォルトでは`カーネル`から現状の仮想環境を選択できません！

この対応は簡単です。  
まずは以下のコマンドを実行して必要なライブラリを追加します。

次に、現状の仮想環境をJupyterに認識させるため、以下を実行します。

terminal

```
poetry run python -m ipykernel install --user --name=your_env_name --display-name "Python (your_env_name)"
```

あとはVisual Studio Codeを再起動してから再度任意の.ipynbを開き、`カーネル`をクリックすると選択肢として先ほど作成したカーネルが表示されます。

## 第7章: 新時代の仮想環境「uv」の紹介

最後に、新たに注目を集める仮想環境ツール`uv`について簡単に紹介します。Poetryに次ぐツールとして期待される`uv`の利点と、現在のPython開発環境における潜在的なユースケースについて触れ、今後の仮想環境管理の方向性について考察します。  
[![スクリーンショット 2024-11-20 16.52.56.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3864803%2F25008d8b-01ce-c2ab-bf21-cfa2608a7e9b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6e75edcd8e10337c56abf88a2cffff69)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3864803%2F25008d8b-01ce-c2ab-bf21-cfa2608a7e9b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6e75edcd8e10337c56abf88a2cffff69)  
※出典: Googleトレンド, [https://trends.google.co.jp/trends/](https://trends.google.co.jp/trends/), 2024年11月20日取得

ご覧の通り、人気急上昇中のuvです。  
結論から申し上げますと、  
**Poetryと使い勝手が近いため、まずはPoetryで様子を見て、uvが継続して人気であれば移行することをお勧めします。**

[公式HP](https://docs.astral.sh/uv/)を見ていただくとわかるように`uv`は、Rustで書かれた非常に高速なPythonパッケージおよびプロジェクトマネージャーです。  
以下にその特徴を箇条書きでまとめます。

### 特徴

- **多機能なツール**  
pip、pip-tools、pipx、poetry、pyenv、twine、virtualenvなど、多数のツールを1つで置き換え可能
- **高速**  
pipより10〜100倍速いパフォーマンス
- **pip互換のインターフェース**  
使い慣れたCLIで性能を向上
- **クロスプラットフォーム対応**  
macOS、Linux、Windowsをサポート

---

あれ？  
Poetryとpyenvよりもいい？と思われたかもしれません。  
ただし`uv`は比較的新しいライブラリであるため、デファクトスタンダードというにはまだ早いです。  
業務で使用するには安定性やサポートに懸念が残るというのが正直なところです。  
よって、繰り返しになりますが結論としては  
**まずはPoetryで様子を見て、uvが継続して人気であれば移行してはどうでしょうか？**

## 第8章: プロジェクトでよく使われる便利ツールの紹介

#### Linter

Linterは、コードの静的解析を行い、問題点が無いかをチェックしてくれるツールです。  
PythonのLinterとしては、**pylint**、**flake8**などが有名です。  
コードの保守性・安全性を保つためにマストなので、必ず使用することをおすすめします。

##### flake8

現在より多く使われているのはflake8になると思います。  
flake8は下記の3つのライブラリがまとまったラッパーライブラリで、文法・コーディング規約・複雑さをまとめてチェックしてれるのが強みです。

- PyFlakes
- Pythonの文法に準拠しているかをチェックします。
- pycodestyle
- 元々はpep8というライブラリでした。
- [PEP8](https://peps.python.org/pep-0008/)というPythonコーディング規約に準拠しているかをチェックします。
- Ned Batchelder’s McCabe script（McCabe)
- Pythonコードの複雑さ([循環的複雑度](https://ja.wikipedia.org/wiki/%E5%BE%AA%E7%92%B0%E7%9A%84%E8%A4%87%E9%9B%91%E5%BA%A6))をチェックします。

**インストール**

[公式ドキュメント](https://flake8.pycqa.org/en/latest/#)では、pipを使ったインストール方法しか紹介されていません。

Poetryを使ったインストール方法は以下の通りです。  
※`--group`(dependency group) はパッケージをグループ単位で管理できる機能であり、1つのtomlファイル内でtest用や実運用のためのライブラリを分けて管理できます。  
グループ管理については[公式ドキュメント](https://python-poetry.org/docs/managing-dependencies/#optional-groups)がわかりやすいです。

```
poetry add flake8 --group test
```

インストール完了後、`flake8 --version`を実行すると、以下の様な結果か表示されるはずです。

```
6.0.0 (mccabe: 0.7.0, pycodestyle: 2.10.0, pyflakes: 3.0.1) CPython 3.11.0 on Darwin
```

上述した3ライブラリ（mmcabe, pycodestyle, pyflakes）がそれぞれ内包されていることがわかりますね。

**使い方**

解析したいプロジェクトディレクトリで、以下のコマンドを実行するだけです。

また、解析対象を特定のファイルに限定することもできます。

#### Formatter

Linterがコードの問題点を解析してくれるのに対して、コードのスタイルをチェックし、自動修正してくれるのがFormatterです。  
Pythonのコードスタイルについては、コード規約であるPEP8に従うのがまず第一なのですが、規約ではカバーしていない部分について、ルールを定めて自動修正してくれます。

例えばシングルクォーテーションとダブルクォーテーションの使い分け、改行の位置など、個人差が生じるような部分については、Formatterでカッチリと定めてしまうほうが、誰にとっても読みやすいコードになります。

##### Black

他にも[**issort**](https://pycqa.github.io/isort/)などのライブラリが存在しますが、現在最もデファクトスタンダードに近いのは**Black**だと言えるでしょう。

Blackの大きな特徴は、個別設定によるバリエーションを許さない厳格さにあります。  
「厳格」というと窮屈に感じるかもしれませんが、フォーマットが厳格に固定されることで、「どう書くか」を気にしたり、議論したりする一切の手間が省ける、ということでもあります。  
その分、よりクリーンなコードの書き方や、より重要なドメイン知識の考察などに割ける時間が増えるのは、エンジニアにとって大きなメリットになります。

**インストール**

こちらも[公式サイト](https://black.readthedocs.io/en/stable/getting_started.html)にはpipでのインストール方法しか書かれていませんが、Poetryでもインストール可能です。

```
poetry add black --group test
```

**使い方**

flake8と同じく、コマンド一発で使用できます。

[公式ドキュメント](https://black.readthedocs.io/en/stable/usage_and_configuration/the_basics.html)で、より発展的な使い方も確認できます。

##### isort

Blackと併用されるパターンが増えて来ているようです。[公式](https://pycqa.github.io/isort/docs/configuration/black_compatibility.html)でも、Blackとの併用・互換性について説明されています。

import文をPEP8準拠にソートしてくれるFormatterです。複数のモジュールをimportすると、import文の順番がぐちゃぐちゃになりやすいので、これを使って修正することで可読性を上げていきたいところです。

#### 単体テスト

単体テスト(ユニットテスト)は、プログラムの最小構成単位(例えば関数)が正しく動作することを確認するために行うテストです。  
機能の実装にばかり追われてテストを書かないままにしていると、いつの間にかプログラム全体の動作の担保が難しく、かつ修正も困難な状況に追い込まれていきます。

単体テストツールは、プロジェクト作成段階から導入すべきです。後回しにして良い理由はありません。

##### pytest

Pythonには標準ライブラリとして**unittest**がありますが、現在のデファクトスタンダードといえば**pytest**になると思います。  
unittestの欠点をカバーする目的で開発されたライブラリで、毎回テストクラスを定義しなければならないunittestと違い、関数単位でシンプルにテストを追加できる点などが魅力です。またunittest用に書かれたテストも実行できるため、unittestからの移行も簡単にできます。

拡張機能も豊富で、テストカバレッジを計算してくれる**pytest-cov**などは特に便利です。

**インストール**

例によってpipでインストールする場合は[公式ドキュメント](https://docs.pytest.org/en/7.2.x/getting-started.html)を参照してください。

Poetryを使う場合は以下です。

```
poetry add pytest --group test
```

**使い方**

下記のコマンドで、実装したテスト関数をテストしてくれます。

テスト関数の書き方などは、ドキュメントに詳しく書いていますが、

- ファイル名のprefixを、 `test_***.py`
- 関数名のprefixを、 `test__×××`

として定義すれば、pytestのテスト対象となります。

#### 型定義・解析

Pythonは動的型付け言語なので、型を定義する必要がありません。  
が、3.5系以降は型ヒントを付けることが可能になり、現在は多くのプロジェクトで、保守性・可読性の観点から用いられています。

エディタの拡張機能なども含め、型の導入・静的解析ができる環境を用意することは、モダンなPythonプロジェクトでは、ほぼ必須条件と言えるでしょう。

##### mypy

Python型チェックライブラリの先駆け的存在であり、かつデファクトスタンダードと呼べるライブラリです。  
若干重いのが欠点ですが、他に依存する要素もなく、シンプルかつ十分な機能を有しています。

**インストール**

Poetryを使ったインストールは下記のとおりです。

```
poetry add mypy --group test
```

**使い方**

`poetry run`のサブコマンドとして実行します。

```
poetry run mypy (ファイル or ディレクトリ)
```

#### テスト・解析管理

##### Nox

Noxは複数のテストや解析ツールを管理してくれるツールで、[tox](https://tox.wiki/en/latest/)の後継にあたります。  
これまで紹介してきた各種ツールを、独立した環境で自由に動かすことができます。  
Noxの特徴としては、設定ファイルをPythonスクリプトとして書ける点です。`noxfile.py`というファイルを作成し、実行したいテストを追加していきます。

**インストール**

```
poetry add nox --group test
```

**使い方**

`noxfile.py`は以下のように記載してきます。

noxfile.py

```
import nox
import nox

@nox.session
def tests(session):
    session.install('pytest')
    session.run('pytest')

@nox.session
def lint(session):
    session.install('flake8')
    session.run('flake8')
```

実行はコマンドを叩くだけです。

#### テスト自動化

CircleCIやGithub ActionsなどのCI/CDサービスは多くのプロジェクトで利用されていますが、コミット前に全てのテストを通しておけば、いたずらにパイプラインを落とすこともなく、他のメンバーに影響を与えることもありません。

Gitには、コミット前に任意のアクションを自動実行してくれる`pre-commit`フックがあります。

が、この設定は`.git/hooks`以下に記載するため、チーム開発などでは設定を簡単に共有できないのがネックです。これを解決するために、**pre-commit**という（名前そのまんまな）多言語パッケージマネージャが開発されています。

##### pre-commit

pre-commitは、全てのコミットの前にあらゆるフックのインストールと実行を行ってくれる管理ツールです。  
フックして登録したいテストや解析は、`.pre-commit-config.yaml`というファイルでステップ別に記述・管理します。`.pre-commit-config.yaml`自体ももちろんコミットすることができるので、コミット前に自動実行したいあらゆる手順をチーム内で共通化することができます。

**インストール**

```
poetry add pre-commit --group test
```

**使い方**

例えばコミット前にflake8を実行したい場合は、以下のような形で`pre-commit-config.yaml`を記述します。

.pre-commit-config.yaml

```
repos:
-   repo: local
    hooks:
    -   id: flake8
        name: flake8
        entry: poetry run flake8
        language: system
        types: [python]
```

yamlファイルの設定は、以下のコマンドで`.git/hooks`以下に反映させます。

これで、設定したフックがコミット前に走るのですが、`pre-commit run --all-files`を叩いて手動実行も可能です。  
より詳しい使い方は、[公式ドキュメント](https://pre-commit.com/#usage)をご覧ください。

## おわりに

本記事では、`Poetry`と`pyenv`を活用した仮想環境管理の利点を解説してきました。  
最後まで見ていただきありがとうございました！  
ぜひ`いいね`ボタンにご協力お願いいたします！

もし「もっと良いツールがある」「これからはxxの時代だ」といったご意見がございましたら、コメントで教えていただけると嬉しいです。

弊社Nucoでは、他にも様々なお役立ち記事を公開しています。よかったら、Organizationのページも覗いてみてください。  
また、Nucoでは一緒に働く仲間も募集しています！興味をお持ちいただける方は、[こちら](https://www.recruit.nuco.co.jp/?qiita_item_id=c2d25daf34bfe9a21ba9)まで。

---