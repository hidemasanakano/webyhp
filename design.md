# WEBY 採用LP デザインシステム

**対象**: `index.html`（単一ファイル構成、約3,537行）
**ブランド**: 株式会社WEBY / THE RED EDGE
**スコープ**: 2026年卒 新卒採用LP

| メタ情報 | 値 |
|---------|---|
| Version | 1.1 |
| 最終更新 | 2026-04-22 |
| ベース実装 | `index.html` @ `c47f492` |
| 更新責任 | lp-designer / lp-qa |
| レビュー周期 | 実装変更ごと、または四半期 |

**変更履歴:**
- `v1.0` (2026-04-22): 初版。§1–§9 の基本構成を整備
- `v1.1` (2026-04-22): P0 補強（§1.6 Z-index / §3.4 Motion A11y / §4.0 States / §5 Accessibility 新設、§5–9 繰り下げ）。P1 補強（§1.2 typo token / §2.1 モバイル優先度 / §4.2 CTA 使い分け / §4.1 コピー長 / §4.4.1 カード使い分け / §4.13 コピー・トーン / §6.3–6.5 画像ガイド）。是正タスクを §9 に追加（#6–15）

このドキュメントは `index.html` から抽出した実装事実を元にしたデザインシステム定義。新規実装・改修時の参照原典とする。

---

## 0. 使い方

- 新しいセクション・要素を追加する前に必ず **§1 トークン** と **§4 コンポーネントパターン** を参照する
- インタラクティブ要素を実装する前に **§4.0 States** と **§5 Accessibility** を確認する
- 既存の命名規則（セクション名プレフィックス、§7 参照）に従う
- 新規スタイルを書く前に、§8「共通化候補」に該当するパターンがないか確認する
- ブランドガイドライン（`brand_guidelines.md`）と本ドキュメントに齟齬があるときは、本ドキュメント（実装事実）を優先し、§9 に是正タスクとして記録する

---

## 1. デザイントークン

### 1.1 Color

CSS変数定義（`index.html:21-29`）と、実装で観測された実用パレット。

| トークン | 値 | 用途 |
|---------|---|-----|
| `--weby-red` | `#C0143C` | ブランドレッド。CTA背景、強調テキスト、ボーダーアクセント。静的な赤はこの変数を使う |
| `--pure-black` | `#000000` | 本文色の基調、ダーク背景への反転色 |
| `--pure-white` | `#FFFFFF` | 背景の基調 |
| `--text-gray` | `#555555` | 本文テキスト（デフォルトカラー） |
| `--line-gray` | `#EEEEEE` | 罫線、薄いボーダー、セパレーター |

**拡張パレット（変数化されていないが頻出の値）:**

| 値 | 用途 |
|----|-----|
| `rgba(255, 31, 75, *)` | **動的・透明度付きの赤**（ホバー、グラデ、オーバーレイ）。※`--weby-red`（`#C0143C`）と色相がわずかにズレている点は §9 参照 |
| `#0d0d0d` | ダークセクション背景（FAQ, Footer） |
| `#111` / `#2a2a2a` | 濃い背景（business-section のカードトップ等） |
| `#f9f9f9` / `#FAFAFA` | ライトセクション背景（training, recruit 等） |
| `#f0f0f0` / `#e8e8e8` | グリッドセパレーター、薄い境界 |

**運用ルール:**
- 不透明な赤は `var(--weby-red)` を使う
- 透明度付きの赤は `rgba(255, 31, 75, x)` を使う（既存パターンに合わせる）
- ダーク背景の反転表現は `#0d0d0d` を使う（`#000` は使わない）

### 1.2 Typography

| トークン | 値 | 用途 |
|---------|---|-----|
| `--font-en` | `'Montserrat', sans-serif` | 英数字・セクションラベル・タグ・CTA |
| `--font-serif` | `'Noto Serif JP', serif` | 日本語本文・日本語見出し・クォート |

**ロード元**: Google Fonts `Montserrat: 400/700/900`, `Noto Serif JP: 300/400/700/900`（`index.html:15-17`）

**Font-size スケール**（観測された代表値）:

| サイズ | 用途 |
|--------|-----|
| `4.8rem` | Hero h1 |
| `3.2–3.8rem` | セクション h2 |
| `2rem` | カード見出し / サブ h2 |
| `1.8rem` | カード見出し |
| `1.1rem` | 本文ベース・セクションラベル |
| `1rem` | UI要素 |
| `0.9–0.95rem` | 本文小・補足 |
| `0.7–0.75rem` | タグ・キャプション（letter-spacing 広め前提） |
| `10rem–22vw` | 背景装飾テキスト（`::before` の `OPERA` `BUSINESS` `CEO` 等） |

**Font-weight 使い分け:**
- `900`: 見出し・ラベル・CTA（デフォルトの強調。英数で多用）
- `700`: 日本語見出し・本文強調
- `400`: 本文

**Letter-spacing パターン:**

| 値 | 用途 |
|---|-----|
| `0.6em` | セクションラベル（`.m-script` 等） |
| `0.4em` | タグ・極小ラベル |
| `0.1em` | 英字 h2 |
| `0.05em` | 日本語見出しの微調整 |

**Line-height:**
- body: `1.9`
- 見出し: `1.25–1.8`
- 本文読ませる: `2.0–2.5`

#### トークン化提案（現状は直書き、将来の変数化案）

現在 font-size は全て数値直書き。以下の変数化で命名できれば一貫性が取りやすい。導入は**非破壊的リファクタ**扱い（§8 共通化候補の延長）。

