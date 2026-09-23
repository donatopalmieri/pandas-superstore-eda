# 📊 US Superstore EDA & Customer Analytics (Pandas Project)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Business Overview

Questo progetto offre un'analisi esplorativa dei dati (**Exploratory Data Analysis - EDA**) e una segmentazione avanzata su un dataset aziendale di **Retail/E-Commerce (US Superstore)** contenente 9.800 transazioni.

L'obiettivo principale è trasformare i dati grezzi in **Business Insights** azionabili per ottimizzare la gestione della base clienti, l'efficienza della logistica di spedizione, le strategie per categoria di prodotto e l'identificazione di anomalie nelle vendite.

---

## 📂 Project Structure

```text
pandas-superstore-eda/
│
├── data/
│   ├── Sample-Superstore.csv       # Dataset grezzo originale (9.800 righe)
│   ├── superstore_cleaned.csv      # Dataset pulito ed elaborato dopo il NB 01
│   ├── monthly_sales_pivot.csv     # Pivot table vendite mensili dal NB 02
│   └── customer_rfm_segments.csv   # Risultati segmentazione RFM dal NB 05
│
├── notebooks/
│   ├── 01_data_cleaning.md         # Cleaning, gestione nulli Postal Code e Feature Engineering
│   ├── 02_sales_time_trends.md     # Trend temporali, stagionalità Q4 e crescita YoY/MoM
│   ├── 03_product_basket.md        # Categorie, Basket Size e Cross-Selling (Co-occurrence)
│   ├── 04_geo_outliers.md          # Analisi geografica, Media vs Mediana e Outlier IQR
│   └── 05_customer_rfm_cohort.md   # Segmentazione RFM e Heatmap Retention Rate di Coorte
│
├── .gitignore                      # File e cartelle escluse dal controllo versione
├── README.md                       # Documentazione completa del progetto
└── requirements.txt                # Dipendenze Python necessarie
```

---

## 🔍 Detailed Notebook Workflow & Methodologies

Il progetto si articola in **5 notebook modulari e sequenziali**, sviluppati con **Pandas**, **NumPy**, **Matplotlib** e **Seaborn**:

### 🧹 Notebook 01: Data Cleaning & Feature Engineering
* **Data Hygiene:** Conversione delle colonne `Order Date` e `Ship Date` in formato `datetime`.
* **Imputazione Mancanti:** Gestione dei valori nulli in `Postal Code` imputando il valore corretto per la città di Burlington, VT (`05401`) e formattazione a 5 cifre.
* **Feature Engineering:** Calcolo della colonna `Shipping Days` (differenza in giorni tra spedizione e ordine), estrazione di componenti temporali (`Year`, `Month`, `DayOfWeek`, `YearMonth`) e stima del prezzo unitario.

### 📈 Notebook 02: Sales & Time Trends Analysis
* **Andamento Storico:** Resampling mensile ed annuale per valutare la traiettoria di crescita dei ricavi.
* **Stagionalità:** Analisi della concentrazione delle vendite con evidenza dei picchi durante l'ultimo trimestre dell'anno (**Q4 / Black Friday / Festività**).
* **Metrics:** Calcolo della crescita percentuale Anno su Anno (**YoY Growth**) e Mese su Mese (**MoM Growth**) con `.pct_change()`.
* **Logistica:** Valutazione dell'efficienza e dei tempi medi/mediani di elaborazione per ciascun `Ship Mode`.

### 🛒 Notebook 03: Product Category & Basket Size Analysis
* **Performance Categorie:** Aggregazione e calcolo della quota di fatturato (*Sales Share %*) per le diverse `Sub-Category`.
* **Product Ranking:** Identificazione dei Top 10 e Bottom 10 prodotti per volume di affari.
* **Basket Size Analysis:** Valutazione del numero medio di articoli e del valore medio per ciascun `Order ID`.
* **Cross-Selling / Co-occurrence:** Costruzione della matrice binaria di acquisto e della matrice di co-occorrenza per identificare le sotto-categorie acquistate più frequentemente insieme.

### 🗺️ Notebook 04: Geographic & Outlier Analysis
* **Analisi Territoriale:** Confronto tra **Media** e **Mediana** del valore degli ordini per Stato e Città per identificare asimmetrie nella distribuzione delle vendite.
* **Outlier Detection (Metodo IQR):** Calcolo delle soglie di normalità tramite l'intervallo interquartile ($IQR = Q3 - Q1$).
* **Business Impact:** Misurazione dell'impatto economico degli ordini "outlier" (valore superiore a $Q3 + 1.5 \times IQR$) sul fatturato complessivo dell'azienda.

### 👥 Notebook 05: Customer RFM Segmentation & Cohort Analysis
* **Metriche RFM:** Calcolo di **Recency** (giorni dall'ultimo ordine), **Frequency** (ordini unici) e **Monetary** (spesa totale) per ciascuno dei clienti unici.
* **Scoring e Segmentazione:** Assegnazione di punteggi da 1 a 4 tramite quantili (`pd.qcut`) e profilazione dei clienti in cluster d'azione (*Champions, Loyal Customers, Promising, At Risk, Can't Lose Them, Lost*).
* **Cohort Retention Rate:** Raggruppamento dei clienti in coorti mensili in base alla data del loro primo acquisto e tracciamento dell'attività nei mesi successivi ($M_0, M_1, M_2, \dots$) tramite tabelle pivot e **Heatmap di Retention**.

---

## 🛠️ Tech Stack & Requirements

* **Python** (v3.10+)
* **Pandas** (Data Manipulation & Time Series analysis)
* **NumPy** (Vectorized operations & matrix dot-products)
* **Matplotlib & Seaborn** (Data Visualization & Heatmaps)
* **Jupyter Notebook** (Interactive Execution Environment)

Per installare l'ambiente e le dipendenze:

```bash
pip install -r requirements.txt
```

---

## 🚀 Quickstart Guide

1. **Clonare il repository:**
   ```bash
   git clone https://github.com/donatopalmieri/pandas-superstore-eda.git
   cd pandas-superstore-eda
   ```

2. **Creare e attivare un ambiente virtuale:**
   ```bash
   python -m venv venv
   # Su macOS/Linux:
   source venv/bin/activate
   # Su Windows:
   venv\Scripts\activate
   ```

3. **Installare i requisiti:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Avviare Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```
   *Eseguire i notebook all'interno della cartella `notebooks/` rispettando l'ordine numerico da `01` a `05`.*

---

## 💡 Key Business Takeaways

* **Stagionalità marcata:** Il Q4 genera costantemente la percentuale maggiore dei ricavi annuali.
* **Segmentazione RFM:** Un numero ridotto di clienti raggruppati come *Champions* e *Loyal Customers* rappresenta la maggior parte del margine aziendale.
* **Asimmetria delle Vendite:** L'analisi degli outlier tramite IQR evidenzia come la media sia fortemente influenzata da grandi ordini aziendali sporadicamente effettuati da alcuni clienti chiave.

---

## 🤝 Author & License

Sviluppato come progetto di portfolio per Data Analysis & Data Science in Pandas.

* **GitHub:** [@donatopalmieri](https://github.com/donatopalmieri)
* **License:** MIT
