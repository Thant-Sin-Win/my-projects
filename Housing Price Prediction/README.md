
# House Price Prediction Project

This project performs data analysis and builds regression models to predict house prices based on various features.

## 🔍 Objective

To explore the dataset, visualize important relationships, and develop linear and polynomial regression models to predict house prices.

## Dataset

The dataset is sourced from a public housing dataset containing features such as:

- Square footage
- Number of bedrooms
- Number of bathrooms
- Presence of waterfront view
- Floors
- Year built
- Renovation details
- Latitude and Longitude
- Property grade
- and more...

## Workflow

1. **Data Cleaning**: Handle missing values and drop irrelevant columns.
2. **Exploratory Data Analysis**: Visualize relationships using seaborn and matplotlib.
3. **Feature Engineering**: Select and transform features.
4. **Model Training**:
   - Linear Regression
   - Polynomial Regression
   - Ridge Regression
5. **Model Evaluation**: Use R² score and train-test split evaluation.

## 📊 Exploratory Data Analysis

### 1. Price Distribution for House With/ Without Waterfront View
![Waterfront View vs Price](Images/Price%20Distribution%20for%20house.png)

- Houses with a **waterfront view (1)** tend to have significantly **higher prices** than those without.
- The boxplot shows higher median and maximum prices for waterfront houses.

### 2. Regression Plot: sqft_above vs price
![sqft_above vs price](Images/Regression%20Plot.png)

- There is a **positive linear relationship** between the above-ground square footage and house price.
- The regression line indicates that larger houses typically have higher prices.

## 🧠 Model Building & Evaluation

- A **Linear Regression model** was built using selected features and achieved reasonable performance.
- A **Polynomial Ridge Regression model** showed better performance due to its ability to model non-linear patterns and reduce overfitting.

### ✅ Final Result Summary

- **Waterfront view** and **above-ground square footage** are strong indicators of house price.
- The **Polynomial Ridge Regression** provided the highest R² score, indicating it is the best-fit model among those tested.

## How to Run

1. Open the Jupyter Notebook file `Housing_Price_Prediction.ipynb`.
2. Run each cell sequentially.
3. Ensure the required Python libraries are installed: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`.

## Dependencies

- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

👤 Author
Thant Sin Win

📧 xeyzo.leo@gmail.com

🌐 https://www.linkedin.com/in/thant-sin-win/
