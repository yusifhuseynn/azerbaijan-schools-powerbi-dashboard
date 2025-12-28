📖 README.md (FULL)
markdown# 📊 Computerized Schools in Azerbaijan | Power BI Dashboard

> **Interactive Power BI dashboard** reflecting the growth dynamics of computerized schools in the Azerbaijani education system over the **9-year** (2016-2024) period.

---

## 🎯 About the Project

This project, based on the statistics of the Ministry of Education of Azerbaijan:
- **Distribution of schools by 14 economic-geographical regions**
- **Comparison of urban and rural** schools
- **Year-over-Year Growth**
- **9-year trend** analysis
- **Visualizes regional inequalities**

### 📈 Key Findings
- 📊 **Overall growth:** +4.7% (4158 → 4352 schools)
- 🏙️ **Urban schools:** 28.9% (1257 schools)
- 🏘️ **Rural schools:** 71.1% (3095 schools)
- 🥇 **Leading region:** Lankaran-Astara (542 schools)
- 📅 **Last year (2024):** +0.5% growth

---

## 🖼️ Dashboard View

### 1. Home
![Dashboard Preview](screenshots/main_dashboard.png)

### 2. Trend Analysis
![Trend Chart](screenshots/trend_chart.png)

### 3. Regional Distribution
![Regional Map](screenshots/regional_distribution.png)

### 4. Heat Map
![Heatmap](screenshots/heatmap.png)

---

## 🛠️ Technologies

