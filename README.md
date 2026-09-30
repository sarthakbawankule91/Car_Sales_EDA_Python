# 🚗 Car Sales Exploratory Data Analysis

## 📌 Project Overview

This project performs an **Exploratory Data Analysis (EDA)** on a Car Sales dataset containing information about more than 9,500 cars sold in Ukraine.

The objective of this project is to understand the structure and quality of the dataset, perform data cleaning and preprocessing, explore relationships between car attributes, and identify useful patterns in used-car sales data.

The analysis was performed using **Python, Pandas, NumPy, Matplotlib, and Seaborn** in Jupyter Notebook.

---

## 🎯 Problem Statement

The dataset contains information about used-car sales in Ukraine. The analysis focuses on understanding different factors related to car sales, including:

* Car brands and models
* Car body types
* Selling price
* Mileage
* Engine volume
* Engine type
* Registration status
* Manufacturing year
* Drive type

The project demonstrates a complete basic EDA workflow:

**Data Loading → Data Profiling → Data Cleaning → Data Preprocessing → Exploratory Analysis → Insights**

---

## 📊 Dataset Information

| Attribute | Details                 |
| --------- | ----------------------- |
| Dataset   | Car Sales               |
| Location  | Ukraine                 |
| Year      | 2019                    |
| Records   | 9,576                   |
| Columns   | 10                      |
| Data Type | Structured tabular data |

### Dataset Columns

| Column         | Description         |
| -------------- | ------------------- |
| `car`          | Car brand           |
| `price`        | Car selling price   |
| `body`         | Body type           |
| `mileage`      | Vehicle mileage     |
| `engV`         | Engine volume       |
| `engType`      | Engine/fuel type    |
| `registration` | Registration status |
| `year`         | Manufacturing year  |
| `model`        | Car model           |
| `drive`        | Drive type          |

---

## 🛠️ Technologies Used

* **Python**
* **Pandas** – Data manipulation and analysis
* **NumPy** – Numerical operations
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical visualization
* **Jupyter Notebook**
* **Pandas Profiling** – Dataset profiling

---

## 🔍 Exploratory Data Analysis Process

### 1. Data Loading

The dataset was imported from an Excel file using Pandas.

```python
CarSales_Data = pd.read_excel("Car_Sales.xlsx")
```

The initial dataset contains:

```text
Rows    : 9,576
Columns : 10
```

---

### 2. Data Understanding

The dataset was examined using:

* `shape`
* `head()`
* `columns`
* `describe()`
* `isnull().sum()`
* Duplicate checks
* Data profiling

The numerical variables include:

* Price
* Mileage
* Engine Volume
* Year

Categorical variables include:

* Car
* Body
* Engine Type
* Registration
* Model
* Drive

---

## 🧹 Data Cleaning & Preprocessing

The following preprocessing steps were performed.

### Duplicate Records

Duplicate records were identified and removed.

```python
CarSales_Data_copy.drop_duplicates(inplace=True)
```

The original dataset contained **113 duplicate rows**.

---

### Missing Values

Missing values were identified in:

* `engV` – 434 missing values
* `drive` – 511 missing values

#### Engine Volume

Missing `engV` values were replaced using the **median engine volume for the corresponding car and body-type group**.

```python
CarSales_Data_copy['engV'] = (
    CarSales_Data_copy
    .groupby(['car', 'body'])['engV']
    .transform(lambda x: x.fillna(x.median()))
)
```

Remaining unresolved missing values were removed.

#### Drive Type

Missing `drive` values were filled using the **most common drive type within the corresponding car and body-type group**.

---

### Invalid Prices

Records where:

```text
price <= 0
```

were removed because they do not represent valid positive selling prices.

---

### Zero Mileage

Zero values in the mileage column were replaced with the median mileage.

```python
b = CarSales_Data_copy["mileage"].median()
CarSales_Data_copy["mileage"] = (
    CarSales_Data_copy["mileage"].replace(0, b)
)
```

---

## 📈 Analysis Questions

The project is designed to investigate the following business and analytical questions:

### 1. Which type of cars are sold the most?

Analyze the distribution of cars by body type and identify the most frequently represented vehicle types.

### 2. What is the relationship between price and mileage?

Study the correlation between vehicle price and mileage using statistical analysis and visualization.

### 3. How many cars are registered?

Analyze the registration status of vehicles and compare registered and non-registered cars.

### 4. How does price differ between registered and non-registered cars?

Compare the price distribution based on registration status.

### 5. How is car price distributed based on engine volume?

Analyze the relationship between engine volume and selling price.

### 6. Which engine type is preferred the most?

Analyze the distribution of:

* Petrol
* Diesel
* Gas
* Other

### 7. What are the correlations between numerical features?

A correlation heatmap can be used to examine relationships between:

* Price
* Mileage
* Engine Volume
* Year

### 8. What is the distribution of car prices?

Analyze the overall price distribution and identify potential outliers and skewness.

---

## 📊 Initial Dataset Findings

Before preprocessing, the dataset contains:

* **9,576 car records**
* **10 features**
* **113 duplicate records**
* **434 missing engine-volume values**
* **511 missing drive-type values**

The most frequently represented:

* **Car brand:** Volkswagen
* **Body type:** Sedan
* **Engine type:** Petrol
* **Drive type:** Front
* **Registration status:** Yes

These values are based on the uploaded dataset.

---

## 📌 Key Data Quality Observations

The dataset contains several data-quality issues that required preprocessing:

1. Duplicate records
2. Missing engine-volume values
3. Missing drive-type values
4. Zero or invalid prices
5. Zero mileage values
6. Potentially extreme values in numerical columns

For example, the original price column ranges from **0 to 547,800**, indicating that price requires validation before analysis.

---

## 📉 Correlation Analysis

The initial dataset shows the following correlations with price:

| Feature       | Correlation with Price |
| ------------- | ---------------------: |
| Mileage       |                  -0.31 |
| Year          |                   0.37 |
| Engine Volume |                   0.05 |

These correlations provide an initial indication of relationships but should not be interpreted as causal relationships.

---

## 🧠 Project Learning Outcomes

Through this project, I practiced:

* Loading Excel data using Pandas
* Understanding dataset structure
* Data profiling
* Detecting duplicate records
* Handling missing values
* Group-based imputation
* Removing invalid records
* Replacing zero values
* Descriptive statistics
* Correlation analysis
* Data visualization
* Exploratory Data Analysis using Python
* Converting raw data into analysis-ready data

---

## 📂 Project Structure

```text
Car-Sales-EDA/
│
├── Car_Sales.xlsx
├── EDAcarsales-checkpoint.ipynb
└── README.md
```

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
```

### 2. Install required libraries

```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

If using Pandas Profiling, install the compatible profiling package/environment required by your notebook.

### 3. Open the Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
EDAcarsales-checkpoint.ipynb
```

### 4. Keep the dataset in the same folder

Make sure:

```text
Car_Sales.xlsx
```

is available in the project directory so that the notebook can load the data.

---

## 📌 Conclusion

This project demonstrates a structured approach to **Exploratory Data Analysis using Python**. The raw car-sales dataset was inspected, profiled, cleaned, and prepared for further analysis.

The project provides a foundation for understanding how factors such as **brand, body type, mileage, engine volume, engine type, registration, year, and drive type** can be explored in relation to used-car sales.

---

## 👨‍💻 Author

**Sarthak Bawankule**

Aspiring **Data Analyst | Python | SQL | Power BI | Excel | Generative AI**

---

## ⭐ If you found this project useful

Feel free to ⭐ star the repository and explore the notebook for the complete analysis workflow.