```css
:root {
  --fs-hero:    4.8rem;   /* Hero h1 */
  --fs-h2:      3.2rem;   /* セクション h2（標準） */
  --fs-h2-lg:   3.8rem;   /* セクション h2（大） */
  --fs-card:    1.8rem;   /* カード見出し */
  --fs-body-lg: 1.1rem;   /* 本文・ラベル */
  --fs-body:    1rem;     /* UI・本文小 */
  --fs-caption: 0.9rem;   /* 補足 */
  --fs-tag:     0.75rem;  /* タグ・極小ラベル */
}
```

**使用ルール（導入後）:**
- 新規実装は必ず変数経由で指定
- 既存の直書きは「当該セクションを触る時についでに置換」で漸進移行
- レスポンシブ時の縮小は `clamp()` との組合せ推奨（例: `font-size: clamp(2rem, 5vw, var(--fs-h2));`）

### 1.3 Spacing

**セクション（垂直）:**

| 値 | 用途 |
|---|-----|
| `200px 0` | message-section（最広） |
| `160px 0` | 標準セクション |
| `120px 0` | タブレット以下での標準置換 |
| `80px 0` | compact / モバイル |

**コンテナ:**
- `max-width: 1260px`
- `padding: 0 40px`
- `margin: 0 auto`

**コンポーネント内 padding（代表）:**
- カードトップ: `48px 48px`
- カルーセル情報: `80px 70px`（デスクトップ）/ `28px 32px`（コンパクト）
- モーダルボックス: `80px 70px`
- テーブル行: `28px 32px`

**Gap:**
- セクション間要素: `40px`
- カード間: `20–24px`
- 密集グリッド: `6px`
- フロー矢印ベース: `0`（疑似要素で矢印）

### 1.4 Radius / Shadow

**Border-radius:**
- `2px`: ボタン（CTA）— ほぼ角を落とさないミニマル
- `6px`: カード・画像・Job Board card・Recruit wrap

**Shadow:**
- `0 4px 15px rgba(255, 31, 75, 0.2)`: CTA（フッター）
- `0 4px 20px rgba(0, 0, 0, 0.08)`: カード（Job Board 等）

### 1.5 Motion / Timing

**Transition の標準 duration:**
- `0.3s`: UI hover（色・padding・scale）
- `0.4s`: モーダル・ナビスライドイン
- `0.5s ease`: ヘッダー scroll 変化
- `0.6–0.7s`: カルーセル・画像 transform
- `1.2s cubic-bezier(0.16, 1, 0.3, 1)`: `.reveal` スクロール表示（プロジェクト標準イージング）
- `1.5s ease`: 背景ゆっくり変化

**標準イージング:**
- `cubic-bezier(0.16, 1, 0.3, 1)`: `.reveal` 専用（ease-out-expo 系）
- `cubic-bezier(0.25, 0.46, 0.45, 0.94)`: カルーセル・ハンバーガー（ease-out-quad 系）
- `cubic-bezier(0.4, 0, 0.2, 1)`: ライトボックス（Material standard）

### 1.6 Z-index レイヤー

実装で使われている全ての z-index を分類したレイヤーシステム。新規要素は必ず以下のいずれかに揃え、中間値を勝手に作らない。

| レイヤー名 | z-index | 用途 | 実装例 |
|----------|---------|------|-------|
| content | `1` | セクション内コンテンツを背景装飾より前に置く | `.biz-cat-top`, section 直下の `z-index:1` インライン |
| content-high | `2` – `3` | フロー矢印等の重ね順制御 | `.training-flow-card::before/after` |
| container | `10` | コンテナ・主要コンテンツ層 | `.container`, `.hero-content`, `.worker-info`, `.m-budo` |
| overlay-hint | `20` | ホバーヒント、scroll indicator | `.worker-hover-hint`, hero scroll line |
| mobile-nav | `999` | モバイルスライドインメニュー | `#nav` モバイル展開時 |
| header | `1000` | 固定ヘッダー | `header` |
| header-toggle | `1001` | ヘッダー上のハンバーガー | `.hamburger` |
| modal | `9999` | モーダル・ライトボックス（最前面） | `.wmodal-overlay`, `.lightbox-overlay` |

**ルール:**
- 上記以外の値（例: `500`, `1500`, `10000`）は禁止
- 新しいレイヤーが必要な場合は、本表に追加してから実装
- 将来的にはトークン化（`--z-header: 1000;` 等）したいが、現状は数値直書きを踏襲

---

## 2. ブレークポイント

**戦略**: Desktop-first（デスクトップ基準から段階的に縮小）

| ブレークポイント | 位置 | 主な役割 |
|----------------|------|---------|
| `max-width: 1024px` | `index.html:1876` | タブレット。grid→flex、2col→1col、section padding 160→120px |
| `max-width: 768px` | `index.html:2007` | スマホ。ハンバーガー有効化、大型見出し縮小、padding 大幅削減、training photos の负マージン解除 |
| `max-width: 480px` | `index.html:2558` | 小型スマホ。モーダル・ライトボックス・カード高さの微調整 |

**新規コンポーネント追加時の必須対応:**
- 最低 `@media (max-width: 1024px)` と `@media (max-width: 768px)` の2段は必ず書く
- `@media (max-width: 480px)` は必要なときのみ（極小調整用）

### 2.1 モバイル優先度原則（残す / 落とす / 差し替える）

モバイル（≤768px）は採用LPの主要チャネル（就活生のスマホ閲覧率が高い）。スクリーン面積が限られるので、要素ごとに優先度を決める。

