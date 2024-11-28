# 📈 Optimizing Customer Engagement in Online Retail  

This project explores customer segmentation in online retail using Python, applying cohort analysis, RFM analysis, and K-means clustering to uncover actionable business insights and improve engagement strategies.  

---  

## 🎯 Problem Statement  

**Identify customer segments within the dataset and recommend tailored strategies for each group.**  

For instance, identifying frequent customers who drive maximum profit and devising strategies to enhance their engagement.  

---  

## 📊 Data Overview  

**Source**: [The UCI Machine Learning Repository](https://www.kaggle.com/datasets/carrie1/ecommerce-data)  
This dataset includes all transactions between 01/12/2010 and 09/12/2011 for a non-store online retail business.  

---  

## 🔍 Data Exploration  

- ✅ Removed null and duplicate values.  
- 🌍 Found maximum transactions originated from the UK.  

![Snapshot](https://user-images.githubusercontent.com/121576163/229271584-9185bbb3-0da0-44dc-8aa7-99940322b33d.png)  

---  

## 📆 Cohort Analysis  

**What is a cohort?**  
A group of users sharing similar characteristics over time, analyzed to study behavioral trends.  

**Types of Cohorts**:
1. **Time Cohorts**: Grouped by purchase behavior over time (used in this project).  
2. **Behavior Cohorts**: Grouped by product/service preference.  
3. **Size Cohorts**: Grouped by spending levels.  

**Steps**:  
1. Identify the cohort month for each customer (first transaction date).  
2. Calculate the cohort index (months since the first transaction).  
3. Group data by cohort month and index.  
4. Create a pivot table and heatmap to visualize retention.  

📈 **Key Insights**:  
- Retention is poor, with only ~10% of users staying active after one year.  
- Marketing adds ~250 new customers monthly, which is satisfactory.  

---  

## 📊 RFM Analysis  

**RFM (Recency, Frequency, Monetary):** Evaluates customers based on their last purchase, purchase frequency, and total spend.  

1. **Recency**: Time since last purchase (calculated as of 2012-01-01).  
2. **Frequency**: Count of purchases.  
3. **Monetary**: Total revenue contribution per customer.  

![RFM Distribution](https://user-images.githubusercontent.com/121576163/229271844-f0d29315-a28f-44ad-ade0-248dc37e11df.png)  

---  

## 📉 Clustering  

### 🔄 Data Transformation  
- Applied **log transformation** to normalize left-skewed RFM data for better clustering.  

### 📍 K-Means Clustering  
- Used **Elbow Method** to determine 3 optimal clusters:  
  1. **Best Customers**  
  2. **Average Customers**  
  3. **At-Risk Customers**  

![Cluster Insights](https://user-images.githubusercontent.com/121576163/229272168-ecae1c1e-117d-472e-a950-91ab9f2e31a0.png)  

---  

## 💡 Suggestions and Cluster Interpretation  

### 🔴 At-Risk Customers  
- **Traits**: Long inactivity, low spending.  
- **Actions**: Investigate churn reasons; re-engage with targeted discounts and promotions.  

### 🟡 Average Customers  
- **Traits**: Recent and regular activity, moderate spending.  
- **Actions**: Focus on converting them into best customers with personalized offers and excellent support.  

### 🟢 Best Customers  
- **Traits**: Frequent purchases, high revenue contribution.  
- **Actions**: Introduce premium products and loyalty rewards; avoid heavy discounts.  

---  

## 🚀 Future Work  

- **Expand Analysis**: Include new customer features, like demographics and lifetime value.  
- **Dynamic Segmentation**: Automate real-time segmentation for evolving behaviors.  
- **Advanced Models**: Explore hierarchical clustering or DBSCAN for complex relationships.  
- **Predictive Insights**: Use predictive analytics to forecast customer behavior and recommend proactive strategies.  

This project sets a strong foundation for tailored customer engagement, paving the way for smarter, data-driven business decisions! 😊  
