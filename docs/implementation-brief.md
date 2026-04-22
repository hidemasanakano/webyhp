# 実装ブリーフ — 全オープン Issue + コンテンツアイデアの詳細仕様

**対象**: 株式会社WEBY 新卒採用LP（2027年卒向け）
**作成**: 2026-04-22
**位置づけ**: 各 Issue を実装する際の **ワイヤーフレーム・本文案・クリエイティブ指示** を網羅した設計書。
**関連ドキュメント**:
- `design.md` — 現行実装のデザインシステム
- `docs/lp-content-ideas.md` — 未決裁アイデアの置き場
- 本書 — **決裁が取れた後、実装者がそのまま動ける仕様**

---

## 目次

### Part A: 決裁のみで完了する Issue（実装コンテンツ軽微）
- [A-1 #1 ブランド赤色決裁](#a-1-1-ブランド赤色決裁)
- [A-2 #3 空ファイル処理](#a-2-3-空ファイル処理)
- [A-3 #4 エージェントパス修正](#a-3-4-エージェントパス修正)

### Part B: コンテンツ実装（Visual + 本文）
- [B-1 #56 Hero コピー刷新](#b-1-56-hero-コピー刷新)
- [B-2 #57 ミニ CEO パネル](#b-2-57-ミニ-ceo-パネル)
- [B-3 #58 内定者の声](#b-3-58-内定者の声)
- [B-4 #59 FAQ 拡充](#b-4-59-faq-拡充)
- [B-5 #63 Job Board 配置](#b-5-63-job-board-配置)
- [B-6 #68 News Bar 整理](#b-6-68-news-bar-整理)

### Part C: 計測・調査基盤
- [C-1 #64 GA4/GTM 導入](#c-1-64-ga4gtm-導入)
- [C-2 #60 Exit-intent Survey](#c-2-60-exit-intent-survey)
- [C-3 #61 Post-application Survey](#c-3-61-post-application-survey)

### Part D: 新規セクション（docs/lp-content-ideas.md より）
- [D-1 AI Era Manifesto](#d-1-ai-era-manifesto)
- [D-2 WHY 事業コンセプト](#d-2-why-事業コンセプト)
- [D-3 選考フロー図](#d-3-選考フロー図)
- [D-4 JOIN US 3 チャネル](#d-4-join-us-3-チャネル)
- [D-5 通年インターン Sticky Side CTA](#d-5-通年インターン-sticky-side-cta)
- [D-6 note / SNS 連携](#d-6-note--sns-連携)
- [D-7 数字で見る WEBY](#d-7-数字で見る-weby)
- [D-9 オフィス動画ツアー](#d-9-オフィス動画ツアー)
- [D-10 親世代向け FAQ](#d-10-親世代向け-faq)

### Part E: 全体像
- [E-1 新セクションオーダー](#e-1-新セクションオーダー)
- [E-2 実装順序ロードマップ](#e-2-実装順序ロードマップ)

---

# Part A: 決裁のみで完了する Issue

## A-1 #1 ブランド赤色決裁

**論点**: `#C0143C`（WCAG AA 本文可）と `#FF1F4B`（AA 大型のみ可）のどちらをブランド公式とするか。

**推奨判断材料:**
- 現実装: `--weby-red: #C0143C` + rgba は`rgba(192,20,60,*)` に統一済（PR #47）
- `#FF1F4B` はガイド上の公式だが WCAG AA 本文 NG
- 多くの採用LP（特に若年層向け）は**視認性優先**で濃い赤を採用

**決裁後のアクション:**
- A. `#C0143C` を公式化 → 何もしない（現状維持）
- B. `#FF1F4B` を公式化 → `rgba(255, 31, 75, *)` に戻す + 本文の赤テキストは避けるガイド追記

**成果物**: ブランドオーナー承認を本 Issue にコメントで残す

---

## A-2 #3 空ファイル処理

**論点**: `text/キャッチコピー`（0バイト）をどうするか。

**推奨**:
```
現在の Hero キャッチコピー「今日よりも明日、大きな社会課題を解決する。」
+ 新提案（#56 決裁後）を追記する原稿管理ファイルとして活用。
```

**実装**:
```markdown
# キャッチコピー（原稿管理）

## 現行（2026-04-22）
今日よりも明日、大きな社会課題を解決する。

## 次期候補（#56 決裁待ち）
- 案A: ...
- 案B: ...
- 案C: ...

## 履歴
| 日付 | 変更 |
|------|------|
| 2026-04-22 | 初版 |
```

---

## A-3 #4 エージェントパス修正

**置換対象** (3 ファイル、全 9 箇所):

```bash
find .claude/agents -name "*.md" -exec sed -i '' \
  's|/Users/togashi/Desktop/会社LP|/Users/nakano/Desktop/cursor/webyhp|g' {} \;
```

**推奨**: 絶対パスではなく**相対パス**（`./` or `../`）に置換すれば、プロジェクトを移動しても動く。

---

# Part B: コンテンツ実装

## B-1 #56 Hero コピー刷新

### 現行

```
2027 RECRUIT
今日よりも明日、
大きな社会課題を解決する。
```

### 課題

- 事業内容（何をしているか）が 5 秒で伝わらない
- 抽象的すぎて他社との差別化が薄い
- 平均 45 秒の LP 閲覧時間で「この会社は？」の回答にならない

### 候補コピー（3 案）

#### 案 A：事業ダブル明示型（推奨）⭐

```
2027 RECRUIT

今日よりも明日、
より大きな社会課題の解決へ。

士業向け Web コンサルティング × 自社メディア運営
```

- **強み**: 理念 + 具体事業の両取り
- **弱み**: やや情報量多い
- **モバイル 3 行化**: OK（h1 2行、サブ 1行）

#### 案 B：具体成果先出し型

```
2027 RECRUIT

士業の集客課題を、
データと戦略で解決する。

2011年設立・銀座／Web コンサルティング企業
```

- **強み**: 何をしているか最速で伝わる
- **弱み**: 理念要素が薄い（CEO メッセージが弱くなる懸念）

#### 案 C：ターゲット明示型

```
2027 RECRUIT

専門家の集客を、
ジブンの手で加速させる。

弁護士・税理士向け Web コンサルティング企業
```

- **強み**: 「ジブン」採用ブランド固有語を継承
- **弱み**: 「加速」はやや業界語

### HTML 実装（案 A 採用時）

```html
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-content reveal">
    <span class="hero-2026">2027 RECRUIT</span>
    <h1 class="hero-h1">今日よりも明日、<br>より大きな社会課題の解決へ。</h1>
    <p class="hero-sub">士業向け Web コンサルティング × 自社メディア運営</p>
  </div>
</section>
```

### CSS 追加

```css
.hero-sub {
  margin-top: 28px;
  font-family: var(--font-en);
  font-size: 0.9rem;
  letter-spacing: 0.2em;
  color: rgba(255, 255, 255, 0.85);
  font-weight: 700;
}
@media (max-width: 768px) {
  .hero-sub {
    font-size: 0.75rem;
    margin-top: 20px;
    padding: 0 16px;
  }
}
```

### クリエイティブ

- 現行 Hero 画像（オフィス風景）はそのまま使用
- opacity 調整は不要（既存 0.7 で可読性確保済み）

### 受入条件

- [ ] ブランドオーナー or CEO が 3 案から選択 or 修正案提示
- [ ] モバイル幅 375px で 4 行以内
- [ ] design.md §4.13 文字数ルール準拠

---

## B-2 #57 ミニ CEO パネル

### ワイヤーフレーム

**配置**: Hero Stats Strip の直下、News Bar の前

```
┌──────────────────────────────────────────────────────┐
│  FROM CEO                                            │
│                                                      │
│  ┌─────┐                                             │
│  │     │  「より大きな社会課題の解決を。」           │
│  │CEO  │                                             │
│  │写真 │  私たちの事業は、信頼を届ける仕事です。      │
│  │     │                                             │
│  └─────┘  代表取締役 中野 秀征                       │
│                                                      │
│              [ CEO メッセージを読む → ]              │
└──────────────────────────────────────────────────────┘
```

### HTML

```html
<section class="mini-ceo">
  <div class="mini-ceo-inner container reveal">
    <span class="m-script">FROM CEO</span>
    <div class="mini-ceo-content">
      <div class="mini-ceo-photo">
        <img src="./ceo_photo/IMG_2072-600w.webp"
             alt="代表取締役 中野秀征"
             width="600" height="900" loading="lazy">
      </div>
      <div class="mini-ceo-text">
        <p class="mini-ceo-quote">「より大きな社会課題の解決を。」</p>
        <p class="mini-ceo-lead">私たちの事業は、信頼を届ける仕事です。</p>
        <p class="mini-ceo-name">代表取締役 <strong>中野 秀征</strong></p>
        <a href="#ceo-section" class="mini-ceo-link">
          CEO メッセージを読む <span aria-hidden="true">→</span>
        </a>
      </div>
    </div>
  </div>
</section>
```

### CSS（簡略）

```css
.mini-ceo { padding: 60px 0; background: #FAFAFA; }
.mini-ceo-content {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 40px;
  align-items: center;
  margin-top: 28px;
}
.mini-ceo-photo img {
  width: 100%; height: auto;
  aspect-ratio: 3/4;
  object-fit: cover;
  object-position: center 25%;
  border-radius: 4px;
}
.mini-ceo-quote {
  font-family: var(--font-serif);
  font-size: 1.6rem;
  font-weight: 700;
  color: #111;
  line-height: 1.5;
  margin-bottom: 14px;
}
.mini-ceo-lead { color: var(--text-gray); font-size: 0.95rem; line-height: 1.8; margin-bottom: 24px; }
.mini-ceo-name { font-size: 0.85rem; color: #666; margin-bottom: 20px; }
.mini-ceo-link {
  display: inline-flex; gap: 8px; align-items: center;
  color: var(--weby-red); font-weight: 700;
  text-decoration: none; transition: gap 0.2s;
}
.mini-ceo-link:hover { gap: 14px; }
@media (max-width: 768px) {
  .mini-ceo-content { grid-template-columns: 1fr; gap: 20px; }
  .mini-ceo-photo { max-width: 200px; margin: 0 auto; }
  .mini-ceo-quote { font-size: 1.25rem; text-align: center; }
  .mini-ceo-text > :not(.mini-ceo-quote) { text-align: center; }
}
```

### クリエイティブ

- 写真: 既存 `ceo_photo/IMG_2072.webp` の 600w variant を使用
- 縦長ポートレート表示（aspect-ratio 3/4）
- object-position: center 25% で顔を上寄りに

### 受入条件

- [ ] 新規セクションが Hero Stats と News Bar の間に挿入
- [ ] 「メッセージを読む」クリックで `#ceo-section` にスムーズスクロール
- [ ] モバイルで縦積み、写真は 200px 四方以内

---

## B-3 #58 内定者の声

### ワイヤーフレーム

**配置**: CEO セクションの**後**、`#recruit` の**前**（新規セクション）

```
┌──────────────────────────────────────────────────────┐
│  VOICE FROM 2026 NEW JOINERS                         │
│  先輩内定者からのメッセージ                          │
│                                                      │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐        │
│  │ [写真]    │  │ [写真]    │  │ [写真]    │        │
│  │           │  │           │  │           │        │
│  │ T.S.      │  │ M.K.      │  │ A.N.      │        │
│  │ 2026 卒   │  │ 2026 卒   │  │ 2026 卒   │        │
│  │           │  │           │  │           │        │
│  │「決め手は  │  │「大手とも │  │「自分を   │        │
│  │ 人でした」 │  │ 比較して」│  │ 信じられる │        │
│  │           │  │           │  │ 環境」    │        │
│  │ [詳しく→] │  │ [詳しく→] │  │ [詳しく→] │        │
│  └───────────┘  └───────────┘  └───────────┘        │
└──────────────────────────────────────────────────────┘
```

### コンテンツ（サンプル、取材後に置換）

#### カード 1: T.S. さん（営業志望）

```
【タグ】FUTURE SALES
【名前】T.S. / 早稲田大学 商学部
【一言】決め手は「人」でした。

【本文】
インターンで様々な会社を見てきました。 
最終的に WEBY を選んだのは、面接でお会いした
一人ひとりに嘘がなかったから。営業として、
胸を張って紹介できる仲間がいる環境で成長したいと思いました。

【選考中、不安だったこと】
ベンチャーの不安定さ。説明会で中野社長から
創業 10 年の実績を詳しく聞き、安心しました。
```

#### カード 2: M.K. さん（コンサル志望）

```
【タグ】FUTURE CONSULTANT
【名前】M.K. / 慶應義塾大学 経済学部
【一言】大手とも比較した結果、ここに。

【本文】
複数社から内定をいただきましたが、
WEBY は 1 年目から実務に深く関われる点が決め手でした。
士業の先生方に直接提案できる機会は、大手では
得られない貴重な経験だと確信しています。

【親への説明】
「銀座の会社で、10 年続いている」と伝えたら
安心してくれました。社員紹介動画を一緒に見ました。
```

#### カード 3: A.N. さん（ディレクター志望）

```
【タグ】FUTURE DIRECTOR
【名前】A.N. / 上智大学 外国語学部
【一言】自分を信じられる環境。

【本文】
文系未経験で Web 業界に飛び込むのが怖かった。
でも研修制度と先輩のインタビューを見て、
「ここなら成長できる」と感じました。
入社前から長期インターンで先行して学んでいます。
```

### HTML（基本構造）

```html
<section class="joiners-voice">
  <div class="container">
    <div class="section-header reveal">
      <span class="m-script">VOICE FROM 2026 NEW JOINERS</span>
      <h2>先輩内定者からの<em>メッセージ</em></h2>
    </div>
    <div class="joiners-grid reveal">
      <article class="joiner-card">
        <div class="joiner-photo">
          <img src="./joiner_photos/ts.webp" alt="T.S.さん">
        </div>
        <span class="joiner-tag">FUTURE SALES</span>
        <div class="joiner-name">T.S. <small>/ 早稲田大学 商学部</small></div>
        <p class="joiner-quote">決め手は「人」でした。</p>
        <p class="joiner-body">インターンで様々な会社を見てきました。...</p>
        <details class="joiner-more">
          <summary>もっと見る</summary>
          <div class="joiner-extra">
            <h4>選考中、不安だったこと</h4>
            <p>ベンチャーの不安定さ。...</p>
          </div>
        </details>
      </article>
      <!-- 2-3 も同様 -->
    </div>
  </div>
</section>
```

### クリエイティブ

- **写真**: 内定者 3 名の顔写真（承諾必須）
  - サイズ: 400×400 ポートレート、真正面〜斜め 15°
  - オフィスで撮影（背景に現社員がいるとさらに良い）
- **顔出しが難しい場合**: シルエット + イニシャル + 大学名のみでも可
- **動画インタビュー版**: 各 30 秒〜1 分のテキスト版動画（オプショナル）

### 取材質問テンプレート

```
1. 自己紹介（大学・学部・ 志望職種）30 秒
2. 就活中、何社と比較しましたか？
3. WEBY を選んだ最大の決め手は何でしたか？
4. 選考中、一番不安だったことは？
5. 親や友人に説明するとき、WEBY の何を強調しましたか？
6. 入社までに期待していること・不安なこと
7. これから応募する後輩に一言
```

### 受入条件

- [ ] 内定者 3 名取材完了・顔写真同意書取得
- [ ] 写真トリミング（300×300 以上、顔中心）
- [ ] LP 新セクション実装、CEO セクション直後に配置
- [ ] 各カードにクリックで詳細モーダル（省略可）

---

## B-4 #59 FAQ 拡充

### 現行 FAQ (6 項目)

1. 面接ではどんなことを見ていますか？
2. 入社後の研修はありますか？
3. 未経験でも活躍できますか？
4. 配属はどのように決まりますか？
5. 社内の雰囲気はどんな感じですか？
6. 福利厚生はありますか？

### 追加 6 項目（推奨順）

#### 7. 選考期間はどのくらいですか？

```
応募から内定までは、平均 3〜4 週間です。

【内訳】
・1 次選考（書類）: 3 営業日以内にご連絡
・2 次選考（面接）: 応募後 1 週間以内
・3 次選考（代表面接）: 2 週間目
・最終結果: 3 週間目

ご状況（他社選考・学業）に応じて柔軟に調整いたします。
```

#### 8. リモートワークは可能ですか？

```
新卒 1 年目は原則出社（銀座本社）です。

入社 2 年目以降、業務や職種に応じて週 1〜2 日のリモート
勤務が可能です。私たちは「対面で積み上げる信頼」を
大事にしていますが、集中できる環境で成果を出すことも
同じく大切だと考えています。

なお沖縄在住の方は那覇支社勤務での選考も可能です。
```

#### 9. 残業は平均どのくらいですか？

```
月平均 20 時間前後です（2025 年度実績）。

繁忙期（四半期末など）で 30 時間、
落ち着く月で 10 時間、といった範囲で推移しています。

残業は「仕組みで減らす」を徹底しており、
業務効率化ツールの導入・会議時間の削減を継続中です。
```

#### 10. 転勤はありますか？

```
基本的にありません。

本社（東京・銀座）または那覇支社での勤務が中心です。
ご本人の希望がない限り、勤務地変更を命じることは
ありません。

※ 新規拠点開設などの機会があれば、希望制でご案内します。
```

#### 11. 会社の規模を教えてください（親御様向け）

```
株式会社WEBY は 2011 年設立、社員数約 50 名の
独立系 Web コンサルティング企業です。

・本社: 東京都中央区銀座
・主事業: 士業向け Web コンサルティング / 自社メディア運営
・代表: 中野 秀征

売上は過去 3 年で 230% 成長。
継続取引のクライアントが事業の基盤となっています。
```

#### 12. 離職率や定着率は？

```
直近 3 年の新卒定着率は 90% 以上です。

辞めた方の理由は主に「独立してフリーランスに」
「海外留学」など前向きなものが中心です。
卒業生とは今もつながりがあり、業務委託として
戻ってくれるケースもあります。

社員一人ひとりのキャリアを尊重する文化が、
この数字の背景にあります。
```

### HTML 実装パターン（既存 .faq-item を踏襲）

```html
<div class="faq-item">
  <button class="faq-q" type="button" aria-expanded="false" aria-controls="faq-a-7">
    <span class="faq-q-mark">Q.</span>
    <span class="faq-q-text">選考期間はどのくらいですか？</span>
    <span class="faq-icon"></span>
  </button>
  <div class="faq-a" id="faq-a-7" role="region">
    <div class="faq-a-inner">
      <span class="faq-a-mark">A.</span>
      <p class="faq-a-text">応募から内定までは、平均 3〜4 週間です。<br><br>【内訳】<br>・1次選考（書類）: ...</p>
    </div>
  </div>
</div>
```

### 受入条件

- [ ] 人事が 6 項目の回答内容を承認（残業時間・離職率は特に精査要）
- [ ] LP に 12 項目すべて配置、初期状態は全て閉じる
- [ ] 既存デザイン（ダーク版）を維持

---

## B-5 #63 Job Board 配置決定

### 現状の構造

```
Recruit(募集要項) → Post-Recruit CTA(直接応募) → Job Board(mynavi/doda) → FAQ → Footer
```

### 選択肢と各 Visual

#### Option A: 現状維持 🟡

```
...Recruit → [CTA 直接応募] → mynavi/doda → FAQ → Footer
```

**効果**: 両方の導線を保持。直接 CTA 追加済で改善済み。
**測定すべき数字**: CTA クリック率 vs Job Board クリック率

#### Option B: Job Board を Footer 下へ 🟢（推奨）

```
...Recruit → [CTA] → FAQ → Footer → Job Board（もし迷ったら）
```

**効果**: 直接応募を主導線に。Job Board は「最後の選択肢」として位置づけ。
**HTML 変更**:

```html
<!-- 変更前: Job Board が recruit-cta の後 -->
<section class="recruit-cta">...</section>
<section class="jobboard-section">...</section>
<section class="faq-section">...</section>
<footer>...</footer>

<!-- 変更後: Job Board は Footer の後 -->
<section class="recruit-cta">...</section>
<section class="faq-section">...</section>
<footer>...</footer>
<section class="jobboard-section jb-footer-alt">
  <div class="container">
    <p class="jb-label">他の媒体でも応募受付中</p>
    <!-- mynavi / doda バナー -->
  </div>
</section>
```

#### Option C: Job Board を Recruit の前 🟡

```
...CEO → [NEW] Job Board → Recruit → [CTA] → FAQ → Footer
```

**効果**: 「この会社を外部でも見つけられる」trust signal として使う。
**弱み**: Recruit 到達前に離脱誘発のリスク。

#### Option D: Job Board 撤去 🔴

```
...Recruit → [CTA] → FAQ → Footer
```

**効果**: 直接応募に完全集中。
**弱み**: mynavi / doda 有料枠の掲載意義が減る（別途掲載ページは維持可能）。

### 推奨プロセス

1. **今すぐ**: Option A で 2 週間データ取得（#64 GA4 完了後）
2. **2 週間後**: クリック率比較
   - 直接 CTA が 70% 以上 → Option B へ移行
   - mynavi/doda 含め合計が多い → Option A 維持
3. **判断材料（人事提供）**: 各媒体の月額掲載料 + 獲得応募数

---

## B-6 #68 News Bar 整理

### 現状（問題あり）

```html
2025.09.21  RECRUIT  2027年卒中途採用 本選考エントリーを開始しました
2024.08.21  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました
2024.08.21  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました  ← 重複
```

### 修正案

#### 案 1: 最小修正（3 項目のまま、誤用・重複を直す）

```
2026.04.01  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました
2026.03.15  EVENT    カジュアル面談の受付を開始しました
2025.09.21  RECRUIT  中途採用 通年エントリー受付中
```

#### 案 2: 拡充版（5 項目、動きのある情報発信）

```
2026.06.10  EVENT    2028 サマーインターンシップ 募集開始（7月中旬〆切）
2026.04.01  RECRUIT  2027年卒 新卒採用 本選考エントリーを受付中
2026.03.15  EVENT    カジュアル面談 毎週水曜 19:00 より開催
2026.02.20  MEDIA    Business+IT に代表インタビューが掲載されました
2025.12.01  RECRUIT  通年長期インターン 募集中（週2日〜）
```

### 実装

既存の `.news-item` 構造を流用。3 項目以上ある場合は CSS `overflow-x: auto` またはマーキー効果で横スクロール。

### 運用ルール（追記推奨）

- 最新 5 項目を表示、古いものは `archive` フラグで非表示
- tag 種別: `RECRUIT` / `EVENT` / `MEDIA` / `NEWS`
- 将来的に CMS 化（WordPress / microCMS / Contentful 等）を検討

---

# Part C: 計測・調査基盤

## C-1 #64 GA4/GTM 導入

### 実装コード

#### 1. GTM snippet (head)

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXX');</script>
<!-- End Google Tag Manager -->
```

#### 2. GTM noscript (body 直後)

```html
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
```

#### 3. ENTRY 系リンクにデータ属性付与

```html
<!-- Nav ENTRY -->
<a href="..." data-event="entry_click" data-location="nav" class="nav-entry">ENTRY</a>

<!-- Post-Recruit CTA -->
<a href="..." data-event="entry_click" data-location="post-recruit" class="recruit-cta-btn">ENTRY →</a>

<!-- Footer PRE-ENTRY -->
<a href="..." data-event="entry_click" data-location="footer">PRE-ENTRY</a>

<!-- Mobile Sticky -->
<a href="..." data-event="entry_click" data-location="mobile-sticky" class="msc-primary">ENTRY</a>

<!-- Job Board -->
<a href="..." data-event="jobboard_click" data-board="mynavi">...</a>
<a href="..." data-event="jobboard_click" data-board="doda">...</a>
```

#### 4. スクロール深度 (GTM 側でトリガー作成、コード不要)

GTM Container 内:
- Trigger: Scroll Depth 25% / 50% / 75% / 90%
- Tag: GA4 Event `scroll_depth` with value = depth percent

### GA4 カスタムイベント設計

| イベント名 | 送信タイミング | パラメータ |
|----------|-----------|----------|
| `page_view` | ロード（自動） | page_title, page_location |
| `entry_click` | ENTRY 系クリック | location(nav/post-recruit/footer/mobile-sticky) |
| `jobboard_click` | Job Board クリック | board(mynavi/doda) |
| `scroll_depth` | 25/50/75/90% 到達 | depth |
| `faq_open` | FAQ アコーディオン開 | question_index |
| `worker_modal_open` | 社員カード開 | worker_index |
| `form_submit_success` | n8n 応募完了 | form_id |

### コンバージョン設定

- Primary conversion: `entry_click` （location を secondary dimension）
- Secondary conversion: `form_submit_success`（n8n 側で実装要）

### ダッシュボード（GA4 Explore）

```
[ 時系列 ]  訪問者数 / ENTRY クリック率 / 直帰率
[ ファネル ] hero_view → scroll_50 → recruit_view → entry_click
[ セグメント ] Mobile / Desktop × ENTRY 率比較
[ ヒートマップ ] Clarity 連携（任意）
```

### 受入条件

- [ ] GTM コンテナ作成・ GA4 プロパティ連携
- [ ] 全 ENTRY 系 `a` タグに `data-event` 属性
- [ ] GTM プレビューモードで 7 イベント全て発火確認
- [ ] GA4 Realtime で 24h 以内に到達確認

---

## C-2 #60 Exit-intent Survey

### UI ワイヤーフレーム

```
┌─────────────────────────────────┐
│                             × │
│  今日はご応募されませんか？     │
│                                 │
│  よろしければ、                 │
│  理由を教えてください。         │
│                                 │
│  ○ 年収・待遇が合わなかった    │
│  ○ 仕事内容が合わない気がした  │
│  ○ もう少し情報を集めたい      │
│  ○ 応募方法が分からなかった    │
│  ○ その他 [__________]          │
│                                 │
│      [ 送信 ]   [ スキップ ]    │
└─────────────────────────────────┘
```

### トリガー条件

- **Desktop**: マウスが画面上端（y < 10px）を横切る + 10 秒以上滞在
- **Mobile**: スクロール後、スクロールアップで 50% 以上戻る

### 実装方法 3 選

| 方法 | 長所 | 短所 |
|------|------|------|
| **Microsoft Clarity** | 無料・軽量 | アンケート機能は限定 |
| **Hotjar** | 多機能・分析付き | 無料枠月 35 sessions |
| **自作（iframe + Google Forms）** | カスタマイズ自由 | UI 作り込みが必要 |

### 推奨: Microsoft Clarity + Google Forms 埋込

#### HTML

```html
<div id="exitSurvey" class="exit-survey" hidden>
  <div class="exit-survey-box" role="dialog" aria-label="離脱アンケート">
    <button class="exit-survey-close" aria-label="閉じる">×</button>
    <h3>今日はご応募されませんか？</h3>
    <p>よろしければ、理由を教えてください（1問・30秒）</p>
    <form id="exitSurveyForm">
      <label><input type="radio" name="reason" value="salary"> 年収・待遇が合わなかった</label>
      <label><input type="radio" name="reason" value="fit"> 仕事内容が合わない気がした</label>
      <label><input type="radio" name="reason" value="info"> もう少し情報を集めたい</label>
      <label><input type="radio" name="reason" value="process"> 応募方法が分からなかった</label>
      <label><input type="radio" name="reason" value="other"> その他</label>
      <textarea name="detail" placeholder="その他を選択した方、具体的に（任意）"></textarea>
      <button type="submit">送信</button>
    </form>
  </div>
</div>
```

#### JS

```js
let exited = false;
document.addEventListener('mouseleave', e => {
  if (exited || e.clientY > 10) return;
  if (Date.now() - window._pageLoadTime < 10000) return;
  exited = true;
  document.getElementById('exitSurvey').hidden = false;
});

document.getElementById('exitSurveyForm').addEventListener('submit', e => {
  e.preventDefault();
  const data = new FormData(e.target);
  // GA4 イベント送信 + Google Forms に POST
  gtag('event', 'exit_survey_submit', { reason: data.get('reason') });
  fetch('https://docs.google.com/forms/...', { method: 'POST', body: data });
  document.getElementById('exitSurvey').hidden = true;
});
```

### 受入条件

- [ ] 訪問 1 回につき最大 1 回のみ表示（localStorage で制御）
- [ ] モバイルでは邪魔にならない実装（Back ボタン or scroll-up trigger）
- [ ] 2 週間実行 → 回答を集計し #60 にコメント

---

## C-3 #61 Post-application Survey

### タイミング

- 応募完了ページ or サンクスメール内リンク

### サンクスページ埋込版 UI

```
┌──────────────────────────────────────┐
│  ✓ ご応募ありがとうございました      │
│                                      │
│  お時間あれば 30 秒、サイト改善に    │
│  ご協力ください。                    │
│                                      │
│  Q1. 応募を決めた瞬間、LP のどの     │
│      セクションを見ていましたか？    │
│  [ プルダウン選択 ]                  │
│                                      │
│  Q2. 応募前、一番迷ったこと・不安は？│
│  [ 自由記述（任意）]                 │
│                                      │
│  Q3. 他社と比較していましたか？      │
│  [ はい / いいえ ]                   │
│  比較した会社名（任意）              │
│  [ ________________ ]                │
│                                      │
│       [ 送信 ]                       │
└──────────────────────────────────────┘
```

### Q1 選択肢

```
- Hero（トップ画像・メインコピー）
- Hero 直下の数値ストリップ
- AI 時代 Manifesto
- 事業内容（Business）
- 研修制度（Training）
- 社員ストーリー（Workers）
- CEO メッセージ
- 数字で見る WEBY
- 内定者の声
- 募集要項
- 選考フロー
- 応募の直前（Recruit 直後 CTA）
- その他
```

### 実装

n8n フォームの送信後、サンクス画面を改修 or redirect URL を Google Forms に変更。

### 受入条件

- [ ] 3 ヶ月運用し、月次でレビュー
- [ ] 結果を Issue #61 にコメント
- [ ] 判明した「決め手セクション」を Hero 近くに前倒し検討

---

# Part D: 新規セクション（docs/lp-content-ideas.md より）

## D-1 AI Era Manifesto

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  AI ERA MANIFESTO                                    │
│                                                      │
│  AIで効率化できる仕事は、AIに任せます。             │
│  だからこそ、私たちは                                │
│  「信頼を築く」仕事に、人を集めます。                │
│                                                      │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐│
│  │  🤖          │ │  🫱           │ │  ⚡          ││
│  │              │ │              │ │              ││
│  │ AIで効率化   │ │ 人間だから   │ │ あなたが     ││
│  │              │ │ こそ担う     │ │ 担当する     ││
│  │ データ分析・ │ │              │ │              ││
│  │ レポート作成 │ │ 信頼関係・   │ │ 後者の       ││
│  │ ・定型業務   │ │ 戦略判断・   │ │ 仕事です。   ││
│  │              │ │ 共創         │ │              ││
│  └──────────────┘ └──────────────┘ └──────────────┘│
│                                                      │
│  ―― 代表 中野 秀征                                  │
└──────────────────────────────────────────────────────┘
```

### 本文（案）

#### 見出し

```
AI ERA MANIFESTO
AIに任せない仕事を、私たちは選ぶ。
```

#### リード文

```
AI で効率化できる仕事は、AI に任せます。
だからこそ、私たちは「信頼を築く」仕事に、人を集めます。
```

#### 3 カラム

**カラム 1: AI で効率化**
```
データ分析
レポート作成
定型的な運用業務
施策の初期案出し

→ AI は強力なアシスタント
```

**カラム 2: 人間だからこそ担う**
```
クライアントとの信頼関係構築
複雑な経営課題の戦略判断
チーム・クライアントとの共創
価値観を賭けた意思決定

→ ここに人の仕事が残る
```

**カラム 3: あなたが担当するのは**
```
後者の、人にしかできない仕事。

AI 時代だからこそ、信頼を築ける人
戦略を描ける人が、必要とされます。

WEBY はそういう人を育てる会社です。
```

#### 結び（代表の一言）

```
「仕事が AI に奪われる」と心配する時代だからこそ、
奪われない仕事の中核 = 信頼 に全振りします。

――― 代表取締役 中野 秀征
```

### 配置

Hero Stats Strip の直後、News Bar の前（新規）

### クリエイティブ

- **背景**: ダークセクション（`#0d0d0d`）で他セクションと差別化
- **アイコン**: Font Awesome の `fa-robot` / `fa-handshake` / `fa-bolt` 等
- **動き**: スクロール到達時、3 カラムが順次フェードイン（`.reveal` + stagger）
- **代表一言**: 手書き風フォント or 既存 Noto Serif JP の italic で 差別化

### 実装（HTML 骨格）

```html
<section class="ai-manifesto">
  <div class="container reveal">
    <span class="m-script">AI ERA MANIFESTO</span>
    <h2>AIに任せない仕事を、<em>私たちは選ぶ</em>。</h2>
    <p class="manifesto-lead">
      AI で効率化できる仕事は、AI に任せます。<br>
      だからこそ、私たちは「信頼を築く」仕事に、人を集めます。
    </p>
    <div class="manifesto-grid">
      <div class="manifesto-card"><!-- AI 側 --></div>
      <div class="manifesto-card"><!-- 人間 側 --></div>
      <div class="manifesto-card highlight"><!-- あなた側（赤枠） --></div>
    </div>
    <blockquote class="manifesto-ceo">
      「仕事が AI に奪われる」と心配する時代だからこそ、
      奪われない仕事の中核 = 信頼 に全振りします。
      <cite>―― 代表取締役 中野 秀征</cite>
    </blockquote>
  </div>
</section>
```

### 受入条件

- [ ] 代表 / ブランドオーナー が本文案を承認
- [ ] Hero Stats 直後に挿入
- [ ] モバイルで 3 カラム → 縦積み
- [ ] `prefers-reduced-motion: reduce` 時は stagger 無効

---

## D-2 WHY 事業コンセプト

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  WHY WE EXIST                                        │
│                                                      │
│  ┌─────────────┐  ┌─────────────────────────┐      │
│  │              │  │                         │      │
│  │ [象徴写真]   │  │ 信頼と専門性が、        │      │
│  │              │  │ まだ届いていない人が    │      │
│  │ (クライアント│  │ いる。                  │      │
│  │ の弁護士と   │  │                         │      │
│  │ 相談する風景)│  │ ・借金で悩む人に、      │      │
│  │              │  │   信頼できる弁護士を    │      │
│  │              │  │                         │      │
│  │              │  │ ・地域の法律事務所に、  │      │
│  │              │  │   まっすぐな問合せを    │      │
│  │              │  │                         │      │
│  │              │  │ 私たちの Web コンサル と│      │
│  │              │  │ 自社メディアは、        │      │
│  │              │  │ この"届かない信頼"を    │      │
│  │              │  │ 繋ぐインフラです。      │      │
│  └─────────────┘  └─────────────────────────┘      │
└──────────────────────────────────────────────────────┘
```

### 本文

#### 見出し

```
WHY WE EXIST
信頼と専門性が、まだ届いていない人がいる。
```

#### 本文

```
私たちのクライアントは、法律事務所・税理士事務所・
社労士事務所などの「士業」の方々です。

彼らは本来、専門的な知識と経験で、
悩む人を救えるはずの専門家です。

でも多くの場合、彼らの存在は
本当に必要としている人に届いていません。

・借金に追われる人が、
  信頼できる弁護士に辿り着けない
・地元の法律事務所に、
  まっすぐで適切な問合せが来ない

この「届かない」を、
Web の力で解決するのが私たちの仕事です。

自社メディア（債務急済・専門家プロファイル 等）と
Web コンサルティングを通じて、私たちは
"届かない信頼" を繋ぐインフラを作っています。

就活のみなさんに問いたい。
この「橋をかける仕事」に、共感できますか？
```

### 配置

Business セクションの**直前**に配置。What の前に Why を先出し。

### クリエイティブ

- **写真**: 以下のいずれか
  - A. クライアントである士業の方との打合せ風景（許諾要）
  - B. メディア画面のモックアップ（債務急済・専門家プロファイルの UI）
  - C. 抽象的なイラスト（「つなぐ」を表現する橋・糸・光など）
- **推奨**: B（UI モックアップ） — 自社アセット、許諾不要、事業内容も伝わる

### 実装

```html
<section class="why-we-exist">
  <div class="container">
    <div class="why-inner reveal">
      <div class="why-visual">
        <img src="./service_pics/platform-mockup.webp" alt="WEBYメディアの実例">
      </div>
      <div class="why-text">
        <span class="m-script">WHY WE EXIST</span>
        <h2>信頼と専門性が、<br><em>まだ届いていない</em>人がいる。</h2>
        <div class="why-body">
          <p>私たちのクライアントは、法律事務所・税理士事務所...</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

## D-3 選考フロー図

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  HIRING PROCESS                                      │
│  応募から内定まで、全 3-4 週間                        │
│                                                      │
│  STEP 1          STEP 2          STEP 3     STEP 4  │
│  ┌──────┐        ┌──────┐        ┌──────┐  ┌──────┐ │
│  │ 🔵   │   →    │ 💬   │   →    │ 👥   │→ │ ✉️   │ │
│  │      │        │      │        │      │  │      │ │
│  │ENTRY │        │1次   │        │最終  │  │内定  │ │
│  │応募  │        │面接  │        │面接  │  │      │ │
│  │      │        │      │        │      │  │      │ │
│  │約3分 │        │1週間 │        │2-3   │  │      │ │
│  │      │        │以内  │        │週目  │  │      │ │
│  │オン  │        │オン  │        │対面  │  │      │ │
│  │ライン│        │ライン│        │銀座  │  │      │ │
│  └──────┘        └──────┘        └──────┘  └──────┘ │
│                                                      │
│  各ステップの詳細 ↓                                  │
│                                                      │
│  [STEP 1: ENTRY]                                     │
│  n8n フォームで 3 項目入力。スマホで約 3 分。        │
│                                                      │
│  [STEP 2: 1次面接 - 人物面談]                        │
│  志望動機・価値観を 1 時間。オンライン（Meet）。     │
│  服装: ビジネスカジュアル可。                        │
│                                                      │
│  [STEP 3: 最終面接 - 代表面談]                       │
│  経営・事業のビジョン擦り合わせを 1 時間。           │
│  対面（銀座本社）。交通費全額支給。                  │
│                                                      │
│  [STEP 4: 内定通知 → 内定承諾書]                     │
│  選考終了から 3 営業日以内にメールでご連絡。         │
│  ご検討期間は 2 週間確保します。                     │
└──────────────────────────────────────────────────────┘
```

### 本文（各ステップの詳細）

※ 上記ワイヤーに記載の通り。人事から実際の期間・服装ルール・回数を確認してから確定。

### 実装（既存 training-flow と同じパターン）

```html
<section class="hiring-flow">
  <div class="container reveal">
    <span class="m-script">HIRING PROCESS</span>
    <h2>応募から内定まで、<em>全 3-4 週間</em></h2>
    <div class="hiring-flow-steps">
      <div class="hiring-step"><!-- STEP 1 --></div>
      <div class="hiring-step"><!-- STEP 2 --></div>
      <div class="hiring-step"><!-- STEP 3 --></div>
      <div class="hiring-step"><!-- STEP 4 --></div>
    </div>
    <div class="hiring-detail">
      <!-- 各ステップ詳細 -->
    </div>
  </div>
</section>
```

### 配置

Recruit セクションの**直下**、Post-Recruit CTA の**前**

### 受入条件

- [ ] 人事より実際のフロー情報取得（ステップ数・期間・場所・服装）
- [ ] `training-flow` の既存 CSS を流用（矢印 ::after の border trick 等）
- [ ] モバイルで縦積み、矢印は「↓」に変換

---

## D-4 JOIN US 3 チャネル

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  JOIN US — エントリーの入り口                        │
│                                                      │
│  一人で応募ボタンを押すのは、怖い。                  │
│  だから、3 つの入り口を用意しました。                │
│                                                      │
│ ┌──────────────┬──────────────┬──────────────┐     │
│ │  🌻          │  📘          │  ☕          │     │
│ │              │              │              │     │
│ │ SUMMER       │ YEAR-ROUND   │ INFO         │     │
│ │ INTERNSHIP   │ INTERNSHIP   │ SESSION      │     │
│ │              │              │              │     │
│ │ 2028 サマー  │ 通年長期     │ カジュアル    │     │
│ │ インターン   │ インターン   │ 面談 27      │     │
│ │              │              │              │     │
│ │ 5 日間集中   │ 週 2 日〜    │ 30 分オンライン│     │
│ │ プログラム   │ 最大 12 ヶ月 │ 毎週水 19:00  │     │
│ │              │              │              │     │
│ │ 次回: 2028/07 │ 通年募集中   │ 次回: 2026/05│     │
│ │              │              │              │     │
│ │ [APPLY →]    │ [APPLY →]    │ [RESERVE →]  │     │
│ └──────────────┴──────────────┴──────────────┘     │
│                                                      │
│  ※ どのチャネルも、本選考とは独立。                 │
│    気軽にご参加ください。                            │
└──────────────────────────────────────────────────────┘
```

### 本文

#### 見出し

```
JOIN US
エントリーの入り口
```

#### リード

```
一人で応募ボタンを押すのは、怖い。
だから、3 つの入り口を用意しました。
```

#### カード 1: SUMMER INTERNSHIP

```
【対象】2028 年卒（大学 3 年生）
【期間】5 日間（例: 2028/08/05 - 2028/08/09）
【内容】
 Day 1: 事業理解 + WEBY のメディア体験
 Day 2: 士業クライアントインタビュー同行
 Day 3: 戦略立案ワークショップ
 Day 4: プレゼン準備
 Day 5: 最終プレゼン + 懇親会

【報酬】交通費全額支給・ランチ支給
【定員】10 名（選考あり）
【応募】[APPLY →]
```

#### カード 2: YEAR-ROUND LONG-TERM INTERNSHIP

```
【対象】学年不問（大学 1 年生〜）
【期間】最低 3 ヶ月、最大 12 ヶ月
【勤務】週 2 日以上（時間応相談）
【時給】1,500 円〜（能力・経験で加算）
【業務】
 ・メディア編集
 ・営業アシスタント
 ・マーケティング施策
 ・リサーチ

【応募】[APPLY →]
【特典】本選考への優遇措置あり
```

#### カード 3: INFO SESSION

```
【対象】2027 年卒（本選考応募検討者）
【形式】オンライン（Meet）
【時間】30 分
【内容】
 ・代表からのメッセージ（10 分）
 ・若手社員とのQ&A（15 分）
 ・質疑応答（5 分）

【開催】毎週水曜日 19:00〜19:30
【定員】各回 10 名
【予約】[RESERVE →]
```

### 配置

Recruit セクションの**前**、または独立セクションとして Workers の後

### 必要な準備（人事）

- [ ] 各チャネルの応募 URL 確定（n8n フォーム別版 or Google Forms）
- [ ] サマーインターンの実施日程確定
- [ ] 説明会予約システム（TimeRex / Googleカレンダー予約 等）設定
- [ ] 長期インターン時給・条件確定

### 実装

```html
<section class="join-us">
  <div class="container reveal">
    <span class="m-script">JOIN US</span>
    <h2>エントリーの<em>入り口</em></h2>
    <p class="join-lead">一人で応募ボタンを押すのは、怖い。<br>だから、3 つの入り口を用意しました。</p>
    <div class="join-grid">
      <article class="join-card">
        <div class="join-card-icon">🌻</div>
        <span class="join-card-tag">SUMMER INTERNSHIP</span>
        <h3>2028 サマーインターン</h3>
        <p class="join-card-info">5 日間集中プログラム / 2028年8月</p>
        <ul class="join-card-list">
          <li>事業理解 + ワークショップ</li>
          <li>クライアント同行</li>
          <li>報酬・交通費支給</li>
        </ul>
        <a href="..." class="join-card-cta">APPLY →</a>
      </article>
      <!-- カード 2, 3 -->
    </div>
  </div>
</section>
```

---

## D-5 通年インターン Sticky Side CTA

### ワイヤーフレーム

```
  [メインコンテンツ領域]          ┌──────────┐
                                  │ 通年長期  │
                                  │ インターン │
                                  │ 募集中    │
                                  │           │
                                  │ 週2〜・   │
                                  │ 時給1500円│
                                  │           │
                                  │ [詳細→]   │
                                  └──────────┘
                                  ↑ 右端固定
                                    スクロール追従
```

### 本文

```
通年長期インターン
募集中

週2日〜 / 時給1,500円〜
最大12ヶ月

[ 詳しく見る → ]
```

### HTML

```html
<aside class="sticky-side-cta" id="stickyInternCta" aria-label="通年長期インターン案内">
  <span class="ssc-label">長期インターン</span>
  <span class="ssc-main">募集中</span>
  <span class="ssc-sub">週2〜・時給1,500円</span>
  <a href="..." class="ssc-cta">詳しく →</a>
</aside>
```

### CSS

```css
.sticky-side-cta {
  position: fixed;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  background: var(--weby-red);
  color: #fff;
  padding: 20px 14px;
  border-radius: 8px 0 0 8px;
  box-shadow: -4px 4px 20px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  z-index: 997;
  transition: transform 0.3s;
}
.sticky-side-cta.is-hidden {
  transform: translate(110%, -50%);
}
@media (max-width: 768px) {
  .sticky-side-cta { display: none; } /* モバイルは #8 下固定 CTA に統合 */
}
```

### 非表示タイミング（JS）

- Hero 表示中（最初の 80vh 以内）
- `.join-us` / `.recruit-cta` / `footer` 表示中
- 上記以外で表示

---

## D-6 note / SNS 連携

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  LEARN MORE                                          │
│  会社をもっと知る                                    │
│                                                      │
│  公式 note で、社員や代表の生の声を発信中            │
│                                                      │
│ ┌────────────┬────────────┬────────────┐            │
│ │ [サムネ]   │ [サムネ]   │ [サムネ]   │            │
│ │ 創業 10 年 │ 社員が語る │ 採用チーム │            │
│ │ の軌跡     │ 1 日       │ 舞台裏     │            │
│ │            │            │            │            │
│ │ 著者       │ 著者       │ 著者       │            │
│ │ 中野秀征   │ M.O.       │ 人事 部長  │            │
│ └────────────┴────────────┴────────────┘            │
│                                                      │
│  [公式 note を読む →]                                │
│                                                      │
│  ――― OFFICIAL SNS ―――                             │
│                                                      │
│      [X]    [Instagram]    [YouTube]    [note]       │
└──────────────────────────────────────────────────────┘
```

### 本文

#### 見出し

```
LEARN MORE
会社をもっと知る
```

#### リード

```
公式 note で、社員や代表の生の声を発信中。
LP では伝えきれない、日常と挑戦をお届けします。
```

#### SNS アカウント行

```
・X (@weby_official) — 日常の気づき・採用ニュース
・Instagram (@weby_inc) — オフィス風景・社員の顔
・YouTube — オフィスツアー・社員インタビュー動画
・note — 長文記事・考え方
```

### 実装

note の API を使って自動で最新記事を取得するか、手動で厳選 3 記事を表示。

手動版 HTML:

```html
<section class="learn-more">
  <div class="container reveal">
    <span class="m-script">LEARN MORE</span>
    <h2>会社を<em>もっと知る</em></h2>
    <p class="learn-lead">公式 note で、社員や代表の生の声を発信中。</p>
    <div class="note-grid">
      <a href="https://note.com/weby_official/n/xxx" target="_blank" rel="noopener noreferrer" class="note-card">
        <img src="./note_thumbs/founding-10-years.webp" alt="">
        <div class="note-card-body">
          <h3>創業 10 年の軌跡</h3>
          <p>著者: 中野秀征（代表取締役）</p>
        </div>
      </a>
      <!-- 2, 3 -->
    </div>
    <a href="https://note.com/weby_official" target="_blank" rel="noopener noreferrer" class="note-main-cta">
      公式 note を読む →
    </a>
    <div class="social-row">
      <a href="https://x.com/weby_official" aria-label="公式 X"><i class="fa-brands fa-x-twitter"></i></a>
      <a href="https://instagram.com/weby_inc" aria-label="公式 Instagram"><i class="fa-brands fa-instagram"></i></a>
      <a href="https://youtube.com/@weby" aria-label="公式 YouTube"><i class="fa-brands fa-youtube"></i></a>
      <a href="https://note.com/weby_official" aria-label="公式 note"><i class="fa-brands fa-google"></i></a>
    </div>
  </div>
</section>
```

### 必要な準備

- [ ] 公式 note アカウント URL（現状: 未確認）
- [ ] 推薦 3 記事の URL + サムネイル画像
- [ ] X / Instagram / YouTube アカウント URL

### 配置

FAQ の**後**、Footer の**前**（離脱直前の「もう少し知りたい」層向け）

---

## D-7 数字で見る WEBY

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  WEBY BY THE NUMBERS                                 │
│  数字で見る WEBY                                     │
│                                                      │
│  ┌────────┬────────┬────────┬────────┐              │
│  │        │        │        │        │              │
│  │ 230%   │ 25歳   │ 120日  │ 6ヶ月  │              │
│  │        │        │        │        │              │
│  │ 成長率 │ 平均   │ 年間   │ 独立   │              │
│  │ (YoY)  │ 年齢   │ 休日   │ 目安   │              │
│  │        │        │        │        │              │
│  │ 3 年   │ 若手が │ 業界   │ 全員が │              │
│  │ 連続   │ 中心の │ 平均以 │ 6ヶ月で│              │
│  │ 成長   │ チーム │ 上     │ 自走へ │              │
│  └────────┴────────┴────────┴────────┘              │
│                                                      │
│  ┌────────┬────────┬────────┬────────┐              │
│  │        │        │        │        │              │
│  │ 50+    │ 15年   │ ¥390万 │ 99%    │              │
│  │        │        │        │        │              │
│  │ 社員数 │ 創業   │ 1年目  │ 定着率 │              │
│  │        │ からの │ 年収   │ (3年)  │              │
│  │        │ 年数   │        │        │              │
│  │ (2026) │ 2011   │ 新卒   │ 直近   │              │
│  │ 年時点 │ 設立   │ 平均   │ 3年    │              │
│  └────────┴────────┴────────┴────────┘              │
└──────────────────────────────────────────────────────┘
```

### 各数字の説明（背景）

```
【230%】成長率（YoY）
直近 3 年、前年比 230% 前後で成長を続けています。
クライアント数と取引継続率の両輪。

【25歳】平均年齢
若手中心のチームで、意思決定のスピードが早い。
ベテラン（30 代〜40 代）も約 20% 在籍。

【120日】年間休日
完全週休 2 日（土日祝） + 年末年始・夏季・慶弔
IT 業界の平均（107 日）を大きく上回ります。

【6ヶ月】独立目安
新卒入社から平均 6 ヶ月で、営業として独立稼働。
研修と OJT で段階的に引き上げます。

【50+】社員数
2026 年現在、約 50 名規模。
3 年で 2.5 倍に拡大、採用を継続中。

【15年】創業からの年数
2011 年設立、2026 年で 15 年目。
メディア事業が安定した収益基盤です。

【¥390万】1年目平均年収
初年度 350 万〜500 万円のレンジで、
実績により 2 年目以降 520 万超えも。

【99%】3 年定着率
直近 3 年卒業者の 3 年後在籍率 99%。
辞めた方は独立・留学など前向きな理由が中心。
```

### 実装

```html
<section class="numbers">
  <div class="container reveal">
    <span class="m-script">WEBY BY THE NUMBERS</span>
    <h2>数字で見る<em>WEBY</em></h2>
    <div class="numbers-grid">
      <div class="number-card">
        <span class="number-value">230%</span>
        <span class="number-label">成長率 (YoY)</span>
        <p class="number-note">3 年連続成長</p>
      </div>
      <!-- 7 more cards -->
    </div>
  </div>
</section>
```

### 配置

CEO セクションの**後**、Recruit の**前**

### 必要な準備

- [ ] 各数字の公表可否を人事で確認
- [ ] 成長率・定着率は特に現在値を再確認（古い数字だと誤解を生む）
- [ ] 注釈文を人事で文言承認

---

## D-9 オフィス動画ツアー

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  ENVIRONMENT                                         │
│  働く環境                                            │
│                                                      │
│  ┌──────────────────────────────────────────┐       │
│  │                                          │       │
│  │  [▶ 1分で分かるオフィスツアー]           │       │
│  │                                          │       │
│  │  YouTube embed (16:9)                   │       │
│  │                                          │       │
│  └──────────────────────────────────────────┘       │
│                                                      │
│  ┌─────────┬─────────┬─────────┐                    │
│  │ LOBBY   │ CREATIVE│ RELAXING│                    │
│  │ (既存)  │ SPACE   │ SPACE   │                    │
│  └─────────┴─────────┴─────────┘                    │
└──────────────────────────────────────────────────────┘
```

### 動画仕様

```
【長さ】60 〜 90 秒
【構成】
  0:00-0:05  ロゴアニメ + キャッチ「働く環境」
  0:05-0:20  エントランス → ワークスペース（広角）
  0:20-0:40  社員が働くシーン（背中 OK）
  0:40-0:55  リラックスエリア・ランチスペース
  0:55-0:60  ENTRY ボタン / URL アウトロ

【BGM】静かめのインストゥルメンタル（ブランド「静と動」にマッチ）
【音声】環境音のみ（ナレーションなし）
【テキスト】最小限のキャプション（セクション名のみ）

【撮影ガイド】
・三脚 + スライダーで低速カメラワーク
・自然光が入る時間帯（10:00-14:00）
・社員の顔は背中 or 横顔のみ（顔出し同意取得しない場合）
```

### 実装

```html
<div class="office-video">
  <iframe
    src="https://www.youtube.com/embed/XXXXXX?rel=0&modestbranding=1"
    title="WEBY オフィスツアー"
    frameborder="0"
    allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    loading="lazy">
  </iframe>
</div>
```

```css
.office-video {
  max-width: 900px;
  margin: 40px auto;
  aspect-ratio: 16/9;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
}
.office-video iframe { width: 100%; height: 100%; border: 0; }
```

### 配置

Facility セクション内、写真グリッドの**上**に配置（動画 → 写真で詳細へ）

### 必要な準備

- [ ] 動画撮影（プロ依頼 or 社員撮影）
- [ ] YouTube アップロード（unlisted でも可、できれば公開）
- [ ] 撮影時の社員同意取得

---

## D-10 親世代向け FAQ

### 構成案

#### 方針 A: 既存 FAQ の**末尾**に「ご家族の方へ」タブ

```
FAQ（応募者向け 12 問） + [ご家族の方へ →] ボタン
→ クリックで以下が展開
  - 会社の規模は？
  - 売上・業績は？
  - 社会保険は？
  - 育休の実績は？
  - 昇給は？
  - 親が会社見学できる機会はある？
```

#### 方針 B: 独立セクション「ご家族の方へ」

```
┌──────────────────────────────────────────────────────┐
│  FOR FAMILIES                                        │
│  ご家族の方へ                                        │
│                                                      │
│  お子様の入社先として、ご安心いただけるよう          │
│  率直にお伝えします。                                │
│                                                      │
│  [FAQ 6 項目アコーディオン]                          │
│                                                      │
│  [親御様向け会社案内 PDF ダウンロード]               │
│                                                      │
│  ご質問・ご心配事は 03-6280-4361 までお気軽に。      │
└──────────────────────────────────────────────────────┘
```

### Q&A 本文

#### Q1. 会社の規模は？

```
A. 社員数約 50 名、2011 年創業の 15 年目の会社です。
   本社は東京都中央区銀座、主要事業は Web コンサルティング
   です。独立系（親会社・グループ会社なし）の中堅 IT 企業に
   位置づけられます。
```

#### Q2. 売上や業績は？

```
A. 直近 3 年で売上 230% 成長を達成しました。
   継続取引のクライアント（士業事務所）が基盤で、
   一時的な案件に依存しないストック型の収益構造です。
   黒字経営を継続しています。

   具体的な売上額は非公開ですが、帝国データバンク
   などの信用情報機関で確認いただけます。
```

#### Q3. 社会保険はどこですか？

```
A. 健康保険・厚生年金・雇用保険・労災保険すべて完備しています。
   健康保険は「協会けんぽ（東京支部）」加入です。
```

#### Q4. 育休・産休の実績は？

```
A. 育児休業は 3 名（男性 1 名、女性 2 名）の取得実績があります。
   全員が復職し、現在も在籍中です。
   男性の育休取得も推奨しており、1 週間〜1 ヶ月の短期取得も可能です。
```

#### Q5. 昇給・賞与はどれくらい？

```
A. 昇給: 年 1 回（4 月）、業績と評価に連動
   賞与: 年 1〜2 回（夏・冬）、業績により支給額決定

   新卒 1 年目平均 390 万円、3 年目で 520 万〜 650 万円が
   一般的なレンジです。
```

#### Q6. 親が会社見学できる機会はありますか？

```
A. 「保護者会社訪問会」を年 2 回（8 月・12 月）開催しています。
   銀座オフィスにお越しいただき、代表からのご挨拶と、
   お子様の先輩社員との座談会を予定しています。

   個別のご見学も随時受け付けています。お電話で
   お気軽にお問い合わせください。
```

### 親御様向け PDF（オプショナル）

```
【内容】
1. 会社概要（会社案内ベース）
2. 事業内容の説明（専門用語なしで）
3. よくあるご質問（本 FAQ の拡張版）
4. 代表からのメッセージ
5. 採用担当連絡先

【形式】A4 × 4 ページ PDF
【配布】LP からダウンロード + 説明会参加者に印刷版配布
```

---

# Part E: 全体像

## E-1 新セクションオーダー

本書 + PR #55 / #69 の実装を全て反映した理想構成:

```
1.  Hero (B-1 で改善)
2.  Hero Stats Strip ✅ 実装済 (PR #55)
3.  [NEW] Mini CEO Panel (B-2)
4.  [NEW] AI Era Manifesto (D-1)
5.  News Bar (B-6 で整理)
6.  Message
7.  [NEW] WHY - 事業コンセプト (D-2)
8.  Facility (+ D-9 オフィス動画)
9.  Business
10. Training
11. Workers (既存 Carousel)
12. CEO Message
13. [NEW] 数字で見る WEBY (D-7)
14. [NEW] 内定者の声 (B-3)
15. Recruit 募集要項
16. [NEW] 選考フロー (D-3)
17. Post-Recruit CTA ✅ 実装済 (PR #55)
18. [NEW] JOIN US 3 チャネル (D-4)
19. Job Board (B-5 で配置決定)
20. FAQ (B-4 で拡充 + D-10 親向け追加)
21. [NEW] LEARN MORE / note (D-6)
22. Footer

[固定要素]
- Sticky Right (desktop): 通年インターン CTA (D-5)
- Sticky Bottom (mobile): ENTRY CTA ✅ 実装済 (PR #69)
```

新規セクション数: **9 個**
置換・変更: **4 箇所**（Hero, News Bar, FAQ, Job Board）

---

## E-2 実装順序ロードマップ

### Wave 1: 計測基盤と決裁（Week 1-2）

| 優先 | 項目 | 担当 | ブロッカー解消 |
|-----|------|-----|--------------|
| P0 | #64 GA4/GTM 導入 | エンジニア + 人事 | 全施策の効果測定 |
| P0 | #1 ブランド赤決裁 | ブランドオーナー | 色系統一 |
| P0 | #56 Hero コピー決裁 | 代表 + コピーライター | Hero 書き換え |
| P0 | D-1 AI Manifesto コピー決裁 | 代表 | コンテンツ起点 |
| P1 | D-4 JOIN US URL 確保 | 人事 | 3 チャネル導線 |
| P1 | D-3 選考フロー情報取得 | 人事 | Hiring Process 節 |

### Wave 2: コンテンツ実装（Week 3-4）

| 項目 | 依存 |
|------|------|
| B-1 Hero 刷新 | #56 決裁後 |
| D-1 AI Manifesto 実装 | コピー決裁後 |
| B-2 Mini CEO Panel | 既存アセットで可 |
| D-2 WHY 事業コンセプト | 代表文案承認後 |
| B-6 News Bar 整理 | 人事から最新ニュース |
| D-3 選考フロー図 | 人事情報後 |

### Wave 3: 信頼アセット拡充（Week 5-6）

| 項目 | 依存 |
|------|------|
| D-7 数字で見る WEBY | 人事の数値確認 |
| B-3 内定者の声（#58） | 取材・写真同意 |
| B-4 FAQ 拡充（#59） | 人事の回答 |
| D-10 親向け FAQ | 人事の回答 |

### Wave 4: エントリーチャネル拡張（Week 6-8）

| 項目 | 依存 |
|------|------|
| D-4 JOIN US 3 チャネル | URL 確定後 |
| D-5 Sticky Side CTA | 長期インターン URL |
| B-5 Job Board 配置 | GA4 データ 2 週間取得後に判断 |

### Wave 5: ナーチャリング導線（Week 8-10）

| 項目 | 依存 |
|------|------|
| D-6 note 連携 | note アカウント URL |
| D-9 オフィス動画 | 動画制作完了 |
| C-2 Exit Survey | GA4 完了後 |
| C-3 Post-app Survey | n8n サンクスページ改修 |

---

## E-3 ディシジョンフロー

```
[人事] ─── Hiring Process 情報 ───→ [D-3 選考フロー]
           Q&A 回答 ───→ [B-4 FAQ拡充] [D-10 親向けFAQ]
           数値確認 ───→ [D-7 数字で見るWEBY]
           取材 ───→ [B-3 内定者の声]

[代表] ─── Hero コピー決裁 ───→ [B-1 Hero]
          AI Manifesto 文案 ───→ [D-1]
          WHY 文案 ───→ [D-2]

[マーケ] ─ 説明会予約システム ──→ [D-4 INFO SESSION]
         長期インターン条件 ───→ [D-4 + D-5]
         サマーインターン企画 ──→ [D-4 SUMMER IS]

[エンジニア] ─ GA4/GTM 実装 ───→ [全施策の効果測定]
              n8n サンクスページ ─→ [C-3 post-app]
              動画撮影・編集 ───→ [D-9]
```

---

## E-4 コンテンツ量概算

- 新規コピー作成量: 約 **4,500 文字**（Hero 刷新 + 5 新セクションの本文）
- 新規 Q&A: **12 問（既存 6 + 追加 6）+ 6 問（親向け）= 18 問**
- 写真撮影: **内定者 3 名 + オフィス動画 60 秒**
- デザイン追加セクション: **9 個**

---

## 付録: 本書の更新運用

- アイデアが具体化したら `docs/lp-content-ideas.md` → `docs/implementation-brief.md`（本書）→ GitHub Issue の順で昇格
- 実装完了した節は見出しに ✅ マークを追加
- 人事・代表決裁が取れた案は本書内の複数案から 1 つに絞って残す（他は「却下案」として履歴に）
- 新規 Issue 起票時は本書の該当節へのリンクを Issue 本文に貼る

---

**最終更新**: 2026-04-22 / v1.0
**次回見直し**: Issue #64 (GA4) 完了後、計測データ反映時
