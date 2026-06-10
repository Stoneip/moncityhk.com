# Google Ads API Setup — moncityhk.com 自動化 ads 管理

目標：將來唔再用 Web UI / Editor，直接用 Python script call Google Ads API 改 ads / keywords / sitelinks。

**Customer ID**: `982-818-1829` (= `9828181829`)
**Account**: stoneip@gmail.com

---

## 一次性設定（~24-48h，主要等 dev token 批核）

### Step 1: 申請 Developer Token（~24h 批核）

1. 入 Google Ads → **Tools & Settings → Setup → API Center**
   - 直接 link: https://ads.google.com/aw/apicenter
2. 撳「**Apply for token**」
3. 填表：
   - Tool name: `MonCity Ads Manager` (內部用名)
   - Tool description: `Internal automation for managing ads, keywords, and sitelinks for moncityhk.com parts store`
   - URL: `https://moncityhk.com`
   - Contact email: stoneip@gmail.com
4. 揀 access level：**Basic** 已夠（free，~24h 批核；只可 manage 自己 account 嘅 ads，唔 access 第三方）
5. Submit → 等 email 回覆

⚠️ **重要**：申請 token 嘅 Google Ads account 必須喺 **good standing**。你而家有 2 條 disapproved ads，**未必影響審批**（只係 policy violation，唔係 account suspension），但如果遲咗，先 manual fix 晒 ads（用 ads.csv），再申請。

### Step 2: 建立 OAuth Credentials（喺 stoneip-dashboard GCP project）

1. 入 GCP Console → 揀 `stoneip-dashboard` project（你已經有 owner role）
2. **APIs & Services → Library** → search「Google Ads API」→ Enable
3. **APIs & Services → OAuth consent screen**:
   - User Type: **External**
   - App name: `MonCity Ads Manager`
   - User support email: stoneip@gmail.com
   - Scopes: 加 `https://www.googleapis.com/auth/adwords`
   - Test users: 加 stoneip@gmail.com
4. **APIs & Services → Credentials → + Create Credentials → OAuth client ID**:
   - Application type: **Desktop app**
   - Name: `moncityhk-ads-cli`
   - Download JSON → 存為 `client_secret.json`

### Step 3: 攞 Refresh Token（一次性）

用 google-ads Python library 嘅內置 utility：

```bash
cd /Users/stoneip/gcloud/moncityhk.com/google-ads
python3 -m venv venv && source venv/bin/activate
pip install google-ads google-auth-oauthlib

# 跑 helper script 攞 refresh token（瀏覽器開，登入授權）
python3 -c "
from google_auth_oauthlib.flow import InstalledAppFlow
SCOPES = ['https://www.googleapis.com/auth/adwords']
flow = InstalledAppFlow.from_client_secrets_file('client_secret.json', SCOPES)
creds = flow.run_local_server(port=0)
print('REFRESH_TOKEN:', creds.refresh_token)
"
```

把 printed `REFRESH_TOKEN` 抄低。

### Step 4: 寫 `google-ads.yaml`

```yaml
# /Users/stoneip/gcloud/moncityhk.com/google-ads/google-ads.yaml
developer_token: <PASTE_DEV_TOKEN_FROM_STEP_1>
client_id: <FROM_client_secret.json>
client_secret: <FROM_client_secret.json>
refresh_token: <FROM_STEP_3>
login_customer_id: "9828181829"   # = 982-818-1829 去咗 dash
use_proto_plus: true
```

**重要**：呢個 file **必須加 .gitignore**！含 secrets，唔好 commit。

---

## Sample Python Script — 將 CSV 推上 Google Ads

呢個係 template，攞嚟你將來自動化用：

