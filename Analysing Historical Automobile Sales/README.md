
# Automobile Sales Analysis During Recession Periods

This project explores historical automobile sales data to identify trends and patterns during recession and non-recession periods. The analysis includes visualizations using line plots, bar charts, pie charts, scatter plots, and maps.

## Dataset Description

The dataset includes the following variables:
- **Date**: Observation date.
- **Recession**: Binary indicator (1: recession, 0: normal period).
- **Automobile_Sales**: Number of vehicles sold.
- **GDP**: Per capita GDP value (USD).
- **Unemployment_Rate**: Monthly unemployment rate.
- **Consumer_Confidence**: Synthetic consumer confidence index.
- **Seasonality_Weight**: Seasonality effect on sales.
- **Price**: Average vehicle price.
- **Advertising_Expenditure**: Company's advertising cost.
- **Vehicle_Type**: Type of vehicles sold.
- **Competition**: Market competition metric.
- **Month**/**Year**: Extracted from the Date column.

## Visualizations Included

![Yearly sales trends with recession indicators](Automobile Sales.png)
![Sales trends by vehicle type during recession periods](Sales by vehicle type.png)
![Comparison of sales between recession and non-recession](Average sales during Recession and Non Recession.png)
![Comparison of sales between recession and non-recession, Vehicle-Wise](Vehicle Wise.png)
![GDP variation during recession vs. non-recession periods](GDP trend.png)
![Bubble plots for seasonal impact on sales](Seasonality Impact.png)
![Correlation between consumer confidence, price, and sales](Consumer Confidence Vs Sales.png)
![Relationship between average vehicle price and automobile sales](Price Vs Sales.png)
![Advertising expenditure analysis](Advertising Expenditure.png)
![Advertising expenditure analysis based on vehicle type](Vehicle Type Wise.png)
![Effect of unemployment rate on sales](Unemployment Rate vs Sales.png)
![Map of top-performing sales regions during recessions](Sales During Recession.png)

## Getting Started

1. Clone the repository or download the notebook.
2. Install required packages:
   ```bash
   pip install pandas matplotlib seaborn folium
   ```
3. Run the `Scenario_polished.ipynb` notebook.

## Sample Visualizations

![Yearly Sales Trend](images/yearly_sales.png)
![Vehicle Type Sales Comparison](images/vehicle_type_comparison.png)
![GDP Trends](images/gdp_trends.png)
![Seasonality Bubble Chart](images/seasonality_bubble.png)

> Replace the placeholder image paths with actual screenshots from your notebook output.

## License

This project is part of the IBM Data Visualization course and is for educational purposes.
