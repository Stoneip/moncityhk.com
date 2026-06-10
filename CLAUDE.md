# moncityhk.com — MonCity 換Mon城

## 項目概要
香港深水埗**手機零件店** Landing Page（iPhone / Samsung / 華為 / Pixel 等手機零件目錄 + 門市選購）。v0.11.0 起重新定位 — 由「手機外觀服務」pivot 至「手機零件店」，配合 Google Ads Third Party Consumer Technical Support policy。

## 技術架構
- **Framework**: Astro 6.x (static output)
- **Hosting**: Cloudflare Pages (native git integration)
- **CSS**: Custom CSS (no framework)
- **語言**: zh-HK

## 項目結構
```
src/
├── layouts/BaseLayout.astro    # 共用 layout（SEO, JSON-LD MobilePhoneStore）
├── components/                 # Header, Hero, Services (零件分類), Process (選購流程), Reviews, FAQ, Contact, GiftBanner, Footer, FloatingWhatsApp, Stats
├── pages/                      # index, parts (零件目錄), privacy, discount, 404
├── content/blog/               # 5 篇零件選購攻略 .md
├── data/parts.ts               # 762 款型號 × 18 品牌 × 12 零件類型 (AUTO-GEN)
└── styles/global.css           # Design tokens + 全局樣式
public/                         # favicon, robots.txt
```

## /parts/ 零件目錄
- `src/data/parts.ts` 係 auto-generated。如要重新生成（例如更新價錢），re-run `/tmp/parse_parts.py`（parser 喺 conversation tool-results 嗰個 first-station markdown 提取數據）
- 18 個 brand tabs：iphone / ipad / watch / samsung / samsung-fold / samsung-tab / huawei / honor / xiaomi / sony / pixel / oneplus / motorola / asus / oppo / surface / ipod / other
- Anchor deep-link：`/parts/#brand-iphone` 直接 jump 去某品牌
- Part keys（`PartPrices` type）：glass / lcd / lcdAfter / lcdDefect / back / battery / faceId / flex / outer / inner / hinge / combo

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
curl -s https://moncityhk.com/ | grep -cE "維修|手機服務"   # 應該係 0
curl -s https://moncityhk.com/parts/ | grep -oE "<title>[^<]+</title>"
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
v0.11.1

## 重要 — 字眼策略（v0.11.0 起）
- **全站避免「維修」、「服務」、「即場更換」、「手機服務」字眼**，改用「零件」/「選購」/「現貨」/「保養」/「批發零售」
- **核心定位**：手機零件店（parts store），唔係 repair shop
- 原因：Google Ads **Third Party Consumer Technical Support** policy 禁第三方 hardware repair ads。例外：consumer technology sales 嘅 site 可有 minor navigational features
- 「即場代裝」字眼**只可出現喺 FAQ 一條**，唔列價、唔放 hero/services
- 品牌名統一用「MonCity 換Mon城」（取代「MonCity 手機維修中心」等）
- WhatsApp 預填訊息：「查詢手機零件價格。型號：」（URL-encoded 已 hardcode 喺 5 個 component）

## GMB（外部 — 用戶手動跟進）
- GMB 個名仍叫「MONCITY 換Mon城維修中心」+ 可能仲係 Repair shop category — **用戶要去 GMB 後台改名 + 改 category 做 Cell phone store**，否則 Google Ads reviewer 一查 GMB 又 disapprove ad
- Google Maps 連結：https://maps.app.goo.gl/rtoUcQDWsXnkjuTSA
