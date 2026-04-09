---
name: lp-build
description: "株式会社WEBY 会社LP（index.html）の構築・編集・改善を行うオーケストレータースキル。「LPを修正して」「セクションを追加して」「コピーを改善して」「デザインを変えて」「LPを更新して」「再実行」「ブラッシュアップ」などLPに関するあらゆる変更・改善依頼で必ずこのスキルを使うこと。ローカルサーバー(http://localhost:8080)でプレビュー中のページに即座に反映させる。"
---

# LP Build — オーケストレーター

## プロジェクト概要

- **ファイル**: `/Users/togashi/Desktop/会社LP/index.html`（単一ファイル構成）
- **ブランド**: 株式会社WEBY / THE RED EDGE / `#FF1F4B` red + black/white
- **用途**: 2026年卒 新卒採用LP
- **プレビュー**: http://localhost:8080（Python http.server 起動中）

## アセットディレクトリ

| パス | 内容 |
|------|------|
| `./photos/` | ロゴ、メインバナー、全体写真 |
| `./facility photos/` | オフィス・設備写真 |
| `./member photo/` | メンバー写真 |
| `./service pics/` | サービス関連画像 |
| `./text/` | 採用メッセージ、事業内容、理念等のテキスト原稿 |
| `brand_guidelines.md` | ブランドガイドライン |

## Phase 0: コンテキスト確認

1. `_workspace/` が存在するか確認する
   - **存在 + 部分修正要求** → 該当エージェントのみ再実行
   - **存在 + 新規要求** → `_workspace_prev/` にリネームし新規実行
   - **未存在** → 初期実行

## Phase 1: 要求分析

1. ユーザーの要求を以下のカテゴリに分類する:
   - **デザイン/レイアウト変更** → `lp-designer` が主担当
   - **コピー/テキスト改善** → `lp-copywriter` が主担当
   - **新セクション追加** → `lp-copywriter`（コピー）→ `lp-designer`（実装）の順
   - **全体ブラッシュアップ** → 全エージェント協働

2. 変更対象セクションを特定する:
   - Hero / Message / Environment / Business / Workers / Recruit / Footer

## Phase 2: エージェント実行

### パターンA: デザイン変更のみ

```
Agent(lp-designer, model=opus) → lp-qa 検証
```

### パターンB: コピー + デザイン（推奨: パイプライン）

```
Agent(lp-copywriter, model=opus)  ←コピー生成
       ↓ コピー確定
Agent(lp-designer, model=opus)    ←HTML実装
       ↓ 実装完了
Agent(lp-qa, model=opus)          ←品質検証
```

### パターンC: 全体改善（エージェントチーム）

TeamCreate → TaskCreate → 並列実行 → 統合

## Phase 3: QA & 確認

1. `lp-qa` エージェントで検証を実施
2. 問題があれば該当エージェントに差し戻し
3. ユーザーに変更箇所のサマリーを報告
4. プレビューURL: **http://localhost:8080** を案内

## エラーハンドリング

- **画像ファイルが見つからない** → `./photos/`, `./facility photos/`, `./member photo/` を Glob で確認し正しいパスを使用
- **スタイル競合** → 既存 CSS クラスを優先し、新規クラスは `--weby-red` 変数を継承
- **文字化け** → `<meta charset="UTF-8">` が存在することを確認

## テストシナリオ

### 正常フロー
1. 「Heroセクションのコピーを改善して」
   - `lp-copywriter` がバリエーション案を生成
   - `lp-designer` が `index.html` に適用
   - `lp-qa` が確認 → 完了

### エラーフロー
1. 存在しない画像パスが指定された場合
   - `lp-designer` が `./photos/` を Glob で確認
   - 最も近いファイル名を使用、またはユーザーに確認

## 変更履歴

変更は `CLAUDE.md` の変更履歴テーブルに記録する。