| 優先度 | 方針 | 対象 |
|-------|-----|------|
| **必ず残す** | レイアウトを崩してでも表示 | Hero コピー・ENTRY CTA・ナビ（ハンバーガー経由）・事業内容・社員紹介・募集要項・エントリーフォーム・フッター連絡先 |
| **縮小して残す** | サイズ・余白・フォント圧縮 | セクションヘッダー、カード（1カラム化）、写真、FAQ、研修フロー |
| **構造変換** | グリッド → 縦積み、横フロー → 縦フロー、矢印 → `↓` | `.biz-categories`, `.training-flow`, `.career-steps`, `.recruit-wrap` |
| **装飾は落として良い** | 視覚ノイズを削除 | 背景大型テキスト（`::before` の `BUSINESS` `CEO` `FAQ`）、パララックス、`trainingFloat` 系のfloat アニメーション、`budoWrite` 装飾 |
| **差し替えが望ましい** | モバイル専用アセット | hero メインバナー（縦長クロップ版）、カルーセル画像（正方形トリミング） |

**実装ルール:**
- 装飾の `display: none` は `@media (max-width: 768px)` で指定して良い
- 「必ず残す」要素は絶対に `display: none` しない
- 「差し替え」は `<picture>` + `<source media="...">` を推奨（現状未使用、§6.2 参照）

---

## 3. アニメーション

### 3.1 `.reveal` — スクロール表示の標準

```css
.reveal { opacity: 0; transform: translateY(30px); transition: all 1.2s cubic-bezier(0.16, 1, 0.3, 1); }
.reveal.is-visible { opacity: 1; transform: translateY(0); }
```

- IntersectionObserver で threshold `0.1` 到達時に `.is-visible` を付与（`index.html:3374-3375`）
- **新規の「見せたい要素」には必ず `.reveal` を付与**

### 3.2 Keyframes 一覧

| 名前 | 行 | 用途 |
|------|---|-----|
| `scrollLineAnim` | `:205` | Hero のスクロール指示赤バー |
| `lightboxIn` | `:322` | ライトボックス出現（scale + opacity） |
| `trainingFloat` | `:764` | Training photos 浮遊 |
| `trainingFloatSlow` | `:768` | Training photos 浮遊（回転付） |
| `trainingScale` | `:772` | Training main photo 呼吸 |
| `trainingSlideIn` | `:776` | Training main photo 初期表示 |
| `trainingFadeUp` | `:780` | Training sub photos 順次表示（stagger） |
| `budoWrite` | `:1727` | 「武運」装飾テキスト（`-webkit-text-stroke` の色遷移） |

### 3.3 Hover パターン（繰り返し）

- 画像拡大: `transform: scale(1.05–1.06)` + `transition: 0.6–1.2s`
- カード浮上: `transform: translateY(-4px)` + shadow 強化
- テキストシフト: `padding-left: +10px` + color→red
- アイコン回転: `rotate(180deg)`（FAQ アコーディオン）

### 3.4 Motion Accessibility（`prefers-reduced-motion`）

`.reveal`、カルーセル、`budoWrite`、`trainingFloat` 等のアニメーションは、前庭障害・めまい・注意障害を持つユーザーには負荷となる。以下の media query を**必須**実装とする。

```css
@media (prefers-reduced-motion: reduce) {
  .reveal {
    opacity: 1;
    transform: none;
    transition: none;
  }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
  .carousel-track { transition: none; }
  html { scroll-behavior: auto; }
}
```

**現状**: 未実装（§9 の P0 是正タスクに登録）
**実装推奨位置**: `<style>` 末尾、または `@keyframes` 群の直後
**例外**: どうしても動きを見せたい装飾（`scrollLineAnim` の赤バー）は、静止画に差し替えではなく、`animation-duration` を延長して存在感を弱める手もある

---

## 4. コンポーネントパターン

### 4.0 State の標準パターン（全インタラクティブ要素共通）

全ての「クリック・タップ・フォーカス可能な要素」は以下の states を定義する。欠落はアクセシビリティ上の欠陥となる。

| State | トリガー | 必須要件 | 実装例 |
|-------|---------|---------|-------|
| default | — | ベーススタイル | すべてのコンポーネント |
| hover | `:hover` | ポインタ操作時の視覚フィードバック | `.nav-entry:hover`, `.worker-card:hover` |
| **focus** | `:focus-visible` | **キーボード操作時の可視アウトライン**（未実装） | 全リンク・ボタン・モーダルclose |
| active | `:active` | 押下の瞬間的フィードバック | CTA, モーダルボタン |
| 展開/選択 | `.open` / `.active` / `.is-visible` | JS による切替ステート | FAQ, lightbox, reveal, carousel dot |
| disabled | `[aria-disabled="true"]` | `opacity: 0.5; cursor: not-allowed;` | 必要時（現在 form が無いので使用シーン限定） |

**Focus の標準実装（プロジェクト規約）:**

```css
:focus-visible {
  outline: 2px solid var(--weby-red);
  outline-offset: 3px;
  border-radius: 2px;
}

/* ダーク背景上の要素用 */
.faq-q:focus-visible,
.wmodal-close:focus-visible,
header.scrolled nav a:focus-visible {
  outline-color: #fff;
}

/* デフォルト :focus のアウトライン消去は禁止 */
```

**適用必須コンポーネント一覧:**
- `.nav-entry` / footer CTA ボタン
- nav `<a>` リンク全て（PC・モバイル両方）
- `.hamburger`
- `.carousel-btn` / `.carousel-dot`
- `.faq-q`（FAQ 質問行）
- `.worker-card`（onclick を持つため）
- `.jb-card`
- `.wmodal-close` / `.lightbox-close`
- `.gallery-item`（onclick を持つ場合）

**現状**: `:focus` / `:focus-visible` の明示実装はゼロ。ブラウザデフォルト outline に依存しており、赤や黒の CTA ではコントラスト不足で不可視。§9 の P0 是正タスク。

---

### 4.1 セクションヘッダー（全セクション共通）

**構造:**
```html
<span class="m-script">LABEL_EN</span>
<h2>日本語タイトル<em>（赤強調）</em></h2>
```

