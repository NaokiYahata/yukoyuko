---
title: Log
type: log
updated: {{DATE}}
---

# Log — 時系列の活動記録

append-only。新しいエントリは末尾に追記する。各エントリは次の形式で始める:

```
## [YYYY-MM-DD] <op> | <タイトル>
```

`<op>` = `ingest` | `query` | `lint` | `release` | `decision` | `note`
直近の流れ: `grep "^## \[" wiki/log.md | tail -5`

---

## [{{DATE}}] note | プロジェクトWikiテンプレートを初期化
- 3レイヤー構成（raw / wiki / wiki/_schema.md）とリリースモデル（backlog + リリースハブ）をセットアップ。
- 次のアクション: `/project-init` でプロジェクト固有設定と最初のリリース月を記入する。
