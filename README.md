# 📊 Exploratory Data Analysis (EDA) Project – Adult Dataset

## 📌 Project Overview

This project focuses on performing **Exploratory Data Analysis (EDA)** on the **Adult dataset** using Python.

The analysis includes:

* Data loading and exploration
* Statistical analysis
* Data cleaning
* Missing-value handling
* Duplicate-value detection
* Outlier detection
* Winsorization
* Data visualization
* Automated EDA using AutoViz, Sweetviz, D-Tale, and YData Profiling

The main objective is to understand the structure of the dataset, identify data-quality issues, and extract useful patterns from the available data.

---

## 🛠️ Technologies & Libraries Used

* **Python**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **SciPy**
* **AutoViz**
* **Sweetviz**
* **D-Tale**
* **YData Profiling**
* **Jupyter Notebook**

---

## 📂 Dataset

The project uses the **Adult dataset (`adult.csv`)**.

The dataset contains information related to demographic and employment characteristics, including:

* Age
* Workclass
* Education
* Education Number
* Occupation
* Income
* Capital Gain
* Capital Loss
* Hours per Week
* Native Country

The `Income` column is used as an important variable during the analysis.

---

## 🔍 Exploratory Data Analysis

The project begins by loading the dataset using Pandas and examining:

* Dataset contents
* First few records
* Column names
* Dataset information
* Number of rows and columns
* Non-null counts
* Descriptive statistics

Example:

```python
import pandas as pd

df = pd.read_csv("adult.csv")

print(df.head())
print(df.columns)
print(df.info())
print(df.shape)
print(df.describe())
```

---

## 📈 Statistical Analysis

Several statistical operations are performed on the dataset.

### Age Analysis

The project calculates:

* Mean age
* Minimum age
* Maximum age
* Median age
* Standard deviation

```python
df["Age"].agg(["mean", "min", "max", "median"])
```

### Hours Per Week

The following statistics are calculated:

```python
df["Hours per Week"].agg(["min", "max", "mean", "median"])
```

### Education Analysis

The project examines:

* Education categories
* Number of unique education levels
* Education frequency

```python
df["Education"].value_counts()
df["Education"].nunique()
```

### Income Analysis

Income categories are also analyzed using:

```python
df["Income"].value_counts()
```

---

## 🧹 Data Cleaning

Data cleaning is performed to improve the quality of the dataset.

### Missing Values

The project replaces `" ?"` values with `None` and checks for missing values.

```python
df = df.replace(" ?", None)

df.isna().sum()
```

Missing values are handled in different columns using appropriate techniques.

For example:

```python
df["Workclass"] = df["Workclass"].fillna("unknown")
df["Occupation"] = df["Occupation"].fillna("Not Available")
df["Age"] = df["Age"].fillna(df["Age"].mean())
```

Forward fill and backward fill are also demonstrated:

```python
df["Age"] = df["Age"].ffill()
df["Native Country"] = df["Native Country"].bfill()
```

---

## 🔁 Duplicate Detection

The project checks whether duplicate records exist in the dataset.

```python
df.duplicated()
df.duplicated().sum()
```

Duplicate records can also be displayed using:

```python
df[df.duplicated(keep=False)]
```

---

## 🚨 Outlier Detection

The project demonstrates two approaches for identifying outliers in the **Age** column.

### 1. IQR Method

The Interquartile Range (IQR) method is used to calculate lower and upper bounds.

```python
Q1 = df["Age"].quantile(0.25)
Q3 = df["Age"].quantile(0.75)

IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```

Records outside these limits are identified as potential outliers.

### 2. Z-Score Method

The project also uses the Z-score method:

```python
from scipy.stats import zscore

df["Age_zscore"] = zscore(df["Age"])

z_outliers = df[df["Age_zscore"].abs() > 3]
```

---

## 📊 Winsorization

Winsorization is demonstrated to reduce the effect of extreme values.

```python
from scipy.stats.mstats import winsorize

df["Age_winsorized"] = winsorize(
    df["Age"],
    limits=[0, 0.5]
)
```

---

## 📉 Data Visualization

Matplotlib is used to create visualizations.

### Bar Chart

The relationship between Education and Education Number is visualized using a bar chart.

```python
import matplotlib.pyplot as plt

plt.bar(df["Education"], df["EducationNum"])

plt.title("Education system")
plt.xlabel("Education")
plt.ylabel("years")

plt.show()
```

### Line Chart

A line chart is also created to visualize Education and Education Number.

```python
plt.plot(df["Education"], df["EducationNum"])

plt.title("Education system")
plt.xlabel("Education")
plt.ylabel("years")

plt.show()
```

---

## 🤖 Automated EDA

The project explores multiple automated EDA libraries.

### AutoViz

AutoViz is used to automatically generate visualizations from the dataset.

```python
from autoviz.AutoViz_Class import AutoViz_Class

AV = AutoViz_Class()

AV.AutoViz(
    filename="adult.csv",
    sep=",",
    depVar="Income",
    dfte=data
)
```

### Sweetviz

Sweetviz is used to generate an automated EDA report.

```python
import sweetviz as sv

report = sv.analyze(data)
report.show_html("sweetviz.report.html")
```

### D-Tale

D-Tale is used for interactive dataset exploration.

```python
import dtale

dtale.show(data)
```

### YData Profiling

YData Profiling is used to generate a detailed profiling report.

```python
from ydata_profiling import ProfileReport

profile = ProfileReport(
    data,
    title="Adult dataset report"
)

profile.to_notebook_iframe()
```

---

## 🎯 Key EDA Tasks Covered

| Area              | Tasks                                      |
| ----------------- | ------------------------------------------ |
| Data Loading      | Read CSV using Pandas                      |
| Data Exploration  | `head()`, `info()`, `shape`, `describe()`  |
| Statistics        | Mean, median, min, max, standard deviation |
| Filtering         | Conditional filtering and `isin()`         |
| Grouping          | Grouping data by Education                 |
| Missing Values    | Detection and filling                      |
| Duplicates        | Duplicate detection                        |
| Outliers          | IQR and Z-score                            |
| Outlier Treatment | Winsorization                              |
| Visualization     | Bar chart and line chart                   |
| Automated EDA     | AutoViz, Sweetviz, D-Tale, YData Profiling |

---

## 📁 Project Structure

```text
EDA-Project/
│
├── Copy_of_EDA_PROJECT.ipynb
├── adult.csv
└── README.md
```

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
```

### 2. Open the project

Open:

```text
Copy_of_EDA_PROJECT.ipynb
```

using **Jupyter Notebook** or **Google Colab**.

### 3. Add the dataset

Place:

```text
adult.csv
```

in the appropriate project directory.

### 4. Install required libraries

```bash
pip install pandas matplotlib scipy autoviz sweetviz dtale ydata-profiling
```

### 5. Run the notebook

Execute the notebook cells sequentially to reproduce the analysis.

---

## 📚 Learning Outcomes

Through this project, I practiced:

* Exploratory Data Analysis using Python
* Pandas data manipulation
* Descriptive statistics
* Data cleaning techniques
* Missing-value treatment
* Duplicate detection
* Outlier detection and treatment
* Data visualization using Matplotlib
* Automated EDA techniques
* Generating data-profiling reports

---

## 👨‍💻 Author

**Sai Nikhil**

Data Analytics Learner | Python | SQL | Excel | Power BI

---

⭐ If you found this project useful, feel free to star the repository!
