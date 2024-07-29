# Global Health Spending Analysis

## Introduction

This project aims to analyze global healthcare resource allocation by examining health expenditure data. The analysis provides insights into how countries allocate resources to health, trends over time, and comparisons between countries. The data used in this analysis comes from reputable sources such as the World Health Organization (WHO) and the OECD Health Expenditure Database.

import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px

# Data Loading
csv_file_path = 'path/to/your/health_expenditure_data.csv'
df = pd.read_csv(csv_file_path)

# Data Cleaning
missing_values = df.isnull().sum()
print("Missing Values:\n", missing_values)
df_cleaned = df.fillna(df.mean())

# Data Description
basic_stats = df_cleaned['Value'].describe()
print(basic_stats)

# Data Visualization
plt.hist(df_cleaned['Value'], bins=50)
plt.title('Distribution of Health Expenditure')
plt.xlabel('Health Expenditure')
plt.ylabel('Frequency')
plt.show()

# Trend Analysis
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

# Country Comparison
average_expenditure = df_cleaned.groupby('Country')['Value'].mean()
top_5_countries = average_expenditure.nlargest(5)
print("Top 5 Countries with Highest Average Health Expenditure:\n", top_5_countries)

# Interactive Dashboard
fig = px.line(df_selected, x='Year', y='Value', color='Country', title='Health Expenditure Over Time')
fig.show()

