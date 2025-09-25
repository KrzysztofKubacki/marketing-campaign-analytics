# Marketing Campaign Analytics & ROAS

## Objective  
Develop a **reproducible analytics pipeline** to:  
- Clean and validate CRM data  
- Engineer key marketing and customer value features  
- Segment customers using unsupervised learning  
- Analyze campaign effectiveness (response, lift, ROI/ROAS) and recommend contact policies  

---

## Dataset  
- **Source:** [Kaggle – Marketing Campaign Dataset](https://www.kaggle.com/datasets/rodsaldanha/marketing-campaign)  
- **Size:** ~2,200 customers, 28 raw features  
- **Content:**  
  - Socio-demographic attributes (age, education, income, family)  
  - Purchase behavior across products and channels  
  - Campaign acceptance flags and final response indicator  

---

## Project Structure  
```bash
P5/
├─ Data/
│  ├─ Raw/         # original dataset (not tracked in git)
│  ├─ Interim/     # cleaned data after ETL
│  └─ Processed/   # engineered features, cluster results, campaign exports
│
├─ notebooks/
│  ├─ 01_sprint_etl.ipynb                 # ETL & data cleaning
│  ├─ 02_sprint_feature_engineering.ipynb # AOV, CLV, RFM, shares
│  ├─ 03_sprint_segmentation.ipynb        # KMeans segmentation
│  └─ 04_sprint_campaign_analytics.ipynb  # Campaign ROI & policy
│
├─ requirements.txt
└─ README.md
```
Sprints:
Sprint 1 — ETL (Data Cleaning & QA)

Parse dates, normalize categoricals

Median imputation for Income

Business rules for realistic Age

Winsorization (1–99 pct) to cap outliers

Normalize binary flags (AcceptedCmp*, Response)

QA assertions for data integrity
Output: Data/Interim/marketing_campaign_clean.csv

Sprint 2 — Feature Engineering

Derived metrics: TotalSpend, TotalPurchases, AOV, tenure

Product basket shares & channel shares (web/catalog/store/deals)

Web conversion proxy

CLV proxy = AOV × frequency/month × 12 × margin

RFM scoring + business labels (Champions, Loyal, New, At Risk, Regulars)
Outputs: customers_master.csv, rfm_segments.csv

Sprint 3 — Customer Segmentation (KMeans + Stability)

Correlation pruning, feature scaling

Grid search over k = 3…6

Model selection by:

Silhouette Score

Calinski–Harabasz / Davies–Bouldin

Mean ARI stability on subsamples

Final cluster labels + profile table (spend, AOV, response, CLV proxy)
Outputs: cluster_labels.csv, cluster_profile.csv, cluster_model_selection.csv

Sprint 4 — Campaign Analytics

Campaign acceptance by cluster

Segment-level: response, lift vs baseline, ROAS/ROI proxies

Contact policy: CONTACT if ROI > 0 and Lift > 1
Outputs: segment_uplift_roi.csv, campaign_by_cluster.csv, contact_policy.csv (ready for BI dashboards)
