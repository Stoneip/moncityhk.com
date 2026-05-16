# Changelog

## v0.9.0 (2026-05-16)

### 變更（Google Ads 友善 — 全站移除「維修」字眼）
- **品牌名**：「MonCity 手機維修」→「MonCity 換Mon城」（統一用 alternateName）
- **替換規則**：
  - 零件名 + 維修 → 零件名 + 服務（e.g.「維修螢幕玻璃」→「螢幕玻璃服務」）
  - 「即場維修」→「即場處理」
  - 「維修服務」→「服務」
  - 「維修費用」→「更換費用」
  - 「維修店」→「服務店」
  - 「維修經驗」→「服務經驗」
  - 「維修攻略」→「保養攻略」
  - 「手機維修 vs 換新機」→「手機換零件 vs 換新機」
- **原因**：「維修」字眼影響 Google Ads 投放（疑似觸發第三方手機維修 / 解鎖類別政策審查）
- **影響範圍**：65+ 處 across 14 檔案
  - Layouts：`BaseLayout.astro`（siteName + JSON-LD `alternateName` + `description`）
  - Components：Hero、Services、Process、Stats、FAQ、Header、Footer、Contact、FloatingWhatsApp
  - Pages：index、blog/index、privacy、404 嘅 SEO meta + body
  - Blog 4 篇：choose-repair-shop、broken-screen-what-to-do、repair-vs-new-phone、iphone-battery-guide
  - public/llms.txt
- **WhatsApp 預填訊息**：URL-encoded `手機維修報價` → `手機服務報價`（Hero/Header/Footer/Contact/FloatingWhatsApp 5 處）
- Verify：`grep -r 維修 dist/` = 0 hit ✅

### 注意
- Blog slug（`choose-repair-shop` / `repair-vs-new-phone` / `broken-screen-what-to-do`）保持不變，避免 SEO equity 損失同 redirect 麻煩
- v0.8.0 為相反方向（改回「維修」），本版重新切換回「服務」定位以配合 Google Ads

---

## v0.2.0 (2026-04-27)

### 變更
- 主色由藍色 (#0066cc) 改為紅色 (#cc0000)，配合品牌形象
- CTA 按鈕、連結、流程步驟等所有 accent 元素改為紅色
- Hero 背景漸層改為淡紅色

### 新增
- Google Analytics 4 追蹤（G-7B53J3CMY2）
- 顧客評價區（Reviews section）：Google Business badge + 3 張評價卡片
- Google Business 連結整合（MONCITY 換Mon城維修中心）
- /sitemap.xml → /sitemap-index.xml 301 redirect（方便 Google Search Console 提交）
- Header 加入「評價」導航連結
- LocalBusiness schema 加入 sameAs（Google Maps）+ alternateName

### 修正
- Google Maps embed 更新為正確嘅 MONCITY Place ID
- 坐標更精確（22.3314439, 114.1618173）
- favicon 改為紅色

## v0.1.0 (2026-04-27)

### 新增
- 建立 Astro 6.x 靜態網站
- 首頁 Landing Page：Hero、服務介紹（6項）、維修流程（3步驟）、FAQ（6題）、聯絡資訊
- BaseLayout 含完整 SEO：meta tags、OG、Twitter Cards、canonical URL
- JSON-LD Schema：LocalBusiness、WebSite、FAQPage
- 私隱政策頁面
- 自定義 404 頁面
- 響應式設計（Mobile-first）
- Sticky header + mobile hamburger menu
- WhatsApp CTA 連結（+852 6996 0711）
- Google Maps 嵌入（深水埗深之都）
- robots.txt 允許所有 crawler 包括 AI crawlers
- @astrojs/sitemap 自動生成 sitemap
- Cloudflare Pages 部署配置
