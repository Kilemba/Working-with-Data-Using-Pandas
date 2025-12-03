# Working-with-Data-Using-Pandas
A comprehensive guide to data manipulation and analysis using Pandas - covering data importing, inspection, filtering, sorting, and DataFrame operations with practical examples.

---
## Table of Contents

- [Overview](#overview)
- [Importing Data: CSV, Excel](#1-importing-data-csv-excel)
- [DataFrames and Series](#2-dataframes-and-series)
- [Inspecting Data](#3-inspecting-data-head-tail-info-describe)
- [Indexing and Selection](#4-indexing-and-selection-loc-iloc-slicing)
- [Filtering Data](#5-filtering-data)
- [Sorting and Renaming Columns](#6-sorting-renaming-columns)
- [Adding and Deleting Columns](#7-adding-and-deleting-columns)
- [Getting Started](#getting-started)

---

## Overview

Pandas (stands for Python Data Analysis) is an open-source software library designed for data manipulation and analysis. This guide provides hands-on examples for working with CSV and Excel files, performing data operations, and mastering essential Pandas functionality.

---

## 1. Importing Data: CSV, Excel

Pandas allows you to load data from multiple formats—most commonly CSV and Excel. The most common function is `pd.read_csv()`, which loads a CSV file into a DataFrame so you can analyze and manipulate it.

### Example

```python
import pandas as pd
from google.colab import files

uploaded = files.upload()

df = pd.read_csv("EVsalesHistory.csv")
df
```

For Excel files you would use:

```python
df_excel = pd.read_excel("file.xlsx")
```

---

## 2. DataFrames and Series

A Pandas **DataFrame** is a two-dimensional table-like structure in Python where data is arranged in rows and columns. A DataFrame contains data, which is the actual values in the table, columns, which are the labels of each field as well as rows/index.

A **Series** on the other hand is a one-dimensional labeled array that can hold data of any type (integer, float, string, Python objects, etc.). A series supports integer-based and label-based indexing, stores heterogeneous data types, and offers a variety of built-in methods for data manipulation and analysis.

**More info on DataFrames:** [https://www.geeksforgeeks.org/pandas/python-pandas-dataframe/](https://www.geeksforgeeks.org/pandas/python-pandas-dataframe/)

**More info on Series:** [https://www.geeksforgeeks.org/python/python-pandas-series/](https://www.geeksforgeeks.org/python/python-pandas-series/)

---

## 3. Inspecting Data: head(), tail(), info(), describe()

Inspecting data helps us understand what data looks like before performing analysis. We inspect data using built-in inspection functions that offer structural and statistical information.

- `head()` displays the first five rows by default to give a glimpse of the dataset's format, data types, and patterns
- `tail()` displays the last five rows to verify whether data was loaded completely or the file has formatting issues
- `info()` provides a summary of the dataframe i.e number of rows and columns, and how many non-null values exist. Helps identifying missing values early.
- `describe()` generates summary statistics for numerical columns i.e mean, minimum, maximum, and quartiles.

### Examples

```python
df.head()  # First 5 rows
df.tail()  # Last 5 rows
df.info()  # Data types + non-null counts
df.describe()  # Statistics for numeric columns
```

```python
# Identify missing values AND preview first rows
print(df.isnull().sum())
df.head()
```

```python
# Describe the dataset then sort by one column
df.describe()
df.sort_values("Value", ascending=False).head()
```

---

## 4. Indexing and Selection: loc[], iloc[], slicing

Indexing refers to selecting data from a series. We can use `.iloc[]` for position-based selection and `.loc[]` for label-based selection.

The `loc[]` method is label-based, meaning it uses the row index labels and column names. This makes it ideal when you know the exact column names or want to select a range of rows using their literal labels. On the other hand, `iloc[]` is strictly position-based and uses integer positions, similar to how lists in Python work. This is useful when selecting rows or columns based on their numerical order.

Slicing dataframes using standard python slicing returns a subset of rows which allows a more specified and precise selections especially during cleaning.

### Examples using real data

```python
# Select a row by integer position
df.iloc[0]
```

```python
# Select specific rows and columns by label
df.loc[0:5, ["Region", "Year", "Value"]]
```

```python
# Slice rows
subset = df[10:20]
```

```python
# Select first 10 rows, then from those rows keep only the 'Region' and 'Value' columns
subset = df.iloc[:10].loc[:, ["Region", "Value"]]
subset
```

---

## 5. Filtering Data

Filtering in pandas involves applying Boolean expressions to extract rows that meet specific conditions. For example, you can filter rows for a specific year, region, or any value-based condition.

### Examples

```python
# All electric vehicle data from 2020
df_2020 = df[df["Year"] == 2020]
```

```python
# Filter by region name
europe_data = df[df["Region"] == "Europe"]
```

```python
# All European records in 2020 with a Value greater than 100,000
df[
    (df["region"] == "Europe") &
    (df["year"] == 2020) &
    (df["value"] > 100000)
]
```

---

## 6. Sorting, Renaming Columns

Sorting helps reorganize data to reveal patterns, such as highest values, earliest years, or alphabetical order. This is done using the `sort_values()` method, which allows ascending or descending sorting. Renaming columns is equally important because it improves readability, especially when column names are unclear or too long.

### Example

```python
# Rename the 'Value' column to 'SalesValue'
Value_renamed = df.rename(columns={"value": "sales_value"})
```

---

## 7. Adding and Deleting Columns

You can create new columns by performing operations on existing ones. For example, dividing a numeric column by a factor can convert units. Adding new columns is central to feature engineering and analysis. Conversely, if a column is unnecessary or temporary, you can remove it using `drop()`.

### Example

```python
# Create a new column converting 'Value' to millions
df["Value_in_Millions"] = df["Value"] / 1_000_000
```

```python
# Remove the column
df = df.drop(columns=["Value_in_Millions"])
```

---

## Getting Started

To get started with Pandas, ensure you have it installed:

```bash
pip install pandas
```

For Google Colab users, Pandas is pre-installed and ready to use!

---

## Contributing

Feel free to contribute to this guide by submitting pull requests or opening issues for suggestions and improvements.

---
