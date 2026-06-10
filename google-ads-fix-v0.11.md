# Google Ads Fix — 配合 moncityhk.com v0.11.0「手機零件店」定位

**Campaign**: Leads-Search (982-818-1829)
**Status**: 2 ads disapproved — Third Party Consumer Technical Support policy
**修復方向**: ad copy + keywords 全部改成 product / parts sales 角度

---

## 操作流程

1. 暫停（**唔好 delete**）舊 2 條 disapproved ads
2. 用下面內容**建立新 RSA**（Responsive Search Ad）
3. **同時**更新 keywords（drop repair-intent，加 product-intent）
4. 更新 sitelinks description
5. Save → 等 review（一般 24h 內覆）
6. 過咗 review 先 delete 舊 ads

---

## 1. Headlines（直接 paste 入 Google Ads，每條 ≤30 chars）

放晒落新 RSA（Google 要求最少 3，最多 15 個 headlines）：

| # | Headline | Chars |
|---|---|---|
| 1 | 深水埗手機零件店 MonCity | 16 |
| 2 | iPhone 零件門市現貨 | 14 |
| 3 | Samsung 螢幕零件批發 | 15 |
| 4 | 手機電池零件 各大品牌 | 13 |
| 5 | 原裝/副廠 手機零件齊備 | 15 |
| 6 | 18 大品牌手機零件目錄 | 14 |
| 7 | iPhone 17 至 5 零件現貨 | 18 |
| 8 | 深之都門市 手機零件 | 13 |
| 9 | 螢幕 後蓋 電池 排線零件 | 15 |
| 10 | 手機零件批發 同行歡迎 | 13 |
| 11 | WhatsApp 查零件價格 | 16 |
| 12 | 700+ 型號零件目錄 | 14 |
| 13 | 深水埗 D2 出口 手機零件 | 15 |
| 14 | 手機零件 即場選購 | 10 |
| 15 | MonCity 換Mon城 零件店 | 15 |

---

## 2. Descriptions（每條 ≤90 chars，填 4 條）

```
[A] 深水埗手機零件店 MonCity 換Mon城。iPhone、Samsung、華為等手機零件目錄，門市現貨，WhatsApp 報型號即時查價。

[B] 700+ 款手機型號零件 — 前螢幕玻璃、螢幕總成、後蓋、電池、Face ID 模組、排線。原裝及副廠選擇齊備。

[C] 深之都 1 樓 230 號鋪手機零件門市。iPhone 17 至 5、Samsung、華為等品牌零件批發零售。深水埗 D2 出口。

[D] iPhone / Samsung / 華為 / 小米 / Pixel 手機零件批發。同行採購歡迎，量大有折扣。WhatsApp 直接查貨。
```

---

## 3. Keywords — DROP 呢啲（加做 Negative Keywords 更穩陣）

呢啲係 repair-intent，**保留風險高**：

```
換手機電池
"換Mon價錢"
深水埗換電
換電價錢
手機換屏幕
換液晶
深水埗換Mon
換mon
換電池
換螢幕
換mon價錢
換mon價
換mon邊好
```

**建議：先 pause，加埋做 negative keyword（避免將來 query 中 match 到觸發新 ads）**

---

## 4. Keywords — ADD 呢啲（product-intent，合 policy）

Broad / Phrase mix（建議 phrase match 用 `"..."` 包住）：

```
手機零件
iPhone 零件
"Samsung 螢幕零件"
"手機電池零件"
手機後蓋玻璃
深水埗手機零件
手機零件批發
"iPhone 螢幕零件"
Face ID 零件
手機螢幕總成
原裝手機零件
副廠手機零件
"深水埗手機零件店"
iPad 零件
Apple Watch 零件
華為零件
小米零件
手機零件目錄
手機零件報價
"手機零件門市"
```

---

## 5. Sitelinks

舊嗰個「WhatsApp 即時報價 / 深水埗店**即日預約更換**」要改。建議 4 個：

| Sitelink 文字 | URL | Description 1 | Description 2 |
|---|---|---|---|
| 手機零件目錄 | https://moncityhk.com/parts/ | 18 品牌 700+ 型號零件 | 門市現貨 即時查貨 |
| iPhone 零件 | https://moncityhk.com/parts/#brand-iphone | iPhone 5 至 17 Pro Max | 螢幕、電池、後蓋零件 |
| Samsung 零件 | https://moncityhk.com/parts/#brand-samsung | Galaxy S/Note/A/Fold 系列 | 原裝及副廠選擇 |
| WhatsApp 查零件 | https://wa.me/85269960711 | 報型號即時查現貨 | 量大有折扣 |

---

## 6. Business Name

你而家寫「MONCITYHK」OK，但 Google 顯示「Wai Ki OR」（你嘅 verified advertiser name）。**唔關 policy 事**，但建議 verified name 都改去 MonCity 相關，long term consistency 好啲（喺 Google Ads → Business name verification 度跟進）。

---

## 7. Display Path

你而家係 `moncityhk.com/手機零件/深水埗` ✓ 已經 OK，唔使改。

---

## 8. 注意事項

- **唔好 Edit 舊 ad** —— Save 之後會即時 re-submit for review，又再被 disapprove，浪費 review quota。**Pause 舊 ad → 建新 ad** 先正路。
- **唔好同時改太多嘢** —— 改完 ad copy + keywords 已經夠，**唔好同時改 final URL 同 landing page**，否則 Google 可能要長一啲時間 review。
- **GMB 仍要跟進**：你個 store 喺 Google Maps 上仲叫「**維修中心**」，category 可能仲係 `Mobile phone repair shop`。即使 ad 過咗 review，Google 將來 audit GMB 仍可以再 flag。手動去 Google Business Profile 改：
  - Name: 「MONCITY 換Mon城**維修中心**」→「MONCITY 換Mon城」/「MonCity 手機零件店」
  - Primary category: `Cell phone store`（Mobile phone repair shop 可保留做 secondary）

---

## 9. Appeal 樣板（500 chars 上限）

**新 ad 過咗 review 之後**，如果想 appeal 舊 disapproved ads（攞返 ad rank / quality history），用呢段：

```
本店係深水埗手機零件實體零售店（深之都 1 樓 230 號鋪），主要售賣 iPhone、Samsung、華為、小米、Pixel 等品牌手機零件，包括螢幕、電池、後蓋、Face ID 模組、排線等。Landing page (moncityhk.com/parts/) 已重新定位為零件目錄與價目表，列出 700+ 型號零件。安裝服務僅為購買零件後嘅 minor navigational feature，於 FAQ 提及，無單獨推廣或定價。Ad copy 同 keywords 已全面更新為 parts sales positioning。
```

---

**Version**: 配合 moncityhk.com v0.11.0 (2026-05-21)
