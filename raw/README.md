# raw/ — 生ソース（テキスト抽出レイヤー）

ここはプロジェクトの **真実の出所（source of truth）** です。ただし **Gitで管理するのは markdown テキストのみ** です。

## 方針

- 元データ（pptx / pdf / xlsx / docx などのバイナリ原本）は **Git管理しない**（`.gitignore` 済み）。
- `/wiki-ingest` がバイナリからテキストを抽出し、**`raw/<slug>.md` として保存する**。このmdがGit上の真実の出所になる。
- **AIは `raw/` のmdを読むだけで、決して書き換えません。** 編集・整理・要約はすべて `wiki/` 側で行われます。

## 置き方

| 種類 | 置き場所 | Git管理 |
|---|---|---|
| バイナリ原本（pptx/pdf/xlsx/docx 等） | `raw/_originals/` | ✗（ignore） |
| 抽出済みテキスト | `raw/<slug>.md` | ✓ |
| 既にテキスト/markdownの資料 | `raw/<slug>.md` に直接置く | ✓ |
| 画像など添付 | `raw/assets/` | 任意 |

## 取り込みフロー

1. バイナリ原本を `raw/_originals/` に置く（または既存のテキストを `raw/` に置く）。
2. Claude Code で **`/wiki-ingest`** を実行。
   - バイナリは pdf / pptx / xlsx / docx のドキュメントスキルで markdown へ抽出し `raw/<slug>.md` に保存。
   - 続けてWikiへ統合（要約ページ作成・関連ページ波及・index/log更新）。

> 抽出mdは原本へのトレーサビリティのため、フロントマターに元ファイル名を記録します（`/wiki-ingest` が行う）。
