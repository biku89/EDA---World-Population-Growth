# EDA---World-Population-Growth
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import warnings

import os

# Podaj pełną ścieżkę do pliku
file_path = r'C:\Users\biklu\Desktop\Projekty python\World population growth\World population growth rate by cities 2024.csv'

# Wczytaj plik CSV do DataFrame
data = pd.read_csv(file_path)

# Wyświetl pierwsze kilka wierszy
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

 ```python
import pandas as pd

# Wczytanie danych
file_path = r'C:\Users\biklu\Desktop\Projekty python\World population growth\World population growth rate by cities 2024.csv'
data = pd.read_csv(file_path)

# Wyświetlenie pierwszych kilku wierszy
print(data.head())
```