**スタイル基準:**
- `.m-script`: `font-weight: 900; letter-spacing: 0.6em; color: var(--weby-red); font-size: 1.1rem;`
- `h2`: `font-size: 3.2rem; font-weight: 700; color: #111; letter-spacing: 0.1em;`

**該当セクション**: MESSAGE, ENVIRONMENT, OUR BUSINESS, TRAINING, WORKERS, RECRUIT, FAQ, JOBBOARD

**コピー長ルール:**
- `.m-script`（英字ラベル）: **1〜2 単語、最大 15 文字**（`OUR BUSINESS` はギリ、`WHAT WE DO TODAY` は長すぎ）
- `h2`（日本語タイトル）: **全角 15 文字以内**。2行になる場合は `<br>` で意図的に改行
- `<em>` 赤強調は **h2 内で1箇所のみ**（複数赤は弱くなる）

> ⚠️ 共通化候補 §8.A

### 4.2 CTAボタン（ENTRY）

**種類と使い分け:**

| バリアント | 見た目 | 使用シーン | 禁止事項 |
|----------|-------|----------|---------|
| **Nav 内 (`.nav-entry`)** | ミニマル、`padding: 12px 35px; border-radius: 2px; background: var(--weby-red);` | ヘッダー常駐 CTA、ページ上部のクイックエントリー | 本文中に流用しない |
| **Footer / Primary** | 上記 + `box-shadow: 0 4px 15px rgba(255, 31, 75, 0.2);` + `padding: 16px 40px;` | ページ最下部・セクション末尾の最終 CTA、強い誘導が必要な場所 | Nav 内に使わない（浮いてしまう） |

共通: テキストは `color: #fff !important; font-weight: 900; letter-spacing: 0.3em; font-family: var(--font-en);`

**1ページ内の配置ルール:**
- **必須位置**: ヘッダー右上（Nav 内）、フッター直前（Primary）、最下部（Primary）
- **推奨位置**: Hero 内（Primary サイズ、半透明背景上に配置可）
- **禁止**: 本文中への3つ以上の連続配置（選択肢過多で決定回避を招く）
- **色**: ブランド赤以外で CTA を作らない。どうしても二次 CTA が必要なら「アウトライン版」を追加提案してから実装

**二次 CTA（将来追加時の提案）:**
- `background: transparent; border: 2px solid var(--weby-red); color: var(--weby-red);`
- 資料DL、会社説明会予約など「エントリー」以外の行動用

### 4.3 ビジネスカード（`.biz-*` プレフィックス）

- 2カラムグリッド（`grid-template-columns: repeat(2, 1fr); gap: 24px;`）
- カードトップ: `linear-gradient(135deg, #111 60%, #2a0008 100%)` + `padding: 48px`
- `::before` に `attr(data-num)` で大型ナンバー（`10rem`, `rgba(255,31,75,0.12)`）
- ホバーで `.biz-service` が `padding-left: +10px`、名前色が赤に

### 4.4 ワーカーカード（`.worker-*`）+ モーダル（`.wm-*` `.wmodal-*`）

**カード:**
- `height: 750px;`（`index.html:897`）、3カラムグリッド（`grid-template-columns: repeat(3, 1fr); gap: 20px;`）
- 画像: `width:100%; height:100%; object-fit: cover; transition: 1.2s;`
- `::after` で底部グラデーションオーバーレイ（`rgba(0,0,0,0.85) → transparent 60%`）
- `.worker-hover-hint`: scale(0.8)→1 + opacity 0→1 on hover
- クリックで `openWorker(i)` → モーダル起動

**モーダル:**
- `.wmodal-overlay`: `position: fixed; inset: 0; background: rgba(0,0,0,0.85);`
- `.wmodal-box`: `width: 90%; max-width: 760px; padding: 80px 70px;`
- データは JS の `workerData` 配列から動的生成

### 4.4.1 カード系の使い分け

LP 内で「カード」と呼べるコンポーネントは複数あり、目的が重複すると保守性が落ちる。以下の用途で使い分ける。

| コンポーネント | 用途 | 中身 | クリック先 |
|--------------|-----|-----|----------|
| `.biz-category` | 事業領域（2 つまで） | 数字・サービス名・説明 | なし（情報提示） |
| `.worker-card` | 社員紹介（3 名×複数列） | 人物写真・肩書・クォート | モーダル（詳細表示） |
| `.carousel-slide` | 社員ストーリー（順次閲覧） | 大判写真・長文インタビュー | なし（スライド移動） |
| `.jb-card` | 外部求人媒体へのリンク | バナー画像のみ | 外部サイト |
| `.faq-item` | Q&A（展開型） | 質問・回答 | 自身を展開 |
| `.r-row` | 募集要項（表） | ラベル・値 | なし（情報提示） |

**選択フロー（新規カード追加時）:**

1. 情報提示だけか？ → `.r-row`（表形式）か `.biz-category`（箱型）
2. 人物紹介か？ → 短い＝`.worker-card`、長い＝`.carousel-slide`
3. 外部誘導か？ → `.jb-card`
4. 展開型 Q&A か？ → `.faq-item`
5. 上記どれでもない → **新規カードを作る前に本表の追加提案**を先行させる（勝手に新種を生やさない）

### 4.5 カルーセル（`.carousel-*`）

- トラック: `transition: transform 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);`
- スライド: `grid-template-columns: 1fr 1fr; min-height: 680px;`
- 画像側: `::after` に右方向グラデ（`transparent 60% → white 100%`）
- クォート: `border-left: 3px solid var(--weby-red);`
- 制御: `.carousel-btn` + `.carousel-dots`（`.active` で現在位置表示）

### 4.6 FAQ（`.faq-*`、ダーク版が実運用）

> ※ ライト版（`index.html:1169-1218`）は旧実装。**ダーク版（`:1347-1504`）を使うこと**。

