# CSV to PostgreSQL Import

This project demonstrates how to import a CSV file into a PostgreSQL database using **Python** and **Pandas**.

---

## 🚀 Steps to Run

### 1. Clone Repository
```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Create Virtual Environment
```bash
python -m venv venv
venv\Scripts\activate   # For Windows
source venv/bin/activate  # For Linux/Mac
```

### 3. Install Dependencies
```bash
pip install pandas psycopg2
```

### 4. Update Database Credentials
Edit the connection details in `main.py`:
```python
conn = psycopg2.connect(
    dbname="test_mining",
    user="test_mining",
    password="your_password",
    host="127.0.0.1",
    port="5432"
)
```

### 5. Run the Script
```bash
python main.py
```

---

## 📂 Project Structure
```
.
├── equipment_metrics1.csv   # Sample CSV file
├── main.py                  # Script to import CSV into PostgreSQL
└── README.md                # Project documentation
```

---

## 🛠️ Example Script (main.py)

```python
import pandas as pd
import psycopg2
from psycopg2 import sql

# Load CSV
csv_file = "equipment_metrics1.csv"
df = pd.read_csv(csv_file, encoding="utf-8")

# Connect to PostgreSQL
conn = psycopg2.connect(
    dbname="test_mining",
    user="test_mining",
    password="your_password",
    host="127.0.0.1",
    port="5432"
)
cur = conn.cursor()

# Create table if not exists
create_table_query = """
CREATE TABLE IF NOT EXISTS equipment_metrics (
    id SERIAL PRIMARY KEY,
    column1 TEXT,
    column2 TEXT,
    column3 TEXT
);
"""
cur.execute(create_table_query)

# Insert data
for _, row in df.iterrows():
    insert_query = sql.SQL("INSERT INTO equipment_metrics (column1, column2, column3) VALUES (%s, %s, %s)")
    cur.execute(insert_query, tuple(row[:3]))

conn.commit()
cur.close()
conn.close()

print("CSV imported successfully into PostgreSQL!")
```

---

## ✅ Output
When the script runs successfully, you will see:
```
CSV imported successfully into PostgreSQL!
```

---

## 📌 Notes
- Make sure PostgreSQL server is running.
- Replace database credentials with your own.
- Modify table schema (`CREATE TABLE`) according to your CSV structure.
