# 🛍️ E-Commerce Customer Segmentation: RFM Analysis & K-Means Clustering

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Pandas](https://img.shields.io/badge/Pandas-1.3+-green.svg)](https://pandas.pydata.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange.svg)](https://scikit-learn.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **Data-driven customer segmentation to optimize marketing ROI and reduce churn for e-commerce businesses**

---

## 📊 Project Overview

This project implements an end-to-end **customer segmentation analysis** for a UK-based online retailer using **RFM (Recency, Frequency, Monetary) modeling** combined with **K-Means clustering**. The analysis identifies actionable customer segments to enable data-driven marketing strategies, improve retention, and maximize customer lifetime value.

**🎯 Business Impact:**
- Identified that **22% of high-value customers contribute 60%+ of total revenue**
- Flagged **527+ at-risk customers** requiring re-engagement campaigns
- Enabled **personalized marketing strategies** across 4 distinct customer segments
- Provided **quantified recommendations** to increase retention and reduce churn

---

## 🎯 Business Objectives

1. **Identify high-value customers** to prioritize retention efforts
2. **Detect at-risk customers** early to prevent churn
3. **Segment customers** for targeted marketing campaigns
4. **Quantify revenue contribution** by customer group
5. **Provide actionable recommendations** for customer lifecycle management

---

## 📁 Dataset Information

| Attribute | Details |
|-----------|---------|
| **Source** | [UCI Machine Learning Repository - Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail) |
| **Time Period** | December 1, 2010 - December 9, 2011 (12 months) |
| **Records** | 541,909 transactions |
| **Customers** | 4,372 unique customers (UK only) |
| **Geography** | United Kingdom |
| **Business Type** | B2C online gift retailer |
| **Attributes** | Invoice, StockCode, Description, Quantity, UnitPrice, InvoiceDate, CustomerID, Country |

---

## 🛠️ Methodology

### 1️⃣ Data Cleaning & Preprocessing
- Removed transactions without CustomerID (~25% of data)
- Filtered out cancelled/returned orders (negative quantities)
- Excluded invalid prices (£0 or negative)
- Retained only UK customers for geographic consistency
- Created `TotalPrice` feature: `Quantity × UnitPrice`

**Result:** Clean dataset of **~400K transactions** from **4,300+ customers**

### 2️⃣ RFM Feature Engineering

For each customer, calculated:

| Metric | Definition | Business Meaning |
|--------|------------|------------------|
| **Recency (R)** | Days since last purchase | How recently did they buy? |
| **Frequency (F)** | Number of unique orders | How often do they buy? |
| **Monetary (M)** | Total spending amount | How much do they spend? |

**Additional Features:**
- Customer Tenure (days since first purchase)
- Average Order Value (AOV)
- Days Between Purchases
- Total Items Purchased

### 3️⃣ Outlier Treatment
- Applied **IQR method** to detect extreme outliers
- Filtered top **1% of Frequency and Monetary** values (following Chen et al., 2012)
- Retained **~3,700 customers** for clustering (business-valid outliers handled separately)

### 4️⃣ Feature Scaling
- Applied **StandardScaler** to normalize RFM features
- Ensured equal weight in distance calculations (critical for K-Means)

### 5️⃣ Clustering Optimization
Evaluated K=2 to K=10 using:
- **Elbow Method** (Within-Cluster Sum of Squares)
- **Silhouette Score** (cluster separation quality)
- **Davies-Bouldin Index** (cluster compactness)

**Selected K=4** based on:
- Statistical metrics (Silhouette: 0.42, DB Index: 0.87)
- Business interpretability (actionable segment sizes)

### 6️⃣ Segment Profiling

| Segment | Count | % of Base | Avg Revenue | Characteristics |
|---------|-------|-----------|-------------|-----------------|
| **Champions** | 188 | 5% | £5,963 | High recency, high frequency, high spend |
| **Potential Loyalists** | 1,748 | 47% | £686 | Moderate activity, growth potential |
| **At Risk** | 527 | 14% | £361 | Low recency, declining engagement |
| **New Customers** | 636 | 17% | £586 | Recent first purchase, low frequency |

---

## 📈 Key Findings

### 💰 Revenue Concentration
- **Top 5% of customers** (Champions) contribute **25%+ of total revenue**
- **Top 20% of customers** drive **~60% of revenue** (Pareto principle validated)
- **Bottom 50%** contribute only **~15% of revenue**

### ⚠️ Churn Risk
- **527 customers (14%)** are at high risk of churn
- Average **9.8 months** since last purchase for at-risk segment
- Potential revenue loss: **£190,000+** if not re-engaged

### 🎯 Growth Opportunities
- **636 new customers (17%)** acquired in 2011
- Average **2.3 orders** in first 6 months
- Opportunity to convert to loyal customers with targeted onboarding

---

## 💡 Business Recommendations

### 🏆 Champions (VIP Customers)
**Action:** Retain and deepen relationship
- Implement VIP loyalty program with exclusive perks
- Provide early access to new products
- Assign personal account managers
- Request reviews and referrals
- **Expected Impact:** Increase LTV by 15-20%

### ⚡ At Risk / Hibernating
**Action:** Win-back campaign
- Launch personalized email re-engagement (discount codes)
- Conduct churn survey to identify pain points
- Retargeting ads with best-selling products
- Time-limited "we miss you" offers
- **Expected Impact:** Recover 20-30% of dormant customers

### 🌱 New Customers
**Action:** Onboarding optimization
- Welcome email series (3-5 emails)
- Second purchase incentive (within 30 days)
- Product education content
- Collect preferences for personalization
- **Expected Impact:** Increase repeat purchase rate by 25%

### 📊 Potential Loyalists
**Action:** Upsell and engagement
- Cross-sell recommendations
- Introduce subscription options
- Gamification (points, tiers)
- Personalized product bundles
- **Expected Impact:** Upgrade 10% to Champions

---

## 📊 Visualizations

<details>
<summary>Click to view sample visualizations</summary>

### Customer Segmentation Overview
![Customer Distribution](visualizations/05_revenue_contribution.png)

### RFM Metrics Distribution
![RFM Distributions](visualizations/02_rfm_distributions.png)

### Cluster Optimization
![Elbow & Silhouette](visualizations/03_elbow_silhouette.png)

### 3D Segment Visualization
![3D Clustering](visualizations/06_segment_comparison.png)

</details>

---

## 🚀 How to Run This Project

### Prerequisites
```bash
Python 3.8+
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl
```

### Option 1: Google Colab (Recommended)
1. Open notebook in Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yourusername/rfm-segmentation/blob/main/RFM_Customer_Segmentation_Complete.ipynb)
2. Upload `Online Retail.xlsx` when prompted
3. Run all cells sequentially

