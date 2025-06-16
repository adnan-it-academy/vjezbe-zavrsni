# 🛠️ Automatski ETL proces u Pythonu
**Modularna struktura za studente (sa MSSQL bazom)**

## 📌 Uvod
ETL proces (Extract – Transform – Load) je osnovni korak u radu s podacima. 
Ovdje prikazujemo kako napraviti automatizovan, modularan ETL sistem koristeći Python i MSSQL bazu podataka.

---

## 📁 Struktura projekta

```
etl_project/
├── data/                          # Ulazni CSV fajl
├── main.py                        # Ulazna tačka koja pokreće ETL proces
├── requirements.txt               # Biblioteke potrebne za rad
└── src/
    ├── __init__.py
    ├── extract/
    │   └── extractor.py           # Učitavanje podataka
    ├── transform/
    │   └── transformer.py         # Čišćenje i obrada podataka
    └── load/
        └── loader.py              # Ubacivanje u MSSQL bazu
```

---

## 🧩 Korak 1: EXTRACT – Učitavanje podataka

```python
import pandas as pd

def load_dataset(path: str) -> pd.DataFrame:
    df = pd.read_csv(path)
    print(f"Loaded {len(df)} rows and {len(df.columns)} columns.")
    return df
```

> Dataset treba biti smješten u folder `data/`, npr. `students_performance.csv`.

---

## 🧪 Korak 2: TRANSFORM – Čišćenje i priprema podataka

```python
def clean_dataset(df):
    df = df.drop_duplicates()
    df = df.fillna(0)
    return df
```

Moguće dodatne transformacije:
- Encoding kategorijalnih vrijednosti
- Formatiranje datuma
- Skaliranje numeričkih vrijednosti

---

## 🗄️ Korak 3: LOAD – Slanje u MSSQL bazu

```python
from sqlalchemy import create_engine

def load_to_mssql(df, table_name, connection_string):
    engine = create_engine(connection_string)
    df.to_sql(table_name, con=engine, if_exists='replace', index=False)
    print(f"Data loaded to table: {table_name}")
```

🔐 Primjer konekcijskog stringa:

```
mssql+pyodbc://USERNAME:PASSWORD@HOSTNAME/DATABASENAME?driver=ODBC+Driver+17+for+SQL+Server
```

---

## ▶️ main.py

```python
from src.extract.extractor import load_dataset
from src.transform.transformer import clean_dataset
from src.load.loader import load_to_mssql

dataset_path = "data/students_performance.csv"
table_name = "students"
connection_string = "mssql+pyodbc://USERNAME:PASSWORD@HOSTNAME/DBNAME?driver=ODBC+Driver+17+for+SQL+Server"

df = load_dataset(dataset_path)
df_clean = clean_dataset(df)
load_to_mssql(df_clean, table_name, connection_string)
```

---

## 📦 requirements.txt

```
pandas
sqlalchemy
pyodbc
```

Instalacija:
```
pip install -r requirements.txt
```

---

## 📈 Zaključak

Ova struktura omogućava:
- Automatizaciju ETL procesa
- Modularnost koda
- Spremnost za nadogradnju i profesionalnu upotrebu

---

## 🧪 Primjer za testiranje

Dataset: [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)  
Fajl: `students_performance.csv` staviti u `data/` folder.

Pokretanje:
```
python main.py
```
