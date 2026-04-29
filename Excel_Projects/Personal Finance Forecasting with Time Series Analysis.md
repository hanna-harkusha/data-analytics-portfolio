# Personal Finance Forecasting with Time Series Analysis 📈

### Objective 🤔
To collect, analyze, visualize, and forecast financial expenses using time series methods.  
The project combines personal finance data with open USDA food expenditure data to explore spending dynamics, identify trends and seasonality, and compare forecasting models for short-term financial prediction.

### Tools & Methods ⚙️
- **Python** – data preparation, time series modeling, forecasting, and evaluation
- **Pandas / NumPy** – data cleaning, transformation, and aggregation
- **Matplotlib / Seaborn** – data visualization and trend analysis
- **ARIMA** – forecasting personal monthly expenses
- **SARIMA** – seasonal forecasting based on open USDA data
- **ETS** – exponential smoothing model for comparison with SARIMA
- **MAE / RMSE** – model accuracy evaluation
- **Google Sheets / Excel** – personal finance tracking and initial data structure

### Data Description 📋

#### Personal Finance Data
- **Source:** Manually collected personal expense records
- **Period:** July 2023 – March 2025
- **Frequency:** Monthly
- **Main categories:** Food expenses and restaurant expenses
- **Target variable:** Total monthly expenses
- **Purpose:** Forecast personal spending for the next six months using ARIMA

#### Open USDA Data
- **Source:** USDA Food Expenditure Series
- **Period:** 1997–2023
- **Frequency:** Monthly
- **Number of observations:** 324
- **Target variable:** Total nominal U.S. food sales with taxes and tips
- **Purpose:** Demonstrate seasonal forecasting using SARIMA and ETS models

### Project Workflow 🔍
1. Collected and structured personal financial data.
2. Aggregated expenses by month and prepared the data for time series analysis.
3. Visualized monthly spending dynamics.
4. Built an ARIMA model for personal expense forecasting.
5. Used USDA open data to analyze a longer seasonal time series.
6. Built and compared SARIMA and ETS models.
7. Evaluated forecasting accuracy using MAE and RMSE.
8. Selected the best-performing model based on test results.

### Results 📈

#### Personal Finance Forecasting
- Built an **ARIMA(0,1,1)** model for monthly personal expense forecasting.
- Generated a six-month forecast for future food and restaurant expenses.
- The model showed acceptable accuracy for medium-term personal budget planning:
  - **MAE:** 1451.14 UAH
  - **RMSE:** 1676.34 UAH

#### Seasonal Forecasting with USDA Data
- Built and compared **SARIMA** and **ETS** models using monthly USDA food expenditure data.
- SARIMA captured seasonal and trend components more effectively.
- SARIMA showed better forecasting accuracy than ETS:
  - **SARIMA MAE:** 3.93
  - **SARIMA RMSE:** 4.59
  - **ETS MAE:** 6.10
  - **ETS RMSE:** 7.17

### Key Insights 💡
- Even a relatively short personal financial history can be used to build a practical forecasting model.
- Personal data was suitable for ARIMA, but not long enough for reliable seasonal modeling.
- Open USDA data provided enough observations to test seasonal forecasting methods.
- SARIMA performed better than ETS on the USDA dataset and was selected as the stronger model for seasonal forecasting.
- Combining personal and open data allows analysis at both individual and macroeconomic levels.

### Files 📂(https://drive.google.com/drive/folders/1YKY8rH1bOs0bElRixeI8H6Adv99Vl9Bc?usp=drive_link)


### Example Visualizations 🖼️

<img width="1515" height="670" alt="image" src="https://github.com/user-attachments/assets/9614b50d-f48c-4023-94e1-0631c7742077" />
<img width="1015" height="536" alt="image" src="https://github.com/user-attachments/assets/35bd4bfd-77cf-4d31-bd50-6067d7297848" />
<img width="1255" height="529" alt="image" src="https://github.com/user-attachments/assets/ca9dd069-1966-4ea6-af0d-f20098741b79" />
<img width="1335" height="631" alt="image" src="https://github.com/user-attachments/assets/6436d129-e9e3-476f-967d-1f86c12f9bb6" />
<img width="1438" height="613" alt="image" src="https://github.com/user-attachments/assets/96a33131-4952-4785-b2ba-b8bdd50cc6be" />
<img width="1391" height="630" alt="image" src="https://github.com/user-attachments/assets/047a98db-bc76-46fe-940a-d29356e7216b" />

