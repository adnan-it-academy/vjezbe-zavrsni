# 🛠️ Python Data & ML Projekat: ETL + Detaljna Analiza podataka

**Modularna struktura za studente – uključuje MSSQL i Jupyter/Pandas analizu**

---

## 📌 Uvod

Ovaj projekat prikazuje kompletan tok obrade podataka: od učitavanja i čišćenja (ETL), preko čuvanja u SQL bazu, do detaljne analize i vizualizacije koristeći Pandas, Matplotlib i Seaborn. Namijenjen je studentima koji žele razumjeti punu obradu podatka i pripremu za mašinsko učenje.

---

## 📁 Struktura projekta

```
AI_project/
├── data/                          # Ulazni CSV fajl
├── etl/                           # ETL moduli (extract, transform, load)
│   ├── extract/
│   │   └── extractor.py
│   ├── transform/
│   │   └── transformer.py
│   └── load/
│       └── loader.py
├── analysis/                      # Analiza podataka (Jupyter notebook + pomoćni moduli)
│   ├── eda.ipynb                  # Exploratory Data Analysis u Jupyteru
│   └── summary.py                 # Tekstualni izvještaji i helper funkcije
├── requirements.txt              # Potrebne biblioteke
├── main.py                        # Pokretanje ETL procesa
└── README.md                      # Objašnjenje projekta
```

---

## ✅ ETL MODUL (kratki podsjetnik)

ETL proces se nalazi u `etl/` direktoriju i sadrži tri osnovna koraka:

- `extractor.py`: učitavanje CSV podataka
- `transformer.py`: čišćenje i priprema
- `loader.py`: slanje u MSSQL bazu

---

## 📊 MODUL ZA ANALIZU PODATAKA

### 📁 Lokacija: `analysis/eda.ipynb`

U ovom Jupyter notebook-u vrši se **Exploratory Data Analysis (EDA)** – proces gdje otkrivamo osnovne obrasce, odnose među kolonama i statističke karakteristike podataka.

### ✅ Koraci analize:

#### 1. Učitavanje podataka
```python
import pandas as pd
df = pd.read_csv("../data/students_performance.csv")
```

#### 2. Osnovne statistike i pregled
```python
df.info()
df.describe()
df.isnull().sum()
df.nunique()
```

> Cilj: razumjeti strukturu podataka, identifikovati tipove kolona, nedostajuće i jedinstvene vrijednosti.

---

#### 3. Grupisanje i agregacije
```python
df.groupby("gender")["math score"].mean()
df.pivot_table(index="lunch", columns="gender", values="reading score", aggfunc="median")
```

> Cilj: pronaći razlike između grupa (npr. po spolu, vrsti ručka, obrazovanju roditelja).

---

#### 4. Vizualizacije
Vizualizacije pomažu u prepoznavanju obrazaca i outliera.

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Histogram
df['math score'].hist()

# Boxplot
sns.boxplot(x="gender", y="writing score", data=df)

# Scatter plot
sns.scatterplot(x="reading score", y="writing score", hue="gender", data=df)

# Heatmap za korelacije
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="coolwarm")
```

📌 **Minimum:** 6 različitih grafova (histogram, boxplot, scatter, bar, pie, heatmap)

---

#### 5. Analiza outliera
```python
sns.boxplot(data=df[['math score', 'reading score', 'writing score']])
```

> Cilj: pronaći vrijednosti koje značajno odstupaju – mogu biti greške, ali i važne poslovne informacije.

---

#### 6. Korelacijska analiza
```python
correlation_matrix = df.corr(numeric_only=True)
sns.heatmap(correlation_matrix, annot=True, cmap="Blues")
```

> Cilj: otkriti koje varijable su najviše povezane – npr. veza između čitanja i pisanja.

---

## 🧠 summary.py

Ovaj pomoćni fajl sadrži funkcije za:
- automatsko izvlačenje top uvida (npr. najbolja grupa, najveće odstupanje),
- tekstualni summary o datumu, broju redova, tipovima kolona itd.
- statističke metrike (mod, medijan, standardna devijacija)

---

## 🧾 requirements.txt

```
pandas
sqlalchemy
pyodbc
matplotlib
seaborn
notebook
```

Instalacija:
```bash
pip install -r requirements.txt
```

---

## 🧪 Primjer testiranja

**Dataset:** [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)  
**Smještaj:** `data/students_performance.csv`

### Pokretanje ETL procesa:
```bash
python main.py
```

### Pokretanje analize:
```bash
jupyter notebook analysis/eda.ipynb
```

---

## ✅ Zaključak

Modularna struktura projekta omogućava:
- odvojeno i pregledno izvođenje svake faze (ETL, EDA, ML),
- upotrebu realnih alata i tehnologija (SQL, Pandas, vizualizacija),
- lakšu evaluaciju, saradnju u timu i profesionalni razvoj.

