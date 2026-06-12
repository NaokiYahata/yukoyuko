---
title: ゆこゆこネット（既存Web）
type: entity
tags: [system, web, existing]
created: 2026-06-12
updated: 2026-06-12
sources: [20260612-yukoyuko-app-plan, 20260527-app-questions]
status: active
---

# ゆこゆこネット（既存Web）

- **種別**: システム（既存の自社Webサービス）
- **一行サマリ**: 温泉宿を予約する既存Webサイト。稼働中でリニューアルが進行中。

## 概要
[[yukoyuko]] が運営する既存の温泉宿予約Webサイト。会員登録・ログイン機能、予約履歴、お気に入り等を持つ。現在リニューアルが進行中。新アプリとは会員アカウントを共通化し、個人情報・予約履歴・旅の記録/投稿・お気に入り設定などを双方向同期する想定。分析には Contentsquare を利用。クーポン等の施策も運用。

## 役割・関係
- アプリとの役割分担: Web=「温泉宿を予約するサービス」、アプリ=「温泉のファンベース」（[[app-web-role-split]]）。
- 会員共通化・双方向同期の対象（[[app-web-role-split]]）。
- 宿情報・コンテンツ更新は[[yukoyuko]]社内で実施（[[content-moderation-and-operation]]）。
- 顧客管理システム（自社開発）と連携（[[external-integration]]）。

## 関連
- [[overview]] / [[index]]
