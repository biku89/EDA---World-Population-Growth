# EDA---World-Population-Growth


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import warnings
import os

# Wczytanie danych
file_path = r'C:\Users\biklu\Desktop\Projekty python\World population growth\World population growth rate by cities 2024.csv'
data = pd.read_csv(file_path)

# Wyświetlenie pierwszych kilku wierszy
print(data.head())

        City     Country      Continent  Population (2024)  Population (2023)  Growth Rate
0      Tokyo       Japan           Asia           37115035           37194105      -0.0021
1      Delhi       India           Asia           33807403           32941309       0.0263
2   Shanghai       China           Asia           29867918           29210808       0.0225
3      Dhaka  Bangladesh           Asia           23935652           23209616       0.0313
4  Sao Paulo      Brazil  South America           22806704           22619736       0.0083

data.info()

Data columns (total 6 columns):
 #   Column             Non-Null Count  Dtype
---  ------             --------------  -----
 0   City               801 non-null    object
 1   Country            801 non-null    object
 2   Continent          790 non-null    object
 3   Population (2024)  801 non-null    int64
 4   Population (2023)  801 non-null    int64
 5   Growth Rate        801 non-null    float64
```
```python
miss_value = data.isnull().sum()

print(miss_value)

City                  0
Country               0
Continent            11
Population (2024)     0
Population (2023)     0
Growth Rate           0
dtype: int64

con = data['Continent'].unique()
print(con)

['Asia' 'South America' 'Africa' 'North America' 'Europe' 'Oceana' nan
 'Oceania']

data_cleaned = data.dropna(subset=['Continent'])

initial_row_count = len(data)
cleaned_row_count = len(data_cleaned)

print(f"Number rows before: {initial_row_count}")
print(f"Number rows after: {cleaned_row_count}")

Number rows before: 801
Number rows after: 790
```
```python
data.describe()
Population (2024)  Population (2023)  Growth Rate
count       8.010000e+02       8.010000e+02   801.000000
mean        2.654327e+06       2.604461e+06     0.020051
std         3.723253e+06       3.661201e+06     0.012180
min         7.500360e+05       7.228360e+05    -0.024900
25%         9.909310e+05       9.698040e+05     0.012200
50%         1.379368e+06       1.363510e+06     0.019700
75%         2.570980e+06       2.514077e+06     0.026600
max         3.711504e+07       3.719410e+07     0.058200
```
```python
# Population Growth by Continent
plt.figure(figsize=(10, 6))
sns.boxplot(x='Continent', y='Growth Rate', data=data_cleaned)
plt.title('Population Growth by Continent')
plt.xlabel('Continent')
plt.ylabel('Growth Rate')
plt.show()
```
![obraz](https://github.com/user-attachments/assets/5eacabb0-ea71-440e-a1b5-7d3511e0350d)

