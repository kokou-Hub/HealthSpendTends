# Global Health Spending Analysis

### Introduction

The Global Health Spending Analysis project aims to investigate trends and patterns in health expenditures across different countries and regions. The analysis is conducted using a Jupyter notebook, "Global Health Spending Analysis.ipynb," which contains detailed steps and code implementations for each stage of the analysis.

### Steps Taken

1. **Data Loading**:
   - The dataset is loaded using pandas for data manipulation.

    ```python
    import pandas as pd

    # Load the dataset
    data = pd.read_csv('path_to_your_dataset.csv')
    ```

2. **Data Cleaning**:
   - Data cleaning is performed to handle missing values, remove duplicates, and correct any inconsistencies.

    ```python
    # Handle missing values
    data.fillna(method='ffill', inplace=True)

    # Remove duplicates
    data.drop_duplicates(inplace=True)

    # Standardize column names
    data.columns = [col.strip().lower().replace(' ', '_') for col in data.columns]
    ```

3. **Exploratory Data Analysis (EDA)**:
   - Summary statistics and visualizations are created to understand the data distribution and identify patterns.

    ```python
    import matplotlib.pyplot as plt

    # Summary statistics
    print(data.describe())

    # Distribution plot
    plt.hist(data['health_expenditure'])
    plt.title('Distribution of Health Expenditure')
    plt.xlabel('Expenditure')
    plt.ylabel('Frequency')
    plt.show()
    ```

4. **Data Transformation**:
   - Data is transformed to create new features and normalize existing ones for better analysis.

    ```python
    # Create per capita expenditure
    data['per_capita_expenditure'] = data['total_expenditure'] / data['population']

    # Normalize expenditure data
    data['normalized_expenditure'] = (data['health_expenditure'] - data['health_expenditure'].mean()) / data['health_expenditure'].std()
    ```

5. **Visualization**:
   - Various plots are generated to visualize the data and uncover trends and patterns.

    ```python
    # Bar chart of average health expenditure by region
    avg_expenditure_by_region = data.groupby('region')['health_expenditure'].mean()
    avg_expenditure_by_region.plot(kind='bar')
    plt.title('Average Health Expenditure by Region')
    plt.xlabel('Region')
    plt.ylabel('Average Expenditure')
    plt.show()
    ```

6. **Statistical Analysis**:
   - Statistical models and tests are applied to draw inferences from the data.

    ```python
    import statsmodels.api as sm

    # Linear regression model
    X = data[['per_capita_income']]
    y = data['health_expenditure']
    X = sm.add_constant(X)  # Adds a constant term to the predictor
    model = sm.OLS(y, X).fit()
    print(model.summary())
    ```

7. **Results and Interpretation**:
   - The results are presented and interpreted, highlighting key findings and their implications for global health spending.


### Conclusion

The Global Health Spending Analysis provides valuable insights into health expenditure patterns worldwide. By following the detailed steps in the notebook, users can reproduce the analysis and explore the data further to inform policy decisions and improve health outcomes.

