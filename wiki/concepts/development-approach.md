---
title: 開発方針・技術スタック・体制
type: concept
tags: [tech, development, infra]
created: 2026-06-12
updated: 2026-06-12
sources: [20260527-app-questions, 20260527-non-functional-requirements]
status: active
---

# 開発方針・技術スタック・体制

## 定義 / 論点
技術スタック、開発手法、インフラ、環境構成、デザイン・テストの進め方。

## 現在の理解
- 対象プラットフォーム: **iOS / Android 両方**（[[20260527-app-questions]] Q18）。
- 技術指定: iOS=Swift/Xcode、Android=Kotlin/AndroidStudio（Q4）。
- 開発手法: **ネイティブとクロスプラットフォーム（Flutter/React Native等）の両方の見積り**を希望。発注側はネイティブのみの経験（Q19）→ 手法選定はこちらの提案・見積り比較が前提。
- インフラ: **AWS**希望（Q6）。スモールスタート（拡張性は持たせつつ最小構成で初期費用を抑える）も選択肢。DAU想定は[[non-functional-requirements]] B-03。
- 環境構成: **DEV / STG / PROD の3環境**で合意（Q39）。
- デザイン: **完全ゼロベースでの自由提案（選択肢①）**（Q5）。ロゴ使用時はデータ提供あり（Q53）。方向性は初回打ち合わせの説明が全て（Q38重複）。
- 管理画面: 施設/運営向け管理画面は**不要**（Q20）。
- モニターテスト: 開発工程への組み込みは**不可**（行う場合は外部依頼）（Q59）。
- 分析: Webでは Contentsquare を使用（Q36）。アプリの分析ツールは未指定。
- 体制: 要件定義フェーズで週1回・2ヶ月前後のMTG（[[schedule-and-scope]]）。

## 未解決の問い・矛盾
- ネイティブ vs クロスプラットフォームの最終選定（両見積り比較の結果待ち）。
- AWS構成の規模（スモールスタート構成 vs DAU50,000耐性）の確定。
- アプリ側の分析ツール選定。

## 関連
- [[overview]] / [[index]] / [[non-functional-requirements]] / [[schedule-and-scope]]
