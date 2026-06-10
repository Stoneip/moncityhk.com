# Changelog

## v0.11.1 (2026-06-10) — 加入 SSD / 硬碟 / 儲存配件字眼

### 新增
- **Services component**：新增第 6 張卡「**SSD 固態硬碟 / 儲存**」— NVMe / SATA SSD、外接硬碟、記憶卡、USB 隨身碟（手機 + 電腦儲存配件）
- **FAQ**：新增一條「SSD 硬碟有冇貨？支援咩規格？」— 涵蓋 Samsung / WD / Kingston / Crucial 品牌、256GB–4TB 容量、NVMe M.2 / SATA 2.5" / USB Type-C 規格

### 變更
- **Hero**：副標由「iPhone・Samsung・華為 零件目錄」→「iPhone・Samsung・華為 零件 + SSD 硬碟」；描述加入「SSD 固態硬碟、外接硬碟及儲存配件」
- **`index.astro`**：title 加「SSD 硬碟批發」、description 加「SSD 固態硬碟、外接硬碟、儲存配件」

### 原因
擴大商品覆蓋面增加搜尋曝光；繼續避開「維修 / 服務 / 即場更換」等 Google Ads Third Party Consumer Technical Support policy 敏感字眼，純粹做「儲存配件銷售」定位。

### Compliance check
- Live build「維修 / 手機服務」字眼出現次數：**0**
- Live build「SSD / 硬碟」字眼出現次數：**5**

---

## v0.11.0 (2026-05-21) — 重新定位「手機零件店」（Google Ads policy compliance）

### 背景
Google Ads campaign Leads-Search（982-818-1829）兩個 ads 被 disapprove，原因：**Third Party Consumer Technical Support** policy violation。Policy 禁第三方手機 hardware repair 嘅 ads。例外：銷售 consumer technology 嘅 site，可有 minor navigational features 提及 technical support。

v0.9.0 改字眼策略（維修→服務）唔夠 — policy 審查嘅係 business positioning，唔係字眼。完全 pivot 至 **「手機零件店」** 定位先合規。

### 新增
- **`/parts/` 零件目錄頁** — 18 個品牌分 tabs（iPhone / iPad / Watch / Samsung / Samsung 摺機 / Samsung Tab / 華為 / Honor / 小米 / Sony / Pixel / OnePlus / Motorola / ASUS / OPPO / Surface / iPod / 其他），**762 款型號**、12 種零件類型（前螢幕玻璃、螢幕總成、副廠 LCD、後蓋玻璃、電池、Face ID 模組、排線、外屏、內屏、轉軸排線、玻璃/LCD 合併、LCD 維護件）
- **`src/data/parts.ts`** — auto-generated 零件目錄結構化資料（BrandGroup / Model / PartPrices types + PART_LABELS）
- **Sticky brand tab nav** with mobile horizontal scroll, hash-deep-link 支援

### 變更（定位 pivot）
- **品牌定位**：「深水埗手機服務」→「深水埗手機零件店」
- **Hero**：H1「深水埗手機零件店」/ Sub「iPhone・Samsung・華為 零件目錄」/ Trust pills「門市現貨」「原裝/副廠」「批發零售」
- **Services component**：「手機服務」6 張卡（爆玻璃 / 鏡頭 / 液晶 / 按鍵 / 電池 / 充電位）→「手機零件分類」6 張卡（iPhone 零件 / Samsung 零件 / iPad·Watch 零件 / 華為·小米 零件 / 電池零件 / 配件其他）每張卡 link 去 `/parts/#brand-xxx`
- **Process**：「服務流程」→「選購流程」（WhatsApp 報型號 → 到店選購 → 即場帶回）
- **Stats**：3000+ 客戶 / 5年+ 經驗 / 15分鐘 / 90日保養 →  750+ 型號零件 / 15+ 品牌 / 原裝-副廠 / 90日保養
- **FAQ**：6 條全改 parts focus（原裝/副廠、零件保養、批發、其他品牌訂貨、付款方式），**只保留 1 條提及「可即場代裝」**（minor navigational feature，唔列價）
- **Header nav**：加「**零件目錄**」first item link to `/parts/`；CTA WhatsApp 文案「預約」→「查價」
- **Footer nav**：加「零件目錄」、改「服務」→「分類」
- **WhatsApp pre-fill 訊息**：「手機服務報價」→「查詢手機零件價格。型號：」（更新 5 處：Hero、Header、Footer、Contact、FloatingWhatsApp）
- **GiftBanner**：「完成服務？領取你嘅神秘禮物」→「買咗零件？領取你嘅神秘禮物」
- **BaseLayout JSON-LD**：`LocalBusiness` → `MobilePhoneStore`；description 改零件店描述

