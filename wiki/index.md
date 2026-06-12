---
title: Index
type: index
updated: 2026-06-12
---

# Index — Wikiカタログ

Wiki全ページのカタログ。`/wiki-ingest` のたびに更新する。
クエリ応答時はまずここを読んで関連ページを特定し、そこから掘る。
（`_schema.md` / `_templates/` などメタ情報はここに載せない）

## Overview
- [[overview]] — プロジェクト全体像と現在のthesis・現在のリリースサイクル

## Backlog
- [[backlog]] — 未割当の要求・アイデアの受け皿

## Releases（リリース）
_(まだありません。初回リリース月が確定したら `releases/YYYY-MM.md` を追加。年内＝2026-12目安だが未確定)_

## Sources（生ソース要約）
- [[20260612-yukoyuko-app-plan]] — 企画資料（キックオフ）: ビジョン・コンセプト・スケジュール
- [[20260527-app-questions]] — アプリ質問事項と回答（全63問）。質問作成元は別ベンダー、内容のみVACANに共有
- [[20260527-non-functional-requirements]] — 非機能要件 参考資料（MVP, v1.0）

## Entities（実体）
- [[vacan]] — 開発ベンダー＝本Wikiの主体（我々）
- [[prior-vendor]] — 質問票を作成した別ベンダー（名称未確認）
- [[yukoyuko]] — 発注企業。温泉宿予約サービスを運営
- [[yukoyuko-app]] — 開発対象の新規アプリ（温泉コミュニティ＋予約）
- [[yukoyuko-net-web]] — 既存の温泉宿予約Webサイト（リニューアル進行中）
- [[japanet]] — 決済基盤の提供元として想定される事業者／グループ
- [[sauna-ikitai]] — ベンチマークとする温泉/サウナ系コミュニティアプリ

## Concepts（概念・論点）
- [[vision-and-positioning]] — 「温泉でNo.1」ビジョンと差別化（お客様評価No.1）
- [[target-and-monetization]] — 国内居住者向け・送客手数料・KPI
- [[app-web-role-split]] — Web=予約/アプリ=ファンベース、会員共通化・双方向同期
- [[core-features]] — 主要機能・MUST（宿予約・クチコミ）・MVPスコープ候補
- [[payment-and-points]] — アプリ内決済（ジャパネット基盤想定）・ポイント制度（未確定）
- [[external-integration]] — 顧客管理システム（自社開発）連携、UIUX提案先行
- [[content-moderation-and-operation]] — UGCモデレーション・運用体制・権限
- [[non-functional-requirements]] — MVP非機能要件（IPA 6項目）
- [[development-approach]] — 技術スタック・ネイティブvsクロス・AWS・3環境
- [[schedule-and-scope]] — 年内リリース目標・マイルストーン・フェーズ・予算
- [[past-app-lessons]] — 過去アプリの経緯と教訓（データギャップ）

## Decisions（意思決定記録 / ADR）
_(まだありません。技術選定・スコープ確定などの判断が出たら追加)_
