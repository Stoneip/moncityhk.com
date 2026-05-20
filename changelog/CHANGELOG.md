# Changelog

## v0.10.1 (2026-05-20)

### 變更
- **禮物 Banner 改為 Modal 登入**：首頁「立即領取」由跳轉 `/discount/` 改為直接彈出 Google Login modal，登入成功後先跳轉
- **sessionStorage 傳遞 credential**：從首頁 modal 登入後，credential 經 sessionStorage 帶去 `/discount/` 頁面，直接顯示禮物結果（跳過重複登入）
- **Google OAuth Client ID 已設定**：`PUBLIC_GOOGLE_CLIENT_ID` 環境變數已配置（stoneip-dashboard project）

### 流程
1. 客人喺首頁 click「立即領取 🎁」
2. 彈出 modal → Google Sign-In 按鈕
3. 登入成功 → sessionStorage 儲存 credential → 跳轉 `/discount/`
4. `/discount/` 讀取 credential → 直接顯示神秘禮物 + 留評按鈕

---

## v0.10.0 (2026-05-20)

### 新增
- **神秘禮物頁面** `/discount/`：Google Sign-In 登入後顯示「神秘禮物」證明（客人名 + 日期），下方有 Google Maps 留評按鈕
  - Google Identity Services（純 client-side，唔需要 backend）
  - GA4 Enhanced Conversions：自動 set `user_data`（hashed email）配對 Google Ads 廣告點擊
  - Fire `discount_claimed` + `review_from_gift` GA4 events
  - 需要設定 `PUBLIC_GOOGLE_CLIENT_ID` 環境變數（Google Cloud OAuth Client ID）
- **首頁禮物 Banner**：FAQ 同 Contact 之間加紅色 CTA banner「完成服務？領取你嘅神秘禮物」，link 去 `/discount/`，fire `gift_banner_click` event
- **Reviews 留評按鈕**：Reviews section 底部加「留低你嘅評價」按鈕，fire `leave_review_click` GA4 event

### 新增 Components
- `GiftBanner.astro`：首頁禮物 banner

### 新增 Pages
- `discount.astro`：Google Login + 禮物領取 + Google Maps 留評

### 注意
- `/discount/` 未加入 Header navigation（只供店內客人使用，由店員提供 URL/QR code）
- Google Sign-In 需要先設定 OAuth Client ID 先至 work（見 CLAUDE.md 或 README）

---

## v0.9.1 (2026-05-18)

### 修正
- **地址修正**：深水埗站出口由 D2 改為 D1（Hero、Contact、llms.txt 共 3 處）

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
