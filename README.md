# Global Health Spending Analysis

## Introduction

This project aims to analyze global healthcare resource allocation by examining health expenditure data. The analysis provides insights into how countries allocate resources to health, trends over time, and comparisons between countries. The data used in this analysis comes from reputable sources such as the World Health Organization (WHO) and the OECD Health Expenditure Database.

## Steps Taken

### 1. Data Loading
- Loaded the CSV file containing global health expenditure data into a pandas DataFrame.

```python
import pandas as pd

csv_file_path = 'path/to/your/health_expenditure_data.csv'
df = pd.read_csv(csv_file_path)

### 2. Data Cleaning

# Check for missing values
missing_values = df.isnull().sum()
print("Missing Values:\n", missing_values)

# Handle missing values (example: filling with mean or dropping)
df_cleaned = df.fillna(df.mean())

### 3. Data Decription

# Calculate basic statistics for the 'Value' column (health expenditure)
basic_stats = df_cleaned['Value'].describe()
print(basic_stats)

### 4. Data Visualization

import matplotlib.pyplot as plt

# Histogram of health expenditure
plt.hist(df_cleaned['Value'], bins=50)
plt.title('Distribution of Health Expenditure')
plt.xlabel('Health Expenditure')
plt.ylabel('Frequency')
plt.show()


### 5. Trend Analysis

# Filter data for selected countries and plot trends over time
selected_countries = ['USA', 'Canada', 'Germany']
df_selected = df_cleaned[df_cleaned['Country'].isin(selected_countries)]

for country in selected_countries:
    country_data = df_selected[df_selected['Country'] == country]
    plt.plot(country_data['Year'], country_data['Value'], label=country)

plt.title('Health Expenditure Over Time')
plt.xlabel('Year')
plt.ylabel('Health Expenditure')
plt.legend()
plt.show()

### 6. Country Comparison

# Calculate the average health expenditure for each country
average_expenditure = df_cleaned.groupby('Country')['Value'].mean()
top_5_countries = average_expenditure.nlargest(5)
print("Top 5 Countries with Highest Average Health Expenditure:\n", top_5_countries)

### 7. Interactive Dashboard

import plotly.express as px

# Interactive time series plot using Plotly
fig = px.line(df_selected,


