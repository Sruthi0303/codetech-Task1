# codetech-Task1
Name: K SRUTHI

Company: CODETECH IT SOLUTIONS

ID:CT6DS710

Domain: DATA SCIENCE

Duration:June 25th to August 10th,2024

Mentor:Muzammil Ahmed

# Overview of the Project

# Project:Explatory Data Analsis (EDA) on Car Features and MSRP Dataset     

# Objective
The objective of this project is to perform a comprehensive analysis of a car dataset to uncover insights and trends related to various car attributes. By cleaning, preprocessing, and visualizing the data, the project aims to provide a deeper understanding of the dataset and reveal meaningful patterns and relationships.

# Key Activities
 ## 1.Data Loading and Inspection:

 - Load the car dataset from a CSV file into a Pandas DataFrame.
 - Examine the initial rows and column data types to understand the dataset’s structure and content.

 ## 2.Data Cleaning :

 - Column Removal: Eliminate columns that are deemed unnecessary for the analysis, such as Engine Fuel Type, Market Category, Vehicle Style, Popularity, Number of 
   Doors, and Vehicle Size.
 - Column Renaming: Rename columns to more intuitive names for easier reference, including Engine HP to HP, Engine Cylinders to Cylinders, and others.
 - Duplicate Removal: Identify and remove any duplicate rows to ensure data quality.
 - Missing Values Handling: Identify and drop rows with missing values to prepare the data for analysis.
 ## 3.Data Visualization:

- Boxplots: Create boxplots to visualize the distribution of key variables such as Price, HP (Engine Horsepower), and Cylinders.
- Bar Plot: Plot the number of cars by make, highlighting the top 40 makes to understand the distribution of car brands.
- Correlation Heatmap: Generate a heatmap to visualize correlations between numeric variables, aiding in understanding relationships between different attributes.
- Scatter Plot: Plot Engine HP against MSRP (Manufacturer’s Suggested Retail Price) to explore the relationship between these two variables.
# Technology Used
- Pandas: For data manipulation, cleaning, and analysis.
- NumPy: Provides support for numerical operations, indirectly used through Pandas.
- Seaborn: For creating statistical plots and visualizations such as boxplots, heatmaps, and bar plots.
- Matplotlib: For plotting and visualizing data, including scatter plots.
- Python: The programming language used to write the analysis script and perform the data operations.

# Car Data Analysis and Visualization

This project involves cleaning, preprocessing, and visualizing a car dataset to extract meaningful insights. The goal is to understand the data better and uncover patterns through various visualizations.

## Overview

The script performs the following key operations:

1. **Load and Inspect Data**
   - Reads the dataset from a CSV file.
   - Displays the top and bottom 5 rows.
   - Checks the data types of each column.

2. **Data Cleaning**
   - **Drop Columns:** Removes irrelevant columns including `Engine Fuel Type`, `Market Category`, `Vehicle Style`, `Popularity`, `Number of Doors`, and `Vehicle Size`.
   - **Rename Columns:** Simplifies column names for clarity:
     - `Engine HP` to `HP`
     - `Engine Cylinders` to `Cylinders`
     - `Transmission Type` to `Transmission`
     - `Driven_Wheels` to `Drive Mode`
     - `highway MPG` to `MPG-H`
     - `city mpg` to `MPG-C`
     - `MSRP` to `Price`

3. **Data Cleaning and Preparation**
   - **Remove Duplicates:** Identifies and removes duplicate rows.
   - **Handle Missing Values:** Checks for missing values and drops rows with missing values.

4. **Visualizations**
   - **Boxplots:** Visualizes distributions of key variables:
     - `Price`
     - `HP` (Engine Horsepower)
     - `Cylinders` (Number of Engine Cylinders)
   - **Bar Plot:** Displays the number of cars by make, focusing on the top 40 makes.
   - **Correlation Heatmap:** Generates a heatmap to show correlations between numeric variables.
   - **Scatter Plot:** Plots Engine HP against MSRP to explore their relationship.

## Libraries Used

- `pandas` for data manipulation and analysis
- `numpy` for numerical operations
- `seaborn` and `matplotlib` for visualization

## Usage

1. **Ensure the Dataset is Available:**
   - Make sure the dataset file `cardata.csv` is located in the specified path (`/content/cardata.csv`).

2. **Run the Script:**
   - Execute the Python script to perform data analysis and generate visualizations.

## Code

Here is the code used for the analysis:

```python
import pandas as pd
import numpy as np
import seaborn as sns                       
import matplotlib.pyplot as plt             
%matplotlib inline
sns.set(color_codes=True)

# Load the dataset
df = pd.read_csv("/content/cardata.csv")

# Display the top 5 rows and data types
print("Top 5 rows:")
print(df.head(5))

print("\nBottom 5 rows:")
print(df.tail(5))

print("\nData types of each column:")
print(df.dtypes)

# Drop specified columns
df = df.drop(['Engine Fuel Type', 'Market Category', 'Vehicle Style', 'Popularity', 'Number of Doors', 'Vehicle Size'], axis=1)

# Rename columns
df = df.rename(columns={
    "Engine HP": "HP",
    "Engine Cylinders": "Cylinders",
    "Transmission Type": "Transmission",
    "Driven_Wheels": "Drive Mode",
    "highway MPG": "MPG-H",
    "city mpg": "MPG-C",
    "MSRP": "Price"
})

# Check for duplicates
duplicate_rows_df = df[df.duplicated()]
print(f"\nNumber of duplicate rows: {duplicate_rows_df.shape[0]}")

# Drop duplicate rows
df = df.drop_duplicates()

# Check for missing values
print("\nMissing values before dropping:")
print(df.isnull().sum())

# Drop rows with missing values
df = df.dropna()

print("\nMissing values after dropping:")
print(df.isnull().sum())

# Plot boxplots for different features
sns.boxplot(x=df['Price'])
plt.title("Price Distribution")
plt.show()

sns.boxplot(x=df['HP'])
plt.title("HP Distribution")
plt.show()

sns.boxplot(x=df['Cylinders'])
plt.title("Cylinders Distribution")
plt.show()

# Plot number of cars by make
plt.figure(figsize=(10,5))
df['Make'].value_counts().nlargest(40).plot(kind='bar')
plt.title("Number of Cars by Make")
plt.ylabel('Number of Cars')
plt.xlabel('Make')
plt.show()

# Plot correlation heatmap
plt.figure(figsize=(10,5))
c = df.corr(numeric_only=True)
sns.heatmap(c, cmap="BrBG", annot=True)
plt.title("Correlation Heatmap")
plt.show()

# Scatter plot of HP vs Price
plt.figure(figsize=(10,6))
plt.scatter(df['HP'], df['Price'])
plt.xlabel('Engine HP')
plt.ylabel('Price')
plt.title('Scatter Plot of HP vs Price')
plt.show()
