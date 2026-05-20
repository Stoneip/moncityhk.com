# moncityhk.com — MonCity 換Mon城

## 項目概要
香港深水埗手機外觀服務 Landing Page（螢幕、電池、鏡頭即場更換）。

## 技術架構
- **Framework**: Astro 6.x (static output)
- **Hosting**: Cloudflare Pages (native git integration)
- **CSS**: Custom CSS (no framework)
- **語言**: zh-HK

## 項目結構
```
src/
├── layouts/BaseLayout.astro    # 共用 layout（SEO, JSON-LD）
├── components/                 # Header, Hero, Services, Process, Reviews, FAQ, Contact, GiftBanner, Footer
├── pages/                      # index, privacy, discount, 404
└── styles/global.css           # Design tokens + 全局樣式
public/                         # favicon, robots.txt
```

## 指令
```bash
npm run dev      # 啟動開發伺服器
npm run build    # 建置靜態檔案到 dist/
npm run preview  # 預覽建置結果
```

## Deploy（**必須手動 wrangler**）
**重要**：CF Pages git auto-deploy 已失效（2026-05 起 production 一直停留喺舊 commit，git push 後唔會自動 trigger）。**每次 ship 必須跑以下命令**，否則 live 唔會更新：

```bash
npm run build
wrangler pages deploy dist/ \
  --project-name=moncityhk-com \
  --branch=main \
  --commit-hash=$(git rev-parse HEAD) \
  --commit-message="$(git log -1 --pretty=%s)"
```

完成後 verify：
```bash
curl -s https://moncityhk.com/ | grep -oE "<title>[^<]+</title>"
curl -s https://moncityhk.com/ | grep -c "維修"   # 應該係 0
```

備註：wrangler 已 login 喺 Stoneip@gmail.com 戶口（Account ID `b4812f835e4370782067c26d741714f3`）。如失敗跑 `wrangler login`。

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
v0.10.2

## 重要 — 字眼策略
- 全站避免「維修」字眼，改用「服務」/「更換」/「處理」/「保養」
- 原因：Google Ads 投放友善（避免第三方手機維修政策觸發）
- 品牌名統一用「MonCity 換Mon城」（取代「MonCity 手機維修」）
