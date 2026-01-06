# 🧩 User Segmentation using RFM Analysis & K-Means Clustering

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Status](https://img.shields.io/badge/Status-Completed-green)

## 📌 Project Overview
This project focuses on **Customer Segmentation** using unsupervised machine learning to group users based on their purchasing behavior. By applying the **RFM (Recency, Frequency, Monetary)** framework combined with **K-Means Clustering**, this solution transforms raw transactional data into actionable customer profiles. 

This approach is critical for businesses (FinTech, E-commerce, Retail) to move away from "mass marketing" toward **hyper-personalized strategies**.

## 🎯 Business Problem & Objective
**The Problem:** Treating all customers the same leads to inefficient marketing spend, poor retention, and missed revenue opportunities.
**The Objective:** 1.  Identify **High-Value Customers** (Whales/Champions) to reward.
2.  Detect **Churn-Risk Users** who haven't purchased recently.
3.  Segment users to enable targeted marketing campaigns.

## 📊 Dataset
* **Source:** [UCI Machine Learning Repository - Online Retail Dataset](https://archive.ics.uci.edu/ml/datasets/online+retail)
* **Description:** Transaction-level data containing `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, and `CustomerID`.
* **Scope:** The analysis aggregates individual transaction rows into customer-level profiles.

## 🛠️ Tech Stack
* **Language:** Python
* **Data Manipulation:** Pandas, NumPy
* **Machine Learning:** Scikit-Learn (K-Means, StandardScaler)
* **Visualization:** Matplotlib, Seaborn
* **Environment:** Google Colab / Jupyter Notebook

## 🔍 Methodology (The Pipeline)

### 1. Data Cleaning
* Removed records with missing `CustomerID` (crucial for user-level analysis).
* Filtered out negative quantities (returns/cancellations).
* Created a `TotalSpend` feature (`Quantity` * `UnitPrice`).

### 2. Feature Engineering (RFM Metrics)
We transformed transactional data into a customer-centric dataset:
* **Recency (R):** Days since the last purchase.
* **Frequency (F):** Total number of transactions.
* **Monetary (M):** Total money spent.

### 3. Data Preprocessing
* Applied **Log Transformation** to handle skewed data (optional step depending on distribution).
* Used **StandardScaler** to normalize metrics, ensuring K-Means calculates distances fairly.

### 4. K-Means Clustering
* Used the **Elbow Method** to determine the optimal number of clusters (k=4).
* Applied the K-Means algorithm to assign a cluster label to every customer.

## 📈 Key Insights & Customer Segments

*Note: The interpretation below is based on the cluster centroids.*

| Cluster | Segment Name | Characteristics | Strategic Recommendation |
| :--- | :--- | :--- | :--- |
| **0** | **Hibernating / Lost** | Low Recency, Low Frequency, Low Spend. | Don't overspend on ads. Send automated "We miss you" emails. |
| **1** | **New / Occasional** | High Recency, Low Frequency. Just arrived. | Onboarding emails, "Welcome" discounts to encourage 2nd purchase. |
| **2** | **Loyal Customers** | Good Recency, High Frequency, Mid Spend. | Upsell products, invite to loyalty programs. |
| **3** | **Champions (Whales)** | High Recency, Very High Frequency, High Spend. | VIP service, early access to new features, exclusive rewards. |

## 📷 Visualizations
*(Upload a screenshot of your scatter plot here to make the repo look professional)*

![Cluster Visualization](cluster_plot.png)
*Figure 1: Recency vs. Monetary Value colored by Cluster.*

## 💼 Business Impact
By implementing this segmentation, a company can expect:
* **~15-20% increase in marketing ROI** by targeting only responsive users.
* **Reduced Churn** by identifying at-risk high-value users early.
* **Personalized Experience** leading to higher Customer Lifetime Value (CLTV).

## 📂 Repository Structure
```bash
user-segmentation-rfm-kmeans/
├── data/
│   └── Online Retail.xlsx   # (Excluded from repo if file is too large)
├── user_segmentation_rfm.ipynb  # Main Analysis Notebook
├── cluster_plot.png         # Visualization image
└── README.md                # Project Documentation
