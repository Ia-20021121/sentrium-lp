# Sentrium LP — Design Tokens（正本）

架空サービス **Sentrium** — モダンインフラ向けのネットワーク可観測性／監視プラットフォーム（B2B）。
方針: 高い信頼感と先進性。余白広め・上質・過剰装飾なし・技術的誠実さ。ライト基調＋確信感のあるブルー1色のアクセント。

---

## 1. カラー（hex）

| トークン | 値 | 用途 |
|----------|-----|------|
| `--bg` | `#FBFBFD` | ページ背景（ほぼ白・やや青み） |
| `--surface` | `#FFFFFF` | カード／面 |
| `--surface-2` | `#F4F6FA` | 薄いセクション背景・タグ |
| `--ink` | `#0E1726` | 主要テキスト（濃紺＝信頼） |
| `--ink-2` | `#3A4658` | 見出し補助 |
| `--muted` | `#5C6779` | 本文補助・キャプション |
| `--line` | `#E6E9F0` | 境界線・区切り |
| `--accent` | `#2F6BFF` | アクセント（先進性・CTA） |
| `--accent-ink` | `#1B4FD6` | アクセント濃（hover/押下） |
| `--accent-soft` | `#EAF0FF` | アクセント淡（バッジ背景） |
| `--dark` | `#0B1220` | 反転セクション背景（深紺） |
| `--dark-ink` | `#C7D0E0` | 反転セクション上の本文 |
| `--ok` | `#1FA971` | ステータス良（監視文脈の最小限の彩り） |

コントラスト: 本文 `--ink` on `--bg` ≈ 15:1、`--muted` on `--bg` ≈ 5.6:1、白文字 on `--accent` ≈ 4.7:1（いずれも WCAG AA 以上を目安）。

## 2. フォント（Google Fonts）

- 見出し: **Space Grotesk**（幾何学的サンセリフ／モダンで先進的）
- 本文・UI: **Inter**（可読性の高いサンセリフ）
- 等幅（数値・コード片）: **Inter** の tabular 数字を使用（追加読込はしない）

`preconnect` + `display=swap` で読み込む。

## 3. タイポグラフィ・スケール

見出しは `clamp()` で流体化。`line-height` は詰め気味、`letter-spacing` は大見出しほど締める。

| 役割 | size (clamp) | line-height | letter-spacing | weight |
|------|--------------|-------------|----------------|--------|
| Display (h1) | `clamp(2.4rem, 1.4rem + 4.2vw, 4.25rem)` | 1.05 | -0.02em | 600 |
| H2 (section) | `clamp(1.7rem, 1.2rem + 2.2vw, 2.6rem)` | 1.12 | -0.015em | 600 |
| H3 (card) | `clamp(1.12rem, 1rem + 0.5vw, 1.3rem)` | 1.25 | -0.01em | 600 |
| Lead | `clamp(1.05rem, 1rem + 0.4vw, 1.25rem)` | 1.6 | 0 | 400 |
| Body | `1rem (16px)` | 1.7 | 0 | 400 |
| Small / eyebrow | `0.8rem` | 1.5 | 0.16em (eyebrow は uppercase) | 500 |

## 4. 余白スケール（8pxベース）

`--s-1:4px` `--s-2:8px` `--s-3:12px` `--s-4:16px` `--s-5:24px` `--s-6:32px` `--s-7:48px` `--s-8:64px` `--s-9:96px` `--s-10:128px`

- セクション縦余白: デスクトップ `--s-10`、モバイル `--s-9`
- コンテナ最大幅: `1160px`、左右パディング `--s-5`〜`--s-6`

## 5. 角丸・影・境界

- radius: `--r-1:10px`（小）`--r-2:14px`（カード）`--r-3:22px`（大面）`--r-full:999px`
- shadow: `--shadow-1: 0 1px 2px rgba(14,23,38,.06)`、`--shadow-2: 0 18px 40px -18px rgba(14,23,38,.22)`
- border: `1px solid var(--line)`

## 6. セクション構成と順序

1. **Header / Nav**（sticky・スクロールで境界線表示、モバイルはハンバーガー＝aria連動＋フォーカストラップ）
2. **Hero**（eyebrow → 大見出し → リード → CTA2つ → 信頼の一言）
3. **Trust bar**（導入企業ロゴ風のテキストプレースホルダ）
4. **Features**（価値訴求カード 3枚：可視化／異常検知／ゼロトラスト連携）
5. **How it works**（3ステップ）
6. **Metrics**（数字 3〜4：カウントアップ）
7. **Use cases（タブ）**（button + aria-selected、キーボード操作可）
8. **FAQ（アコーディオン）**（button + aria-expanded、grid 0fr→1fr）
9. **CTA band**（資料請求／問い合わせ誘導・反転 `--dark` 面）
10. **Contact**（ダミーフォーム：label 紐付け・必須表示）
11. **Footer**

## 7. モーション言語

- **出現**: `[data-fade]` を IntersectionObserver で一度だけ。`translateY(16px)+opacity0 → 0/1`、`520ms cubic-bezier(.2,.7,.2,1)`、軽いstagger。
- **ホバー**: カードは `translateY(-4px)` ＋ `--shadow-2`、リンクは下線がアンダーラインで伸びる、ボタンは背景濃色化。すべて `200ms`。
- **スクロール**: ヘッダーの境界線フェードイン。任意でCTAボタンの磁石(マグネット)効果を `requestAnimationFrame + lerp` で自前実装。
- **数値**: カウントアップ `easeOutCubic`、約1.4s。
- **無効化**: `prefers-reduced-motion: reduce` で全アニメ・スムーススクロールを停止し即表示。

## 8. アクセシビリティ方針

- スキップリンク、`:focus-visible` の明示リング（`--accent`）、ランドマーク（header/nav/main/footer）。
- タブ＝`role=tablist/tab/tabpanel`、アコーディオン＝`aria-expanded`＋`aria-controls`、ナビ＝`aria-expanded`＋フォーカストラップ＋Escで閉じる。
- 画像は意味に応じた `alt`、装飾は `aria-hidden`。フォームは `label` 関連付け＋必須明示。
- `noscript` フォールバックでJS無効時もコンテンツ到達可能。
