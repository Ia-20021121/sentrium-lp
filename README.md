# Sentrium — Landing Page

架空の B2B SaaS **Sentrium**（モダンインフラ向けネットワーク可観測性／監視プラットフォーム）の、デザイン性重視・単一ファイルのランディングページです。検証案件のため内容・実績・社名はすべてダミーです。

## 特徴・制約

- **単一HTMLファイル / 依存ゼロ / 手書きCSS**（Tailwind等フレームワーク不使用）
- 外部参照は **Google Fonts の `<link>` のみ**（`preconnect` + `font-display: swap`）
- **絵文字なし**、アクセシビリティ（a11y）を一貫して維持
- ビルド不要。`index.html` を**ダブルクリックでブラウザ表示**できます

## デザイントークン（正本）

設計の正本は [`design-tokens.md`](./design-tokens.md) にまとめています。要約:

- 配色: 背景 `#FBFBFD` / 文字 `#0E1726` / アクセント `#2F6BFF`（＋反転面 `#0B1220`）
- フォント: 見出し **Space Grotesk** / 本文 **Inter**
- 見出しは `clamp()` で流体化、余白は 8px ベースのスケール、角丸 10/14/22px
- モーション言語: スクロール出現フェード（一度だけ）／ホバーで微浮上／数値カウントアップ／上品な範囲

## 実装している動き（バニラJS・依存ゼロ）

- `[data-fade]` を IntersectionObserver で一度だけフェード出現（stagger 付き）
- 数値のカウントアップ（easeOutCubic）
- タブ（roving tabindex・矢印/Home/End キー対応、`aria-selected`）
- アコーディオン（`aria-expanded` ＋ `grid-template-rows: 0fr→1fr`）
- モバイルナビ（`aria-expanded` 連動・フォーカストラップ・Escで閉じる）
- マグネットCTA（`requestAnimationFrame` + lerp、`pointer:fine` 時のみ）
- `prefers-reduced-motion: reduce` で全アニメ無効化、`noscript` フォールバックあり

## ローカルでの開き方

```bash
# そのまま開く
# index.html をダブルクリック

# もしくは簡易サーバー
python -m http.server 8000
# http://localhost:8000/index.html
```

## 検証結果（375 / 768 / 1440px）

- 1440: 3カラム構成・余白広め、横溢れなし
- 768: ヒーロー縦積み＋2カラム再構成、横溢れなし
- 375: ハンバーガーナビ・1カラム、横溢れ／見切れなし

`overflow-x: clip` を予防的に適用し、見出しは `clamp()` で明示しています。
