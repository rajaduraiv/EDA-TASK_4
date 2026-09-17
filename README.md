# Exploratory Data Analysis (EDA) – Shopify Stock Data

## 1. Project Title

**Exploratory Data Analysis on Shopify Stock Data**

## 2. Objective

The objective of this task is to perform Exploratory Data Analysis (EDA) on Shopify stock market data. The dataset contains daily stock information such as Open, High, Low, Close, Adjusted Close and Trading Volume.

The analysis includes data loading, data inspection, data cleaning, feature creation, descriptive statistics, return analysis and data visualization.

## 3. Technologies Used

* Python
* Google Colab / Jupyter Notebook
* Pandas
* Matplotlib
* CSV Dataset

## 4. Dataset

**Dataset Name:** SHOP.csv

The dataset contains Shopify stock information.

### Main Columns

| Column    | Description                    |
| --------- | ------------------------------ |
| date      | Trading date                   |
| open      | Opening stock price            |
| high      | Highest stock price of the day |
| low       | Lowest stock price of the day  |
| close     | Closing stock price            |
| adj_close | Adjusted closing price         |
| volume    | Number of shares traded        |

The dataset initially contains **2469 rows and 7 columns**.

---

# 5. Operations Performed

## Operation 1 – Import Libraries

### Code

```python
import pandas as pd
import matplotlib.pyplot as plt
```

### Purpose

Pandas is used for data loading and data manipulation. Matplotlib is used for creating graphs and visualizations.

---

## Operation 2 – Load Dataset

### Code

```python
df = pd.read_csv("/content/SHOP.csv")
```

### Purpose

The Shopify stock CSV file is loaded into a Pandas DataFrame.

---

## Operation 3 – Display First Five Records

### Code

```python
print(df.head())
```

### Output

```text
                        date   open   high    low  close  adj_close     volume
0  2015-05-21 00:00:00-04:00  2.800  2.874  2.411  2.568      2.568  123039000
1  2015-05-22 00:00:00-04:00  2.607  3.110  2.600  2.831      2.831   28412000
2  2015-05-26 00:00:00-04:00  2.980  3.034  2.908  2.965      2.965    8202000
3  2015-05-27 00:00:00-04:00  3.067  3.081  2.700  2.750      2.750    7976000
4  2015-05-28 00:00:00-04:00  2.755  2.774  2.648  2.745      2.745    4000000
```

### Result

The first five rows of the dataset were displayed successfully.

---

# 6. Dataset Shape

### Code

```python
print(df.shape)
```

### Output

```text
(2469, 7)
```

### Result

The dataset contains:

* **Rows:** 2469
* **Columns:** 7

---

# 7. Dataset Information

### Code

```python
print(df.info())
```

### Output

```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2469 entries, 0 to 2468
Data columns (total 7 columns):

date        2469 non-null   object
open        2469 non-null   float64
high        2469 non-null   float64
low         2469 non-null   float64
close       2469 non-null   float64
adj_close   2469 non-null   float64
volume      2469 non-null   int64
```

### Result

The dataset contains:

* 1 date column
* 5 floating-point price columns
* 1 integer volume column

---

# 8. Missing Value Checking

### Code

```python
print(df.isnull().sum())
```

### Output

```text
date         0
open         0
high         0
low          0
close        0
adj_close    0
volume       0
dtype: int64
```

### Result

There are **no missing values** in the original dataset.

---

# 9. Remove Duplicate Records

### Code

```python
df = df.drop_duplicates()
```

### Purpose

Duplicate records are removed to improve data quality and avoid repeated observations during analysis.

---

# 10. Convert Date Column

### Code

```python
df["date"] = pd.to_datetime(
    df["date"],
    format="mixed",
    errors="coerce"
)
```

### Purpose

The date column is converted into a datetime format so that it can be sorted and used as a time-series index.

---

# 11. Sort Data by Date

### Code

```python
df = df.sort_values("date")
```

### Purpose

The stock records are arranged chronologically.

---

# 12. Set Date as Index

### Code

```python
df = df.set_index("date")
```

### Purpose

The date column is made the DataFrame index, which is useful for time-series analysis and visualization.

---

# 13. Remove Missing Values

### Code

```python
df = df.dropna()
```

### Purpose

Any remaining rows containing missing values are removed.