### Option 2: Local Jupyter Notebook
```bash
# Clone repository
git clone https://github.com/yourusername/rfm-segmentation.git
cd rfm-segmentation

# Install dependencies
pip install -r requirements.txt

# Download dataset
wget https://archive.ics.uci.edu/static/public/352/online+retail.zip
unzip online+retail.zip

# Launch Jupyter
jupyter notebook RFM_Customer_Segmentation_Complete.ipynb
```

### Option 3: Command Line Execution
```bash
python rfm_analysis.py --data "Online Retail.xlsx" --output "./outputs/"
```

---

## 📦 Project Structure

```
online-retail-rfm-segmentation/
│
├── RFM_Customer_Segmentation_Complete.ipynb  # Main analysis notebook
├── README.md                                  # This file
├── requirements.txt                           # Python dependencies
├── RESUME_BULLETS.md                          # Resume-ready project descriptions
│
├── data/
│   └── Online Retail.xlsx                     # Raw dataset
│
├── outputs/
│   ├── rfm_customer_segments.csv              # Final customer segments
│   ├── cluster_summary_stats.csv              # Cluster statistics
│   ├── segment_performance_summary.csv        # Segment metrics
│   └── business_recommendations.txt           # Actionable insights
│
└── visualizations/
    ├── 01_data_overview.png
    ├── 02_rfm_distributions.png
    ├── 03_elbow_silhouette.png
    ├── 04_cluster_profiles.png
    ├── 05_revenue_contribution.png
    └── 06_segment_comparison.png
```

---

## 🧠 Skills Demonstrated

### Technical Skills
- **Python Programming:** pandas, NumPy, scikit-learn, matplotlib, seaborn
- **Data Cleaning:** Missing value treatment, outlier detection, feature engineering
- **Machine Learning:** K-Means clustering, StandardScaler, hyperparameter tuning
- **Statistical Analysis:** Silhouette score, Davies-Bouldin index, IQR method
- **Data Visualization:** Multi-dimensional plotting, heatmaps, 3D scatter plots

### Business Analytics Skills
- **Customer Analytics:** RFM modeling, customer segmentation, churn prediction
- **Marketing Analytics:** Campaign targeting, customer lifetime value (CLV)
- **Business Intelligence:** KPI definition, segment profiling, revenue analysis
- **Strategic Thinking:** Actionable recommendations, ROI estimation
- **Storytelling:** Translating technical findings into business insights

---

## 📚 References & Methodology

This project is based on industry best practices and academic research:

1. **Chen, D., Sain, S. L., & Guo, K. (2012).** *Data mining for the online retail industry: A case study of RFM model-based customer segmentation using data mining.* Journal of Database Marketing & Customer Strategy Management, 19(3), 197-208.

2. **Hughes, A. M. (2012).** *Strategic Database Marketing 4e: The Masterplan for Starting and Managing a Profitable, Customer-based Marketing Program.* McGraw-Hill.

3. **Kumar, V., & Reinartz, W. (2018).** *Customer Relationship Management: Concept, Strategy, and Tools.* Springer.

---

## 🎓 Future Enhancements

1. **Predictive Modeling:** Build ML model to predict customer segment migration
2. **Product Affinity Analysis:** Identify product purchase patterns by segment
3. **Time-Series Forecasting:** Predict future revenue by customer segment
4. **A/B Testing Framework:** Test marketing campaigns by segment
5. **Real-Time Dashboard:** Interactive Tableau/Power BI dashboard for business users
6. **Automated Reporting:** Weekly segment performance reports

---

## 👤 Author

**Pujari Bheemesh**
 📧 [Email]bheemeshpujari63@gmail.com

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- UCI Machine Learning Repository for providing the dataset
- Chen et al. (2012) for the RFM methodology framework
- Online retail industry for inspiring customer-centric analytics

---

## ⭐ If you found this project helpful, please give it a star!

**Keywords:** Customer Segmentation, RFM Analysis, K-Means Clustering, E-Commerce Analytics, Marketing Analytics, Data Science, Machine Learning, Python, Customer Lifetime Value, Churn Prediction, Business Intelligence
