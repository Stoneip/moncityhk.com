# moncityhk.com — MonCity 手機維修

香港深水埗手機外觀維修服務網站。

## 簡介

MonCity 手機維修位於深水埗深之都，提供各類手機維修服務包括爆玻璃維修、鏡頭更換、液晶維修、按鍵維修、換電池等。

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

## 版本歷史

### v0.1.0 (2026-04-27)
- 初始版本
- Landing page：首頁、服務介紹、維修流程、FAQ、聯絡資訊
- SEO: LocalBusiness + FAQPage JSON-LD schema
- Cloudflare Pages 部署