- 背景: `#0d0d0d`
- 質問クリックで `.faq-item.open` を toggle → `max-height` 展開
- アイコン: `.faq-icon` の `::before/::after` が `+/-` を表現、回転でトグル

### 4.7 Recruit（`.r-*`）— 表型カード

- 外枠: `grid-template-columns: 1fr 1fr; gap: 2px; background: #e8e8e8;`（gap を罫線として見せる）
- 行: `.r-row` = `background: #fff; padding: 28px 32px;`
- 横長行: `.r-row.r-wide` = `grid-column: 1/3;`

### 4.8 Job Board（`.jb-*`）— 画像カード

- `height: 220px; border-radius: 6px; box-shadow: 0 4px 20px rgba(0,0,0,0.08);`
- `.jb-card-overlay`: 底部グラデ + opacity 0→1 on hover

### 4.9 Lightbox（ギャラリー画像拡大）

- `position: fixed; inset: 0; background: rgba(0,0,0,0.92);`
- 画像: `max-width: 90vw; max-height: 88vh; object-fit: contain;`
- 表示: `animation: lightboxIn 0.3s cubic-bezier(0.4,0,0.2,1);`
- Escape キーで閉じる

### 4.10 Header / Navigation

- デフォルト: `.top-transparent`（高さ 90px、透明、ロゴに drop-shadow）
- スクロール後: `.scrolled`（高さ 75px、`background: rgba(255,255,255,0.95); backdrop-filter: blur(25px);`）
- ナビリンク: `font-family: var(--font-en); font-weight: 800; font-size: 0.75rem; letter-spacing: 0.3em;`
- モバイル（≤768px）: ハンバーガー → `position: fixed; right: -100% → 0; width: 80%; max-width: 320px;`

### 4.11 Training Flow（矢印フロー）

- 複数カード横並び（`display: flex; gap: 0;`）
- カード間の矢印は **CSS border trick**（`::after` の `border-top/bottom: 50px solid transparent; border-left: 20px solid #fff;`）
- 最終カードのみ `background: red;` で強調

### 4.12 背景装飾テキスト（セクション共通パターン）

- `.business-section::before`, `.ceo-section::before`, `.faq-section::before` 等が、それぞれ `"BUSINESS"` `"CEO"` `"FAQ"` を大型表示
- 共通スペック: `font-size: 18–22vw; font-weight: 900; color: rgba(0,0,0,0.03);`（視認性ぎりぎり）

> ⚠️ 共通化候補 §8.B

### 4.13 コピー・トーンガイド（lp-copywriter 向け）

採用LPのコピーは「力強く、野心的、誠実」（`brand_guidelines.md`）を基本方針とする。本節はその具体運用。

#### 4.13.1 文字数の上限（要素別）

| 要素 | 推奨文字数 | 絶対上限 | 備考 |
|-----|----------|---------|------|
| Hero 縦書きコピー | 8〜14 文字 | 18 文字 | 一呼吸で読める長さ |
| Hero サブコピー | 15〜25 文字 | 35 文字 | 1行収まり |
| `.m-script`（英ラベル） | 1〜2 単語 | 15 文字 | 空白含む |
| `h2`（セクションタイトル） | 8〜15 全角 | 20 全角 | 2行なら `<br>` 明示 |
| `.biz-cat-top-title` | 10〜20 全角 | 28 全角 | カードヘッダ |
| `.biz-service-desc` | 40〜80 全角 | 120 全角 | 2〜3行想定 |
| `.worker-quote` | 15〜30 全角 | 40 全角 | 一言の印象 |
| `.carousel-quote`（大判） | 30〜60 全角 | 100 全角 | 写真と並立 |
| `.faq-q-text` | 15〜40 全角 | 60 全角 | 1問1要点 |
| `.faq-a-text` | 80〜200 全角 | 400 全角 | 改行 `<br>` 可 |
| `.r-data`（募集要項値） | 事実ベース | — | 装飾語禁止 |

#### 4.13.2 トーン & ボイス

**採用する表現:**
- 力強い動詞（「創る」「挑む」「超える」「切り拓く」「賭ける」）
- 一人称・二人称の直接話法（「ジブン」「君」「あなた」）
- 短く区切るリズム（体言止め、読点を減らす）
- 具体数字（「平均年齢25歳」「成長率230%」「120日休日」）

**避ける表現:**
- 業界内ジャーゴン（「KPI」「PDCA」「ソリューション」「シナジー」）— 就活生には届かない
- 権威主義語（「弊社は〜」「〜させていただきます」）— 距離を作る
- 抽象語の羅列（「成長」「挑戦」「革新」だけ並べる）— 無内容に聞こえる
- 絵文字・記号装飾（ブランド一貫性を損なう）

**赤強調（`<em>`）の使い方:**
- タイトルで**1箇所のみ**、最も届けたい1語に付ける
- 「未来を創るのは、<em>ジブン</em>だ。」のように**主語や目的語**に当てる
- 動詞・修飾語に付けると弱くなる

#### 4.13.3 英字ラベル（`.m-script`）の命名基準

- **大文字 + 単語スペース区切り**（例: `OUR BUSINESS`, `PEOPLE`, `RECRUIT`）
- 冠詞は原則省略（`THE` は例外的に「THE RED EDGE」等の固有名のみ）
- カンマ・句読点禁止
- 1〜2 単語に絞る（Montserrat + letter-spacing 0.6em で長文は破綻）

#### 4.13.4 禁則処理

- 行末に助詞のみを残す「ダンス改行」を避ける（CSS `word-break: keep-all` or `<br>` で意図的改行）
- 長い英字カタカナ（「コンサルティングファーム」など）は文中で折り返さないよう `<span style="white-space: nowrap;">` で保護

---

## 5. Accessibility

