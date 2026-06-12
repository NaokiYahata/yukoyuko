---
title: ゆこゆこアプリ（新規アプリ）
type: entity
tags: [product, app]
created: 2026-06-12
updated: 2026-06-12
sources: [20260612-yukoyuko-app-plan, 20260527-app-questions, 20260527-non-functional-requirements]
status: active
---

# ゆこゆこアプリ（新規アプリ）

- **種別**: 成果物（開発対象のスマートフォンアプリ）
- **一行サマリ**: 温泉特化のコミュニティ＋予約アプリ。本プロジェクトの開発対象そのもの。

## 概要
「温泉ならゆこゆこ」を体現し、温泉好きが集うファンベースを形成する温泉特化のコミュニティアプリ。同時に温泉宿の予約フローも備える。iOS / Android 両対応のネイティブアプリ（クロスプラットフォームも見積り比較対象）。対象施設は温泉旅館のみ、ターゲットは国内居住者、対応言語は日本語のみ。既存Web（[[yukoyuko-net-web]]）とは会員を共通化し、データを双方向同期する。

## 役割・関係
- 発注: [[yukoyuko]]。ベンチマーク: [[sauna-ikitai]]。
- 役割分担: Web=予約サービス、アプリ=ファンベース（[[app-web-role-split]]）。
- 主要機能・MUST機能: [[core-features]]。
- 技術・開発条件: [[development-approach]]。非機能要件: [[non-functional-requirements]]。
- 決済・ポイント: [[payment-and-points]]（決済は[[japanet]]基盤想定）。
- 過去にもアプリが存在したがクローズ済み（[[past-app-lessons]]）。

## 関連
- [[overview]] / [[index]]
