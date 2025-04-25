# COVID-19 Pilot Analysis Project: Bangladesh & India (Jan–Jun 2020)
 ![Python](https://img.shields.io/badge/-Python-3670A0?style=flat-square&logo=python&logoColor=white)
  ![Data Analysis](https://img.shields.io/badge/-Data_Analysis-teal?style=flat-square)



  <img src="https://github.com/almazid82/COVID19-Pilot-Analysis-Ban-vs-Ind-/blob/main/Screenshot_20250424-202036~2.png?raw=true" width="600" alt="COVID-19 Comparison Chart" />
</p>

![ Covid 19 ( Ban vs Ind) dataset analysis](https://github.com/almazid82/COVID19-Pilot-Analysis-Ban-vs-Ind-/blob/main/pilot_covid_data_bangladesh_india.csv)



## :mag_right: Uncovering Early Pandemic Patterns in South Asia

In early 2020, COVID-19 began to spread rapidly across the globe. Governments were scrambling to understand the virus, track its movement, and respond effectively. This project zooms in on two densely populated South Asian countries — **Bangladesh** and **India** — to understand how the pandemic unfolded during its initial phase (January–June 2020).

By performing a focused **Exploratory Data Analysis (EDA)** using **Python** and **SQL**, this pilot lays the foundation for future large-scale and AI-driven epidemic monitoring systems.

---

## :bar_chart: Objectives of This Pilot Study

- Conduct a country-specific pilot analysis using a global dataset.
- Identify early trends in infections and deaths across **Bangladesh** and **India**.
- Compare key metrics using both SQL and Python-based methods.
- Visualize outbreak dynamics and mortality patterns.
- Prepare a reusable template for future global or regional analyses.

---

## :floppy_disk: Dataset Information

- **Dataset Source:** [Our World in Data (OWID)](https://covid.ourworldindata.org/data/owid-covid-data.csv)  
- **Filtered for:** Bangladesh & India  
- **Date Range:** January to June 2020  
- **Key Variables:**
  - `date`, `location`, `new_cases`, `total_cases`
  - `new_deaths`, `total_deaths`, `population`



---

## :snake: Python-Based Analysis with explanation (scripts/covid_analysis_python.ipynb)

- Filtering and comparing country-wise case growth
- Monthly average new cases and deaths
- Time-series visualization using `Matplotlib` and `Seaborn`
- Anomaly detection and pattern observation

---

```python
# 1. Total Cases in Bangladesh (as of June 2020)
import pandas as pd

df = pd.read_csv("covid_data.csv")
bd_total_cases = df[df['location'] == 'Bangladesh']['total_cases'].max()
print("Total Cases in Bangladesh:", bd_total_cases)
```

**Explanation:**  
এই কোডটি pandas দিয়ে CSV ডেটাসেট লোড করে এবং বাংলাদেশের সর্বোচ্চ মোট কেস বের করে। SQL এর প্রথম কোয়েরির মতোই কাজ করে, তবে Python দিয়ে।  
**Expected Output (example):**  
`Total Cases in Bangladesh: 47153`

---

```python
# 2. Average New Cases in India (May 2020)
india_may = df[(df['location'] == 'India') & 
               (df['date'] >= '2020-05-01') & 
               (df['date'] <= '2020-05-31')]
avg_new_cases = india_may['new_cases'].mean()
print("Average New Cases in India (May 2020):", avg_new_cases)
```

**Explanation:**  
এই অংশে India-র মে ২০২০ সালের নতুন কেস গুলো ফিল্টার করে তাদের গড় হিসাব করা হয়েছে। এটা SQL এর দ্বিতীয় কোয়েরির মতো।  
**Expected Output (example):**  
`Average New Cases in India (May 2020): 6360.84`

---

```python
# 3. Total Deaths per 100,000 Population
df_grouped = df.groupby('location').agg({
    'total_deaths': 'max',
    'population': 'max'
})
df_grouped['deaths_per_100k'] = df_grouped['total_deaths'] * 100000 / df_grouped['population']
print(df_grouped[['deaths_per_100k']].head())
```

**Explanation:**  
এই অংশে প্রতিটি দেশের জন্য সর্বোচ্চ মৃত্যু সংখ্যা এবং জনসংখ্যা নিয়ে ১ লাখ জনে কতজন মারা গেছে তার হার বের করা হয়েছে। SQL এর তৃতীয় কোয়েরির মতোই কাজ করে।  
**Expected Output (example):**

| location   | deaths_per_100k |
|------------|------------------|
| Bangladesh | 0.83             |
| India      | 1.91             |
| ...        | ...              |


## :floppy_disk: SQL-Based Analysis (scripts/sql_queries.sql)



## Sample SQL Queries with Explanation

```sql
-- 1. Total Cases in Bangladesh (as of June 2020)
SELECT MAX(total_cases) AS total_cases_bangladesh
FROM covid_data
WHERE location = 'Bangladesh';
```

**Explanation:**  
এই কোয়েরিটি বাংলাদেশের সর্বোচ্চ মোট কেস (total_cases) কত ছিল সেটা বের করে দিবে। যেহেতু ডেটা আপডেটেড থাকে, তাই সর্বশেষ তারিখ অনুযায়ী সর্বোচ্চ সংখ্যাটি পাওয়া যাবে।  
**Expected Output (example):**  
| total_cases_bangladesh |
|------------------------|
| 47153                  |

---

```sql
-- 2. Average New Cases in India (May 2020)
SELECT AVG(new_cases) AS avg_new_cases_may
FROM covid_data
WHERE location = 'India'
  AND date BETWEEN '2020-05-01' AND '2020-05-31';
```

**Explanation:**  
এই কোয়েরিটি ২০২০ সালের মে মাসে ভারতের দৈনিক গড় নতুন কেস (average new cases) বের করে। এটি সময়ভিত্তিক বিশ্লেষণে সহায়ক।  
**Expected Output (example):**  
| avg_new_cases_may |
|-------------------|
| 6360.84           |

---

```sql
-- 3. Total Deaths per 100,000 Population
SELECT location,
       MAX(total_deaths) * 100000.0 / MAX(population) AS deaths_per_100k
FROM covid_data
GROUP BY location;
```

**Explanation:**  
এই কোয়েরিটি প্রতিটি দেশের প্রতি ১ লাখ জনসংখ্যায় মোট মৃত্যুর সংখ্যা কত সেটি বের করে। জনসংখ্যা অনুপাতে মৃত্যুর হারের তুলনা করতে খুবই কার্যকর।  
**Expected Output (example):**  
| location   | deaths_per_100k |
|------------|------------------|
| Bangladesh | 0.83             |
| India      | 1.91             |
| ...        | ...              |






---
## Data Visualization

```python
import matplotlib.pyplot as plt

# 1. Daily New Cases in Bangladesh (May–June 2020)
bd_cases = df[(df['location'] == 'Bangladesh') & 
              (df['date'] >= '2020-05-01') & 
              (df['date'] <= '2020-06-30')]

plt.figure(figsize=(10,5))
plt.plot(bd_cases['date'], bd_cases['new_cases'], label='New Cases')
plt.xticks(rotation=45)
plt.title('Daily New COVID-19 Cases in Bangladesh (May–June 2020)')
plt.xlabel('Date')
plt.ylabel('New Cases')
plt.legend()
plt.tight_layout()
plt.show()
```

**Explanation:**  
এই visualization টি বাংলাদেশে মে থেকে জুন পর্যন্ত নতুন কেসের দৈনিক প্রবণতা দেখায়। সময় অনুযায়ী ট্রেন্ড বোঝার জন্য খুব কার্যকর।

---

## Key Insights

- **Bangladesh:** মে ও জুনে দৈনিক কেস বৃদ্ধি পেয়েছে, তবে জুনের শেষদিকে কিছুটা স্থিরতা লক্ষ্য করা যায়।
- **India:** মে মাসে গড় দৈনিক কেস ছিল ৬ হাজারের বেশি, যা সেসময়ের জন্য গুরুত্বপূর্ণ public health concern ছিল।
- **Mortality Rate:** বেশিরভাগ দেশে প্রতি ১ লাখ জনসংখ্যায় মৃত্যুর হার কম থাকলেও কিছু দেশে তা তুলনামূলকভাবে বেশি।

---

## Future Scope / Applicability

- **AI-driven Alert System:** এমন ডেটার উপর ভিত্তি করে future outbreaks শনাক্ত করতে predictive AI মডেল বানানো যেতে পারে।
- **Bangladesh Context:** স্বাস্থ্য মন্ত্রণালয় চাইলে AI ভিত্তিক local outbreak tracking system তৈরি করতে পারে যা সময়মতো hotspot ধরতে পারবে।
- **Policy Making:** এই ডেটা এনালাইসিস policymaker দের জন্য গুরুত্বপূর্ণ সিদ্ধান্ত নেয়ার ভিত্তি হিসেবে কাজ করতে পারে (যেমন, কোন জেলায় আগে lockdown প্রযোজ্য)।

---

## Repository Structure

```
├── data/
│   └── covid_data.csv
├── notebooks/
│   └── pilot_analysis.ipynb
├── README.md
└── requirements.txt
```

---

## How to Run

1. Clone the repo  
   `git clone https://github.com/yourusername/covid19-pilot-analysis.git`

2. Install dependencies  
   `pip install -r requirements.txt`

3. Run the notebook  
   Open `pilot_analysis.ipynb` in Jupyter or VS Code.

---

## Author

- **Your Name:** [Shamsul Al Mazid]
- **Project:** COVID-19 Pilot Data Analysis (Bangladesh & India)


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

___


## 🔗 Related Projects
- [Global Temperature HeatMap Analysis](https://github.com/almazid82/HeatMap-Understanding-Global-Temperature-Anomalies)


---



## ⭐ Feedback
If you like this project or have suggestions, feel free to star the repo or open an issue. Your feedback is valuable!




---

:scroll: License

MIT License – free to use and modify with attribution.

---
## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![SQL](https://img.shields.io/badge/SQL-005C84?style=for-the-badge&logo=sqlite&logoColor=white)
![Power BI](https://img.shields.io/badge/PowerBI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Visual Studio](https://img.shields.io/badge/Visual%20Studio-5C2D91?style=for-the-badge&logo=visual%20studio&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![Microsoft 365](https://img.shields.io/badge/Microsoft_365-D83B01?style=for-the-badge&logo=microsoft&logoColor=white)
![Google Workspace](https://img.shields.io/badge/Google_Workspace-4285F4?style=for-the-badge&logo=google&logoColor=white)
