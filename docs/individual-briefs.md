# 依頼ブリーフ集（要素別）

各要素を **独立した依頼テキスト** として記載したドキュメントです。各節は `---` で区切られており、該当節だけを切り出して外部デザイナー・コピーライター・エンジニア・人事担当などに渡せる形式になっています。

---

## このドキュメントの使い方

1. 依頼したい要素の節を探す（目次参照）
2. その節の冒頭から `---` までをコピー
3. メール・Slack・Notion などに貼り付けて、そのまま依頼として使える

各節には以下が完結した形で含まれています:
- 依頼先ロール・優先度・関連 Issue
- プロジェクト背景（WEBY とは何の会社か）
- 現状と課題
- 依頼内容（具体的な成果物）
- 実装仕様・本文案・ワイヤーフレーム
- 受入条件・必要な情報

---

## 目次

### Part A: 決裁系
- [A-01 ブランド赤色統一方針](#a-01-ブランド赤色統一方針)
- [A-02 空ファイル text/キャッチコピー の処理](#a-02-空ファイル-textキャッチコピー-の処理)
- [A-03 エージェント定義の絶対パス修正](#a-03-エージェント定義の絶対パス修正)

### Part B: コンテンツ実装
- [B-01 Hero コピー刷新](#b-01-hero-コピー刷新)
- [B-02 ミニ CEO パネル追加](#b-02-ミニ-ceo-パネル追加)
- [B-03 内定者の声 取得＆実装](#b-03-内定者の声-取得実装)
- [B-04 FAQ 6→12 項目拡充](#b-04-faq-612-項目拡充)
- [B-05 Job Board 配置戦略決定](#b-05-job-board-配置戦略決定)
- [B-06 News Bar コンテンツ整理](#b-06-news-bar-コンテンツ整理)

### Part C: 計測・調査基盤
- [C-01 GA4/GTM 計測導入](#c-01-ga4gtm-計測導入)
- [C-02 Exit-intent Survey](#c-02-exit-intent-survey)
- [C-03 応募後アンケート](#c-03-応募後アンケート)

### Part D: 新規セクション
- [D-01 AI Era Manifesto](#d-01-ai-era-manifesto)
- [D-02 WHY 事業コンセプト](#d-02-why-事業コンセプト)
- [D-03 選考フロー図](#d-03-選考フロー図)
- [D-04 JOIN US 3 チャネル](#d-04-join-us-3-チャネル)
- [D-05 通年インターン 追従サイド CTA](#d-05-通年インターン-追従サイド-cta)
- [D-06 note/SNS 連携ブロック](#d-06-notesns-連携ブロック)
- [D-07 数字で見る WEBY](#d-07-数字で見る-weby)
- [D-09 オフィス動画ツアー](#d-09-オフィス動画ツアー)
- [D-10 親世代向け FAQ](#d-10-親世代向け-faq)

---
---
---

# Part A: 決裁系

---

## A-01 ブランド赤色統一方針

**依頼先ロール**: ブランドオーナー（代表 or マーケ責任者）
**優先度**: P0（ブロッカー）
**関連 Issue**: #1

### 依頼概要

株式会社WEBY 新卒採用LP におけるブランドレッドの色コードを、正式に 1 つに統一してください。

### プロジェクト背景

株式会社WEBY（2011年設立、東京・銀座本社）は士業向け Web コンサルティング企業。本 LP は 2027年卒向けの新卒採用サイト。ブランドコンセプト: 「THE RED EDGE — 力強い・野心的・誠実」。

### 現状と課題

LP 内で赤色が 2 つの異なる値で使われており、実装・デザインシステムとしては不整合:

| コード | 色味 | 現状の使われ方 | WCAG AA |
|--------|-----|------------|---------|
| `#C0143C`（濃い赤） | CSS 変数 `--weby-red` 既定値 | 静的な赤（全セクション） | 5.9:1（本文 OK） |
| `#FF1F4B`（明るい赤） | `brand_guidelines.md` で指定 | 現在 `rgba(192,20,60,*)` に統一済（PR #47） | 3.9:1（大型テキスト限定） |

### 依頼内容

以下 A / B から選択:

**選択肢 A: `#C0143C` を公式化（現状維持）**
- 追加実装: なし
- メリット: 本文にも赤を使える（AA 本文 pass）
- デメリット: ブランドガイドライン要修正

**選択肢 B: `#FF1F4B` を公式化**
- 追加実装: `--weby-red` 変更 + rgba を `rgba(255,31,75,*)` に戻す
- メリット: 当初ブランド設計通り
- デメリット: 本文の赤テキスト不可（AA 不適合）

### 受入条件

- [ ] A / B いずれかの決定がドキュメント化
- [ ] WCAG AA 観点の確認記録（contrast checker スクリーンショット）

### 参考

- 現実装: `index.html:89` の `--weby-red: #C0143C`
- `brand_guidelines.md`
- https://webaim.org/resources/contrastchecker/

---

## A-02 空ファイル text/キャッチコピー の処理

**依頼先ロール**: 人事 or コピーライター
**優先度**: P2
**関連 Issue**: #3

### 依頼概要

リポジトリ内の空ファイル `text/キャッチコピー`（0 バイト）の今後の扱いを決めてください。

### プロジェクト背景

株式会社WEBY 新卒採用LP のリポジトリに `text/` ディレクトリがあり、LP 原稿（理念・社長メッセージなど）を管理しています。その中の `キャッチコピー` ファイルが空のまま存在しています。

### 依頼内容

以下 3 択から選択:

**選択肢 A: 原稿管理ファイルとして活用（推奨）**

以下の雛形で埋める:

```markdown
# キャッチコピー（原稿管理）

## 現行（2026-04-22 時点）
今日よりも明日、大きな社会課題を解決する。

## 次期候補（Brief B-01 と連動）
- 案A: 今日よりも明日、より大きな社会課題の解決へ。
- 案B: 士業の集客課題を、データと戦略で解決する。
- 案C: 専門家の集客を、ジブンの手で加速させる。

## 変更履歴
| 日付 | 変更内容 | 決裁者 |
|------|---------|-------|
| 2026-04-22 | 初版 | — |
```

**選択肢 B: `採用メッセージ` に統合 → 本ファイル削除**

**選択肢 C: 削除** (`git rm text/キャッチコピー`)

### 受入条件

- [ ] A / B / C いずれかを決定
- [ ] `ls text/` で空ファイル非存在

---

## A-03 エージェント定義の絶対パス修正

**依頼先ロール**: エンジニア（Claude Code 利用者）
**優先度**: P2
**関連 Issue**: #4

### 依頼概要

`.claude/agents/lp-*.md` 内の絶対パスを現プロジェクトルートに更新してください。

### プロジェクト背景

当プロジェクトは Claude Code（AI エージェント）を使った開発フローを採用。`.claude/agents/` に3体のエージェント定義（designer / copywriter / qa）を配置しています。

### 現状

3 ファイル内に旧プロジェクトルート `/Users/togashi/Desktop/会社LP` が残存:

```
.claude/agents/lp-designer.md
.claude/agents/lp-copywriter.md
.claude/agents/lp-qa.md
```

現プロジェクトルート: `/Users/nakano/Desktop/cursor/webyhp/`

### 依頼内容

**選択肢 A（推奨）**: 相対パスに置換

```bash
find .claude/agents -name "*.md" -exec sed -i '' \
  's|/Users/togashi/Desktop/会社LP|../..|g' {} \;
```

**選択肢 B**: 現絶対パスに置換

```bash
find .claude/agents -name "*.md" -exec sed -i '' \
  's|/Users/togashi/Desktop/会社LP|/Users/nakano/Desktop/cursor/webyhp|g' {} \;
```

A が推奨（プロジェクト移動時も動作）。

### 受入条件

- [ ] `grep -r "togashi\|会社LP" .claude/` → ゼロ
- [ ] `lp-qa` エージェント実行でエラー無し

---
---

# Part B: コンテンツ実装

---

## B-01 Hero コピー刷新

**依頼先ロール**: コピーライター + ブランドオーナー（代表）
**優先度**: P0
**関連 Issue**: #56

### 依頼概要

LP トップ（Hero）のキャッチコピーを、5 秒で事業内容が伝わる表現に書き換えてください。

### プロジェクト背景

株式会社WEBY（2011 年設立、東京・銀座本社）の新卒採用LP。ターゲット: 2027年3月卒業予定の大学 3-4 年生。

事業内容: **士業向け Web コンサルティング + 自社メディア運営**。クライアントは法律事務所・税理士事務所・社労士事務所。借金整理や税務相談で悩む人に、信頼できる専門家を届けるインフラを作っている会社です。

ブランドコンセプト: 「THE RED EDGE — 力強い・野心的・誠実」

### 現状と課題

現行コピー:

```
2027 RECRUIT
今日よりも明日、
大きな社会課題を解決する。
```

課題:
- 「大きな社会課題」が抽象的で、**何の会社か 5 秒で分からない**
- 就活生は平均 50-80 社を流し見、1 サイト滞在約 45 秒
- 他社 LP との差別化が薄い

### 依頼内容

以下 3 案から 1 つを選択、または新案を作成:

**案 A（推奨）事業ダブル明示型:**

```
2027 RECRUIT

今日よりも明日、
より大きな社会課題の解決へ。

士業向け Web コンサルティング × 自社メディア運営
```

**案 B 具体成果先出し型:**

```
2027 RECRUIT

士業の集客課題を、
データと戦略で解決する。

2011年設立・銀座／Web コンサルティング企業
```

**案 C ターゲット明示型:**

```
2027 RECRUIT

専門家の集客を、
ジブンの手で加速させる。

弁護士・税理士向け Web コンサルティング企業
```

### 実装仕様（案 A 採用時）

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
  .hero-sub { font-size: 0.75rem; margin-top: 20px; padding: 0 16px; }
}
```

### クリエイティブ

- Hero 背景画像は現行（`./photos/mainbanner.webp`）を継続使用
- opacity 0.7（既存）で可読性確保済

### 受入条件

- [ ] 代表 or ブランドオーナーが選定
- [ ] h1 は 全角 20 文字以内、サブコピー 全角 25-35 文字
- [ ] モバイル幅 375px で 4 行以内

---

## B-02 ミニ CEO パネル追加

**依頼先ロール**: デザイナー + コピーライター
**優先度**: P2
**関連 Issue**: #57

### 依頼概要

ページ上部（Hero 直下付近）に代表の顔写真 + 一言メッセージパネルを追加し、早期の trust signal として機能させてください。

### プロジェクト背景

株式会社WEBY（代表: 中野 秀征、2011 年設立）の新卒採用LP。現在 CEO メッセージはページの中盤（8 番目のセクション）にあり、ユーザーがそこまで辿り着く前に離脱するケースを想定。

### 依頼内容

Hero 直下の Stats Strip セクションのすぐ下に、以下のコンパクトなパネルを追加:

### ワイヤーフレーム

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

### CSS

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
  font-size: 1.6rem; font-weight: 700; color: #111;
  line-height: 1.5; margin-bottom: 14px;
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

### 素材・クリエイティブ

- 写真: 既存 `ceo_photo/IMG_2072-600w.webp` を流用
- 縦長 3:4 表示、object-position: center 25% で顔を上寄り

### 受入条件

- [ ] Hero Stats Strip と News Bar の間に挿入
- [ ] 「メッセージを読む」で既存 `#ceo-section` にスムーズスクロール
- [ ] モバイルで縦積み、写真 200px 以内
- [ ] 既存 `.reveal` クラスを付けてスクロール連動フェードイン

---

## B-03 内定者の声 取得＆実装

**依頼先ロール**: 人事（取材） + デザイナー（実装） + コピーライター（文字起こし）
**優先度**: P2
**関連 Issue**: #58

### 依頼概要

2026 卒内定者 3 名を取材し、顔写真 + 一言 + 本文コメントのセットを LP に追加してください。

### プロジェクト背景

株式会社WEBY 2027年卒新卒採用LP。既存 LP に 3 名の社員カルーセルはあるが、**就活生に最も近い立場の「内定者の声」が無い**。応募検討中の就活生にとっての「最後の一押し」として機能するコンテンツを新規追加。

### 依頼内容

### Step 1: 内定者取材（人事担当）

2026 卒内定者 3 名に以下のインタビューを実施。各名 15-30 分。

**質問テンプレート:**

```
1. 自己紹介（大学・学部・志望職種）30 秒
2. 就活中、何社と比較していましたか？
3. WEBY を選んだ最大の決め手は？
4. 選考中、一番不安だったことは？
5. 親や友人に WEBY を説明するとき、何を強調しましたか？
6. 入社までに期待していること・不安なこと
7. これから応募する後輩に一言
```

**顔写真撮影**:
- 400×400 以上、正面〜斜め 15°
- 背景は銀座オフィス推奨
- 顔出し承諾書の取得必須
- 顔出し不可の場合: シルエット + イニシャル + 大学名のみでも可

### Step 2: コメント編集（コピーライター）

取材ログから 3 枚の「カード」分のコンテンツを作成。

### サンプル内容

**カード 1: T.S. さん**

```
【タグ】FUTURE SALES
【名前】T.S. / 早稲田大学 商学部
【一言】決め手は「人」でした。

【本文】
インターンで様々な会社を見てきました。最終的に WEBY を
選んだのは、面接でお会いした一人ひとりに嘘がなかったから。
営業として、胸を張って紹介できる仲間がいる環境で成長したい
と思いました。

【選考中、不安だったこと】
ベンチャーの不安定さ。説明会で中野社長から創業 10 年の
実績を詳しく聞き、安心しました。
```

**カード 2: M.K. さん**

```
【タグ】FUTURE CONSULTANT
【名前】M.K. / 慶應義塾大学 経済学部
【一言】大手とも比較した結果、ここに。

【本文】
複数社から内定をいただきましたが、WEBY は 1 年目から
実務に深く関われる点が決め手でした。士業の先生方に直接
提案できる機会は、大手では得られない貴重な経験だと
確信しています。
```

**カード 3: A.N. さん**

```
【タグ】FUTURE DIRECTOR
【名前】A.N. / 上智大学 外国語学部
【一言】自分を信じられる環境。

【本文】
文系未経験で Web 業界に飛び込むのが怖かった。でも研修
制度と先輩インタビューを見て、「ここなら成長できる」と
感じました。入社前から長期インターンで先行して学んでいます。
```

### Step 3: LP 実装（デザイナー）

CEO セクションの**後**、Recruit セクションの**前**に新セクション追加。

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
      </article>
      <!-- 2, 3 同構造 -->
    </div>
  </div>
</section>
```

### 受入条件

- [ ] 内定者 3 名の顔写真同意書取得
- [ ] 各 400×400 以上の写真（WebP 形式に変換後 ~80KB 以内）
- [ ] CEO セクション直後に新セクション配置
- [ ] モバイルで 3 カラム → 縦積み

---

## B-04 FAQ 6→12 項目拡充

**依頼先ロール**: 人事（回答作成） + コピーライター（文言整理） + デザイナー（実装）
**優先度**: P2
**関連 Issue**: #59

### 依頼概要

LP の FAQ セクションを現在の 6 項目から 12 項目に拡充し、未回答の主要な就活生疑問をカバーしてください。

### プロジェクト背景

株式会社WEBY 2027年卒新卒採用LP。現 FAQ は 6 項目しかなく、応募検討中の就活生の重要な疑問（選考期間・残業時間・リモート可否・会社規模・離職率など）に未回答。

### 現行 FAQ

```
1. 面接ではどんなことを見ていますか？
2. 入社後の研修はありますか？
3. 未経験でも活躍できますか？
4. 配属はどのように決まりますか？
5. 社内の雰囲気はどんな感じですか？
6. 福利厚生はありますか？
```

### 依頼内容

以下 6 項目を追加。回答は人事で承認必須。

### 追加 Q&A

**Q7. 選考期間はどのくらいですか？**

```
応募から内定までは平均 3〜4 週間です。
・1次選考（書類）: 3 営業日以内にご連絡
・2次選考（面接）: 応募後 1 週間以内
・3次選考（代表面接）: 2 週間目
・最終結果: 3 週間目

ご状況（他社選考・学業）に応じて柔軟に調整いたします。
```

**Q8. リモートワークは可能ですか？**

```
新卒 1 年目は原則出社（銀座本社）です。
入社 2 年目以降、業務や職種に応じて週 1〜2 日のリモート
勤務が可能です。

なお沖縄在住の方は那覇支社勤務での選考も可能です。
```

**Q9. 残業は平均どのくらいですか？**

```
月平均 20 時間前後です（2025 年度実績）。
繁忙期で 30 時間、落ち着く月で 10 時間程度。

残業は「仕組みで減らす」を徹底し、業務効率化ツール導入・
会議時間削減を継続中です。
```

**Q10. 転勤はありますか？**

```
基本的にありません。
本社（東京・銀座）または那覇支社での勤務が中心。
ご希望がない限り、勤務地変更を命じることはありません。
```

**Q11. 会社の規模を教えてください**

```
株式会社WEBY は 2011 年設立、社員数約 50 名の独立系
Web コンサルティング企業です。

・本社: 東京都中央区銀座
・主事業: 士業向け Web コンサルティング / 自社メディア運営
・代表: 中野 秀征

売上は過去 3 年で 230% 成長。継続取引のクライアントが
事業の基盤です。
```

**Q12. 離職率や定着率は？**

```
直近 3 年の新卒定着率は 90% 以上です。
辞めた方の理由は主に「独立」「海外留学」など前向きなもの
中心。卒業生とは今もつながりがあり、業務委託として戻って
くれるケースもあります。
```

### 実装仕様

既存 `.faq-item` 構造を踏襲（index.html:3261 付近）:

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
      <p class="faq-a-text">応募から内定までは平均 3〜4 週間です。...</p>
    </div>
  </div>
</div>
```

### 受入条件

- [ ] 人事が 6 項目の回答を承認（特に残業時間・離職率は精査）
- [ ] 既存デザイン（ダーク版）を維持
- [ ] 初期状態は全項目閉じる
- [ ] design.md §4.13 文字数ルール準拠（質問 40 字以内、回答 120-400 字）

---

## B-05 Job Board 配置戦略決定

**依頼先ロール**: 人事 + マーケ担当
**優先度**: P1
**関連 Issue**: #63

### 依頼概要

mynavi / doda バナー（Job Board セクション）の配置を戦略的に決定してください。

### プロジェクト背景

株式会社WEBY 2027年卒新卒採用LP の現 section order:

```
Recruit(募集要項) → Post-Recruit CTA(直接応募) → Job Board(mynavi/doda) → FAQ → Footer
```

### 課題

募集要項を読み終えた応募意欲 MAX の瞬間に、外部 ATS（mynavi/doda）への導線が挟まっており、**直接応募の前に外部サイトへ流出するリスク**がある。

### 依頼内容

以下 4 選択肢から意思決定:

**Option A: 現状維持**
- Recruit → 直接 CTA → Job Board → FAQ → Footer
- 効果: 両導線並存、直接 CTA 追加済（PR #55）で改善済み

**Option B: Job Board を Footer の下へ移動（推奨）**
- Recruit → 直接 CTA → FAQ → Footer → Job Board（もし迷ったら）
- 効果: 直接応募を主導線に、Job Board は「最後の選択肢」

**Option C: Job Board を Recruit の前に移動**
- CEO → Job Board → Recruit → 直接 CTA → FAQ → Footer
- 効果: 「外部でも見つけられる」trust signal、ただし Recruit 到達前に離脱誘発のリスク

**Option D: Job Board 撤去**
- Recruit → 直接 CTA → FAQ → Footer
- 効果: 直接応募に完全集中、mynavi/doda 有料枠の価値が変化

### 判断に必要な情報

- 現在の応募経路別比率（直接 / mynavi / doda）
- mynavi / doda の月額掲載料 vs 獲得応募数の費用対効果
- ATS 側と各媒体経由の応募者プール質の差

### 推奨プロセス

1. **今週**: Option A のまま、GA4 導入（Brief C-01 参照）
2. **2 週間後**: クリック率比較
   - 直接 CTA が 70% 以上 → Option B へ移行
   - mynavi/doda 合計が多い → Option A 維持
3. **判断材料**: 各媒体の月額コスト vs 獲得数（人事提供）

### 受入条件

- [ ] 人事・マーケで Option A〜D のいずれかを意思決定
- [ ] 決定後、必要なら HTML セクション順序入れ替え PR 作成

---

## B-06 News Bar コンテンツ整理

**依頼先ロール**: コピーライター + 人事
**優先度**: P2
**関連 Issue**: #68

### 依頼概要

LP トップ付近の News Bar にある 3 項目のテキスト不備（重複・誤用）を修正してください。

### プロジェクト背景

株式会社WEBY 新卒採用LP の Hero 下部に News Bar があり、3 件の告知が並んでいます。現在、以下の問題があります:

```
2025.09.21  RECRUIT  2027年卒中途採用 本選考エントリーを開始しました
2024.08.21  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました
2024.08.21  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました ← 完全重複
```

問題:
1. 中途採用に「年卒」が付与されており不自然
2. 2 件目と 3 件目が完全重複

### 依頼内容

以下 2 案から選択:

**案 1（最小修正）**:

```
2026.04.01  RECRUIT  2027年卒 新卒採用 本選考エントリーを開始しました
2026.03.15  EVENT    カジュアル面談の受付を開始しました
2025.09.21  RECRUIT  中途採用 通年エントリー受付中
```

**案 2（拡充版・5 項目、動きのある情報発信）**:

```
2026.06.10  EVENT    2028 サマーインターンシップ 募集開始（7月中旬〆切）
2026.04.01  RECRUIT  2027年卒 新卒採用 本選考エントリーを受付中
2026.03.15  EVENT    カジュアル面談 毎週水曜 19:00 より開催
2026.02.20  MEDIA    Business+IT に代表インタビューが掲載されました
2025.12.01  RECRUIT  通年長期インターン 募集中（週2日〜）
```

### 実装

既存 `.news-item` 構造を流用。3 項目以上なら CSS `overflow-x: auto` で横スクロール。

### 運用ルール（推奨追記）

- 最新 5 項目を表示、古いものは `archive` フラグで非表示
- tag 種別: `RECRUIT` / `EVENT` / `MEDIA` / `NEWS`
- 将来的に CMS 化（microCMS / Contentful 等）を検討

### 受入条件

- [ ] 3 項目すべて独立した意味のある告知になっている
- [ ] 中途採用項目は「年卒」表記なし
- [ ] 日付が実ニュース日時と整合

---
---

# Part C: 計測・調査基盤

---

## C-01 GA4/GTM 計測導入

**依頼先ロール**: エンジニア + マーケ担当
**優先度**: P0（すべての CRO 施策の前提）
**関連 Issue**: #64

### 依頼概要

Google Analytics 4 と Google Tag Manager を導入し、ENTRY クリック・Job Board クリック・スクロール深度の 3 大イベントを計測開始してください。

### プロジェクト背景

株式会社WEBY 新卒採用LP（2027年卒向け）。現在、応募経路ごとのクリック数・応募数・離脱率が**一切計測されていない**。

この状態では:
- 他施策が効いたか分からない
- A/B テストのベースラインが取れない
- どこで離脱しているか不明
- 意思決定がすべて「推測」になる

### 依頼内容

### 1. GTM snippet を `<head>` に追加

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXX');</script>
```

### 2. `<body>` 直後に noscript 追加

```html
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
```

### 3. ENTRY 系リンクに `data-*` 属性付与

```html
<!-- Nav ENTRY -->
<a href="..." data-event="entry_click" data-location="nav" class="nav-entry">ENTRY</a>

<!-- Post-Recruit CTA -->
<a href="..." data-event="entry_click" data-location="post-recruit" class="recruit-cta-btn">ENTRY →</a>

<!-- Footer PRE-ENTRY -->
<a href="..." data-event="entry_click" data-location="footer">PRE-ENTRY</a>

<!-- Mobile Sticky -->
<a href="..." data-event="entry_click" data-location="mobile-sticky">ENTRY</a>

<!-- Job Board -->
<a href="..." data-event="jobboard_click" data-board="mynavi">...</a>
<a href="..." data-event="jobboard_click" data-board="doda">...</a>
```

### 4. GTM タグ設定（GTM Container 内）

| イベント名 | 送信タイミング | パラメータ |
|----------|-----------|----------|
| `page_view` | ロード（自動） | page_title, page_location |
| `entry_click` | ENTRY 系クリック | location(nav/post-recruit/footer/mobile-sticky) |
| `jobboard_click` | Job Board クリック | board(mynavi/doda) |
| `scroll_depth` | 25/50/75/90% 到達 | depth |
| `faq_open` | FAQ 開 | question_index |
| `worker_modal_open` | 社員モーダル開 | worker_index |
| `form_submit_success` | n8n 応募完了 | form_id |

### 5. コンバージョン設定

- Primary conversion: `entry_click`
- Secondary conversion: `form_submit_success`（n8n 側実装必要）

### 受入条件

- [ ] GTM コンテナ作成・GA4 プロパティ連携
- [ ] 全 ENTRY 系 a タグに `data-event` 属性
- [ ] GTM プレビューモードで 7 イベント全て発火確認
- [ ] GA4 Realtime で 24h 以内に到達確認
- [ ] 1 週間データ取得してベースライン確定

### 追加推奨

- Microsoft Clarity（無料ヒートマップ）を同時導入

### 参考

- GTM: https://tagmanager.google.com
- GA4: https://analytics.google.com
- Clarity: https://clarity.microsoft.com

---

## C-02 Exit-intent Survey

**依頼先ロール**: エンジニア
**優先度**: P2（GA4 導入後に着手）
**関連 Issue**: #60

### 依頼概要

ページ離脱しようとした瞬間に 1 問アンケートを表示し、なぜ応募しないのか直接ヒアリングする仕組みを実装してください。

### プロジェクト背景

GA4（Brief C-01）だけでは「どこで離脱したか」は分かるが「**なぜ**」が分からない。定性調査で離脱理由を直接ヒアリングする。

### 依頼内容

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

### 実装選択肢

| 方法 | 長所 | 短所 |
|------|------|------|
| Microsoft Clarity | 無料・軽量 | アンケート機能限定 |
| Hotjar | 多機能 | 無料枠 35 sessions/月 |
| 自作 + Google Forms | 無料・自由 | UI 作り込み必要 |

### 推奨: 自作 + Google Forms バックエンド

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
  gtag('event', 'exit_survey_submit', { reason: data.get('reason') });
  fetch('https://docs.google.com/forms/...', { method: 'POST', body: data });
  document.getElementById('exitSurvey').hidden = true;
});
```

### 受入条件

- [ ] 訪問 1 回につき最大 1 回（localStorage 制御）
- [ ] モバイル対応（邪魔にならないトリガー）
- [ ] 2 週間実行 → 集計結果を Issue #60 にコメント
- [ ] 上位 3 位の離脱理由に対し O/CO テーブル作成

---

## C-03 応募後アンケート

**依頼先ロール**: エンジニア + 人事
**優先度**: P2
**関連 Issue**: #61

### 依頼概要

応募完了直後に「応募の決め手」を 3 問ヒアリングし、LP のどこが一番効いたかをデータ化してください。

### プロジェクト背景

就活生は応募ボタンを押すまでの心理プロセスを言語化できる瞬間（応募直後）がある。ここで決め手を聞き、LP 改善の根拠データを取得。

### 依頼内容

### 配置

n8n 応募フォームのサンクスページ、または完了時自動返信メール内のリンク。

### UI ワイヤーフレーム

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
- 事業内容
- 研修制度
- 社員ストーリー（Workers）
- CEO メッセージ
- 数字で見る WEBY
- 内定者の声
- 募集要項
- 選考フロー
- 応募の直前（Recruit 直後 CTA）
- その他
```

### 実装方法

- n8n のサンクス画面を改修 or redirect URL を Google Forms に変更
- 回答は Google Spreadsheet 自動集計

### 受入条件

- [ ] 3 ヶ月運用、月次レビュー
- [ ] 結果を Issue #61 にコメント
- [ ] 判明した「決め手セクション」を Hero 近くに前倒し検討

---
---

# Part D: 新規セクション

---

## D-01 AI Era Manifesto

**依頼先ロール**: コピーライター + 代表（文案承認） + デザイナー
**優先度**: P0
**関連 Issue**: 未起票（本書 D-01 として扱う）

### 依頼概要

「AI 時代に人間がやる仕事」を明確に宣言する新セクションを Hero 直下付近に追加し、2027 卒の最大不安（「AI に仕事を奪われる」）への明確な会社スタンスを示してください。

### プロジェクト背景

株式会社WEBY 2027年卒新卒採用LP。2027 卒の就活生にとって最大の不安は「AI 時代に自分の仕事が残るか」。この不安への明確なスタンス表明は、他社との最大の差別化要因。

### 依頼内容

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
│  │              │ │              │ │              ││
│  │ データ分析・ │ │ 信頼関係・   │ │ 後者の       ││
│  │ レポート作成 │ │ 戦略判断・   │ │ 仕事です。   ││
│  │ ・定型業務   │ │ 共創         │ │              ││
│  └──────────────┘ └──────────────┘ └──────────────┘│
│                                                      │
│  ―― 代表 中野 秀征 からの一言 ――                    │
└──────────────────────────────────────────────────────┘
```

### 本文案

```
【見出し】
AI ERA MANIFESTO
AIに任せない仕事を、私たちは選ぶ。

【リード】
AI で効率化できる仕事は、AI に任せます。
だからこそ、私たちは「信頼を築く」仕事に、人を集めます。

【カラム1: AI で効率化】
・データ分析
・レポート作成
・定型的な運用業務
・施策の初期案出し
→ AI は強力なアシスタント

【カラム2: 人間だからこそ担う】
・クライアントとの信頼関係構築
・複雑な経営課題の戦略判断
・チーム・クライアントとの共創
・価値観を賭けた意思決定
→ ここに人の仕事が残る

【カラム3: あなたが担当するのは】
後者の、人にしかできない仕事。

AI 時代だからこそ、信頼を築ける人
戦略を描ける人が、必要とされます。

WEBY はそういう人を育てる会社です。

【結び - 代表の一言】
「仕事が AI に奪われる」と心配する時代だからこそ、
奪われない仕事の中核 = 信頼 に全振りします。

――― 代表取締役 中野 秀征
```

### 実装仕様

**配置**: Hero Stats Strip の直後、News Bar の前

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

### クリエイティブ指示

- 背景: ダーク（`#0d0d0d`）で他セクションと差別化
- アイコン: Font Awesome の `fa-robot` / `fa-handshake` / `fa-bolt`
- 動き: スクロール到達で 3 カラム順次フェードイン（`.reveal` + stagger）
- 代表一言: italic 書体で差別化

### 受入条件

- [ ] 代表 or ブランドオーナーが本文承認
- [ ] Hero Stats 直後に挿入
- [ ] モバイルで 3 カラム → 縦積み
- [ ] `prefers-reduced-motion: reduce` で stagger 無効

---

## D-02 WHY 事業コンセプト

**依頼先ロール**: コピーライター + 代表 + デザイナー
**優先度**: P1
**関連 Issue**: 未起票

### 依頼概要

Business（何をしているか）セクションの前に、**WHY**（なぜこの事業をやっているか）を語る新セクションを追加してください。

### プロジェクト背景

株式会社WEBY 採用LP。現在 Business セクションは事業内容（士業向け Web コンサル / 自社メディア）を並べているが、「なぜこの事業なのか」の WHY が語られていない。就活生の共感フックを作るには WHY が必要。

### 依頼内容

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  WHY WE EXIST                                        │
│                                                      │
│  ┌─────────────┐  ┌─────────────────────────┐      │
│  │              │  │                         │      │
│  │ [象徴写真]   │  │ 信頼と専門性が、        │      │
│  │              │  │ まだ届いていない人が    │      │
│  │ (メディア UI │  │ いる。                  │      │
│  │ モックアップ │  │                         │      │
│  │ 等)          │  │ ・借金で悩む人に、      │      │
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

### 本文案

```
【見出し】
WHY WE EXIST
信頼と専門性が、まだ届いていない人がいる。

【本文】
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

現 Business セクションの**直前**

### クリエイティブ（象徴写真の 3 候補）

- **A**: クライアント（士業）との打合せ風景（顔出し許諾要）
- **B**: 自社メディア UI のモックアップ（債務急済・専門家プロファイル）★推奨（許諾不要・事業内容も伝わる）
- **C**: 抽象イラスト（「つなぐ」を表現する橋・糸・光）

### HTML

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
        <div class="why-body"><p>私たちのクライアントは...</p></div>
      </div>
    </div>
  </div>
</section>
```

### 受入条件

- [ ] 代表 / ブランドオーナーが本文案承認
- [ ] Business セクションの前に配置
- [ ] モバイル: 写真 → テキスト の縦積み

---

## D-03 選考フロー図

**依頼先ロール**: 人事（フロー情報） + デザイナー
**優先度**: P0
**関連 Issue**: 未起票

### 依頼概要

ENTRY 後の選考プロセスをビジュアルタイムラインで可視化し、「応募してからどうなるか」の不透明感を解消してください。

### プロジェクト背景

株式会社WEBY 採用LP。現在「応募した後に何が起こるか」の情報がなく、応募前の不安（Effort objection）を残した状態。就活生にとって選考期間の不透明さは離脱要因。

### 依頼内容

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

※ 上記フローの日数・回数・場所・服装等は **人事が実運用に合わせて確定** してください。

### 配置

Recruit セクションの**直下**、既存の Post-Recruit CTA の**前**。

### 実装仕様

既存 `.training-flow` パターン流用（矢印 ::after の border trick 等）:

```html
<section class="hiring-flow">
  <div class="container reveal">
    <span class="m-script">HIRING PROCESS</span>
    <h2>応募から内定まで、<em>全 3-4 週間</em></h2>
    <div class="hiring-flow-steps">
      <div class="hiring-step"><!-- STEP 1 --></div>
      <!-- STEP 2, 3, 4 -->
    </div>
    <div class="hiring-detail">
      <!-- 各ステップ詳細カード -->
    </div>
  </div>
</section>
```

### 受入条件

- [ ] 人事より実際のフロー情報（ステップ数・期間・場所・服装）取得
- [ ] 既存 training-flow の CSS を流用（矢印 ::after border trick）
- [ ] モバイルで縦積み、矢印「↓」に変換

---

## D-04 JOIN US 3 チャネル

**依頼先ロール**: 人事 + マーケ + デザイナー
**優先度**: P0
**関連 Issue**: 未起票

### 依頼概要

サマーインターン・通年長期インターン・説明会の 3 つの低コミットメントな入口を追加し、「今はまだ応募しないがキープしたい」層を囲い込んでください。

### プロジェクト背景

株式会社WEBY 2027年卒新卒採用LP。現在のエントリーポイントは「本選考応募（ENTRY）」のみ。まだ情報収集段階の学生や 2028 卒の学生に対する入り口が存在しない。

### 依頼内容

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

### カード 1: SUMMER INTERNSHIP

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
```

### カード 2: YEAR-ROUND LONG-TERM INTERNSHIP

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

【特典】本選考への優遇措置あり
```

### カード 3: INFO SESSION

```
【対象】2027 年卒（本選考応募検討者）
【形式】オンライン（Meet）
【時間】30 分
【内容】
 ・代表からのメッセージ（10 分）
 ・若手社員との Q&A（15 分）
 ・質疑応答（5 分）

【開催】毎週水曜日 19:00〜19:30
【定員】各回 10 名
```

### 配置

Recruit セクションの**前**、または独立セクションとして Workers の後

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

### 受入条件・必要な準備

- [ ] サマーインターン URL + 実施日程 + 定員確定
- [ ] 長期インターン URL + 時給・条件確定
- [ ] 説明会予約システム（TimeRex / Googleカレンダー予約等）設定
- [ ] カード 3 枚の本文・日付を人事で承認

---

## D-05 通年インターン 追従サイド CTA

**依頼先ロール**: デザイナー + 人事
**優先度**: P1
**関連 Issue**: 未起票

### 依頼概要

長期インターン募集中であることを常時表示する追従型 CTA を、デスクトップ右端に固定で配置してください。

### プロジェクト背景

長期インターンは早期接触 × 採用直結の強力な武器。スクロール中常に目に入る位置に置けば、意欲の高い学生を取り逃がさない。

モバイル版は Brief D-8（実装済 PR #69）の下固定 CTA バーに統合されているので、本ブリーフは **デスクトップのみ** の対応。

### 依頼内容

### ワイヤーフレーム

```
  [メインコンテンツ領域]          ┌──────────┐
                                  │ 長期     │
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
  .sticky-side-cta { display: none; } /* モバイルは下固定 CTA に統合 */
}
```

### 非表示タイミング（JS）

- Hero 表示中（最初の 80vh 以内）
- `.join-us` / `.recruit-cta` / `footer` 表示中
- 上記以外では表示

### 受入条件

- [ ] 長期インターン応募 URL 確定
- [ ] モバイル（≤768px）では完全非表示
- [ ] 関連セクション表示中は自動で隠れる
- [ ] `:focus-visible` 対応

---

## D-06 note/SNS 連携ブロック

**依頼先ロール**: 広報 + デザイナー
**優先度**: P2
**関連 Issue**: 未起票

### 依頼概要

公式 note の推薦記事 3 本と、主要 SNS リンクを並べた「会社をもっと知る」セクションを Footer 直前に追加してください。

### プロジェクト背景

株式会社WEBY は note 等で情報発信しているが、LP 内に導線が無い。応募には至らないが興味深い人を note 購読 → メール取得 → ナーチャリングの導線として機能させる。

### 依頼内容

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

### 本文案

```
【見出し】
LEARN MORE
会社をもっと知る

【リード】
公式 note で、社員や代表の生の声を発信中。
LP では伝えきれない、日常と挑戦をお届けします。

【SNS アカウント行】
・X (@weby_official) — 日常の気づき・採用ニュース
・Instagram (@weby_inc) — オフィス風景・社員の顔
・YouTube — オフィスツアー・社員インタビュー動画
・note — 長文記事・考え方
```

### 配置

FAQ セクションの**後**、Footer の**前**。

### HTML

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

- [ ] 公式 note アカウント URL
- [ ] 推薦 3 記事の URL + サムネイル画像（1200×630 程度）
- [ ] X / Instagram / YouTube アカウント URL

### 受入条件

- [ ] FAQ の後・Footer の前に配置
- [ ] note カード 3 枚、クリックで別タブ遷移（rel=noopener noreferrer）
- [ ] SNS アイコンに aria-label 付与

---

## D-07 数字で見る WEBY

**依頼先ロール**: 人事（数値確認） + デザイナー
**優先度**: P1
**関連 Issue**: 未起票

### 依頼概要

会社を特徴づける 8 つの数字を一覧表示するインフォグラフィック・セクションを追加してください（特に親世代の信頼獲得）。

### プロジェクト背景

Hero 直下の Stats Strip（5 項目）は入口の名刺として機能。本セクションはディープダイブとして**ページ中盤**に配置し、成長率・定着率など具体指標で信頼強化。

### 依頼内容

### ワイヤーフレーム

```
┌──────────────────────────────────────────────────────┐
│  WEBY BY THE NUMBERS                                 │
│  数字で見る WEBY                                     │
│                                                      │
│  ┌────────┬────────┬────────┬────────┐              │
│  │ 230%   │ 25歳   │ 120日  │ 6ヶ月  │              │
│  │ 成長率 │ 平均   │ 年間   │ 独立   │              │
│  │ (YoY)  │ 年齢   │ 休日   │ 目安   │              │
│  │ 3 年   │ 若手が │ 業界   │ 全員が │              │
│  │ 連続成長│ 中心の │ 平均以 │ 6ヶ月で│              │
│  │        │ チーム │ 上     │ 自走へ │              │
│  └────────┴────────┴────────┴────────┘              │
│                                                      │
│  ┌────────┬────────┬────────┬────────┐              │
│  │ 50+    │ 15年   │ ¥390万 │ 99%    │              │
│  │ 社員数 │ 創業   │ 1年目  │ 定着率 │              │
│  │        │ からの │ 年収   │ (3年)  │              │
│  │ (2026) │ 2011   │ 新卒   │ 直近   │              │
│  │ 年時点 │ 設立   │ 平均   │ 3年    │              │
│  └────────┴────────┴────────┴────────┘              │
└──────────────────────────────────────────────────────┘
```

### 各数字の背景説明文

```
【230%】成長率（YoY）
直近 3 年、前年比 230% 前後で成長を続けています。
クライアント数と取引継続率の両輪。

【25歳】平均年齢
若手中心のチームで、意思決定のスピードが早い。
ベテラン（30-40 代）も約 20% 在籍。

【120日】年間休日
完全週休 2 日（土日祝）+ 年末年始・夏季・慶弔。
IT 業界平均（107 日）を大きく上回ります。

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

### 配置

CEO セクションの**後**、Recruit の**前**。

### HTML

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

### 必要な準備

- [ ] 各数字の公表可否を人事で確認
- [ ] 成長率・定着率は**最新実績値**を再確認（古い数字は誤解を生む）
- [ ] 注釈文を人事で文言承認

### 受入条件

- [ ] 全 8 カード表示、モバイルで 2×4 or 1 カラム
- [ ] 数字サイズは目立つ（2.5-3rem）
- [ ] 注釈文は 40 文字以内

---

## D-09 オフィス動画ツアー

**依頼先ロール**: 映像制作者（外注 or 社員） + 総務
**優先度**: P2
**関連 Issue**: 未起票

### 依頼概要

銀座オフィスを 60-90 秒で紹介する動画を制作し、Facility セクションに埋め込んでください。

### プロジェクト背景

現 Facility セクションは静止画 3 枚のみ。動画 1 本の方が雰囲気が圧倒的に伝わる。

### 依頼内容

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

### 実装（LP 側）

YouTube アップロード後、以下埋込み:

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

Facility セクション内、写真グリッドの**上**（動画 → 写真の順に詳細化）。

### 必要な準備

- [ ] 撮影依頼（プロ依頼 or 社員撮影）
- [ ] YouTube アップロード（unlisted でも可、できれば公開）
- [ ] 撮影時の社員同意取得

### 受入条件

- [ ] 60-90 秒、MP4、1920×1080 以上
- [ ] 音声: 環境音 + BGM、ナレーションなし
- [ ] LP に埋込、モバイルでも問題なく再生

---

## D-10 親世代向け FAQ

**依頼先ロール**: 人事（回答作成） + コピーライター
**優先度**: P2
**関連 Issue**: 未起票

### 依頼概要

内定承諾時の親との会話を想定し、親世代向けの会社説明 FAQ を追加してください。

### プロジェクト背景

内定承諾の最終局面で、親のブロックが発生するケースあり。事前に親世代が知りたい情報を提示することで、承諾率を上げる。

### 依頼内容

### 構成選択肢

**方針 A**: 既存 FAQ の**末尾**に「ご家族の方へ」タブで追加

**方針 B**: 独立セクション「ご家族の方へ」を新規作成（推奨）

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

**Q1. 会社の規模は？**

```
社員数約 50 名、2011 年創業の 15 年目の会社です。
本社は東京都中央区銀座、主要事業は Web コンサルティング。
独立系（親会社・グループ会社なし）の中堅 IT 企業に位置づけられます。
```

**Q2. 売上や業績は？**

```
直近 3 年で売上 230% 成長を達成しました。
継続取引のクライアント（士業事務所）が基盤で、
一時的な案件に依存しないストック型の収益構造。黒字経営を継続。

具体的な売上額は非公開ですが、帝国データバンク等の信用情報機関で確認いただけます。
```

**Q3. 社会保険はどこですか？**

```
健康保険・厚生年金・雇用保険・労災保険すべて完備しています。
健康保険は「協会けんぽ（東京支部）」加入です。
```

**Q4. 育休・産休の実績は？**

```
育児休業は 3 名（男性 1 名、女性 2 名）の取得実績。
全員が復職し、現在も在籍中です。
男性の育休取得も推奨、1 週間〜1 ヶ月の短期取得も可能。
```

**Q5. 昇給・賞与はどれくらい？**

```
昇給: 年 1 回（4 月）、業績と評価に連動
賞与: 年 1〜2 回（夏・冬）、業績により支給額決定

新卒 1 年目平均 390 万円、3 年目で 520 万〜 650 万円が一般的なレンジ。
```

**Q6. 親が会社見学できる機会は？**

```
「保護者会社訪問会」を年 2 回（8 月・12 月）開催しています。
銀座オフィスにお越しいただき、代表からのご挨拶と、
お子様の先輩社員との座談会を予定しています。

個別見学も随時受け付け。03-6280-4361 までお気軽に。
```

### 親御様向け PDF（オプショナル）

```
【内容】A4 × 4 ページ PDF
1. 会社概要（会社案内ベース）
2. 事業内容の説明（専門用語なしで）
3. よくあるご質問（本 FAQ の拡張版）
4. 代表からのメッセージ
5. 採用担当連絡先

【配布】LP からダウンロード + 説明会参加者に印刷版配布
```

### 必要な準備

- [ ] 人事で 6 項目の回答を承認（売上数字は公表範囲を精査）
- [ ] 親御様向け PDF 制作（デザイナー依頼）

### 受入条件

- [ ] FAQ セクション末尾 or 独立セクションで配置
- [ ] 既存 FAQ アコーディオン UI と視覚的に差別化（見出し色・背景色）
- [ ] PDF ダウンロードリンクに `download` 属性
