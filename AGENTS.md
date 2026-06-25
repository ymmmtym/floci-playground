# floci-playground — AGENTS.md

Docker で動く LocalStack 互換 AWS モックサービス。

## 起動・操作（Taskfile）

```bash
task up        # コンテナ起動 (docker compose up -d)
task down      # 停止
task logs      # ログ tail
task health    # ヘルスチェック
task restart   # 再起動
task clean     # 停止 + データ削除
task reset     # clean → up（フルリセット）
```

AWS エンドポイント: `http://localhost:4566`

## 環境変数

`.mise.toml` で設定済み（エンドポイント・クレデンシャル・リージョン）。`mise` が有効な状態で利用する。

AWS CLI 例: `aws s3api list-buckets --endpoint-url http://localhost:4566`

## 状態データ

`.floci/` 以下に JSON ファイルとして保存（gitignore 済み）。`FLOCI_DATA_DIR` / `FLOCI_STORAGE_MODE` は `compose.yaml` 経由で環境変数により制御可能。デフォルトは `hybrid`。

## このリポジトリの性質

- ビルド・テスト・lint・typecheck 等は存在しない（設定ファイルのみ）
- Docker ソケットをマウントする（Lambda の Docker 実行用）
- 編集対象のコードはない。`.mise.toml` / `compose.yaml` / `Taskfile.yml` が実質的な全内容。
