# COVID-19 Pilot Analysis Project: Bangladesh & India (Jan–Jun 2020)

A focused exploratory data analysis (EDA) on COVID-19 data for **Bangladesh** and **India**, using both **Python (Pandas/Matplotlib)** and **SQL**. This pilot aims to lay the groundwork for larger-scale global analysis.

---

## :bar_chart: Project Objectives

- Conduct a pilot analysis using a subset of global COVID-19 data
- Compare COVID-19 trends in Bangladesh and India (new cases, deaths, etc.)
- Practice SQL-based data analysis for scalable applications
- Use Python for visualization and trend analysis
- Build a structured, reusable data science workflow

---

## :file_folder: Folder Structure

COVID19-Pilot-Analysis/ ├── data/ │   └── pilot_covid_data_bangladesh_india.csv ├── scripts/ │   ├── covid_analysis_python.ipynb │   └── sql_queries.sql ├── visuals/ │   └── trend_charts.png ├── README.md └── .gitignore

---

## :bar_chart: Dataset Details

- **Name:** pilot_covid_data_bangladesh_india.csv  
- **Source:** Derived from OWID Global COVID-19 dataset  
- **Time Range:** January to June 2020  
- **Countries:** Bangladesh and India only  
- **Key Columns:**  
  - `date`  
  - `location`  
  - `new_cases`  
  - `new_deaths`  
  - `total_cases`  
  - `total_deaths`  
  - `population`

---

## :snake: Python-Based Analysis (scripts/covid_analysis_python.ipynb)

- Filtering and comparing country-wise case growth
- Monthly average new cases and deaths
- Time-series visualization using `Matplotlib` and `Seaborn`
- Anomaly detection and pattern observation

---

## :floppy_disk: SQL-Based Analysis (scripts/sql_queries.sql)

**Sample SQL Queries:**

1. **Total Cases in Bangladesh (as of June 2020):**
   ```sql
   SELECT MAX(total_cases) AS total_cases_bangladesh
   FROM covid_data
   WHERE location = 'Bangladesh';

2. **Average New Cases in India (May 2020):**
   ```sql
SELECT AVG(new_cases) AS avg_new_cases_may
FROM covid_data
WHERE location = 'India'
  AND date BETWEEN '2020-05-01' AND '2020-05-31';


3. **Total Deaths per 100,000 Population:**
   ```sql
SELECT location,
       MAX(total_deaths) * 100000.0 / MAX(population) AS deaths_per_100k
FROM covid_data
GROUP BY location;




---

:computer: Technologies Used

Language: Python, SQL

Libraries: Pandas, Matplotlib, Seaborn

Database: SQLite / MySQL (for SQL-based queries)

Version Control: Git + GitHub

Tools: Jupyter Notebook, VS Code



---

:clipboard: Future Scope

Expand analysis to global level with all countries

Add machine learning-based forecasting (e.g., ARIMA, Prophet)

Integrate COVID-19 policy and mobility data for deeper insights

Build interactive dashboard (Power BI / Tableau)



---

:handshake: Contributing

This is an open-source educational project. Contributions, improvements, and suggestions are always welcome!


---

:scroll: License

MIT License – free to use and modify with attribution.

---
