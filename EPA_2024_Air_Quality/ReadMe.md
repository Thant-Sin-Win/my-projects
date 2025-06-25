# 🏙️ Victoria Air Quality Analysis – 2024

This project analyzes hourly air quality data collected across EPA Victoria’s monitoring stations during 2024. Using Python for data preparation and Tableau for interactive visualization, the project highlights trends in pollutants such as PM2.5, PM10, Ozone, and more — helping uncover patterns in air quality across seasons and suburbs.

---

## 📁 Files Included

| File                         | Description                                                                                  |
|------------------------------|----------------------------------------------------------------------------------------------|
| [Original EPA dataset (Excel)](https://data.gov.au/dataset/ds-vic-89c912fe-8bb7-4d35-8190-cda6f02919e5/distribution/dist-vic-23b5d43f-ad8a-457e-9326-ec3b3e8b438d/details?q=) | Link to original EPA dataset (raw hourly readings across all sites) |
| `cleaned_data/clean_air_quality_data.zip` | Compressed CSV of cleaned and pre-processed data ready for visualization           |
| `EPA data.ipynb`             | Jupyter Notebook for data cleaning and preparation                                          |
| `EPA_air_quality.twb`        | Tableau workbook file for interactive dashboard visualization                               |

---

## 🧹 Data Preparation Steps (Python)

Performed using `pandas` in the notebook:
- Parsed datetime columns and extracted hour, weekday, month, and season
- Removed duplicate records
- Applied parameter-specific rules for negative values and direction angles
- Capped extreme outliers (99.9th percentile) for pollutant values
- Exported the cleaned dataset for Tableau visualization

---

## 📊 Interactive Tableau Dashboard

Explore the live dashboard hosted on Tableau Public:  
🔗 [Click here to view the dashboard](https://public.tableau.com/app/profile/thant.sin.win/viz/EPA_Air_Quality_2024/Dashboard1)

### Dashboard Features:
- **📈 Pollution Over Time:** Line chart showing pollutant trends by date
- **📊 Pollution by Location:** Bar chart comparing average pollutant levels by suburb
- **🌡️ Hourly Pollution Patterns:** Heatmap of PM2.5 by hour and weekday
- **🗺️ Station Map:** Geographic distribution of pollutant readings across Victoria

Includes interactive filters for:
- **Parameter name** (e.g., PM2.5, NO₂)
- **Location name** (suburb/station)
- **Season** (summer, autumn, winter, spring)

---

## 🛠️ Tools & Technologies

- **Python 3 (pandas, numpy)**
- **Jupyter Notebook**
- **Tableau Public**
- **EPA Victoria 2024 AirWatch Data**

---

## 📌 Example Insight

> In winter 2024, PM2.5 levels spiked notably on July 31st and August 4th, peaking at 19.24 µg/m³. These values are likely influenced by cold-weather conditions such as stagnant air and wood heater usage. Such insights support better public awareness and planning for seasonal pollution spikes.

---

## 🚀 Possible Future Enhancements

- Integrate local weather data (temperature, wind speed, humidity)
- Predictive modeling for future pollution events
- Add real-time API connections for live monitoring (if available)

---

## 👤 Author

**Thant Sin Win**  
📌 Data Analyst | Python • SQL • Tableau  
🔗 [LinkedIn Profile](https://www.linkedin.com/in/thant-sin-win)

---

## 📄 License

This project is for educational and portfolio use only.  
All source data is publicly provided by **EPA Victoria**.
