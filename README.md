# Data Analysis Using Python and Seaborn

## Overview
This Python script is designed to perform exploratory data analysis (EDA) on a sales dataset. It includes data cleaning, statistical descriptions, and visualizations of both continuous and categorical variables. The code utilizes libraries like `pandas` and `seaborn` to simplify data manipulation and visualization.

## Prerequisites
To run this script, you need the following:
- Python installed (preferably version 3.7 or later)
- Libraries: `pandas`, `seaborn`
- Access to Google Colab (optional but recommended for seamless execution)
- Sales dataset (CSV file) located in your Google Drive

## Steps to Execute

### 1. Mount Google Drive
The script begins by mounting Google Drive to access the dataset:
```python
from google.colab import drive
drive.mount('/content/drive')
```

### 2. Load the Dataset
The dataset is loaded into a pandas DataFrame:
```python
df = pd.read_csv('/content/drive/MyDrive/cognizant Forage /Dataset Task1 /sample_sales_data.csv')
```
The `Unnamed: 0` column is dropped for clarity:
```python
df.drop(columns=['Unnamed: 0'], inplace=True)
```

### 3. Data Overview
The following operations provide an overview of the data:
- `df.head()` displays the first five rows.
- `df.describe(include='all')` gives a statistical summary.
- `df.columns` lists the column names.
- `df.isnull()` and `df.isnull().sum()` check for missing values.
- `df.dtypes` shows the data types of each column.

### 4. Continuous Variable Distribution
The `plot_continuous_distribution` function visualizes the distribution of continuous variables using Seaborn's KDE plots:
```python
def plot_continuous_distribution(data: pd.DataFrame = None, column: str = None, height: int = 8):
    _ = sns.displot(data, x=column, kde=True, height=height, aspect=height/5).set(title=f'Distribution of {column}');
```
Example usage:
```python
plot_continuous_distribution(df, 'unit_price')
plot_continuous_distribution(df, 'quantity')
plot_continuous_distribution(df, 'total')
```

### 5. Unique Value Analysis
The `get_unique_values` function identifies unique values in categorical columns and provides their counts:
```python
def get_unique_values(data, column):
    num_unique_values = len(data[column].unique())
    value_counts = data[column].value_counts()
    print(f"Column: {column} has {num_unique_values} unique values\n")
    print(value_counts)
```
Example usage:
```python
get_unique_values(df, 'category')
get_unique_values(df, 'customer_type')
get_unique_values(df, 'payment_type')
```

### 6. Categorical Variable Distribution
The `plot_categorical_distribution` function visualizes the distribution of categorical variables:
```python
def plot_categorical_distribution(data: pd.DataFrame = None, column: str = None, height: int = 8, aspect: int = 2):
    _ = sns.catplot(data=data, x=column, kind='count', height=height, aspect=aspect).set(title=f'Distribution of {column}');
```
Example usage:
```python
plot_categorical_distribution(df, 'category')
plot_categorical_distribution(df, 'customer_type')
plot_categorical_distribution(df, 'payment_type')
```

Additional visualizations for categorical data:
```python
sns.countplot(df, y='category').set(title=f'Distribution of Category')
```

### 7. Correlation Heatmap
The `correlation_plot` function visualizes the correlation matrix using Seaborn's heatmap:
```python
def correlation_plot(data: pd.DataFrame = None):
    corr = data.corr()
    sns.heatmap(corr, annot=True, cmap='coolwarm').set(title='Correlation Heatmap');
```
Example usage:
```python
correlation_plot(df)
```

---

## Output
The script generates:
1. KDE plots for continuous variables like `unit_price`, `quantity`, and `total`.
2. Bar plots for categorical variables like `category`, `customer_type`, and `payment_type`.
3. A heatmap showing correlations among numeric variables.

## Customization
You can replace the dataset path and columns with your own data. Additionally, adjust the visualization parameters like `height` and `aspect` for better aesthetics.

## Acknowledgements
This script was developed for exploratory data analysis, leveraging Python's powerful data manipulation and visualization libraries.

--- 