採用LPは求職者にリーチしないと事業KPIに直撃する。本節は「努力目標」ではなく**実装要件**として扱う。目標準拠: WCAG 2.1 AA。

### 5.1 コントラスト（WCAG AA）

**最低基準**: 本文 4.5:1 / 大型テキスト（18pt 以上 or 14pt bold 以上） 3.0:1。

| 組合せ | 比率 | 判定 | 用途 |
|-------|------|------|------|
| `#000` on `#FFFFFF` | 21.0:1 | ✓ AAA | 見出し・本文 |
| `#555` (`--text-gray`) on `#FFFFFF` | 7.5:1 | ✓ AAA | 本文 |
| `#C0143C` (`--weby-red`) on `#FFFFFF` | 5.9:1 | ✓ AA | 赤いテキスト・アクセント |
| `#FFFFFF` on `#C0143C` | 5.9:1 | ✓ AA | CTA ボタン内文字 |
| `#FFFFFF` on `#0d0d0d` | 19.5:1 | ✓ AAA | ダーク背景上のテキスト |
| `rgba(255,255,255,0.8)` on `#0d0d0d` | ~15:1 | ✓ AAA | 半透明本文 |
| `rgba(255,255,255,0.5)` on ダーク画像上 | 不定 | ⚠️ 要確認 | hero テキスト（画像次第） |

**禁止:**
- `#AAA` 以上の明度を本文テキストに使う
- 画像オーバーレイなし（半透明の黒レイヤーなし）で画像上にテキストを直置き
- `color` のみで情報を伝える（エラー・成功・リンク）

### 5.2 キーボードナビゲーション

**必須対応:**
- 全インタラクティブ要素が `Tab` で到達可能
- `:focus-visible` アウトラインをブランド色で明示（§4.0 参照）
- モーダル / ライトボックス / モバイルメニュー展開中は**フォーカストラップ**（Tab が裏側に逃げない）
- `Escape` キーでモーダル・ライトボックス・モバイルメニューを閉じる
- カルーセルは左右矢印キーで移動（推奨）

**現状の実装状況:**

| 項目 | 状態 |
|------|------|
| `Escape` でライトボックスを閉じる | ✓ 実装済 |
| `Escape` でモーダルを閉じる | 要確認 |
| モーダルのフォーカストラップ | ✗ 未実装（P0） |
| `:focus-visible` 全要素対応 | ✗ 未実装（P0） |
| カルーセルのキーボード操作 | ✗ 未実装（P1） |
| モバイルメニューのフォーカストラップ | ✗ 未実装（P1） |

### 5.3 ARIA と Semantic HTML

**インタラクティブコンポーネント別の必須 ARIA:**

| コンポーネント | 必須属性 |
|--------------|---------|
| モーダル (`.wmodal-overlay`) | `role="dialog"`, `aria-modal="true"`, `aria-labelledby="wm-name"` |
| ライトボックス | `role="dialog"`, `aria-modal="true"`, `aria-label="画像拡大表示"` |
| FAQ 質問 (`.faq-q`) | `aria-expanded="true/false"`, `aria-controls="faq-a-id"` |
| FAQ 回答 (`.faq-a`) | `id="faq-a-id"`, `role="region"` |
| カルーセルトラック | `aria-label="社員ストーリー"`, `aria-live="polite"` |
| カルーセルドット | `aria-current="true"`（アクティブ時のみ） |
| ハンバーガー (`.hamburger`) | `aria-expanded="true/false"`（JS で切替）, `aria-controls="nav"` |
| アイコンのみボタン | `aria-label` 必須 |
| 装飾のみの画像 | `alt=""` + `role="presentation"` |

**現状**: `aria-label="Menu"` が `.hamburger` にあるのみ。他は全て未実装（§9 P0/P1 タスク）。

### 5.4 Motion Accessibility

§3.4 参照。`prefers-reduced-motion: reduce` 未実装は P0。

### 5.5 外部リンク

- `target="_blank"` を付けるリンクには `rel="noopener noreferrer"` を必ずセットする
- スクリーンリーダー向けに「新しいタブで開く」旨を `aria-label` に含めるか、視覚非表示テキスト（`.sr-only`）で伝える

**現状**: mynavi 外部リンクに `rel="noopener"` のみ（`noreferrer` 欠如）。他の外部リンクも監査対象。

### 5.6 画像 alt テキスト

| 画像の性質 | alt の書き方 |
|----------|-------------|
| 装飾画像（背景、グラデ下の写真等） | `alt=""` （空文字）+ `role="presentation"` |
| 内容を伝える画像（社員、オフィス、図解） | 内容を簡潔な日本語で記述 |
| リンクを兼ねる画像 | リンク先の目的を記述 |
| ロゴ | `alt="WEBY"`（現状通り） |

**現状**: 全画像に `alt` あり。ただし「LOBBY」「研修風景」等英字 or 短文のため、装飾/内容の区別を監査要。

### 5.7 対応優先度（accessibility 是正タスク）

| P | 項目 | 関連 § |
|---|------|-------|
| P0 | `:focus-visible` 全インタラクティブ要素に適用 | §4.0 |
| P0 | `prefers-reduced-motion` メディアクエリ実装 | §3.4 |
| P0 | モーダル `role="dialog"` + `aria-modal` + フォーカストラップ | §5.3 |
| P0 | FAQ `aria-expanded` + `aria-controls` | §5.3 |
| P1 | ハンバーガー `aria-expanded` の動的切替 | §5.3 |
| P1 | カルーセル ARIA とキーボード操作 | §5.2/5.3 |
| P1 | 外部リンク `rel="noopener noreferrer"` 統一 | §5.5 |
| P2 | 装飾画像の `alt=""` 仕分け | §5.6 |
| P2 | コントラスト自動検証（Pa11y / axe）を CI に組込 | §5.1 |

