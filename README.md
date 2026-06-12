# ゆこゆこアプリ プロジェクトWiki

[ゆこゆこ](./wiki/entities/yukoyuko.md) の新規スマートフォンアプリ（温泉特化のコミュニティ＋予約アプリ）を企画・開発するプロジェクトの **知識ベース**。開発／ベンダー側の視点で、要件・意思決定・ソースを「複利的に育つWiki」として蓄積します。

> **このプロジェクトについて**
> - **目的**: 「温泉ならゆこゆこ」を体現し、温泉好きのファンベースを形成する新規アプリを企画・開発・リリースする。
> - **役割分担**: Web（[ゆこゆこネット](./wiki/entities/yukoyuko-net-web.md)）＝温泉宿を予約するサービス／アプリ＝温泉のファンベース（ただし予約フローも必須）。
> - **最重要KPI**: アプリのお客様評価（成功像＝評価No.1かつDL50万）。収益は送客手数料。
> - **リリース目標**: 2026年内（納品10月末→受入検証11月末→ストア申請12月上旬）。
> - **現状**: 初回3資料（企画・質問回答・非機能要件）を取り込み済み。詳細は [`wiki/overview.md`](./wiki/overview.md)。

知識は質問のたびにゼロから生ソースを探すRAGではなく、AI（Claude Code）が一度コンパイルして恒久的に最新化し続けます。相互リンク・矛盾の指摘・統合済みの考察が蓄積され、ソースを足すほど・問うほどWikiが賢くなります。

> 人間の仕事 = ソース収集・方向づけ・良い問い・意思決定。AIの仕事 = それ以外（要約・相互参照・整理・記帳・矛盾検出）。

## まず読むべきもの

- [`wiki/overview.md`](./wiki/overview.md) — プロジェクト全体像・thesis・現在のリリースサイクル（**可変状態の単一の真実**）
- [`wiki/index.md`](./wiki/index.md) — 全ページカタログ
- [`wiki/_schema.md`](./wiki/_schema.md) — Wikiの構造・規約・ワークフロー定義（Wikiを操作する前に必読）

Obsidian で `wiki/` フォルダを開くと、グラフビューで知識の形を見ながらブラウズできます（Obsidian = ビューア、Claude = 書き手、Wiki = 成果物）。

## 進め方

1. 新しい資料（pptx/pdf/xlsx/docx など）を `raw/_originals/` に置く。テキスト/mdならそのまま `raw/` へ。
2. Claude Code で **`/wiki-ingest`** を実行 → バイナリは markdown に抽出して `raw/` 保存し、`wiki/` へ波及更新。
3. **`/wiki-query`** でWikiに問う（引用付きで回答、良い回答はページとして還元）。
4. 区切りで **`/wiki-lint`** を実行し、矛盾・陳腐化・孤立ページを点検。
5. リリース月が決まったら `wiki/releases/YYYY-MM.md` を起こし、`overview.md` の「現在のリリースサイクル」を更新。

## 構成（3レイヤー）

| レイヤー | 場所 | 所有者 | 説明 |
|---|---|---|---|
| Raw（生ソース） | `raw/` | 人間 | 元バイナリ（pptx/pdf/xlsx/docx）は**Git管理せず**、抽出した markdown のみコミット。AIは読むだけ。 |
| Wiki（知識ベース） | `wiki/` | AI | AIが生成・維持する相互リンクされたmarkdown群。 |
| Schema（スキーマ） | `wiki/_schema.md` | 人間+AI | Wikiの構造・規約・ワークフロー定義。 |

```
raw/
├── _originals/   元バイナリ（git管理外）   wiki/
├── <slug>.md     抽出済みテキスト          ├── _schema.md  Wikiの仕様（規約）
└── assets/       画像など                  ├── _templates/ ページ雛形
                                            ├── index.md    全ページカタログ
                                            ├── log.md      時系列ログ
                                            ├── overview.md 全体像/thesis/現在のリリース
                                            ├── backlog.md  未割当の要求・アイデア
                                            ├── releases/   リリース(月)ハブ YYYY-MM.md
                                            ├── sources/    ソース要約
                                            ├── entities/   人物/組織/システム
                                            ├── concepts/   概念/論点
                                            └── decisions/  意思決定記録(ADR)
```

## スキル（`/<name>` で起動）

| スキル | 用途 |
|---|---|
| `/project-init` | プロジェクトの初期化（実施済み） |
| `/qmd-setup` | 検索エンジン qmd のインストール・セットアップ（実施済み） |
| `/wiki-ingest` | `raw/` のソース（pptx/pdf/xlsx/docx は抽出）をWikiへ取り込み・波及更新 |
| `/wiki-query` | qmdでWikiを検索し、引用付きで回答・還元 |
| `/wiki-lint` | 矛盾・陳腐化・孤立ページ等の健全性チェック |

## 検索（qmd）

Wikiの検索には [qmd](https://github.com/tobi/qmd)（ローカルのBM25/ベクトル/ハイブリッド検索）を使用。コレクションは `wiki-yukoyuko`（`wiki/`）と `wiki-yukoyuko-sources`（`raw/`）。新規ページを追加したら `qmd update`（再インデックス）→ `qmd embed`（埋め込み）の順で更新します。

## リリースモデル（イテレーティブ）

最初に全工程を決める滝モデルではなく、短いサイクルで回します。

```
backlog に貯める → 直近リリースだけ詳細化（releases/YYYY-MM.md を作りスコープ確定）
→ 関連ページに release: YYYY-MM タグを付けて作業 → リリース
→ ハブに振り返りを追記し status: released → 未完は backlog/次リリースへ持ち越し
```

- **`backlog.md`**: 未割当の要求・アイデアの受け皿（最初に詳細化しない、1行で貯める）
- **`releases/YYYY-MM.md`**: リリース月ごとのハブ（ゴール/スコープ/振り返り/持ち越し）
- **`release: YYYY-MM` タグ**: 任意のページ（decisions/concepts/sources等）を特定リリースに紐づけ

Wikiの規約・ワークフローの詳細は [`wiki/_schema.md`](./wiki/_schema.md) を参照してください。