```python
# /Users/stoneip/gcloud/moncityhk.com/google-ads/push_ads.py
import csv
from google.ads.googleads.client import GoogleAdsClient

CUSTOMER_ID = "9828181829"
client = GoogleAdsClient.load_from_storage("google-ads.yaml")

# === 1. 建 Responsive Search Ad（from ads.csv） ===
def create_rsa(ad_group_id: str, row: dict):
    ad_service = client.get_service("AdGroupAdService")
    ad_op = client.get_type("AdGroupAdOperation")
    ad = ad_op.create
    ad.ad_group = client.get_service("AdGroupService").ad_group_path(CUSTOMER_ID, ad_group_id)
    ad.status = client.enums.AdGroupAdStatusEnum.ENABLED
    rsa = ad.ad.responsive_search_ad
    ad.ad.final_urls.append(row["Final URL"])

    for i in range(1, 16):
        text = row.get(f"Headline {i}", "").strip()
        if text:
            h = client.get_type("AdTextAsset")
            h.text = text
            rsa.headlines.append(h)
    for i in range(1, 5):
        text = row.get(f"Description {i}", "").strip()
        if text:
            d = client.get_type("AdTextAsset")
            d.text = text
            rsa.descriptions.append(d)
    if row.get("Path 1"): rsa.path1 = row["Path 1"]
    if row.get("Path 2"): rsa.path2 = row["Path 2"]

    resp = ad_service.mutate_ad_group_ads(customer_id=CUSTOMER_ID, operations=[ad_op])
    print(f"Created RSA: {resp.results[0].resource_name}")

# === 2. 加 Keywords（from keywords-add.csv） ===
def add_keywords(ad_group_id: str, csv_path: str):
    kw_service = client.get_service("AdGroupCriterionService")
    ops = []
    match_map = {
        "Broad": client.enums.KeywordMatchTypeEnum.BROAD,
        "Phrase": client.enums.KeywordMatchTypeEnum.PHRASE,
        "Exact": client.enums.KeywordMatchTypeEnum.EXACT,
    }
    with open(csv_path) as f:
        for row in csv.DictReader(f):
            op = client.get_type("AdGroupCriterionOperation")
            crit = op.create
            crit.ad_group = client.get_service("AdGroupService").ad_group_path(CUSTOMER_ID, ad_group_id)
            crit.status = client.enums.AdGroupCriterionStatusEnum.ENABLED
            crit.keyword.text = row["Keyword"]
            crit.keyword.match_type = match_map[row["Match type"]]
            ops.append(op)
    resp = kw_service.mutate_ad_group_criteria(customer_id=CUSTOMER_ID, operations=ops)
    print(f"Added {len(resp.results)} keywords")

# === 3. 加 Campaign-level Negative Keywords ===
def add_negative_keywords(campaign_id: str, csv_path: str):
    cc_service = client.get_service("CampaignCriterionService")
    ops = []
    match_map = {
        "Broad": client.enums.KeywordMatchTypeEnum.BROAD,
        "Phrase": client.enums.KeywordMatchTypeEnum.PHRASE,
        "Exact": client.enums.KeywordMatchTypeEnum.EXACT,
    }
    with open(csv_path) as f:
        for row in csv.DictReader(f):
            op = client.get_type("CampaignCriterionOperation")
            crit = op.create
            crit.campaign = client.get_service("CampaignService").campaign_path(CUSTOMER_ID, campaign_id)
            crit.negative = True
            crit.keyword.text = row["Keyword"]
            crit.keyword.match_type = match_map[row["Match type"]]
            ops.append(op)
    resp = cc_service.mutate_campaign_criteria(customer_id=CUSTOMER_ID, operations=ops)
    print(f"Added {len(resp.results)} negative keywords")

# === 4. Helper: list campaigns + ad groups to find IDs ===
def list_campaigns_and_ad_groups():
    ga_service = client.get_service("GoogleAdsService")
    query = """
        SELECT campaign.id, campaign.name, ad_group.id, ad_group.name
        FROM ad_group
        WHERE campaign.status = 'ENABLED'
    """
    for row in ga_service.search(customer_id=CUSTOMER_ID, query=query):
        print(f"Campaign: {row.campaign.id} {row.campaign.name} | Ad group: {row.ad_group.id} {row.ad_group.name}")

if __name__ == "__main__":
    # 第一次 run: list_campaigns_and_ad_groups() → 攞 campaign_id + ad_group_id
    list_campaigns_and_ad_groups()
    # 然後 hardcode IDs 入下面，再 uncomment：
    # CAMPAIGN_ID = "XXXXXXXX"
    # AD_GROUP_ID = "XXXXXXXX"
    # with open("ads.csv") as f:
    #     for row in csv.DictReader(f):
    #         create_rsa(AD_GROUP_ID, row)
    # add_keywords(AD_GROUP_ID, "keywords-add.csv")
    # add_negative_keywords(CAMPAIGN_ID, "negative-keywords.csv")
```

執行：

```bash
cd /Users/stoneip/gcloud/moncityhk.com/google-ads
source venv/bin/activate
python3 push_ads.py
```

---

## 安全 / Best Practice

| 規則 | 點解 |
|---|---|
| `google-ads.yaml` + `client_secret.json` 加 `.gitignore` | 含 secrets |
| `venv/` 加 `.gitignore` | Python deps 唔需要入 repo |
| Token 入 GCP **Secret Manager** | 比 yaml 文件安全；可選 |
| Script 跑前先 `list_campaigns_and_ad_groups()` | 確認 ID 對先 mutate |
| Mutate operation **set `validate_only=True`** 試一次 | 確認 API call 結構啱先真正 push |
| Schedule 跑 monthly audit（list disapproved ads + flag） | 預防將來 again policy hit |

---

## 將來可以做嘅自動化

```
1. Disapproval Monitor    -- daily check status, Slack/email alert
2. Auto-pause Keywords    -- 低 quality score / 高 CPA / 0 conversion 自動 pause
3. A/B Test Headlines     -- 程式生成 variations，輪流 test
4. Sync /parts/ 庫存       -- 當 parts.ts 加 model → 自動 add 對應 ad group keyword
5. Compliance Linter      -- pre-commit hook 掃 ad copy 有冇 banned words
```

---

## Reference

- Google Ads API docs: https://developers.google.com/google-ads/api/docs/start
- Python library: https://github.com/googleads/google-ads-python
- Policy reference: https://support.google.com/adspolicy/answer/13527027
- Customer ID format: `9828181829` (10 digits, no dash) for API；`982-818-1829` for human display
