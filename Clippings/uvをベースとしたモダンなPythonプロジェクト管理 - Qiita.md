---
title: "uvをベースとしたモダンなPythonプロジェクト管理 - Qiita"
source: "https://qiita.com/Kotaro_Kinoshita/items/aef1392af301ceef00d9?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[Kotaro_Kinoshita]]"
published: 2024-11-24
created: 2024-11-24
description: "はじめに最近、個人的に新しいPythonパッケージを開発する機会がありました。その中で、pythonの比較的、モダンな技術を採用して、パッケージの品質管理のためのCI/CDワークフローを構築してみ…"
tags:
  - "clippings"
---
## はじめに

最近、個人的に新しいPythonパッケージを開発する機会がありました。その中で、pythonの比較的、モダンな技術を採用して、パッケージの品質管理のためのCI/CDワークフローを構築してみました。あくまでも自己的な方法ですが、備忘録ついでに内容をまとめてみました。本記事内では、最低限のみ実装となっています。細かい設定は各種ライブラリのドキュメントや他の記事を参考にしてください。

## 使用ライブラリ

今回は以下のような技術を利用しています。

- [uv](https://docs.astral.sh/uv/): パッケージ&プロジェクト管理
- [Ruff](https://docs.astral.sh/ruff/): Linter&Formatter
- [MKDocs](https://www.mkdocs.org/): ドキュメント
- [tox](https://tox.wiki/en/4.23.2/): タスク、テスト自動化
- [mypy](https://mypy-lang.org/): 型チェック
- [pytest](https://docs.pytest.org/en/latest/): テストフレームワーク
- [Github Actions](https://docs.github.com/ja/actions): CI/CD

## パッケージ&プロジェクト管理

本記事では、uvでパッケージとプロジェクトの管理を行います。uvはpythonのバージョン管理からパッケージ管理までを一つのツールで実現可能です。以前はpyenvとpoetryのようpythonのバージョン管理とパッケージ管理はそれぞれ個別のツールで実現していましたが、uvを使うことで、これらの管理を一つのツールで実現できます。また、uv自体はRustで開発されており、パッケージのインストールや依存関係の解決が非常に高速に実現できる点も優れています。

プロジェクトの作成とパッケージのインストール

```
# プロジェクトの作成(Project名: example, pythonバージョン: 3.10)
uv init example -p 3.10

cd example

# 例としてnumpyをインストールする
uv add numpy
```

uvではプロジェクトの管理を`pyproject.toml`で行います。上記でプロジェクトを作成することで以下のような`pyproject.toml`が生成されます。

pyproject.toml

```
[project]
name = "example"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.10"
dependencies = [
    "numpy>=2.1.3",
]
```

すでに`pyproject.toml`が存在する場合は以下のコマンドを実行することで、パッケージのインストールが可能です。インストールされたパッケージは直下の.venvにインストールされます。

## Linter&Formatter

LinterやFormmatterにはRuffを用いました。RuffはこれまでFlake8, Black, isort, etc..など複数のツールを使って静的コード解析を行っていたところ、これらのツールをRuffに統合し、一つのツールで実行可能です。  
また、uvと同じくRustで開発されているため、高速に動作します。

uvで管理されているプロジェクトでは、以下のLinterを実行可能です。`uvx`を使用すると、Ruffをインストールなしに実行可能です。また、`--fix`オプションを使用すると、自動でエラーを修正できます。

Linterによるチェックが完了したら、以下のコマンドでformatterを実行し、自動でコードを整形できます。

また、Ruffのlinterやformatterの設定は`pyproject.toml`で行います。例えば、1行あたりに許容する文字列帳を100にするには、以下のように設定します。本記事では、述べませんが、他にも無視するエラーの種類など細かく設定することができます。

```
[tool.ruff]
line-length = 100
```

EditerにVS Codeを使用する場合は`settings.json`に以下のような設定を記述すると、ファイル保存時に自動でフォーマットを適用できます。

settings.json

```
{
    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.formatOnSave": true,
    },
    "files.autoSave": "onFocusChange",
}
```

## ドキュメント

ドキュメントには、MKDocsを使用しました。MKDocsは静的サイトジェネレーターで、markdown形式で記述したソースファイルから、静的サイトを生成することができます。基本的にdocs配下にmarkdownで記載したファイルを入れるだけでよく、単純な手順でドキュメントサイトを作成することできます。FastAPIやPydanticといった有名ライブラリのドキュメントでも採用されています。プラグインを利用することでソースコード内のdocstringからドキュメントを自動生成することも可能です。

materialテーマを使用したいので、materialテーマをインストールします。

```
uv add --dev mkdocs mkdocs-material
```

MKDocsのプロジェクトファイルを生成します。`docs`フォルダと`mkdocs.yaml`が生成されます。

mkdocs.yamlを以下のように編集し、materialテーマを適用します。

mkdocs.yaml

```
site_name: example
theme:
  name: material
  features:
      - navigation.tabs
nav:
  - Home: index.md
```

以下のコマンドを実行するとローカルホストにサイトが立ち上がります。

[![Screenshot from 2024-11-24 04-42-07.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3941105%2Fe9c3352c-645e-68a4-8da1-906189b2b5e7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6a5c242cbe576f6f617065b4ec1f4865)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3941105%2Fe9c3352c-645e-68a4-8da1-906189b2b5e7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=6a5c242cbe576f6f617065b4ec1f4865)

ここで作成したドキュメントは後ほど、Gihub Actionsを利用して、Github Pagesに公開します。

## タスク、テスト自動化

toxはプロジェクトのタスク実行を自動化するためツールです。実行タスクの定義を一つのファイルに集約したり、異なるpythonやライブラリのバージョンのテストを実行することが可能です。今回は、mypy, pytest, MKDocs, Ruffの実行コマンドをすべてToxで記述し、`pyproject.toml`にタスクの定義を集約します。

uvでtoxを実行するためのプラグインとして、[tox-uv](https://github.com/tox-dev/tox-uv)があるので、インストールします。

```
uv tool install tox --with tox-uv
```

`pyproject.toml`に以下を追記します。今回、`src`下にソースコード、`tests`下にテストコードが存在する状況を想定しています。envlistにタスク一覧を定義し、\[testenv:lint\]のようにタスクの詳細を定義します。`py310`のように記述し、タスクで使用するpythonバージョンを明示することができます。ここでは、pytestは３種類のバージョンでテストしています。今回は記述していませんが、`deps`にバージョンを記載することで使用するライブラリのバージョンを明示することが可能です。

pyproject.toml

```
[tool.tox]
legacy_tox_ini = """
[tox]
envlist = lint, mypy, py310, py311, py312

[testenv]
deps = pytest
commands = 
    pytest tests

[testenv:lint]
deps = ruff
commands = 
    ruff check --fix
    ruff format

[testenv:mypy]
deps = mypy
commands = mypy src tests --ignore-missing-imports --strict-optional --disallow-untyped-defs 
"""
```

以下のコマンドを実行すると、pytest, Ruff, mypyが一括で実行されます。pytestでは、python3.10, 3.11, 3.12の３つのバージョンのテストが実行されます。`-p`オプションはタスクを並列で実行するためのオプションです。

特定のタスクのみ実行するには`-e`オプションを利用します。

## pre-commit

commit時にコード解析ツールをを走らせるためにpre-commitの設定を行います。

リポジトリの初期化

次に`.pre-commit-config.yaml`を作成します。今回は、toxで作成した環境をpre-commitで利用しています。

.pre-commit-config.yaml

```
repos:
  - repo: local
    hooks:
      - id: lint
        name: lint
        entry: bash -c '.tox/lint/bin/ruff check --fix'
        language: system
        types: [python]
      - id: format
        name: format
        entry: bash -c '.tox/lint/bin/ruff format'
        language: system
        types: [python]
      - id: mypy
        name: mypy
        entry: bash -c '.tox/mypy/bin/mypy src tests --ignore-missing-imports --strict-optional --disallow-untyped-defs '
        pass_filenames: false
        language: system
        types: [python]
```

pre-commitのフックをリポジトリにインストールすることで、commit時にLint&format、mypyの型チェックが実行されます。

## CI/CD

今回、以下のタスクを実施するようにGithub Actionsの設定を行いました。

1. github runnerでのテストの実行
2. MKDocsで作成したドキュメントをgithub pagesにデプロイ

### テストの実行

開発ブランチからmainブランチへのPRをトリガーにテストを実行します。  
`.github/workflows/test.yaml`を作成し、以下の内容を記述します。ここでは、複数のバージョンのpythonのテストをrunnner上で並列実行します。

```
name: Test
on:
  pull_request:
    branches:
      - main

permissions:
  contents: read

jobs:
  Test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - name: Install uv
        uses: astral-sh/setup-uv@v3
        with:
          enable-cache: true
      - name: pin python version
        run: uv python pin 3.12
      - name: Install tox-uv
        run: uv tool install tox --with tox-uv
      - name: Run tests
        run:  tox r -p -e py310,py311,py312
```

### mkdocsをgithub pagesにデプロイ

mkdocsで作成されたドキュメントをgithub pagesにデプロイします。以下のワークフローを実行すると、mainにマージされるタイミングで新たにgh-deployブランチが作成・更新されます。

.github/workflows/deploy-docs.yml

```
name: Deploy Docs
on:
  push:
    branches:
      - main
permissions:
  contents: write
jobs:
  deploy-docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: pip install mkdocs mkdocs-material
      - run: mkdocs gh-deploy --force
```

最後にgithubリポジトリのsettings/pagesのBranchを以下のように`gh-pages`に変更すると、github pagesにMKDocsで生成したサイトがデプロイされます。

[![Screenshot from 2024-11-24 07-07-49.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3941105%2Fc3982aa7-9d3e-093b-4115-2fa7b14d8707.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=81b3422dc5d02e7acf950ac32825c710)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3941105%2Fc3982aa7-9d3e-093b-4115-2fa7b14d8707.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=81b3422dc5d02e7acf950ac32825c710)

## まとめ

本記事では、uvをベースにプロジェクト管理、コードの品質管理、CI/CDの設定を行いました。各種ツールが統合されたり、高速なものに置き換わり、シンプルな方法で快適に管理できるようになってきていますね。今回、紹介した内容のコードは以下のリポジトリにあります。本記事の内容はベストプラクティスではないと思いますので、より良い方法、設定等がありましたら、コメントをお願いします。