# Big Data Analysis with PySpark and Dask

This project demonstrates scalable data analysis using distributed computing frameworks: **PySpark** and **Dask**.

Created by **Aarthi Vanshette**

---

## 🔧 Tools Used
- Apache Spark (PySpark)
- Dask
- Python 3.x

## 📁 Dataset
Place your CSV file in the `data/` folder. The sample dataset should have:
- `trip_distance`
- `fare_amount`

---

## 🚀 How to Run

### Install dependencies
```bash
pip install pyspark dask
```

### Run the script
```bash
python insights_analysis.py
```

---

## 📜 Code with Insights

```python
# Big Data Insights using PySpark and Dask
# Author: Aarthi Vanshette

# --- PYSPARK INSIGHTS ---
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Insights with PySpark").getOrCreate()
df = spark.read.csv("data/sample_data.csv", header=True, inferSchema=True)

# Basic stats
stats = df.select("trip_distance", "fare_amount").describe()
stats.show()

# Insight 1: Trips above average distance
avg_distance = df.agg({"trip_distance": "avg"}).collect()[0][0]
long_trips = df.filter(df["trip_distance"] > avg_distance)
print(f"\n[PySpark] Trips above average distance ({avg_distance:.2f} miles): {long_trips.count()}")

# Insight 2: Correlation between distance and fare
correlation = df.stat.corr("trip_distance", "fare_amount")
print(f"[PySpark] Correlation between trip distance and fare: {correlation:.2f}")

spark.stop()

# --- DASK INSIGHTS ---
import dask.dataframe as dd

df_dask = dd.read_csv("data/sample_data.csv")

# Basic stats
print("\n[Dask] Basic Statistics:")
print(df_dask[["trip_distance", "fare_amount"]].describe().compute())

# Insight 3: Most common trip distance
common_distance = df_dask["trip_distance"].value_counts().nlargest(1).compute()
print("\n[Dask] Most Common Trip Distance:")
print(common_distance)

# Insight 4: Average fare for short vs. long trips
short = df_dask[df_dask["trip_distance"] < 2]["fare_amount"].mean().compute()
long = df_dask[df_dask["trip_distance"] >= 2]["fare_amount"].mean().compute()
print(f"\n[Dask] Avg fare - Short trips (<2 mi): ${short:.2f}")
print(f"[Dask] Avg fare - Long trips (>=2 mi): ${long:.2f}")
```

---

## 📊 Insights Derived

- 🚕 **Trips above average distance:** Identified using PySpark filtering.
- 💰 **Correlation between distance and fare:** Measured to understand pricing patterns.
- 📈 **Most common trip distance:** Found using Dask's value count aggregation.
- 🧮 **Average fare for short vs. long trips:** Compared to derive pricing trends.

---

## 🧠 Purpose
To showcase distributed processing and demonstrate how tools like PySpark and Dask can scale data analysis and generate insights from large datasets.
