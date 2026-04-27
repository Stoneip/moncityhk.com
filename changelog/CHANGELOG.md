# Changelog

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
