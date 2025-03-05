# 📊 Global Commodity Prices - Exploratory Data Analysis (EDA)

## 📌 Project Overview  
This project explores global commodity price trends using **Exploratory Data Analysis (EDA)**. The analysis identifies key trends, correlations, and statistical insights for various commodities, including **oil, coffee, sugar, and natural gas**.  

---

## 📂 Dataset Details  
- **Dataset Name:** Global Commodity Prices  
- **Source:** *Intellipaat*  
- **Size:** *756 rows, 12 columns*  
- **Key Attributes:**  
  - `date`: Time-series data  
  - `oil_brent`, `oil_dubai`: Oil price variations  
  - `coffee_arabica`, `coffee_robustas`: Coffee price trends  
  - `sugar_eu`, `sugar_us`: Regional sugar prices  
  - `natural_gas`: Global natural gas prices  

---

## 🔧 Libraries Used  
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
```

---

## 🔍 Key Exploratory Analysis & Findings  

### 1️⃣ What is the maximum price of Robusta coffee?  
```python
df["coffee_robustas"].max()
```
✅ **Max Price:** *$6.88*  

### 2️⃣ What is the 75th percentile of sugar prices in the European Union (EU)?  
```python
df["sugar_eu"].quantile(0.75)
```
✅ **75th Percentile:** *$0.5695*  

### 3️⃣ Skewness of Arabica coffee price distribution  
```python
df["coffee_arabica"].skew()
```
✅ **Skewness:** *0.59 (Moderately Right-Skewed)*  

### 4️⃣ Is the distribution of US sugar prices normal?  
```python
shapiro_test_stat, shapiro_p_value = stats.shapiro(df['sugar_us'])
```
✅ **Shapiro-Wilk Test p-value:** *0.000 (Not Normally Distributed)*  
✅ **Visualization:**  
- Right-skewed distribution  
- Heavy tails (higher kurtosis)  

### 5️⃣ How many times did Dubai oil price exceed Brent oil price by $10?  
```python
(df['oil_dubai'] - df['oil_brent'] > 10).sum()
```
✅ **Result:** *0 occurrences* (Prices are closely related)  

### 6️⃣ Overall Price Trend for Each Commodity  
```python
plt.figure(figsize=(15, 10))
for commodity in commodities:
    plt.plot(df['date'], df[commodity], label=commodity)
plt.legend()
plt.show()
```
✅ **Insights:**  
- Oil prices show high volatility  
- Natural gas spiked significantly in **2022**  
- Agricultural commodities display moderate fluctuations  

### 7️⃣ Which commodity had the highest price fluctuations?  
```python
fluctuations = {c: df[c].max() - df[c].min() for c in df.columns[2:]}
highest_fluctuation = max(fluctuations, key=fluctuations.get)
```
✅ **Highest Volatility:** **Brent Oil** *(Fluctuation of ~$132.66)*  

### 8️⃣ Quarterly Variations in Brent Oil Prices (Last 5 Years)  
```python
df.resample('Q', on='date')['oil_brent'].mean().plot(kind='line', marker='o')
```
✅ **Findings:**  
- **Lowest price:** *Q2 2020 (~$31)*  
- **Highest price:** *Q2 2022 (~$113)*  
- **Recent stability:** *$88-$99 range*  

### 9️⃣ Correlation between global & regional sugar prices  
```python
df[['sugar_world', 'sugar_eu', 'sugar_us']].corr()
```
✅ **Correlation Matrix:**  
- **World vs. US Sugar:** *0.79 (Strong Positive Correlation)*  
- **EU vs. US Sugar:** *0.59 (Moderate Correlation)*  
- **World vs. EU Sugar:** *0.30 (Weak Correlation)*  

### 🔟 Is there a significant difference in sugar prices between EU & US?  
```python
t_stat, p_value = stats.ttest_ind(df['sugar_eu'], df['sugar_us'], nan_policy='omit')
```
✅ **T-test p-value:** *0.0048* (Significant difference between distributions)  

---

## 📊 Visualizations  
| Analysis | Graph |
|----------|-------|
| US Sugar Prices Distribution | Histogram & Q-Q Plot 📈 |
| Brent Oil Quarterly Prices | Line Chart 📊 |
| Commodity Trends | Multi-Line Chart 📈 |
| Correlation between Sugar Prices | Heatmap 🔥 |

---

