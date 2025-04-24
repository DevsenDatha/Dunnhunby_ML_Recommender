# 🛒 Dunnhumby Recommender System

This project builds a collaborative filtering-based product recommender system using the Dunnhumby retail dataset, hosted and developed end-to-end in Databricks using PySpark and Delta Lake.

---

## 📌 Project Goals
- Recommend products to households based on past purchase behavior
- Use implicit feedback (purchase frequency)
- Build a pipeline that covers EDA, preprocessing, model training, and recommendation generation

---

## 📁 Dataset Overview

| File | Description |
|------|-------------|
| `transaction_data.csv` | Contains all household-level purchase transactions |
| `product.csv` | Metadata about each product (brand, category, etc.) |
| `hh_demographic.csv` | Household-level demographic data |
| `campaign_desc.csv` | Descriptions of marketing campaigns |
| `campaign_table.csv` | Mapping of households to campaigns |
| `coupon.csv` | Coupons issued in campaigns |
| `coupon_redempt.csv` | Coupon redemption info |
| `causal_data.csv` | Data on promotional events |

Files were stored and accessed using Unity Catalog Volumes in Databricks.

---

## 🔍 Exploratory Data Analysis
- Top brands and categories by transaction volume
- Weekly and yearly sales trends using `WEEK_NO`
- Spend patterns by age group and household demographics
- Insights created using PySpark joins and aggregations

---

## 🛠️ Preprocessing
- Grouped data by `household_key` and `PRODUCT_ID` to build a user-item interaction matrix
- Generated numeric `user_id` and `item_id` using `row_number()` (StringIndexer not available in workspace)
- Saved results to Delta: `/Volumes/workspace/default/basketdata/indexed_user_item_matrix`

---

## 🤖 ALS Model Training
- Trained using PySpark ML's ALS model
- Parameters:
  - `rank = 10`
  - `regParam = 0.1`
  - `maxIter = 10`
  - `implicitPrefs = True`
- Cold start strategy: `drop`

---

## 🎯 Recommendations Output
- Generated top-5 product recommendations per user
- Output schema: `user_id | item_id | predicted_rating`
- Saved results to: `/Volumes/workspace/default/basketdata/user_recommendations`

---

## 📊 Evaluation Metrics
- **Recall@K**: Measures how many relevant items were recommended
- **Precision@K**: Measures how many recommended items were relevant
- Metrics calculated using a sampled hold-out set
- Provides insight into recommendation accuracy

---

## 🧩 Personalization Features
- Joined `item_id` back to product metadata to display readable names
- Potential to filter recommendations by household age group or brand preferences
- Can extend to include campaign-based targeting or promotional uplift

---

## 📊 Streamlit + Power BI Dashboards
- Built a simple dashboard in Streamlit to display recommendations
- Power BI dashboard connected to Delta tables for interactive filtering
- Visualizations include: Top brands, weekly trends, and personalized product cards

---

## 📈 Next Steps
- Expand evaluation to include coverage, diversity, and novelty
- Deploy recommendations API with real-time scoring
- Integrate with customer segmentation and loyalty tiers

---

## 🧠 Tech Stack
- Databricks (Unity Catalog + Volumes)
- PySpark (SQL, MLlib, Delta Lake)
- Spark ML ALS
- Delta Tables for intermediate outputs
- Streamlit, Power BI for visualization

---

## 📬 Author
**Devsen Datha Mukkamala**  
Senior Software Engineer / Data Scientist  
[LinkedIn](https://www.linkedin.com/in/devsendatham) | [Portfolio](https://www.devsendatham.com)