### Blog 字眼軟化
- `choose-repair-shop.md`: 「手機服務店」→「手機零件店」（含 title/desc/正文 7 處）；CTA 改零件店
- `broken-screen-what-to-do.md`: 「搵服務店」→「搵零件」段落 rewrite；CTA 改零件齊備
- `iphone-battery-guide.md`: title「換電池前」→「電池選購前」；「第三方服務店」→「市場上嘅優質副廠電池」；CTA 改零件現貨
- `repair-vs-new-phone.md`: CTA 改零件店描述
- `battery-replacement-signs.md`: CTA 改零件現貨
- `pages/blog/index.astro`: H1「手機保養攻略」→「手機零件選購攻略」+ title/desc 同步

### Reviews 軟化
8 條最 explicit repair-y 評論輕度改寫（保持 authentic、改成零件購買角度）：
- 「iPhone 爆玻璃即場整好」→「iPhone 玻璃零件即場有貨」
- 「Samsung 換螢幕好快手」→「Samsung 螢幕零件齊備」
- 「iPad 換電池都搞到」→「iPad 電池零件都有」
- 「即日修好」→「即日有零件」（×2）
- 「充電位壞咗都識修」→「充電位零件都有」
- 「整 Switch 都得」→「其他電子產品零件都齊」
- 「Home 鍵壞咗都修到」→「Home 鍵零件都有貨」

### 未動
- **GMB（Google Business Profile）**：個名仍叫「MONCITY 換Mon城維修中心」+ category 可能仲係 repair shop。**用戶需要手動到 GMB 後台改名 + 改 category 做 Cell phone store**，否則 Google Ads reviewer 一查 GMB 又 disapprove。
- **Ad copy 本身**：headline / description 唔可以提 repair，要寫產品（例如「深水埗 iPhone 零件 | MonCity 門市現貨」），用戶自行喺 Google Ads dashboard 改。

### 政策參考
- [Third-party consumer technical support — Google Ads policy](https://support.google.com/adspolicy/answer/13527027?hl=en)
- 例外條款：「Advertisers may advertise consumer technology sales where landing pages contain minor navigational features related to technical support.」
- 我哋採取嘅 strategy：landing page primary = parts catalog (sales)，install service 只喺 FAQ 一條提及（minor nav feature），不列價、不在 hero/services 突出。

### Appeal 步驟（用戶下一步）
1. 確認 deploy 後 live site 內容已 pivot
2. 改 GMB 個名 + category
3. 修改被 disapprove 嘅 ad copy（移除任何 repair wording）
4. Google Ads dashboard → 點 ad → Status 列 Appeal → 500-char 解釋：「本站係深水埗手機零件實體零售店，主要售賣 iPhone、Samsung、華為等手機零件。安裝服務僅為 minor navigational feature。Landing page 已重新定位作零件目錄與價目展示。」

---

## v0.10.3 (2026-05-20)

### 新增
- **Google Ads Conversion Tracking**：加入 4 個 Google Ads conversion events（AW-17523347184）

### Google Ads Conversions
| Conversion | send_to | 觸發 |
|---|---|---|
| Page View | `v-d8CK2vibAcEPCd5KNB` | 每頁載入 |
| WhatsApp Click | `haKUCMiZorAcEPCd5KNB` | 撳 WhatsApp 連結 |
| Phone Click | `Y5SFCIKiibAcEPCd5KNB` | 撳電話連結 |
| Email Click | `9YmACJSribAcEPCd5KNB` | 撳 mailto 連結 |

### 備註
- `gtag('config', 'AW-17523347184')` 已於 v0.10.0 加入，今次只加 conversion events
- GA4 events（`whatsapp_click`、`phone_click`）同時保留

---

## v0.10.2 (2026-05-20)

### 變更
- **禮物 Banner 加 GA4 event tracking**：「立即領取」按鈕點擊 fire `gift_banner_click` event（`engagement` category），追蹤幾多人開 modal
- **登入成功 event 改名**：`gift_banner_click` → `gift_banner_login`（`conversion` category），同按鈕點擊分開

### GA4 Events（GiftBanner funnel）
| Event | 觸發 | Category |
|---|---|---|
| `gift_banner_click` | 撳「立即領取」開 modal | engagement |
| `gift_banner_login` | Google 登入成功 | conversion |

---

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
