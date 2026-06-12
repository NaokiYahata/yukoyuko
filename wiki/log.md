---
title: Log
type: log
updated: 2026-06-12
---

# Log — 時系列の活動記録

append-only。新しいエントリは末尾に追記する。各エントリは次の形式で始める:

```
## [YYYY-MM-DD] <op> | <タイトル>
```

`<op>` = `ingest` | `query` | `lint` | `release` | `decision` | `note`
直近の流れ: `grep "^## \[" wiki/log.md | tail -5`

---

## [2026-06-12] note | プロジェクトWikiテンプレートを初期化
- 3レイヤー構成（raw / wiki / wiki/_schema.md）とリリースモデル（backlog + リリースハブ）をセットアップ。
- 次のアクション: `/project-init` でプロジェクト固有設定と最初のリリース月を記入する。

## [2026-06-12] note | プロジェクト初期化: ゆこゆこアプリ（新規アプリ企画・開発）
- ゴール: ゆこゆこの新規スマホアプリを企画・開発しリリース。当面は要件整理・仕様策定。役割は開発／ベンダー側。
- 初回リリース月: 未定（決まり次第 overview.md に記録）。
- 設定内容: `{{DATE}}` を 2026-06-12 へ置換（_templates/ は保持）／CLAUDE.md プロジェクト固有設定を記入／overview.md を status: active に更新／backlog に初期項目を投入。
- qmd 検索: 有効（コレクション wiki-yukoyuko / wiki-yukoyuko-sources）。
- raw/_originals/ に企画資料(pptx)・質問事項(xlsx)・非機能要件(xlsx)の3点を確認済み。
- 次のアクション: `/wiki-ingest` で raw/_originals/ の3資料を取り込み、overview の背景・thesis・主要機能を更新する。

## [2026-06-12] ingest | 初回3資料の取り込み（企画/質問回答/非機能要件）
- 抽出:
  - raw/yukoyuko-app-plan.md（元: ゆこゆこアプリ.pptx）
  - raw/app-questions-260527.md（元: アプリ質問事項_ゆこゆこ記載（260527）.xlsx）
  - raw/non-functional-requirements-mvp.md（元: 非機能要件資料.xlsx）
- 作成したソース要約: [[20260612-yukoyuko-app-plan]], [[20260527-app-questions]], [[20260527-non-functional-requirements]]
- 作成した実体: [[yukoyuko]], [[yukoyuko-app]], [[yukoyuko-net-web]], [[japanet]], [[sauna-ikitai]]
- 作成した概念: [[vision-and-positioning]], [[target-and-monetization]], [[app-web-role-split]], [[core-features]], [[payment-and-points]], [[external-integration]], [[content-moderation-and-operation]], [[non-functional-requirements]], [[development-approach]], [[schedule-and-scope]], [[past-app-lessons]]
- 更新: [[index]], [[overview]]（背景/ゴール/thesis/論点）, [[backlog]]（機能・ADR候補・データギャップに刷新）
- 主な発見: 温泉特化コミュニティ＋予約アプリ。Web=予約/アプリ=ファンベース（予約も必須）、会員共通化・双方向同期。MUSTは宿予約・クチコミ。年内リリース目標（納品10月末→検証11月末→申請12月上旬）。iOS/Android両対応、ネイティブvsクロス両見積り、AWS・3環境。非機能MVPは確定済み（稼働率99%/DAU5,000→50,000/TLS1.2+/通報ブロック必須）。収益=送客手数料、KPI=お客様評価。決済はジャパネット基盤想定、ポイント制度は意向のみ。
- 矛盾の扱い: 質問票で「同時接続想定値は未定」だが非機能資料がDAU想定を提示 → 非機能資料（共通条件として配布）を採用と明記（[[non-functional-requirements]]）。
- 次に取り込むべき: キックオフ会の議事録・資料（過去アプリの教訓・既存資産との関係などが「共有済み」で未取り込み＝データギャップ）。

## [2026-06-12] ingest | 出所訂正: 主体=VACAN／質問票は別ベンダー作成
- 訂正内容（新規ソースではなく既存理解の修正）:
  1. 本Wikiの主体（開発側ベンダー）は **VACAN**。
  2. 質問票 [[20260527-app-questions]] は VACAN作成ではなく、別ベンダー（[[prior-vendor]]）が作成した質問にゆこゆこ様が回答したもの。VACANは内容の共有を受けている立場。
- 作成: [[vacan]], [[prior-vendor]]
- 更新: [[20260527-app-questions]]（出所注意書き追加）, [[overview]], [[yukoyuko]], [[index]]
- 主な示唆: 質問者の意図・キックオフ口頭共有など、VACANが直接持たない文脈が存在しうる（既知のデータギャップを補強）。複数ベンダー比較の可能性（Q37）。
