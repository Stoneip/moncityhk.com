# moncityhk.com — MonCity 手機維修

## 項目概要
香港深水埗手機外觀維修服務 Landing Page。

## 技術架構
- **Framework**: Astro 6.x (static output)
- **Hosting**: Cloudflare Pages (native git integration)
- **CSS**: Custom CSS (no framework)
- **語言**: zh-HK

## 項目結構
```
src/
├── layouts/BaseLayout.astro    # 共用 layout（SEO, JSON-LD）
├── components/                 # Header, Hero, Services, Process, Reviews, FAQ, Contact, Footer
├── pages/                      # index, privacy, 404
└── styles/global.css           # Design tokens + 全局樣式
public/                         # favicon, robots.txt
```

## 指令
```bash
npm run dev      # 啟動開發伺服器
npm run build    # 建置靜態檔案到 dist/
npm run preview  # 預覽建置結果
```

## Deploy
Push to `main` branch → Cloudflare Pages 自動部署。

## 重要資訊
- **Domain**: moncityhk.com (Cloudflare DNS)
- **GCP Account**: stoneip@gmail.com
- **GitHub**: https://github.com/Stoneip/moncityhk.com
- **Cloudflare Account**: Stoneip@gmail.com (Account ID: b4812f835e4370782067c26d741714f3)
- **Zone ID**: 50451c63752fb2aeb58cacca350f6d77

## Analytics
- **GA4**: G-7B53J3CMY2

## 設計
- **主色**: 紅色 (#cc0000)
- **Google Business**: https://maps.app.goo.gl/rtoUcQDWsXnkjuTSA

## 版本
v0.2.0
