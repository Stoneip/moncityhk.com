# moncityhk.com — MonCity 換Mon城

香港深水埗手機外觀服務網站（螢幕、電池、鏡頭即場更換）。

## 簡介

MonCity 換Mon城 位於深水埗深之都，提供各類手機外觀更換服務，包括爆玻璃更換、鏡頭更換、液晶更換、按鍵處理、換電池等。

## 技術架構

- Astro 6.x 靜態網站
- Cloudflare Pages 託管
- 自定義 CSS（無 CSS framework）
- 繁體中文（zh-HK）

## 開發

```bash
npm install
npm run dev
```

## 部署

Push 到 `main` 分支後，Cloudflare Pages 會自動部署。

或手動部署：

```bash
npm run build
wrangler pages deploy dist/ --project-name=moncityhk-com
```

## 版本歷史

### v0.10.0 (2026-05-20)
- 新增 `/discount/` 神秘禮物頁面（Google Sign-In + GA4 Enhanced Conversions）
- 首頁加禮物 Banner（FAQ 同 Contact 之間）
- Reviews section 加「留低你嘅評價」按鈕 + GA4 event tracking
- 需設定 `PUBLIC_GOOGLE_CLIENT_ID` 環境變數啟用 Google Login

### v0.9.1 (2026-05-18)
- 修正深水埗站出口 D2 → D1

### v0.9.0 (2026-05-16)
- 全站移除「維修」字眼以配合 Google Ads 投放（改用「服務」/「更換」/「處理」/「保養」）
- 品牌名統一用「MonCity 換Mon城」
- 影響 65+ 處 across 14 檔案（components、pages、blog、layouts、llms.txt）
- WhatsApp 預填訊息「手機維修報價」→「手機服務報價」

### v0.8.0
- 全站改回「維修」定位（已於 v0.9.0 反向）

### v0.7.0
- 加入統計列、30 條評價牆、Blog 系統、WhatsApp/電話追蹤

### v0.6.x
- Google Ads conversion tag、重新定位為「零件專門店」

### v0.5.0
- WhatsApp 預填訊息、懸浮按鈕、SEO 優化

### v0.4.x
- 官方 logo、SVG icon、PageSpeed/GEO 優化

### v0.3.x
- 紅色 Header/Footer、GA4 events

### v0.2.0 (2026-04-27)
- 主色由藍改紅、GA4、評價區、Google Business 整合

### v0.1.0 (2026-04-27)
- 初始版本
- Landing page：首頁、服務介紹、服務流程、FAQ、聯絡資訊
- SEO: LocalBusiness + FAQPage JSON-LD schema
- Cloudflare Pages 部署
