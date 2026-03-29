# Real Estate Investment Analysis — Île-de-France

## Overview

This project provides a data pipeline and analytical tool designed to identify high-potential real estate investment opportunities in Île-de-France.

It combines transaction data (DVF), rental estimates, and geographic indicators to compute key investment metrics such as price per square meter and rental yield.

---

## Objective

The goal is to transform raw, heterogeneous real estate datasets into a clean and enriched dataset that can be used to:

- Evaluate investment opportunities
- Compare geographic areas
- Identify high-yield properties
- Support data-driven decision making

---

## Data Sources

The project integrates multiple public datasets:

- DVF (Demandes de Valeurs Foncières) — real estate transactions
- Rental data (€/m² estimates)
- INSEE geographic data (urban areas, postal codes)

Raw data is stored in `data/raw/` and processed into analytical datasets in `data/processed/`.

---

## Data Pipeline

The data pipeline is implemented in `src/data/prepare_dataset.py`.

### Main steps

1. **Data ingestion**
   - Loading DVF and auxiliary datasets
   - Handling encoding and format inconsistencies

2. **Data cleaning**
   - Type conversion (numeric, datetime)
   - Missing values filtering
   - Domain-based constraints (surface, price ranges)

3. **Outlier detection**
   - IQR-based filtering (per department)
   - Quantile trimming (1%–99%)

4. **Feature engineering**
   - Price per m²
   - Property categorization (T1–T5+)
   - Geographic segmentation (Paris / Petite / Grande couronne)

5. **Data enrichment**
   - Merge with rental data
   - Compute investment indicators

6. **Output**
   - Clean dataset exported in Parquet format

---

## Key Features

- Robust outlier detection combining statistical methods and business rules
- Multi-source data integration
- Scalable processing using pandas
- Structured pipeline separated from notebooks
- Reproducible data preparation workflow

---

## Project Structure

```text
├── data/
│ ├── raw/
│ ├── interim/
│ └── processed/
├── notebooks/
│ └── app/
├── src/
│ ├── data/
│ ├── features/
│ ├── visualization/
│ └── utils/
├── reports/
├── config/
├── tests/
├── main.py
├── requirements.txt

```
---

## Installation

```bash
git clone https://github.com/kenzi0228/real-estate-investment-analysis.git
cd real-estate-investment-analysis

python -m venv venv
venv\Scripts\activate

pip install -r requirements.txt
```
## Usage
Run data pipeline
```bash 
python src/data/prepare_dataset.py
```
Launch analysis dashboard
```bash
jupyter notebook notebooks/app/dashboard_app.ipynb
```
## Outputs

The pipeline produces:

- Cleaned transaction dataset (Parquet)
- Aggregated rental data
- Enriched dataset ready for analysis

Key computed metrics include:

- Price per m²
- Estimated rental yield
- Geographic segmentation indicators

## Limitations
- Rental data is aggregated and may lack fine-grained precision
- Accessibility data is only partially integrated
- No predictive modeling is included (descriptive analytics only)

## Future Work
- Add machine learning models for price prediction
- Integrate geospatial analysis (GeoPandas)
- Develop a web application (Streamlit)
- Automate pipeline execution (Airflow / Prefect)

## Author

Mohamed Kenzi Lali
Engineering student in Data Science / Data Engineering