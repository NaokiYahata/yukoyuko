---
title: Backlog
type: backlog
tags: [backlog]
created: 2026-06-12
updated: 2026-06-12
---

# Backlog — 未割当の要求・アイデア

まだリリースに割り当てていない要求・アイデア・やりたいことの受け皿。
**最初に全部を詳細化しない。** ここには1行で気軽に貯め、リリース月が決まったものだけを詳細化する。

各項目は1行で:
- `- [優先度] タイトル — 一言メモ`（優先度の目安: H / M / L）

リリースが決まったら → 該当リリースハブ（`releases/YYYY-MM.md`）の「スコープ」へ移し、
詳細化が必要なら `concepts/` や `decisions/` にページを作って frontmatter に `release: YYYY-MM` タグを付ける。

## 項目

### 機能・スコープ
- [H] 宿を予約する機能 — MUST（[[core-features]]）。アプリ内予約フロー
- [H] クチコミ投稿機能 — MUST（[[core-features]]）。UGC、通報・ブロック必須（[[content-moderation-and-operation]]）
- [H] 会員共通化・Web⇄アプリ双方向同期 — 既存Web会員でログイン、個人情報/予約履歴/お気に入り等を同期（[[app-web-role-split]]）
- [M] 温泉特化の検索・提案体験 — Web絞り込み再現 or 行動シナリオ提案。企画提案で差別化（[[core-features]]）
- [M] コミュニティ機能（意見交換・募集等） — どこまでをMVPに含めるか要検討
- [M] アプリ独自ポイント制度 — 導入意向あり、仕様未確定（[[payment-and-points]]）
- [L] 音声ルーム等リアルタイム機能 — 要否・採否を提案で判断（[[core-features]]）

### 運用・基盤
- [H] UIUX提案（先行タスク） — 顧客管理システムAPI連携より前に進める（[[external-integration]]）
- [M] 社内運営向け権限設計 — 管理者権限＋制限権限の2種（[[content-moderation-and-operation]]）
- [M] アプリ分析ツール選定 — Webは Contentsquare（[[development-approach]]）

### 意思決定が必要（ADR候補 → `decisions/`）
- [H] ネイティブ vs クロスプラットフォーム — 両見積り比較で選定（[[development-approach]]）
- [H] 初回リリース月とスコープの確定 — 年内＝2026-12目安。Release 1/2 の切り分け（[[schedule-and-scope]]）
- [M] AWS構成規模 — スモールスタート vs DAU50,000耐性（[[development-approach]] / [[non-functional-requirements]]）
- [M] 決済基盤 — ジャパネット決済基盤の採否・仕様（[[payment-and-points]]）

### 要入手（データギャップ）
- [H] キックオフ会の議事録・資料 — 過去アプリのクローズ理由/教訓、既存資産との関係等が未取り込み（[[past-app-lessons]]）
- [M] 顧客管理システムのAPI仕様 — UIUX提案後に開示予定（[[external-integration]]）

## 関連
- [[overview]] — 現在のリリースサイクル
- [[index]]
