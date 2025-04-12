# Big Data Analysis with PySpark and Dask

This project demonstrates scalable data analysis using distributed computing frameworks: **PySpark** and **Dask**.

Created by **Aarthi Vanshette**.

## 🔧 Tools Used
- Apache Spark (PySpark)
- Dask
- Python 3.x

## 📁 Dataset
Place your large CSV file (e.g., NYC taxi data) in the `data/` folder. Ensure it has columns like:
- `trip_distance`
- `fare_amount`

Or use the provided `sample_data.csv`.

---

## 🚀 How to Run

### PySpark
```bash
python pyspark_analysis.py
```

### Dask
```bash
python dask_analysis.py
```

---

## 📜 PySpark Code

```python
from pyspark.sql import SparkSession

# Initialize Spark session
spark = SparkSession.builder \
    .appName("Big Data Analysis with PySpark") \
    .getOrCreate()

# Load data
df = spark.read.csv("data/sample_data.csv", header=True, inferSchema=True)

# Show schema
df.printSchema()

# Perform analysis
df.select("trip_distance", "fare_amount").describe().show()

# Average fare per trip distance
df.groupBy("trip_distance").avg("fare_amount").show()

spark.stop()

```

---

## 📜 Dask Code

```python
import dask.dataframe as dd

# Load data
df = dd.read_csv("data/sample_data.csv")

# Show basic info
print(df.head())

# Basic stats
print(df[["trip_distance", "fare_amount"]].describe().compute())

# Average fare per trip distance
avg_fare = df.groupby("trip_distance")["fare_amount"].mean().compute()
print(avg_fare)

```

---

## 📊 Output
- Basic statistics (mean, std, min, max) of trip distances and fares
- Average fare per trip distance bucket

---

## 🧠 Purpose
To showcase distributed processing and demonstrate how tools like PySpark and Dask can scale data analysis on large datasets efficiently.
