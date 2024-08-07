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
continent_pop = data_cleaned.groupby('Continent')['Population (2024)'].sum().reset_index()

fig = px.pie(
    continent_pop,
    names='Continent',
    values='Population (2024)',
    title='Distribution of Continents',
    labels={'Population (2024)': 'Population'}
)

fig.show()
```
![obraz](https://github.com/user-attachments/assets/572cf675-3a2d-4e5f-8f9c-22670bad18ff)


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

```python
plt.figure(figsize=(10,6))
sns.barplot(data=data_cleaned, x='Continent', y='Growth Rate')
plt.title('Average growth rate by continent')
plt.show()
```
![obraz](https://github.com/user-attachments/assets/224164dd-bc22-45df-a95f-737efef360ae)

```python
Top 10 Countries with Highest Average Growth Rate

average_growth_rate = data_cleaned.groupby('Country')['Growth Rate'].mean().reset_index()
average_growth_rate_sorted = average_growth_rate.sort_values(by='Growth Rate', ascending=False)
top_10_countries = average_growth_rate_sorted.head(10)

# Tworzenie wykresu słupkowego
plt.figure(figsize=(12, 8))
sns.barplot(data=top_10_countries, x='Growth Rate', y='Country', palette='viridis')

plt.title('Top 10 Countries with Highest Average Growth Rate')
plt.xlabel('Average Growth Rate')
plt.ylabel('Country')

plt.show()
```
![obraz](https://github.com/user-attachments/assets/950a5238-bf9a-459a-bfd0-3d5c34ce0e28)

```python
Top 10 Cities with Highest Average Growth Rate
average_growth_rate_city = data_cleaned.groupby('City')['Growth Rate'].mean().reset_index()
average_growth_rate_city_sorted = average_growth_rate_city.sort_values(by='Growth Rate', ascending=False)

top_10_cities = average_growth_rate_city_sorted.head(10)

plt.figure(figsize=(12, 8))
sns.barplot(data=top_10_cities, x='Growth Rate', y='City', hue='City', palette='viridis', dodge=False)

plt.title('Top 10 Cities with Highest Average Growth Rate')
plt.xlabel('Average Growth Rate')
plt.ylabel('City')
plt.show()
```
![obraz](https://github.com/user-attachments/assets/9300f73b-1f96-466c-8c36-15b444d57833)

```python
average_growth_rate_country = data_cleaned.groupby('Country')['Growth Rate'].mean().reset_index()
average_growth_rate_country_sorted = average_growth_rate_country.sort_values(by='Growth Rate', ascending=True)
bottom_10_countries = average_growth_rate_country_sorted.head(10)


plt.figure(figsize=(12, 8))
sns.barplot(data=bottom_10_countries, x='Growth Rate', y='Country', hue='Country', palette='coolwarm', dodge=False)

plt.title('Bottom 10 Countries with Lowest Average Growth Rate')
plt.xlabel('Average Growth Rate')
plt.ylabel('Country')
plt.show()
```
![obraz](https://github.com/user-attachments/assets/2526a984-173e-4a3a-ad36-b0b1a6c6f671)

```python
average_growth_rate_city = data_cleaned.groupby('City')['Growth Rate'].mean().reset_index()
average_growth_rate_city_sorted = average_growth_rate_city.sort_values(by='Growth Rate', ascending=True)
bottom_10_cites = average_growth_rate_city_sorted.head(10)


plt.figure(figsize=(12, 8))
sns.barplot(data=bottom_10_cites, x='Growth Rate', y='City', hue='City', palette='coolwarm', dodge=False)


plt.title('Bottom 10 Cites with Lowest Average Growth Rate')
plt.xlabel('Average Growth Rate')
plt.ylabel('City')

plt.show()
```
![obraz](https://github.com/user-attachments/assets/1be14fca-08d0-4722-a454-d6664e2a6e5d)

```python
coor
correlation_matrix = data_cleaned[['Population (2024)', 'Population (2023)', 'Growth Rate']].corr()
print(correlation_matrix)

plt.figure(figsize=(10, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()
```

![corr_matrix](https://github.com/user-attachments/assets/83156f7a-f474-4c2a-b02c-707a00dbbd14)

Zrób jeszcze 10 miast z najwyższą i najniższą populacją

