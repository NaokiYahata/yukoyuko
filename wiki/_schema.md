---
title: Wiki Schema
type: schema
updated: 2026-06-12
---

# Wiki Schema — 構造・規約・ワークフロー定義

このファイルは **Wikiレイヤーの仕様書** であり、AIエージェントがWikiを操作する際の唯一のルールブックです。
Wiki操作（ingest / query / lint など）の前に必ずこのファイルを読むこと。

**エージェント非依存**です。Claude Code 以外のエージェント（例: Codex の `AGENTS.md`）からも、このファイルを参照すれば同じ規律で操作できます。

> このスキーマ自体もプロジェクトと共に進化させてよい。規約を変えたら既存ページとの整合を `/wiki-lint` で確認すること。

---

## 1. 基本思想

RAG（質問のたびに生ソースから断片を再発見する）ではなく、**知識を一度コンパイルして恒久的に最新化し続ける**。

- Wikiは **恒久的で複利的に育つ成果物**。相互リンク・矛盾の指摘・統合済みの考察が常に蓄積されている。
- 人間の仕事: ソースの収集、探索の方向づけ、良い問いを立てること、意思決定。
- AIの仕事: それ以外すべて（要約・相互参照・整理・記帳・矛盾検出・ドラフト生成）。
- **Wiki本文は原則として人間が書かない。** AIが書き、人間はレビューする。
- メタファ: Obsidian = IDE、AI = プログラマ、Wiki = コードベース。

## 2. 3レイヤー・アーキテクチャ

| レイヤー | 場所 | 所有者 | 性質 |
|---|---|---|---|
| **Raw（生ソース）** | `raw/` | 人間 + AIが抽出 | バイナリ原本（pptx/pdf/xlsx/docx）はGit管理せず、抽出した markdown（`raw/<slug>.md`）が真実の出所。抽出後は書き換えない。 |
| **Wiki（知識ベース）** | `wiki/` | AI | AIが全面的に所有・生成・維持。人間は読む。 |
| **Schema（スキーマ）** | `wiki/_schema.md`（このファイル） | 人間 + AI | Wikiの仕様。共進化させる。 |

### ディレクトリ構成

```
wiki/
├── _schema.md        # このファイル（Wikiの仕様）
├── _templates/       # ページ雛形（source / entity / concept / decision / release）
├── index.md          # 全ページのカタログ（コンテンツ指向）。ingestのたびに更新。
├── log.md            # 時系列の追記ログ（append-only）
├── overview.md       # プロジェクト全体像・thesis・★現在のリリースサイクル（可変状態はここに一元化）
├── backlog.md        # 未割当の要求・アイデアの受け皿
├── releases/         # リリース（月）ごとのハブページ（YYYY-MM.md）
├── sources/          # 生ソース1件ごとの要約ページ
├── entities/         # 人物・組織・システム・機能・成果物などの実体ページ
├── concepts/         # 概念・トピック・テーマ・論点のページ
└── decisions/        # 意思決定記録（ADR）
```

`_` 接頭辞のファイル/ディレクトリ（`_schema.md`, `_templates/`）はメタ情報であり、**index.md には載せない**。

### Raw レイヤーの扱い

- バイナリ原本（pptx / pdf / xlsx / docx 等）は `raw/_originals/` に置き、**Git管理しない**（`.gitignore` 済み）。
- `/wiki-ingest` がドキュメントスキル（pdf / pptx / xlsx / docx）でテキストを抽出し、`raw/<slug>.md` として保存する。このmdがGit上の真実の出所。
- 抽出mdの冒頭には元ファイル名と抽出日を記録し、トレーサビリティを保つ。

## 3. ページ規約

### 雛形を使う

新規ページは必ず `wiki/_templates/` の対応する雛形から作る（`source.md` / `entity.md` / `concept.md` / `decision.md` / `release.md`）。

### 共通フロントマター（YAML）

```yaml
---
title: ページタイトル
type: source | entity | concept | decision | release | backlog | overview | index | log | schema
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [source-slug-1]   # 根拠とした生ソース要約ページのslug
release: YYYY-MM           # 任意。このページが紐づくリリース（月）。Dataview / qmd で集計できる
status: draft | active | stale | superseded   # 任意
---
```

**`release` タグ**: decisions / concepts / sources など任意のページに `release: YYYY-MM` を付けると、そのリリースに属する作業として扱える。リリースハブ（`releases/YYYY-MM.md`）から逆引きできる。

### リンク

- ページ間リンクは **`[[ファイル名]]`**（拡張子・パス無しのWikiLink）。例: `[[overview]]`, `[[backlog]]`, `[[2026-07]]`, `[[20260612-kickoff-notes]]`。
- このため **ファイル名はWiki全体で一意にする**こと（Obsidian の WikiLink はファイル名解決のため）。
- リンクは積極的に張る。まだ存在しないページへのリンクも可（作るべきページの目印になる）。
- **ディレクトリへのリンクは張らない**（無効になる）。カテゴリに言及するときは `entities/` のようにコードスパンで書く。