---

## 6. アイコン / アセット

### 6.1 アイコンライブラリ

- **Font Awesome 6.5.0**（`index.html:19`）— 実装で使用。`<i class="fa-solid fa-*">` で記述
- **Lucide**（`index.html:18`）— ロードされているが主用途は `lucide.createIcons()` 初期化のみ

> 新規アイコンは Font Awesome を優先。

### 6.2 画像パス規則

| ディレクトリ | 用途 |
|-------------|-----|
| `./photos/` | ロゴ、メインバナー、全体写真 |
| `./facility_photos/` | オフィス・設備（※`facility photos/` のスペース版も存在、§9 参照） |
| `./member_photos/` | メンバー写真 |
| `./ceo_photo/` | CEO 写真 |
| `./service_pics/` | サービス関連画像 |
| `./trial_photos/` | トライアル・雰囲気写真 |

**ルール:**
- 画像を追加するときは `_` 版（アンダースコア）を使う
- 相対パス `./` を必ず付ける
- ファイル名は**半角英数とアンダースコアのみ**（日本語・全角数字・スペース禁止）

### 6.3 画像ガイドライン（アスペクト比・サイズ・`object-fit`）

各コンポーネントが要求する表示サイズと、推奨する画像アスペクト比。

| コンポーネント | 表示サイズ（デスクトップ） | 推奨アスペクト比 | `object-fit` |
|--------------|------------------------|---------------|------------|
| Hero 背景 | 100vw × 100vh | 16:9 以上の横長（`3:2` 以上推奨） | `cover` |
| Worker card | 1col 幅 × `750px` 固定 | 2:3（縦長ポートレート） | `cover` |
| Carousel image | 50% × `700px` | 1:1 or 4:5 | `cover` |
| Gallery item | 可変 × `450px` | 3:2 | `cover` |
| Facility thumbnail | タイル可変 | 4:3 | `cover` |
| CEO portrait | 50% × `900px` | 4:5（縦） | `cover` |
| Job Board card | カラム幅 × `220px` | 16:9 バナー | `cover` |
| Lightbox 拡大 | `max 90vw × 88vh` | オリジナル維持 | `contain` |
| ロゴ | 自動 × `28px` | 正方 or 横長 | — |

**切り抜き時の配慮:**
- 人物写真は**顔が中心〜上寄り**に来るよう元画像を撮影／トリミング
- 必要に応じて `object-position: center top;` 等で固定点を指定
- `cover` 使用時は元画像のアスペクト比を厳守（縦長素材を横長枠に入れると頭や足が切れる — 既知事故あり、§9 履歴参照）

### 6.4 画像重量・フォーマット

**現状の問題（監査結果）:**

| ファイル | サイズ | 判定 |
|---------|-------|-----|
| `photos/sales.jpg` | 20 MB | ✗ 即座に圧縮必要 |
| `photos/営業 (3).jpg` | 20 MB | ✗ 即削除（日本語ファイル名かつ重複） |
| `photos/mainbanner.png` | 4.8 MB | ✗ 要圧縮 |
| `trial_photos/IMG_1548.JPG` | 6.4 MB | ✗ 要圧縮 |
| `trial_photos/IMG_1638.JPG` | 5.9 MB | ✗ 要圧縮 |

**重量ルール（新規追加時の上限）:**

| 用途 | フォーマット | 最大サイズ（目標） |
|-----|-----------|-----------------|
| Hero メインバナー | WebP / AVIF | **300 KB** |
| Worker / CEO 人物 | WebP | **150 KB** |
| Gallery / facility | WebP | **200 KB** |
| サムネイル・カード小 | WebP | **80 KB** |
| ロゴ | SVG or PNG | **20 KB** |

**フォーマット優先順位:**
1. **SVG** — ロゴ・アイコン・図解（可能なら常に）
2. **AVIF** — 写真（対応ブラウザが主流、`<picture>` fallback 前提）
3. **WebP** — 写真（AVIF 未対応ブラウザ向け fallback）
4. **JPEG** — 最終 fallback
5. **PNG** — 透過必須の時だけ（透過無しなら WebP/JPEG）

**実装パターン（`<picture>` 活用）:**

```html
<picture>
  <source type="image/avif" srcset="./photos/hero.avif">
  <source type="image/webp" srcset="./photos/hero.webp">
  <img src="./photos/hero.jpg" alt="..." loading="lazy" width="1920" height="1080">
</picture>
```

**必須属性:**
- `loading="lazy"` — ファーストビュー外の画像全てに（Hero 背景は例外で eager）
- `width` / `height` 属性 — CLS（Cumulative Layout Shift）対策。CSS で size 指定していても HTML 属性は残す
- `decoding="async"` — 装飾画像に推奨

### 6.5 レスポンシブ画像（将来提案）

現状は単一サイズのみ。将来的には `srcset` で解像度別に提供する:

```html
<img src="./photos/hero-1200.webp"
     srcset="./photos/hero-600.webp 600w,
             ./photos/hero-1200.webp 1200w,
             ./photos/hero-1920.webp 1920w"
     sizes="(max-width: 768px) 100vw, 1200px"
     alt="..." loading="lazy">
```

モバイル専用クロップ版は `<picture><source media="(max-width: 768px)">` で差し替え（§2.1 参照）。

---

## 7. 命名規則

### 7.1 セクション名プレフィックス（BEM 風、ハイフン短縮形）

1セクション = 1プレフィックス。セクション内部の子要素は全部そのプレフィックスを持つ。