After cleaning, the dataset contains **2469 records** with 6 data columns and the date as the index.

---

# 14. Feature Engineering

Three new features were created.

## 14.1 Daily Price Change

### Code

```python
df["Daily_Price_'Change"] = df["close"] - df["open"]
```

This calculates the difference between the closing price and opening price.

---

## 14.2 Daily Return Percentage

### Code

```python
df["Daily_Return_%"] = ((df["close"] - df["open"]) / df["open"]) * 100
```

This calculates the daily percentage return.

---

## 14.3 Price Range

### Code

```python
df["Price_Range"] = df["high"] - df["low"]
```

This calculates the difference between the highest and lowest price of the day.

---

# 15. Display Processed Data

### Code

```python
df.head()
```

### Sample Output

| Date       |  Open |  High |   Low | Close | Daily Price Change | Daily Return % | Price Range |
| ---------- | ----: | ----: | ----: | ----: | -----------------: | -------------: | ----------: |
| 2015-05-21 | 2.800 | 2.874 | 2.411 | 2.568 |             -0.232 |        -8.2857 |       0.463 |
| 2015-05-22 | 2.607 | 3.110 | 2.600 | 2.831 |              0.224 |         8.5923 |       0.510 |
| 2015-05-26 | 2.980 | 3.034 | 2.908 | 2.965 |             -0.015 |        -0.5034 |       0.126 |
| 2015-05-27 | 3.067 | 3.081 | 2.700 | 2.750 |             -0.317 |       -10.3358 |       0.381 |
| 2015-05-28 | 2.755 | 2.774 | 2.648 | 2.745 |             -0.010 |        -0.3630 |       0.126 |

---

# 16. Descriptive Statistics

### Code

```python
print(df.describe())
```

### Important Output

| Statistic |    Open |    High |     Low |   Close |
| --------- | ------: | ------: | ------: | ------: |
| Count     |    2469 |    2469 |    2469 |    2469 |
| Mean      |  48.464 |  49.505 |  47.348 |  48.457 |
| Minimum   |   1.939 |   1.985 |   1.848 |   1.933 |
| Maximum   | 171.800 | 176.292 | 168.510 | 169.060 |

The descriptive statistics also include volume, daily price change, daily return percentage and price range.

---

# 17. Mean Daily Return

### Code

```python
print("Mean Return:",
      df["Daily_Return_%"].mean())
```

### Output

```text
Mean Return: 0.08640631099421993
```

### Result

The mean daily return is approximately **0.0864%**.

---

# 18. Return Variance

### Code

```python
print("Return Variance:",
      df["Daily_Return_%"].var())
```

### Output

```text
Return Variance: 9.733081984179565
```

---

# 19. Return Standard Deviation

### Code

```python
print("Return Standard Deviation:",
      df["Daily_Return_%"].std())
```

### Output

```text
Return Standard Deviation: 3.1197887723657773
```

The standard deviation measures the variation in daily returns.

---

# 20. Trading Volume Trend

### Code

```python
plt.figure(figsize=(12,5))
plt.plot(df.index, df["volume"])
plt.title("Shopify Trading Volume Trend")
plt.xlabel("Date")
plt.ylabel("Volume")
plt.xticks(rotation=45)
plt.show()
```

### Output

A line graph showing the **Shopify trading volume trend over time**.

<img width="1001" height="491" alt="image" src="https://github.com/user-attachments/assets/eb248890-b09e-4cfd-9584-99788efddf68" />


### Purpose

This visualization helps examine how trading volume changes across the available dates.

---

# 21. Daily Return Distribution

### Code

```python
plt.figure(figsize=(12,5))
plt.hist(df["Daily_Return_%"], bins=30)
plt.title("Shopify Daily Return Distribution")
plt.xlabel("Daily Return (%)")
plt.ylabel("Frequency")
plt.show()
```

### Output

A histogram showing the distribution of Shopify's daily returns.

<img width="1005" height="470" alt="image" src="https://github.com/user-attachments/assets/36f13062-bd80-4fd2-9ba6-2a1825bf1ffb" />


### Purpose

The histogram helps understand the frequency and spread of daily returns.

---

# 22. Price Range Trend

### Code

