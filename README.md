# WORLD BILLIONAIRES 2026 PROJECT ANALYTICS
This project aims to analyze over 3,384 billionaires across 80 countries in real time as provided by the Forbe's 2026.  The analysis aims to investigate contributory factors of Billionaires statuses. This is an end to end Data Science Project. It utilizes Jupyter Notebooks fully covering;Exploratory Analysis, Statistical Computation and Predictive Modelling.

## PROJECT OBJECTIVES
- To investigate the distribution of billionaires across te world
- To determine the countries with the most number billionaires with total net worth in USD Billions
- To investigate how gender and age factors contribute to billionaire level statsus
- To investigate which industry dominance are mostly associated with world billionaires
- To investigate distribution of countries having monopoly on industries affect the birth of billionaires per country.
- To investigate how billionaires wealth compares to the average GDP Ratio per country


## OUTLINE OF STEPS TAKEN
With respect to Data Science spectrum, this project is done in a stepwise procedure to ensure all aspects are fully covered

### Understanding the Data Context
The data was firstly investigated to fully understand its context and structure. This included:
- Properly setting up the JupyterNotebook environment by installing ad importing all the necessary libraries.
- Importing the data into the Notebook
- Understanding the data shape (Total number of rows and columns)
- Fully understanding the context of what each column truly represent in the data
- Checking if the data has any duplicates and missing records.
```python
def data_quality_check(df_1):
info_report = {
'shape': df_1.shape,
'total_records': len(df_1),
'missing_records': df_1.isnull().sum(),
'duplicate_rows': df_1.duplicated().sum(),
 }
return info_report

info_report = data_quality_check(df_1)
print(info_report)
## RESULTS: Data has 3384 rows and 25 columns, Total records are 3384, There are NO Duplicate rows. However there are NULLS in some rows in respect to the column names displayed
```

The data was then appropriately cleaned to ensure it is consistent so that the data  findings in the end run are accurate and truly mirror what the data analysis was intendd for.
Some of the procedures done:
- For the rows with mssing values in this case nulls: They were appropriately filled with respect of their data types. Numeric data were filled with their respective average values whereas text data were fillied with "Unknown"
Numeric data:
```python
def filled_null_records(df_1):
fill_nulls = {
'age': df_1['age'].fillna(65.0, inplace=True),
'birth_year' : df_1['birth_year'].fillna(1960.0, inplace=True),
'wealth_per_citizen_usd' : df_1['wealth_per_citizen_usd'].fillna(297.6, inplace=True),
'wealth_gdp_ratio_pct' : df_1['wealth_gdp_ratio_pct'].fillna(0.8, inplace=True),
 }
return fill_nulls
fill_nulls = filled_null_records(df_1) print(fill_nulls)
```
Text data:
```python
def fill_nulls(df_1):
filled_null_cols = {
'state':df_1['state'].fillna('Unknown', inplace=True),
'city':df_1['city'].fillna('Unknown', inplace=True),
 } return filled_null_cols
filled_null_cols = fill_nulls(df_1)
print(filled_null_cols)
```
### Exploratory Data Analysis
After fully understanding the context of our data and apllying all the data cleaning procedures, this phase is where the data was thoroughly investigated further to help answer some questions and  discover more insights.
- Sample Question: For each primary industry, what is the Total and Average Networth in USD Billions among the billionaires? How many billionares belong to each industry? Which are the top 10 primary industry with the highest total net worth?
```python
## Obtain net_worth in USD Billions
df_1['net_worth_usd_b'] = df_1['net_worth_usd_m']/1000
print(df_1['net_worth_usd_b'])

## Define more data metrics so as to allow grouping by the Primary Industry
billionaire_analysis = df_1.groupby('primary_industry').agg(
billionaire_count = ('person_name', 'count'),
total_net_worth = ('net_worth_usd_b', 'sum'),
avg_net_worth = ('net_worth_usd_b', 'mean'),
max_net_worth =('net_worth_usd_b', 'max'),
min_net_worth =('net_worth_usd_b', 'min')).reset_index()

## The Top 10 Primary Industry with Highest Total networth?
top_10_industry = billionaire_analysis.nlargest(10, 'total_net_worth')
top_10_industry
```
  

## TOOLS UTILIZED
- JupyterNotebooks.

## DATA SOURCE
The data was sourced from Kaggle platform : https://www.kaggle.com/datasets/kanchana1990/global-billionaire-wealth-to-gdp-2026.


## DATA FINDINGS
