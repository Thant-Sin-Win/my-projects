# 📊 Automobile Sales Statistics Dashboard

This project is an interactive **Dash web application** for visualizing and analyzing historical automobile sales data, focusing on two key perspectives:

- **Yearly Statistics**
- **Recession Period Statistics**

It enables users to explore trends, patterns, and relationships between economic factors and automobile sales through interactive plots.

---

## 🔧 Features

- Dropdown menu to select report type:
  - `Yearly Statistics`
  - `Recession Period Statistics`
- Year selection enabled only for Yearly Statistics
- Interactive visualizations built with **Plotly**:
  - Line charts
  - Bar charts
  - Pie charts
- Dynamic rendering of graphs based on user input

---

## 📂 Files Included

| File                                  | Description                                                  |
|---------------------------------------|--------------------------------------------------------------|
| `Automobile_Sales_Statistics_Interactive_Dashboard.py` | Main Python script for Dash app                             |
| `dashboard_explained.ipynb`          | Jupyter Notebook with explanation and annotated code         |
| `README.md`                           | Project documentation and usage guide                        |

---

## 🗃️ Dataset

The dataset is loaded directly from a public cloud URL: https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DV0101EN-SkillsNetwork/Data%20Files/historical_automobile_sales.csv


The dataset contains monthly data with the following features:

| Feature | Description |
|--------|-------------|
| `Date` | Timestamp of the observation |
| `Recession` | 1 if recession, 0 otherwise |
| `Automobile_Sales` | Number of vehicles sold |
| `GDP` | Per capita GDP in USD |
| `Unemployment_Rate` | Monthly unemployment percentage |
| `Consumer_Confidence` | Index reflecting consumer sentiment |
| `Seasonality_Weight` | Impact of seasonality on sales |
| `Price` | Average price of vehicles |
| `Advertising_Expenditure` | Total ad spend by the company |
| `Vehicle_Type` | Vehicle category |
| `Competition` | Level of market competition |
| `Month`, `Year` | Extracted from `Date` |

---

## 📉 Recession Periods Considered

- **1980**
- **1981–1982**
- **1991**
- **2000–2001**
- **Late 2007 to mid-2009**
- **Sep–Dec 2020 (COVID-19)**

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Thant-Sin-Win/my-projects.git
cd my-projects/Automobile\Sales\Statistics\Interactive\Dashboard

2. Install dependencies

You can use pip to install required libraries:
pip install dash pandas plotly

3. Run the app

python Automobile_Sales_Statistics_Interactive_Dashboard.py
Open your browser and navigate to:
http://127.0.0.1:8050/

🧠 Insights You Can Discover
How recession impacts average automobile sales

Vehicle types most affected during economic downturns

Seasonal trends in monthly sales

Influence of advertising and unemployment on consumer behavior

📘 Jupyter Notebook
Refer to dashboard_explained.ipynb for:

Annotated code

Markdown commentary

Logical breakdown of callback functions and plots

🧑‍💻 Author
Thant Sin Win

📄 License
This project is part of IBM Data Analyst Professional Course and is for educational purposes.