```python
plt.figure(figsize=(12, 5))
plt.plot(df.index, df["Price_Range"])
plt.title("Shopify Stock Price Trend")
plt.xlabel("date")
plt.ylabel("Price_Range")
plt.xticks(rotation=45)
plt.show()
```

### Output

A line graph showing the variation in the daily price range.

<img width="1010" height="491" alt="image" src="https://github.com/user-attachments/assets/b08937d4-0219-444e-938b-af75e442d3a8" />


---

# 23. OHLC Price Visualization

### Code

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12,5))
plt.plot(df.index, df["open"], label="Open")
plt.plot(df.index, df["high"], label="High")
plt.plot(df.index, df["low"], label="Low")
plt.plot(df.index, df["open"], label="Close")

plt.title("Shopify OHLC Prices")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.show()
```

### Output

A line chart displaying the stock price values over time.

<img width="1005" height="491" alt="image" src="https://github.com/user-attachments/assets/a651efa0-4150-4eb2-abe2-615495b75232" />


### Purpose

The visualization compares the Open, High, Low and Close price values.

---

# 24. Moving Average

### Code

```python
df["MA_20"] = df["close"].rolling(20).mean()

df["MA_50"] = df["close"].rolling(50).mean()
```

### Purpose

Two moving averages are calculated:

* **20-Day Moving Average**
* **50-Day Moving Average**

Moving averages help observe the general movement of the closing price.

---

# 25. Closing Price and Moving Averages

### Code

```python
plt.figure(figsize=(12,5))

plt.plot(df.index, df["close"], label="Daily Close")
plt.plot(df.index, df["MA_20"], label="20-Day MA")
plt.plot(df.index, df["MA_50"], label="50-Day MA")

plt.title("Shopify Closing Price and Moving Averages")
plt.xlabel("Date")
plt.ylabel("Price")
plt.legend()
plt.xticks(rotation=45)
plt.show()
```

### Output

A line graph comparing:

* Daily closing price
* 20-day moving average
* 50-day moving average

<img width="1005" height="491" alt="image" src="https://github.com/user-attachments/assets/203a7971-3352-493c-bcbe-5f4c71d7ca52" />

---

# 26. KDE of Daily Returns

### Code

```python
plt.figure(figsize=(10,5))

df["Daily_Return_%"].plot(kind="kde")

plt.title("KDE of Shopify Daily Returns")
plt.xlabel("Daily Return (%)")

plt.show()
```

### Output

A KDE plot showing the estimated distribution of Shopify's daily returns.

<img width="855" height="470" alt="image" src="https://github.com/user-attachments/assets/68918e7c-9c14-4b4a-9ff2-bbb976c4679f" />


---

# 27. EDA Summary

The following EDA operations were performed:

1. Imported Pandas and Matplotlib.
2. Loaded the Shopify stock CSV dataset.
3. Displayed the first five records.
4. Checked the dataset shape.
5. Checked column information and data types.
6. Checked missing values.
7. Removed duplicate records.
8. Converted the date column to datetime.
9. Sorted the data by date.
10. Set the date as the index.
11. Removed remaining missing values.
12. Created Daily Price Change.
13. Created Daily Return Percentage.
14. Created Price Range.
15. Generated descriptive statistics.
16. Calculated mean daily return.
17. Calculated return variance.
18. Calculated return standard deviation.
19. Visualized trading volume.
20. Visualized daily return distribution.
21. Visualized price range.
22. Visualized OHLC prices.
23. Calculated 20-day and 50-day moving averages.
24. Visualized closing price with moving averages.
25. Created a KDE plot for daily returns.

---

# 28. Key Results

* The dataset contains **2469 records** and initially has **7 columns**.
* No missing values were found in the original dataset.
* The date column was processed for time-series analysis.
* Three additional analytical features were created.
* Mean daily return: **0.0864%**
* Return variance: **9.7331**
* Return standard deviation: **3.1198**
* Multiple graphs were created to understand trading volume, returns, price range and stock-price movement.

---

# 29. Conclusion

The EDA provided an overview of Shopify's historical stock data. Data cleaning and preprocessing were performed before calculating additional financial features. Statistical measures were used to understand the distribution and variability of returns, while graphical visualizations helped examine stock prices, trading volume, price ranges and moving averages.

This analysis demonstrates how Python, Pandas and Matplotlib can be used to explore and understand financial time-series data.
