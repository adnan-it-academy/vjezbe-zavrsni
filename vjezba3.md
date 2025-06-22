# 🛠️ Python Data & ML Projekat: ETL, Analiza i Machine Learning

**Modularna struktura za završni projekat – uključuje MSSQL, Pandas, Jupyter i Scikit-learn**

---

## 📌 Uvod

Ovaj projekat demonstrira potpuni tok rada sa podacima: od učitavanja i čišćenja (ETL), preko skladištenja u SQL bazu, zatim vizualne i statističke analize podataka, pa sve do izgradnje jednostavnog modela mašinskog učenja.

---

## 📁 Struktura projekta

```
zavrsni_projekat/
├── data/                          # Ulazni CSV fajlovi
├── etl/                           # ETL moduli (Extract, Transform, Load)
│   ├── extract/
│   │   └── extractor.py
│   ├── transform/
│   │   └── transformer.py
│   └── load/
│       └── loader.py
├── analysis/                      # Analiza podataka
│   ├── eda.ipynb                  # Exploratory Data Analysis u Jupyteru
│   └── summary.py                 # Helper funkcije za izvještaje
├── ml/                            # Machine Learning modul
│   ├── model.py                   # Trening i evaluacija modela
│   └── train_model.ipynb          # ML Notebook
├── requirements.txt              # Lista biblioteka
├── main.py                        # Glavna ETL skripta
└── README.md                      # Dokumentacija projekta
```

---

## ✅ ETL (Extract – Transform – Load)

ETL proces čisti i priprema podatke za analizu i skladišti ih u MSSQL bazu.

- **extractor.py** – učitava CSV fajl pomoću Pandasa
- **transformer.py** – uklanja duplikate, popunjava prazna polja, formatira kolone
- **loader.py** – šalje obrađene podatke u MSSQL koristeći SQLAlchemy

---

## 📊 Exploratory Data Analysis (EDA)

Notebook `eda.ipynb` koristi biblioteke Pandas, Matplotlib i Seaborn za:

- Opisne statistike (`df.describe()`, `info()`, `value_counts()`)
- Vizualizacije: histogrami, boxplot, heatmap, scatter plot
- Analizu korelacija i outliera
- Grupisanje i pivot tabele

---

## 🤖 Machine Learning – Treniranje i evaluacija modela

Modul `ml/` uključuje kod za treniranje prediktivnog modela korištenjem `scikit-learn`.

### 📁 Lokacije
- `train_model.ipynb` – Notebook koji vodi korisnika kroz cijeli proces modeliranja
- `model.py` – Python skripta sa pomoćnim funkcijama za trening, evaluaciju i vizualizaciju

### ✅ Koraci modeliranja:

#### 1. Odabir ciljne varijable (`target`) i feature-a (`X`)
U zavisnosti od cilja analize, korisnik treba izabrati:
- `target` kolonu koju želi predvidjeti (npr. `"math score"`)
- `X` (sve ostale kolone koje utiču na target)

#### 2. Podjela na trening i test skup
```python
from sklearn.model_selection import train_test_split

X = df.drop(columns=["math score"])
y = df["math score"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

#### 3. Trening modela
```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
```

> Alternativni modeli:
- **Klasifikacija**: `LogisticRegression`, `RandomForestClassifier`
- **Regresija**: `Ridge`, `Lasso`
- **Clustering**: `KMeans`, `DBSCAN`

#### 4. Evaluacija performansi
```python
from sklearn.metrics import mean_squared_error, r2_score

y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"MSE: {mse:.2f}")
print(f"R² Score: {r2:.2f}")
```

#### 5. Vizualizacija predikcija
```python
import matplotlib.pyplot as plt

plt.scatter(y_test, y_pred)
plt.xlabel("Stvarne vrijednosti")
plt.ylabel("Predviđene vrijednosti")
plt.title("Predikcija vs Stvarnost")
plt.grid()
plt.show()
```

#### 6. Sačuvaj model (opcionalno)
```python
import joblib
joblib.dump(model, "ml/trained_model.pkl")
```

---

## 🧠 summary.py

Sadrži pomoćne funkcije za:
- Izračun statističkih metrika
- Sažetak modela i podataka
- Tekstualne interpretacije i automatske preporuke

---

## 🧾 requirements.txt

```
pandas
sqlalchemy
pyodbc
matplotlib
seaborn
notebook
scikit-learn
joblib
```

Instalacija:
```bash
pip install -r requirements.txt
```

---

## ▶️ Pokretanje

1. Postavi dataset u `data/` direktorij (npr. `students_performance.csv`)
2. Pokreni ETL:
```bash
python main.py
```
3. Analiza:
```bash
jupyter notebook analysis/eda.ipynb
```
4. Machine Learning:
```bash
jupyter notebook ml/train_model.ipynb
```

---

## ✅ Zaključak

Ova struktura projekta omogućava:
- **odvojenu obradu podataka** (ETL),
- **vizualnu i statističku analizu** (EDA),
- **treniranje modela** i automatsku evaluaciju (ML),
- fleksibilno proširivanje projekta u pravcu naprednog učenja i proizvodne primjene.

