# 🚗 Automobile Sales Trend Analysis During Recession Periods

This project analyzes historical automobile sales data in the United States, focusing on how various **recession periods** have impacted the automotive industry. The analysis includes visualizations comparing key metrics such as sales trends, GDP, unemployment, pricing, advertising, and consumer confidence.

---

## 📁 Dataset Overview

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

## 📊 Visualizations Included

### Yearly sales trends with recession indicators
![Yearly sales trends with recession indicators](images/Automobile%20Sales.png)

### Sales trends by vehicle type during recession periods
![Sales trends by vehicle type during recession periods](images/Sales%20by%20vehicle%20type.png)

### Comparison of sales between recession and non-recession
![Comparison of sales between recession and non-recession](images/Average%20sales%20during%20Recession%20and%20Non%20Recession.png)

### Comparison of vehicle-wise sales in both periods
![Comparison of sales between recession and non-recession, Vehicle-Wise](images/Vehicle%20Wise.png)

### GDP variation during recession vs. non-recession periods
![GDP variation during recession vs. non-recession periods](images/GDP%20trend.png)

### Bubble plot: seasonality impact on sales
![Bubble plots for seasonal impact on sales](images/Seasonality%20Impact.png)

### Consumer confidence vs sales (scatter plot)
![Correlation between consumer confidence, price, and sales](images/Consumer%20Confidence%20Vs%20Sales.png)

### Vehicle price vs sales (scatter plot)
![Relationship between average vehicle price and automobile sales](images/Price%20Vs%20Sales.png)

### Ad expenditure: recession vs non-recession
![Advertising expenditure analysis](images/Advertising%20Expenditure.png)

### Ad expenditure by vehicle type (recession only)
![Advertising expenditure analysis based on vehicle type](images/Vehicle%20Type%20Wise.png)

### Unemployment rate vs sales by vehicle type
![Effect of unemployment rate on sales](images/Unemployment%20Rate%20vs%20Sales.png)

### Map of top-performing regions during recession
![Map of top-performing sales regions during recessions](images/Sales%20During%20Recession.png)

---

## 🛠️ How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/Thant-Sin-Win/my-projects.git
   cd my-projects/Analysing\ Historical\ Automobile\ Sales

2. Install required packages:

pip install pandas matplotlib seaborn folium

3. Open and run the notebook:

Analysing Historical Automobile Sales.ipynb

📌 Insights Summary
Sports cars are highly sensitive to economic downturns.

Supermini and executive cars face sales drops in recessions.

Advertising and consumer sentiment are key influencers.

Unemployment rate inversely affects sports and luxury models.

🧑‍💻 Author
Thant Sin Win

📧 xeyzo.leo@gmail.com

🌐 https://www.linkedin.com/in/thant-sin-win/
