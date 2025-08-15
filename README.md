# 📊 Slowly Changing Dimension (SCD) Type II with PySpark

This project demonstrates the implementation of **Slowly Changing Dimension (SCD) Type II** using PySpark.  
Two approaches are provided:
1. **With Spark SQL**
2. **Without Spark SQL** (using PySpark DataFrame APIs)

SCD Type II is used in data warehousing to preserve the full history of changes in dimension tables by adding new rows instead of updating existing ones.

---

## 📁 Project Files

| File Name | Description |
|-----------|-------------|
| `SCD_TYPE_II_With_Spark_SQL.ipynb` | Implementation of SCD Type II using **Spark SQL** queries |
| `SCD_TYPE_II_Without_Spark_SQL.ipynb` | Implementation of SCD Type II using **PySpark DataFrame APIs** |
| `customer.csv` | Existing customer dataset (historical data) |
| `newcustomer.csv` | New incoming customer dataset (incremental data) |

---

## 🛠 Prerequisites

Before running the project, make sure you have:

- **Python 3.8+**
- **Java 8 or higher**
- **Apache Spark 3.x**
- **PySpark**
- Jupyter Notebook / JupyterLab

You can install PySpark with:
```bash
pip install pyspark
```

---

## 🚀 How to Run

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/ikrlalit/SCD-Type-II.git
cd SCD-Type-II
```

### 2️⃣ Open Jupyter Notebook
```bash
jupyter notebook
```

### 3️⃣ Open and Run the Notebooks
- **Option 1**: Open `SCD_TYPE_II_With_Spark_SQL.ipynb` and run all cells.
- **Option 2**: Open `SCD_TYPE_II_Without_Spark_SQL.ipynb` and run all cells.

Both notebooks will:
1. Load `customer.csv` and `newcustomer.csv`
2. Compare old and new records
3. Insert updated records as new rows
4. Mark old records as inactive with an end date

---

## 📊 Sample Data

### `customer.csv` (Existing data)
| cust_id | name    | city     | start_date | end_date   | flag |
|---------|--------|----------|------------|------------|------|
| 1       | John   | New York | 2021-01-01 | 9999-12-31 | Y    |
| 2       | Alice  | Chicago  | 2021-03-15 | 9999-12-31 | Y    |

### `newcustomer.csv` (Incoming data)
| cust_id | name    | city      |
|---------|--------|-----------|
| 1       | John   | Boston    |
| 3       | David  | New York  |

---

## 📜 Output Example

After running SCD Type II, you'll get:
| cust_id | name    | city     | start_date | end_date   | flag |
|---------|--------|----------|------------|------------|------|
| 1       | John   | New York | 2021-01-01 | 2023-08-15 | N    |
| 1       | John   | Boston   | 2023-08-15 | 9999-12-31 | Y    |
| 2       | Alice  | Chicago  | 2021-03-15 | 9999-12-31 | Y    |
| 3       | David  | New York | 2023-08-15 | 9999-12-31 | Y    |

---

## 🧠 Key Concepts

- **Type II SCD** keeps history by:
  - Adding a new row for the updated record
  - Expiring the old record by setting an **end date** and changing the active flag
- **Effective Date Ranges** track when each version of the record is valid
- **Flag** column (Y/N) indicates the current active record

---

## 📌 Author
**Lalit Kumar**  
💼 Python Developer | Data Engineering Enthusiast | Machine Learning

---
