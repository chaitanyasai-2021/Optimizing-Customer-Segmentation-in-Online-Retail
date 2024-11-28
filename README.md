# 📈 Optimizing Customer Engagement in Online Retail  

In this project, I analyzed various customer segments in an Online Retail dataset using Python. For this task, I employed cohort analysis, RFM Analysis, and k-means clustering.  

## 🔍 Problem Statement  

**Identify the customer segments in the dataset and prescribe a course of business action for each segment.**  

Example of a segment might be the customers who bring the max profit and visit frequently.  

## 📊 Data Overview  

**Source:** [The UCI Machine Learning Repository](https://www.kaggle.com/datasets/carrie1/ecommerce-data)  

This dataset contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a non-store online retail.  

## 🖼️ Data Snapshot  

![Screenshot (516)](https://user-images.githubusercontent.com/121576163/229271541-059cf0f3-272b-41ba-a53c-fae854fbe90e.png)  

## 🛠️ Data Exploration  

- 🧹 Removed Null Values  
- ✂️ Removed Duplicate Values  
- 📍 Maximum transactions are from the UK  

![Screenshot (517)](https://user-images.githubusercontent.com/121576163/229271584-9185bbb3-0da0-44dc-8aa7-99940322b33d.png)  

### 📅 Cohort Analysis  

A cohort is a set of users who share similar characteristics over time. Cohort analysis groups users into mutually exclusive groups, and their behavior is measured over time.  

There are three types of cohort analysis:  
- **📅 Time Cohorts:** Groups customers by their purchase behavior over time.  
- **📦 Behavior Cohorts:** Groups customers by the product or service they signed up for.  
- **📏 Size Cohorts:** Groups customers by their spending within a period.  

For this project, I chose **time cohorts**. The steps are as follows:  

1. 🗓️ Identified cohort month for each customer (the month when the customer first transacted).  
   ```python  
   # First Transaction month (Cohort Month) for each customer  
   df3['Cohort Month'] = df3.groupby('CustomerID')['InvoiceFormat'].transform(min)  
   ```  

2. 🔢 Identified cohort index (difference between transaction month and cohort month) for each transaction.  
   ```python  
   # This function calculates difference between invoice format and cohort month  
   def diff(d, x1, y1):  
       l = []  
       for i in range(len(d)):  
           xyear = d[x1][i].year  
           xmonth = d[x1][i].month  
           yyear = d[y1][i].year  
           ymonth = d[y1][i].month  
           diff = ((xyear - yyear) * 12) + (xmonth - ymonth) + 1  
           l.append(diff)  
       return l  
   ```  

3. 📊 Grouped data by cohort month and cohort index.  
4. 📋 Developed a pivot table.  

![Screenshot (518)](https://user-images.githubusercontent.com/121576163/229271650-bda075f9-bb60-4f31-a862-6286d2f35c6e.png)  

5. 🔥 Developed a time cohort heatmap.  

![Screenshot (519)](https://user-images.githubusercontent.com/121576163/229271678-4586ca52-ba15-4ff9-a155-3fa704b9a698.png)  

### 📌 Summary  

1. 💔 Roughly 10% of new joiners remain after a year. Retention is quite poor.  
2. 🎯 About 250 new people join each month, which indicates marketing efforts are satisfactory.  

---

## 📈 RFM Analysis  

**RFM** stands for ***Recency, Frequency, Monetary***. It evaluates:  
- **📅 Recency:** How recently a customer transacted.  
- **🔄 Frequency:** How often they transacted.  
- **💰 Monetary:** How much they spent.  

These scores help group customers for further analysis.  

### 🗓️ Recency  
- The last transaction in the dataset was on 2011-12-09. Thus, recency was calculated using 2012-01-01 as the snapshot date.  

### 🔢 Frequency  
   ```python  
   freq = df6.groupby(["CustomerID"])[["InvoiceNo"]].count()  
   ```  

### 💵 Monetary  
   ```python  
   df6["total"] = df6["Quantity"] * df6["UnitPrice"]  
   money = df6.groupby(["CustomerID"])[["total"]].sum()  
   ```  

![Screenshot (520)](https://user-images.githubusercontent.com/121576163/229271844-f0d29315-a28f-44ad-ade0-248dc37e11df.png)  

---

## 📚 Clustering  

Before applying **K-means clustering**, I addressed data skewness.  

- 📊 **RFM Distribution**  
  ![Screenshot (521)](https://user-images.githubusercontent.com/121576163/229271877-21dc4f67-cec0-41c3-a96f-1fbaa82a758d.png)  

  The data was left-skewed, so I used log transformation:  

- 🔄 **After Log Transformation**  
  ![Screenshot (522)](https://user-images.githubusercontent.com/121576163/229271922-92a7cc2f-9317-4cb0-a2b9-6ef13ea62b70.png)  

### 🤖 Implementing K-means  

```python  
inertia = []  
for i in range(1, 11):  
    kmeans = KMeans(n_clusters=i)  
    kmeans.fit(scaled)  
    inertia.append(kmeans.inertia_)  
```  

- 📉 **Elbow Curve**  
  ![Screenshot (523)](https://user-images.githubusercontent.com/121576163/229271974-815eed30-2924-449e-8da2-247b62ca0e7c.png)  

From the graph, I chose **3 clusters**.  

### 🏷️ Customer Segments  

1. **🌟 Best Customers**: High-frequency, high-monetary value, recent transactions.  
2. **⚠️ At-Risk Customers**: Long time since the last transaction, low spending.  
3. **💼 Average Customers**: Regular transactions, moderate spending.  

![Screenshot (526)](https://user-images.githubusercontent.com/121576163/229272126-72f39a4d-683d-435b-8786-c67406d4f1cc.png)  

---

## 💡 Suggestions and Cluster Interpretation  

1. **⚠️ At Risk Customers**:  
   - Suggestion: Analyze why they left; offer sales or discounts to win them back.  

2. **💼 Average Customers**:  
   - Suggestion: Convert to best customers through discounts, excellent support, and targeted promotions.  

3. **🌟 Best Customers**:  
   - Suggestion: Focus advertising and product launches on this group. Heavy discounts aren’t needed.  

![Screenshot (528)](https://user-images.githubusercontent.com/121576163/229272921-b22fda1a-15cd-485d-89b8-4495489a8676.png)  

---  

Let me know if you need further edits! 😊  

---  

## 🚀 Future Work  

- **Expand Analysis**: Include new customer features, like demographics and lifetime value.  
- **Dynamic Segmentation**: Automate real-time segmentation for evolving behaviors.  
- **Advanced Models**: Explore hierarchical clustering or DBSCAN for complex relationships.  
- **Predictive Insights**: Use predictive analytics to forecast customer behavior and recommend proactive strategies.  

This project sets a strong foundation for tailored customer engagement, paving the way for smarter, data-driven business decisions! 😊  
