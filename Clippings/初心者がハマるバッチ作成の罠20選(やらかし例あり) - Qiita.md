---
title: "初心者がハマるバッチ作成の罠20選(やらかし例あり) - Qiita"
source: "https://qiita.com/yoshiizu/items/48d9a9701ba66617eab0?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[yoshiizu]]"
published: 2024-11-18
created: 2024-11-29
description: "初心者がハマるバッチ作成の罠20選バッチ処理は、業務を効率化するために欠かせない技術です。しかし、初心者がバッチ作成に挑戦する際、多くの罠(やらかし)が発生します。本記事では、よくある罠とその…"
tags:
  - "clippings"
---
## 初心者がハマるバッチ作成の罠20選

バッチ処理は、業務を効率化するために欠かせない技術です。  
しかし、初心者がバッチ作成に挑戦する際、多くの罠(やらかし)が発生します。

本記事では、よくある罠とその対策、さらに具体例を交えながら解説します。  
同じミスをしないように、ぜひ参考にしてください！

## 1\. 絶対パスをハードコーディングしてしまう

**罠**: ファイルのパスをコード内に直接書いてしまい、別の環境で動作しなくなることがあります。  
**対策**: 環境変数や設定ファイルを使用して、環境ごとに変更しやすい設計にします。  
**具体例**:  
NG:

```
input_file="/home/user/data/input.csv"
```

OK:

```
input_file="${BASE_DIR}/data/input.csv"
```

## 2\. 実行環境を考慮しない

**罠**: 開発環境と本番環境の設定が異なると、バッチが動かないことがあります。  
**対策**: 環境ごとの設定ファイルやDockerを活用して、環境差をなくします。  
**具体例**: 開発環境ではSQLite、本番ではMySQLを使い、環境変数でDB接続を切り替える。

## 3\. ログ出力を実装しない

**罠**: 処理状況が分からず、原因調査が難航する。  
**対策**: 処理の開始・終了やエラーを適切にログ出力します。  
**具体例**:

```
import logging
logging.basicConfig(filename='batch.log', level=logging.INFO)
logging.info("バッチ開始")
```

## 4\. エラーハンドリングが甘い

**罠**: エラーでバッチ全体が停止する。  
**対策**: 必要に応じてリトライ処理やスキップ機能を実装する。  
**具体例**: try-except で特定処理のみスキップする。

## 5\. 再実行時の影響を考慮しない

**罠**: 再実行でデータが重複する。  
**対策**: 処理済みデータにフラグを付ける、一意制約を利用する。  
**具体例**: 基本的には上記の対策は、設計段階で考慮されています。  
バッチで更新日時を用いて処理対象を中止する具体例は以下です(ちょっと複雑です)

```
import sqlite3
from datetime import datetime

# データベースのセットアップ
conn = sqlite3.connect("example.db")
cursor = conn.cursor()

# テーブル作成（例: データには id, content, updated_at, processed フィールドがある）
cursor.execute("""
CREATE TABLE IF NOT EXISTS data (
    id INTEGER PRIMARY KEY,
    content TEXT,
    updated_at DATETIME,
    processed BOOLEAN DEFAULT 0
)
""")
conn.commit()

# サンプルデータ挿入（初回のみ）
sample_data = [
    (1, "Task 1", "2024-11-01 10:00:00", 0),
    (2, "Task 2", "2024-11-10 15:00:00", 0),
    (3, "Task 3", "2024-11-15 12:00:00", 1)  # すでに処理済み
]
cursor.executemany("INSERT OR IGNORE INTO data (id, content, updated_at, processed) VALUES (?, ?, ?, ?)", sample_data)
conn.commit()

# 再実行時の処理
def process_unprocessed_data():
    # 処理対象: processed = 0 のデータのみ選択
    cursor.execute("SELECT id, content FROM data WHERE processed = 0")
    rows = cursor.fetchall()
    
    for row in rows:
        data_id, content = row
        print(f"Processing data ID {data_id}: {content}")
        
        # 処理済みとしてフラグを更新
        cursor.execute("UPDATE data SET processed = 1 WHERE id = ?", (data_id,))
    
    conn.commit()

# 処理を実行
print("=== 初回実行 ===")
process_unprocessed_data()

# 再実行 (processed = 1 のデータはスキップされる)
print("=== 再実行 ===")
process_unprocessed_data()

# 処理後のデータ確認
cursor.execute("SELECT * FROM data")
for row in cursor.fetchall():
    print(row)

# データベース接続を閉じる
conn.close()
```