### 引用・根拠

- 主張には必ず根拠（`sources` フロントマター + 本文中の `[[ソース要約slug]]`）を併記する。
- **出所のない断定をしない。** ソースに無いことは「未確認」と明記する。
- 新情報が既存の主張と矛盾する場合、**消さずに矛盾を明示** し、より新しい/信頼できる根拠を示す。

### ファイル名（slug）

- 小文字・ケバブケース。例: `auth-service.md`, `q3-pricing-decision.md`。
- ソース要約は `sources/YYYYMMDD-<short-title>.md`。

## 4. index.md と log.md

### index.md（コンテンツ指向のカタログ）
- カテゴリ（releases / backlog / sources / entities / concepts / decisions）ごとに全ページを列挙。
- 各行: `- [[ファイル名]] — 一行サマリ`。
- **ingestのたびに更新する。** 小規模なうちは index がそのまま検索の入口になる。

### 検索: qmd
- Wikiが育つと index だけでは探しきれないため、ローカル検索エンジン **qmd** を使う（`/qmd-setup` で導入）。
- `wiki/`（必要なら `raw/`）をコレクション登録し、`qmd query "..." -c wiki` で検索する。
- ソース取り込み・ページ還元のたびに `qmd embed` でインデックスを更新する。
- 未導入時は index.md → 関連ページ → `grep` のフォールバックで対応する。

### log.md（時系列の追記ログ）
- **append-only**。エントリは必ず次のプレフィックスで始める:
  ```
  ## [YYYY-MM-DD] <op> | <タイトル>
  ```
  `<op>` = `ingest` | `query` | `lint` | `release` | `decision` | `note`
- 直近の流れ: `grep "^## \[" wiki/log.md | tail -5`

## 5. オペレーション

| 操作 | スキル | 概要 |
|---|---|---|
| Ingest | `/wiki-ingest` | `raw/` の新規ソース（バイナリは抽出）を読み、要約ページを作り、関連ページ・index・logへ波及更新。1ソースで10〜15ページに波及しうる。 |
| Query | `/wiki-query` | qmdでWikiを検索して掘り、引用付きで回答。良い回答はWikiページとして還元。 |
| Lint | `/wiki-lint` | 矛盾・陳腐化・孤立ページ・欠落概念・データギャップの検出。 |
| Project Init | `/project-init` | テンプレートの具体化。プロジェクト固有設定・最初のリリース月の設定・`2026-06-12` 置換。 |
| qmd Setup | `/qmd-setup` | 検索エンジン qmd のインストールとセットアップ。 |

共通原則:
- すべての ingest / query / lint / decision を **log.md に記録** する。
- 大きな編集の前に何をするか一言告げ、編集後は触れたページを列挙する。
- 日付は常に実際の絶対日付を使う（「先週」「来月」を避ける）。

## 6. リリースモデル（イテレーティブ）

このテンプレートは滝モデル（最初に全工程を決める）を採らない。**月次など短いサイクルで「決まったものから順にリリースする」イテレーティブな進行** を前提とする。

### 3つの要素

1. **`backlog.md`** — 未割当の要求・アイデアの受け皿。**最初に全部を詳細化しない。** ここには1行で気軽に貯める。
2. **`releases/YYYY-MM.md`**（リリースハブ）— リリース月が決まったら雛形（`_templates/release.md`）から作る。ゴール・スコープ（やる/やらない）・関連ページ・振り返り・持ち越しを持つ。`status: planning | in-progress | released`。
3. **`release: YYYY-MM` タグ** — decisions / concepts / sources など任意のページに付け、どのリリースの作業かを紐づける。ハブから逆引きできる。

### サイクルの流れ

```
backlog に貯める → 直近リリースだけ詳細化（ハブ作成＋スコープ確定）
→ 関連ページに release タグを付けて作業 → リリース
→ ハブに振り返りを追記し status: released → 未完は backlog/次リリースへ持ち越し
```

- **詳細化するのは直近のリリースだけ。** 先のリリースは backlog の粗い項目のままでよい。
- **現在のリリースサイクルは `overview.md` の「現在のリリースサイクル」セクションのみに記録する**（CLAUDE.md など他の場所に重複させない。可変状態の単一の真実）。
- リリースハブの更新は、`/wiki-ingest` で関連ソースを取り込む際や手動編集で随時行う。
- リリースをまたぐ重要な判断は `decisions/` にADRを残す。

## 7. 出力形式の指針

- 通常はWikiページ（markdown）として還元できる形で。
- 比較は表で。意思決定はADR。スライドは Marp。図は mermaid または matplotlib。
- **良い回答はチャット履歴に消えさせず、Wikiページとして還元する** ことを常に検討する。