| プレフィックス | セクション |
|--------------|----------|
| `biz-` | Business |
| `training-` | Training |
| `carousel-` | Workers Carousel |
| `worker-` | Workers card |
| `wm-` / `wmodal-` | Worker Modal |
| `faq-` | FAQ |
| `r-` | Recruit |
| `jb-` | Job Board |
| `g-` / `gallery-` | Facility Gallery |
| `m-` | Message |
| `ceo-` | CEO |
| `news-` | News Bar |
| `hero-` | Hero |

### 7.2 グローバル・ユーティリティ

- `.reveal` / `.is-visible`: スクロール表示
- `.container`: max-width ラッパー
- `.nav-entry`: CTA
- `.hamburger` / `.logo`

### 7.3 ステートクラス

| クラス | 意味 |
|--------|-----|
| `.scrolled` / `.top-transparent` | header 状態 |
| `.is-visible` | `.reveal` の可視状態 |
| `.active` | カルーセルドット、モーダルオーバーレイ |
| `.open` | FAQ 展開、ライトボックス表示 |

### 7.4 命名の原則

- 新規セクションを作るときは 2〜8文字のプレフィックスを決め、内部要素はすべてそれを使う
- **汎用ユーティリティクラスは基本作らない**（セマンティックな命名を優先）
- グローバルで再利用するものだけ短い命名を許容

---

## 8. 共通化候補（リファクタリング機会）

### 8.A セクションヘッダーパターン
**複数セクションで同一構造が繰り返される**（§4.1）。
→ `.section-header` / `.section-label` / `.section-title` の共通クラス化を検討。

### 8.B 背景装飾大型テキスト
`.business-section::before` / `.ceo-section::before` / `.faq-section::before` が同じスペック（§4.12）。
→ 共通 mixin または `.section-bg-text` クラスで統一。

### 8.C カード hover 効果
`.biz-service:hover` / `.worker-card:hover` / `.jb-card:hover` / `.training-photos > div:hover` が類似パターン。
→ `.card-hover-lift` / `.card-hover-scale` ユーティリティ化検討。

### 8.D グラデーションオーバーレイ
`.hero-bg`, `.gallery-item::after`, `.worker-card::after`, `.carousel-img::after`, `.jb-card-overlay` がすべて類似の暗→透過グラデ。
→ `.gradient-overlay-bottom` / `.gradient-overlay-right` 共通化検討。

### 8.E 2つのFAQ実装が併存
ライト版（`:1169-1218`）とダーク版（`:1347-1504`）の両方が CSS に残っている。
→ ライト版を削除して整理。

---

## 9. 既知のズレ・是正タスク

実装と他資料との間の齟齬。新規実装時はこの節を確認し、必要なら是正する。

| # | ズレ | 内容 | 推奨対応 |
|---|-----|-----|--------|
| 1 | ブランド赤の色相 | CSS変数 `--weby-red: #C0143C`（赤寄り）と rgba で使われる `#FF1F4B`（ピンク寄り）が異なる。`brand_guidelines.md` と `CLAUDE.md` は `#FF1F4B` を指定 | ブランド決裁で片方に統一。統一後、変数1つで管理 |
| 2 | ディレクトリ名の二重化 | `facility photos/` と `facility_photos/`、`member photo/` と `member_photos/` が両方存在 | `_` 版に統一、スペース版を削除 |
| 3 | FAQ 実装が2系統併存 | ライト版（旧）とダーク版（新）の両方が CSS に残存 | ライト版を削除 |
| 4 | `text/キャッチコピー` が空 | 参照元テキストが未記入 | 原稿を書くか、他ファイルに統合 |
| 5 | エージェント定義の絶対パスが古い | `.claude/agents/lp-*.md` が `/Users/togashi/Desktop/会社LP/` を参照 | 現在のプロジェクトルートに書き換え |
| 6 | **`:focus-visible` 全要素未実装**（P0 / A11y） | キーボードユーザーにフォーカス位置が見えない | §4.0 の標準実装を CSS に追加 |
| 7 | **`prefers-reduced-motion` 未実装**（P0 / A11y） | 動きに敏感なユーザーへの配慮ゼロ | §3.4 のメディアクエリを追加 |
| 8 | **モーダル ARIA + フォーカストラップ未実装**（P0 / A11y） | スクリーンリーダー非対応、Tab が背景に逃げる | §5.3 参照 |
| 9 | **FAQ `aria-expanded` 未実装**（P0 / A11y） | 開閉状態がスクリーンリーダーに伝わらない | §5.3 参照 |
| 10 | ハンバーガー `aria-expanded` 動的切替未実装（P1） | 同上（モバイルメニュー） | `.hamburger` クリック時に toggle |
| 11 | 外部リンク `rel="noopener noreferrer"` が不統一（P1） | mynavi は `noopener` のみ | 全外部リンクに `noopener noreferrer` 付与 |
| 12 | **画像が過大**（P0 / Performance） | `sales.jpg` 20MB、`mainbanner.png` 4.8MB 等。モバイル回線で致命的 | §6.4 の重量ルールに従い圧縮・WebP 化 |
| 13 | 日本語ファイル名の画像が存在（P1） | `営業 (3).jpg`, `メインバナー.JPG` 等 | 半角英数ファイル名に統一、参照 HTML も更新 |
| 14 | `<picture>` によるモバイル画像差し替え未実装（P2） | 全デバイスで同一画像配信 | §6.5 に従い段階導入 |
| 15 | `width` / `height` 属性が `<img>` に無い（P1 / CLS） | Cumulative Layout Shift が発生 | 全画像に HTML 属性として追加 |

---

## 10. 参考情報

- `brand_guidelines.md` — 演出コンセプト "Ethereal & Energetic"、セクション構成案
- `CLAUDE.md` — ハーネス構成、エージェントチーム役割分担
- `.claude/skills/lp-build/SKILL.md` — オーケストレーター実行規則

本ドキュメントは実装（`index.html`）を一次ソースとする。実装を変更したら本ドキュメントを更新すること。
