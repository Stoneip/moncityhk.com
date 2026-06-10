# Google Ads — moncityhk.com 修復檔案

Customer ID: **982-818-1829** (account: stoneip@gmail.com)
Campaign: **Leads-Search**
Ad group: **Ads Group - Lead Search**
版本: 配合 moncityhk.com v0.11.0「手機零件店」pivot

---

## 📁 檔案

| 檔案 | 用途 | 操作 |
|---|---|---|
| `ads.csv` | 1 條新 RSA（15 headlines + 4 descriptions） | Import to Editor → 新 RSA |
| `keywords-add.csv` | 20 個 product-intent keywords | Import → 新 keywords |
| `keywords-pause.csv` | 7 個舊 repair-intent keywords pause | Import → 改 status |
| `negative-keywords.csv` | 13 個 campaign-level negative keywords | Import → 加 negatives |
| `sitelinks.csv` | 4 個新 sitelinks（含 description） | Import → 取代舊 sitelinks |

---

## 用 Google Ads Editor Import

1. 下載 Google Ads Editor: https://ads.google.com/intl/en/home/tools/ads-editor/
2. 開 Editor → 登入 stoneip@gmail.com → 揀 account 982-818-1829
3. Download latest changes (Cloud icon)
4. **File → Import → From file** → 揀其中一個 CSV
5. Editor 會 show preview，**留意有冇 error**（中文 column header 可能會 conflict，必要時改用 English header）
6. **檢查無誤先撳 Apply**
7. 全部 5 個 CSV 重複，然後喺 toolbar 撳 **Post Changes**（推上 Google Ads）

### 唔用 Editor 嘅替代做法

`ads.csv` / `sitelinks.csv` 直接喺 web dashboard 手動建立都好快。`keywords-*.csv` 可以喺 Web UI **Tools & Settings → Bulk Actions → Uploads** 度 upload。

---

## ⚠️ 操作順序

**唔好一次過 import 晒**。建議步驟：

1. **先 import `negative-keywords.csv`** —— 即時 block 任何將來 repair-query
2. **import `keywords-pause.csv`** —— pause 舊 repair keywords
3. **import `keywords-add.csv`** —— 加新 product keywords
4. **import `ads.csv`** —— 建立新 RSA（pause 舊兩條 disapproved ads，**唔好 delete**，保留歷史）
5. **import `sitelinks.csv`** —— 取代舊 sitelink「即日預約更換」
6. **Post Changes** to Google Ads
7. 等 24h review

---

## 中文 column 注意事項

Google Ads Editor 啲 column 名係**根據你 Editor 嘅 UI 語言**。我寫 English column header（最 portable），如果你 Editor 設定咗中文 UI，可能要：

- 改 Editor → Preferences → Language: **English**（一次性，import 完可以改返）
- 或者用「Make multiple changes」嘅 paste-to-textbox 方法（cell by cell，但唔需要 column header match）

---

## 後路：Web UI Manual Paste

如果 CSV import 撞 wall，每個 csv 嘅 row 其實都可以**手動** copy 過去 web UI：

- `ads.csv` → Ad group → + New ad → Responsive search ad → 逐個 paste headlines & descriptions
- `keywords-*.csv` → Keywords tab → + → paste keyword list（一行一個）
- `negative-keywords.csv` → Keywords → Negative keywords → 揀 Campaign level → paste
- `sitelinks.csv` → Ads & assets → Assets → Sitelinks → + → 逐個 fill

實際上你而家只需要改 1 條 ad + 20 keywords + 13 negatives + 4 sitelinks，**Web UI 手動 paste 嗰陣 30 分鐘搞掂**。CSV import 主要好處係將來如果你做 multiple campaigns / variations 時可以 reuse。

---

## 下一步（將來自動化）

`api-setup.md` 內有完整步驟：申請 dev token、OAuth 設定、Python script template，方便將來用 Google Ads API 直接 mutate ads，唔再需要手動操作。
