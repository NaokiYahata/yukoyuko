---
title: コンテンツモデレーションと運用体制
type: concept
tags: [ugc, moderation, operation]
created: 2026-06-12
updated: 2026-06-12
sources: [20260527-app-questions, 20260527-non-functional-requirements]
status: active
---

# コンテンツモデレーションと運用体制

## 定義 / 論点
ユーザー投稿（UGC）の監視・管理、運用主体・権限、データ更新の責任分担。

## 現在の理解
- 投稿フロー: クチコミは**リアルタイム反映**しつつ、運営側で**削除・修正**することがある流れ（[[20260527-app-questions]] Q27）。
- モデレーション体制: **社内で敷く**（Q27）。
- 通報・ブロック機能: **必須**。UGCアプリはApp Store / Google Play審査でも必須要件（[[20260527-non-functional-requirements]] E-05）。
- 宿情報（掲載データ）の更新・メンテナンス: [[yukoyuko]] **社内**で実施（ゆこゆこサイトと同様）（Q28）。施設側が自ら登録する管理画面は不要（Q20）。
- 運用人数: 制限なし、必要に応じ**増員可**（Q29）。
- 権限設計: **管理者権限**（全操作可、システム部門想定）と**制限権限**（一部権限を制限）の2種を用意できればよい（Q30）。

## 未解決の問い・矛盾
- リアルタイム反映と事後削除・修正の運用ルール（NG基準、対応SLA）は未確認。
- 権限の細目（どの操作をどの権限に割り当てるか）は未確認。

## 関連
- [[overview]] / [[index]] / [[core-features]] / [[non-functional-requirements]]