## 6\. 入力データのバリデーションを省略する

**罠**: 想定外のデータでエラーが発生する。  
**対策**: データ形式や値の範囲を検証する。  
**具体例**: CSVの列数やデータ型を検証し、不正行をログに記録する。

## 7\. 処理結果の確認を怠る

**罠**: 正常終了でも結果がおかしい。  
**対策**: 処理件数や異常データをチェックする仕組みを追加する。  
**具体例**: 処理後の件数と入力件数を比較する。

## 8\. スケジュール管理を忘れる

**罠**: 実行タイミングのズレで影響が出る。  
**対策**: cronやタスクスケジューラを使い、正確に管理する。  
**具体例**:

```
0 3 * * * /path/to/batch.sh
```

## 9\. 並列処理を軽視する

**罠**: 大量データ処理に時間がかかりすぎる。  
**対策**: 並列処理を取り入れる。  
**具体例**: Pythonの concurrent.futures でスレッド分割する。

## 10\. ファイルのロック機構を考慮しない

**罠**: 複数のバッチが同時にファイルを操作してデータが壊れる。  
**対策**: ファイルロックを使用する。  
**具体例**:

```
import fcntl
with open('file.txt', 'w') as f:
    fcntl.lockf(f, fcntl.LOCK_EX)
```

## 11\. バッチの終了コードを確認しない

**罠**: 実行失敗を正常終了と誤認する。  
**対策**: 終了コードを確認し、エラー時に通知を出す。  
**具体例**:

```
bash batch.sh
if [ $? -ne 0 ]; then
  echo "エラーが発生しました"
  exit 1
fi
```

## 12\. デバッグ機能を実装しない

**罠**: 問題箇所の特定に時間がかかる。  
**対策**: デバッグ用ログや簡易実行モードを実装する。  
**具体例**:

```
DEBUG = True
if DEBUG:
print("デバッグモード有効")
```

## 13\. 外部リソースの障害を想定しない

**罠**: APIやDB障害でバッチが停止する。  
**対策**: リトライ処理やバックアッププランを設ける。  
**具体例**: Pythonでリトライ処理を実装する。

## 14\. メモリ使用量を軽視する

**罠**: メモリ不足で処理が停止する。  
**対策**: ストリーム処理やデータの分割処理を導入する。  
**具体例**: チャンク分けでデータを順次処理する。

## 15\. 古いバッチスクリプトを放置する

**罠**: 誰も触れなくなり、修正が困難になる。  
**対策**: バージョン管理を導入し、メンテナンスする。  
**具体例**: Gitでバッチスクリプトを管理する。

## 16\. 他のプロセスへの影響を考えない

**罠**: リソース消費で他のプロセスが遅延する。  
**対策**: 優先度を調整したりリソース制限を設ける。  
**具体例**:

## 17\. 時間依存の処理を明示しない

**罠**: 時間依存ロジックが原因でバグが発生する。  
**対策**: コメントやドキュメントで時間依存を明確にする。  
**具体例**: 「月初のみ処理」など時間依存の処理を明示する。

## 18\. バッチの並列実行を無計画に行う

**罠**: 並列実行で処理順序が崩れ、データ不整合が発生する。  
**対策**: 依存関係や順序を整理する。  
**具体例**: ID範囲ごとに分けて並列実行する。

## 19\. 不必要な出力を残す

**罠**: 不要なログや中間ファイルがストレージを圧迫する。  
**対策**: 古いファイルを定期的に削除する。  
**具体例**:

```
find /path/to/logs -type f -mtime +7 -exec rm {} \;
```

## 20\. テストを怠る

**罠**: 本番環境でしか不具合を発見できない。  
**対策**: 入力データやエッジケースを網羅したテストを実施する。  
**具体例**: Pythonのユニットテストで検証する。

## まとめ

バッチ処理は自動化の要ですが、一つ一つの罠(やらかし)が積み重なるとトラブルの原因になります。本記事を参考にトラブルを未然に防ぎ、効率的なバッチ処理を実現しましょう！