| Technology | Purpose |
|------------|----------------|
| ![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white) | Data preparation and preprocessing |
| ![Pandas](https://img.shields.io/badge/-Pandas-150458?logo=pandas&logoColor=white) | Data manipulation and transformation |
| ![Power BI](https://img.shields.io/badge/-Power%20BI-F2C811?logo=powerbi&logoColor=black) | Dashboard development
| ![Power Query](https://img.shields.io/badge/-Power%20Query-217346?logo=microsoft&logoColor=white) | Data cleaning and shaping
| ![DAX](https://img.shields.io/badge/-DAX-FF6C37) | Calculated measures and KPIs
| ![Excel](https://img.shields.io/badge/-Excel-217346?logo=microsoft-excel&logoColor=white) | Primary data source |

---

## 📂 Project Structure
azerbaijan-schools-powerbi-dashboard/
│
├── data/
│ ├── raw/ # Raw data files
│ │ └── schools_data_2016_2024.xlsx
│ ├── processed/ # Cleaned data
│ │ └── schools_cleaned.csv
│ └── coordinates/ # Region coordinates
│ └── region_coordinates.csv
│
├── scripts/
│ ├── data_preprocessing.py # Python data preparation script
│ ├── coordinate_mapping.py # Coordinate addition
│ └── requirements.txt # Python dependencies
│
├── powerbi/
│ ├── Azerbaijan_Schools_Dashboard.pbix # Power BI file
│ └── dax_measures.txt # DAX formulas
│
├── screenshots/ # Dashboard screenshots
│ ├── main_dashboard.png
│ ├── trend_chart.png
│ ├── regional_distribution.png
│ └── heatmap.png
│
├── docs/
│ ├── METHODOLOGY.md # Methodology
│ ├── DATA_SOURCES.md # Data sources
│ └── TECHNICAL_GUIDE.md # Technical guide
│
├── README.md # This file
├── README_EN.md # English version
├── LICENSE # MIT License
└── .gitignore

---

## 🚀 Installation and Usage

### Requirements
- **Power BI Desktop** (latest version)
- **Python 3.8+** (for data preprocessing)
- **Git**

### Step 1: Clone the Repository
```bash
git clone https://github.com/[username]/azerbaijan-schools-powerbi-dashboard.git
cd azerbaijan-schools-powerbi-dashboard
```

### Step 2: Install Python dependencies
```bash
pip install -r scripts/requirements.txt
```

### Step 3: Data preprocessing
```bash
python scripts/data_preprocessing.py
```

### Step 4: Open Power BI Dashboard
```bash
# Open with Power BI Desktop:
powerbi/Azerbaijan_Schools_Dashboard.pbix
```

---

## 📊 Dashboard Elements

### 1. **KPI Cards** (3 pcs)
- ✅ Total number of schools
- ✅ Urban schools (by percentage)
- ✅ Rural schools (by percentage)
- ✅ Growth percentages compared to the previous year (↑↓)

### 2. **Line Chart** - Dynamics by Years
- 3 lines: General, Urban, Rural
- 2016-2024 trend analysis
- Interactive tooltips

### 3. **Stacked Column Chart** - Urban/Rural Comparison
- Stacked comparison by year
- Change in ratio

### 4. **Clustered Bar Chart** - Regions
- Horizontal bars by 14 regions
- Sorted from highest to lowest
- Conditional formatting (color gradient)

### 5. **Heatmap (Matrix)** - Heat Map
- Region × Year matrix
- Color intensity (yellow → red)
- Values ​​on hover

### 6. **Interactive Slicer**
- Year filter (2016-2024)
- Cross-filtering affects all visuals

- ## 🔧 Technical Details

### Power Query Transformations
1. **Date format correction:** `01.01.2024` → `2024` (integer)
2. **Null handling:** Checking for null values
3. **Data type optimization:** Text → Whole Number
4. **Pivot transformation:** Structuring regional data

### DAX Measures

#### Growth percentage over the previous year:
```dax
Growth_Percentage =
VAR SelectedYear = SELECTEDVALUE('Data'[Year_Number])
VAR CurrentValue = SUM('Data'[Total_Schools])
VAR PreviousValue =
CALCULATE(
SUM('Data'[Total_Schools]),
'Data'[Year_Number] = SelectedYear - 1
)
RETURN
IF(
ISBLANK(PreviousValue) || PreviousValue = 0,
BLANK(),
DIVIDE(CurrentValue - PreviousValue, PreviousValue) * 100
)
```

#### City Percentage:
```dax
City_Percentage =
DIVIDE(
SUM('Data'[City_Schools]),
SUM('Data'[Total_Schools]),
0
) * 100
```

### Python Data Processing

**Basic Operations:**
```python
import pandas as pd

# Data Loading
df = pd.read_excel('data/raw/schools_data.xlsx')

# Year Column Conversion
df['Year_Number'] = pd.to_datetime(df['Year']).dt.year

# Region Name Standardization
region_mapping = {
'Lankaran': 'Lankaran-Astara',
'Ganja': 'Ganja-Dashkasan',
# ...
}
df['Region_Standard'] = df['Region'].map(region_mapping)

# Coordinate Addition to be
coordinates = pd.read_csv('data/coordinates/region_coordinates.csv')
df = df.merge(coordinates, on='Region_Standard')

# Export
df.to_csv('data/processed/schools_cleaned.csv', index=False)
```

---

## 📈 Data Sources

- **Main source:** Statistics of the Ministry of Education of Azerbaijan
- **Period:** 2016-2024
- **Frequency:** Annual
- **Coverage:** 14 economic-geographical regions
- **Last update:** December 2024

### Regions:
1. Baku city
2. Absheron-Khizi
3. Mountainous Shirvan
4. Ganja-Dashkan
5. Lankaran-Astara
6. Guba-Khachmaz
7. Sheki-Zagatala
8. Shirvan-Salyan
9. Mil-Mugan
10. Central-Aran
11. Karabakh
12. Gazakh-Tovuz
13. Eastern Zangezur
14. Nakhchivan Autonomous Republic

---

## 💡 Key Learnings

Techniques and methods used in this project:

✅ **Time-series analysis** - Trend analysis by years
✅ **YoY growth calculation** - Comparison with the previous year
✅ **Geospatial visualization** - Coordinate-based mapping
✅ **Conditional formatting** - Color-based visualization
✅ **DAX time intelligence** - Time-based calculations
✅ **Power Query M** - Data transformation
✅ **Cross-filtering** - Interactive filter system

---
