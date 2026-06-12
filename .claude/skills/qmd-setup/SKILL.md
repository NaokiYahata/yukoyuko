---
name: qmd-setup
description: Wiki検索エンジン qmd のインストールとセットアップを行う。qmd は markdown 用のローカル検索（BM25/ベクトル/ハイブリッド+リランク）。collection 登録・embed・MCP連携まで設定する。「qmdをセットアップ」「検索を使えるようにして」「qmd install」と言われたとき、または wiki-query で qmd 未導入が判明したときに使う。
---

# qmd-setup — Wiki検索エンジンのセットアップ

[qmd](https://github.com/tobi/qmd) は markdown ファイル向けのローカル検索エンジン（BM25 / ベクトル / ハイブリッド+LLMリランク、すべてオンデバイス）。
Wikiが育つと index.md だけでは探しきれなくなるため、`wiki/`（必要なら `raw/`）を qmd で検索可能にする。

## 前提

- **Node.js >= 22** または **Bun >= 1.0**
- **macOS**: SQLite拡張のため `brew install sqlite` が必要
- 初回利用時にモデルが自動DL（合計 ~2GB が `~/.cache/qmd/models/` にキャッシュ）

## 手順

1. **インストール状況を確認**
   ```bash
   qmd --version || echo "qmd 未インストール"
   ```

2. **インストール**（未導入なら。人間に確認のうえ実行）
   ```bash
   npm install -g @tobilu/qmd
   # または: bun install -g @tobilu/qmd
   # 都度実行でよければ: npx @tobilu/qmd <cmd>
   ```
   macOSでSQLite未導入なら先に `brew install sqlite`。

3. **コレクションを登録**（このプロジェクトのWikiを対象に）
   ```bash
   qmd collection add ./wiki --name wiki
   # 抽出した生ソースも検索したい場合:
   qmd collection add ./raw --name raw
   ```

4. **コンテキストを付与**（検索精度向上、任意）
   ```bash
   qmd context add qmd://wiki "プロジェクトWiki: 要約・実体・概念・意思決定・リリース・backlog"
   qmd context add qmd://raw "抽出済みの生ソーステキスト"
   ```

5. **埋め込み生成**
   ```bash
   qmd embed
   ```

6. **動作確認**
   ```bash
   qmd query "テスト検索したいトピック" -c wiki --json -n 5
   ```

## MCPサーバ連携（任意・推奨）

CLIシェルアウトの代わりに、qmd を Claude Code のネイティブツールとして使える。
`.claude/settings.json`（プロジェクト）または `~/.claude/settings.json`（ユーザー全体）に追加:

```json
{
  "mcpServers": {
    "qmd": { "command": "qmd", "args": ["mcp"] }
  }
}
```

> 注意: この設定をコミットすると、qmd 未インストールのteammateで起動時エラーになりうる。
> チーム共有テンプレートでは `~/.claude/settings.json`（個人）への追加を推奨し、プロジェクトには含めない。

MCPサーバは `query` / `get` / `multi_get` ツールを公開する。常駐させるなら:
```bash
qmd mcp --http --daemon   # localhost:8181 で常駐 / 停止は qmd mcp stop
```

## 運用メモ
- 新しいソースを取り込んだら `qmd update`（再インデックス）→ `qmd embed` の順で再実行してインデックスを更新する（`qmd embed` だけでは新規ファイルが検索に入らない。`/wiki-ingest` の手順にも含まれる）。
- 検索は `wiki-query` から利用する。導入後は CLAUDE.md の「プロジェクト固有設定」に「検索: qmd 有効」と記録しておくとよい。
