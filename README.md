# Luxury-Watches-Analysis
Cryptocurrency Prices Analysis: Data Cleaning, Preparation, Analysis, and Interactive Visualization Using Python and Tableau

## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Data Overview](#data-overview)
- [Tools](#tools)
- [Data Cleaning and Analysis](#data-cleaning-and-analysis)
- [Key Findings](#key-findings)
- [Business Insights](#business-insights)
- [Visualization](#visualization)
  
## Project Overview

This project involves analyzing a dataset of luxury watch listings to uncover insights into the market. The dataset contains 14 columns and 284,492 rows, including information about the watch brand, model, price, movement type, case material, year of production, and more. The goal of this analysis was to clean and visualize the data to answer key business questions, such as identifying the most popular brands, the relationship between price and condition, and price distribution across different watch characteristics.

## Data Sources

Source: The dataset used for this analysis is the "Watches.csv" file, found on Kaggle. The final version is "Luxury_Watches_Final.csv".

## Data Overview

The dataset consists of the following columns:

- **index:** Row identifier
- **name:** Name of the watch
- **brand:** Watch brand
- **price:** Price of the watch
- **model:** Model number
- **ref:** Reference number
- **mvmnt:** Type of movement (e.g., automatic, manual)
- **casem:** Material used for the case
- **bracem:** Material used for the bracelet
- **yop:** Year the watch was produced
- **cond:** Condition of the watch (e.g., new, used)
- **sex:** Gender for which the watch is intended
- **size:** Diameter of the watch in millimeters

## Business Questions Explored

- Price Distribution: How is the price of luxury watches distributed across different brands and conditions?
- Popular Brands: Which brands have the highest number of listings and highest prices?
- Condition and Price Relationship: How does the condition of a watch (new vs. used) affect its price?
- Material Analysis: What impact do materials (case, bracelet) have on the watch price?
- Year of Production and Price: Is there a correlation between the year of production and price?
- Size Analysis: What is the typical size (diameter) of luxury watches, and how does it correlate with price?


## Tools 

- **Excel**: Dataset for preliminary data inspection
- **Python**: Pandas for data cleaning and manipulation in jupyter notebook 
- **Tableau**: Visualization with interactive dashboard

## Data Cleaning and Analysis

Import neccessary libraries

```python
import pandas as pd
import numpy as np
```

Import dataset and display the DataFrame

```python
df = pd.read_csv(r"C:\Users\corvi\OneDrive\Desktop\Data Sets\Luxury Watch Listings\Watches.csv", low_memory=False)
df
```
Output:

  <table border="1" class="dataframe">
    <thead>
      <tr style="text-align: right;">
        <th></th>
        <th>Unnamed: 0</th>
        <th>name</th>
        <th>price</th>
        <th>brand</th>
        <th>model</th>
        <th>ref</th>
        <th>mvmt</th>
        <th>casem</th>
        <th>bracem</th>
        <th>yop</th>
        <th>cond</th>
        <th>sex</th>
        <th>size</th>
        <th>condition</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th>0</th>
        <td>0</td>
        <td>Audemars Piguet Royal Oak Offshore Chronograph...</td>
        <td>$43,500</td>
        <td>Audemars Piguet</td>
        <td>Royal Oak Offshore Chronograph</td>
        <td>26237ST.OO.1000ST.01</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2019</td>
        <td>Unworn</td>
        <td>Men's watch/Unisex</td>
        <td>42 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>1</th>
        <td>1</td>
        <td>Audemars Piguet Royal Oak Selfwinding\n39mm Bl...</td>
        <td>$71,500</td>
        <td>Audemars Piguet</td>
        <td>Royal Oak Selfwinding</td>
        <td>15300ST.OO.1220ST.02</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2012</td>
        <td>Very good</td>
        <td>Men's watch/Unisex</td>
        <td>39 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>2</th>
        <td>2</td>
        <td>Audemars Piguet Royal Oak Chronograph\nBlue Di...</td>
        <td>$79,191</td>
        <td>Audemars Piguet</td>
        <td>Royal Oak Chronograph</td>
        <td>26331ST</td>
        <td>Automatic</td>
        <td>Steel</td>
        <td>Steel</td>
        <td>Unknown</td>
        <td>Unworn</td>
        <td>NaN</td>
        <td>41 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>3</th>
        <td>3</td>
        <td>Audemars Piguet Royal Oak Chronograph\nSelfwin...</td>
        <td>$108,000</td>
        <td>Audemars Piguet</td>
        <td>Royal Oak Chronograph</td>
        <td>26715ST.OO.1356ST.01</td>
        <td>Automatic</td>
        <td>Steel</td>
        <td>Steel</td>
        <td>2022 (Approximation)</td>
        <td>New</td>
        <td>Men's watch/Unisex</td>
        <td>38 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>4</th>
        <td>4</td>
        <td>Audemars Piguet Royal Oak Offshore Chronograph...</td>
        <td>$27,500</td>
        <td>Audemars Piguet</td>
        <td>Royal Oak Offshore Chronograph</td>
        <td>26170ST.OO.1000ST.01</td>
        <td>Automatic</td>
        <td>Steel</td>
        <td>Steel</td>
        <td>Unknown</td>
        <td>Very good</td>
        <td>Men's watch/Unisex</td>
        <td>42 x 54 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>...</th>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
        <td>...</td>
      </tr>
      <tr>
        <th>284486</th>
        <td>6438</td>
        <td>Zenith Defy El Primero\n21 TITANIUM 95.9000.90...</td>
        <td>$9,790</td>
        <td>Zenith</td>
        <td>Defy El Primero</td>
        <td>95.9000.9004/78.M9000</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2022</td>
        <td>Very good</td>
        <td>Men's watch/Unisex</td>
        <td>44 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>284487</th>
        <td>6439</td>
        <td>Zenith Chronomaster Sport\n41mm White 03.3100....</td>
        <td>$8,450</td>
        <td>Zenith</td>
        <td>Chronomaster Sport</td>
        <td>03.3100.3600/69.M3100</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2021 (Approximation)</td>
        <td>Very good</td>
        <td>Men's watch/Unisex</td>
        <td>41 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>284488</th>
        <td>6440</td>
        <td>Zenith El Primero\n50th Anniversary A386 Limited</td>
        <td>$16,500</td>
        <td>Zenith</td>
        <td>El Primero</td>
        <td>30.A386.400/69.C807</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2019</td>
        <td>Very good</td>
        <td>Men's watch/Unisex</td>
        <td>38 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>284489</th>
        <td>6441</td>
        <td>Zenith Chronomaster Sport\nWhite Dial Chronogr...</td>
        <td>$9,000</td>
        <td>Zenith</td>
        <td>Chronomaster Sport</td>
        <td>03.3100.3600/69.M3100</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>NaN</td>
        <td>2021</td>
        <td>Unworn</td>
        <td>Men's watch/Unisex</td>
        <td>41 mm</td>
        <td>NaN</td>
      </tr>
      <tr>
        <th>284490</th>
        <td>6442</td>
        <td>Zenith El Primero Chronomaster\n03.2040.400/69...</td>
        <td>$6,833</td>
        <td>Zenith</td>
        <td>El Primero Chronomaster</td>
        <td>NaN</td>
        <td>Automatic</td>
        <td>Steel</td>
        <td>Leather</td>
        <td>2019</td>
        <td>Very good</td>
        <td>NaN</td>
        <td>42 mm</td>
        <td>NaN</td>
      </tr>
    </tbody>
  </table>
  <p>284491 rows × 14 columns</p>
  </div>

Drop "Unnamed" column

```python
df.drop(columns = 'Unnamed: 0', inplace = True)
```

Remove duplicates

```python
df = df.drop_duplicates()
```

Display the dimensions of the DataFrame. The .shape attribute returns a tuple representing the number of rows and columns in the DataFrame.

```python
print(df.shape)
```

Output:

    (273093, 13)

Display information about the DataFrame.

```python
df.info()
```

Output:

    <class 'pandas.core.frame.DataFrame'>
        Index: 273093 entries, 0 to 284490
        Data columns (total 13 columns):
         #   Column     Non-Null Count   Dtype 
        ---  ------     --------------   ----- 
         0   name       206862 non-null  object
         1   price      272783 non-null  object
         2   brand      273028 non-null  object
         3   model      243114 non-null  object
         4   ref        230967 non-null  object
         5   mvmt       84667 non-null   object
         6   casem      113932 non-null  object
         7   bracem     104257 non-null  object
         8   yop        273025 non-null  object
         9   cond       203593 non-null  object
         10  sex        184005 non-null  object
         11  size       250359 non-null  object
         12  condition  65258 non-null   object
        dtypes: object(13)
        memory usage: 29.2+ MB

Check for missing values

```python
df.isnull().sum()
```
Output:

    name          66231
    price           310
    brand            65
    model         29979
    ref           42126
    mvmt         188426
    casem        159161
    bracem       168836
    yop              68
    cond          69500
    sex           89088
    size          22734
    condition    207835
    dtype: int64

Display count of unique name values

```python
print(df['name'].value_counts())
```

Output:

    name
    Omega Speedmaster Professional Moonwatch\nCo-Axial Master Chronometer                    169
    Omega De Ville Prestige\nCo-axial                                                        150
    Breitling Navitimer\nAutomatic 35                                                        143
    Zenith Defy El Primero\n21                                                               143
    Longines La Grande Classique\nDe Longines                                                130
                                                                                              ... 
    Jaeger-LeCoultre Reverso Lady\nPink Dial                                                   1
    Jaeger-LeCoultre Master Ultra Thin\nYellow Gold                                            1
    Jaeger-LeCoultre Reverso\n267.1.08                                                         1
    Jaeger-LeCoultre Reverso Grande Taille\nRef. 270.1.62 - 18K/750 Gelbgold - Handaufzug      1
    Zenith El Primero Chronomaster\n03.2040.400/69.c494                                        1
    Name: count, Length: 148689, dtype: int64

Display count of unique price values

```python
print(df['price'].value_counts())
```

Output:

    price
    Price on request    11934
    $6,500                249
    $4,500                239
    $4,026                236
    $12,500               236
                        ...  
    $126,802                1
    $88,286                 1
    $289,294                1
    $64,993                 1
    $45,998                 1
    Name: count, Length: 36830, dtype: int64

Display count of unique brand values

```python
print(df['brand'].value_counts())
```

Output:

    brand
    Rolex                  66130
    Omega                  38658
    Seiko                  19141
    Breitling              17572
    Cartier                16121
    Longines               15020
    TAG Heuer              12729
    Audemars Piguet        12673
    Patek Philippe         12174
    Hublot                 12004
    IWC                    10043
    Tudor                   9687
    Panerai                 7224
    Zenith                  6278
    Jaeger-LeCoultre        5801
    Oris                    4840
    Vacheron Constantin     3795
    A. Lange & Söhne        1300
    Richard Mille           1149
    Sinn                     677
    NOMOS                      3
    Edox                       2
    Montblanc                  2
    Tissot                     1
    Hamilton                   1
    Meistersinger              1
    Rado                       1
    Ebel                       1
    Name: count, dtype: int64

Display count of unique model values

```python
print(df['model'].value_counts())
```

Output:

    model
    Datejust 36                      8357
    Daytona                          6909
    Datejust 41                      5359
    Submariner Date                  5074
    GMT-Master II                    4227
                                     ... 
    Neo                                 1
    HyperChrome                         1
    Miles                               1
    Artelier Translucent Skeleton       1
    Tangente Neomatik                   1
    Name: count, Length: 948, dtype: int64

Display count of unique reference values

```python
print(df['ref'].value_counts())
```

Output:

    ref
    126334                                 1731
    126300                                 1263
    126234                                  831
    16233                                   789
    16570                                   745
                                            ... 
    279171 MOP Diamond Jubilee                1
    126233 Golden Palm Diamond Oyster         1
    126233 Golden Fluted Diamond Oyster       1
    126201 MOP Diamond Jubilee                1
    30.A386.400/69.C807                       1
    Name: count, Length: 33073, dtype: int64


Display count of unique movement values

```python
print(df['mvmt'].value_counts())
```

Output:

    mvmt
    Automatic         63144
    Quartz            14178
    Manual winding     7345
    Name: count, dtype: int64

Display count of unique case material values


```python
print(df['casem'].value_counts())
```

Output:

    casem
    Steel          72373
    Gold/Steel     10166
    Rose gold       8621
    Yellow gold     7549
    White gold      4908
    Titanium        4871
    Ceramic         2474
    Platinum        1120
    Red gold         569
    Bronze           530
    Carbon           433
    Silver           176
    Plastic           72
    Aluminum          31
    Tantalum          23
    Palladium         13
    Tungsten           3
    Name: count, dtype: int64

Display count of unique bracelet material values

```python
print(df['bracem'].value_counts())
```

Output:

    bracem
    Steel             47387
    Leather           15498
    Rubber            10648
    Gold/Steel         9074
    Crocodile skin     7915
    Yellow gold        3999
    Rose gold          2487
    White gold         1672
    Textile            1599
    Titanium           1310
    Calf skin          1239
    Platinum            458
    Ceramic             388
    Silicon             226
    Lizard skin          83
    Plastic              72
    Red gold             63
    Satin                60
    Ostrich skin         34
    Snake skin           14
    Silver               13
    Aluminium             9
    Shark skin            9
    Name: count, dtype: int64

Display count of unique year of production values

```python
print(df['yop'].value_counts())
```

Output:

    yop
    Unknown                         91387
    2023                            45716
    2022                            19657
    2021                            10286
    2023 (Approximation)             5493
                                    ...  
    2014, 2015, 2016, 2017, 2018        1
    1790 (Approximation)                1
    2006, 2018, 2019, 2020, 2021        1
    1960, 1963, 1968, 1969, 1970        1
    1650 (Approximation)                1
    Name: count, Length: 410, dtype: int64

Display count of unique cond values

```python
print(df['cond'].value_counts())
```

Output:

    cond
    Very good     71007
    New           65565
    Unworn        32182
    Good          27203
    Fair           7446
    Poor            148
    Incomplete       42
    Name: count, dtype: int64

Display count of unique sex values

```python
print(df['sex'].value_counts())
```

Output:

    sex
    Men's watch/Unisex    155235
    Women's watch          28770
    Name: count, dtype: int64

Display count of unique size values

```python
print(df['size'].value_counts())
```

Output:

    size
    40 mm               32650
    41 mm               26496
    42 mm               24319
    36 mm               18493
    44 mm               13938
                        ...  
    26.8 x 32.5 mm          1
    25 x 37.5 mm            1
    38mm x 34.5mm mm        1
    32.50 mm                1
    48 x 57.5 mm            1
    Name: count, Length: 6699, dtype: int64


Display count of unique condition values

```python
print(df['condition'].value_counts())
```

Output:

    condition
    Very good     33267
    Unworn        12453
    New           10186
    Good           8004
    Fair           1300
    Poor             45
    Incomplete        3
    Name: count, dtype: int64


Get summary of numerical columns in the DataFrame

```python
df.describe()
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>price</th>
      <th>brand</th>
      <th>model</th>
      <th>ref</th>
      <th>mvmt</th>
      <th>casem</th>
      <th>bracem</th>
      <th>yop</th>
      <th>cond</th>
      <th>sex</th>
      <th>size</th>
      <th>condition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>206862</td>
      <td>272783</td>
      <td>273028</td>
      <td>243114</td>
      <td>230967</td>
      <td>84667</td>
      <td>113932</td>
      <td>104257</td>
      <td>273025</td>
      <td>203593</td>
      <td>184005</td>
      <td>250359</td>
      <td>65258</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>148689</td>
      <td>36830</td>
      <td>28</td>
      <td>948</td>
      <td>33073</td>
      <td>3</td>
      <td>17</td>
      <td>23</td>
      <td>410</td>
      <td>7</td>
      <td>2</td>
      <td>6699</td>
      <td>7</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Omega Speedmaster Professional Moonwatch\nCo-A...</td>
      <td>Price on request</td>
      <td>Rolex</td>
      <td>Datejust 36</td>
      <td>126334</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Unknown</td>
      <td>Very good</td>
      <td>Men's watch/Unisex</td>
      <td>40 mm</td>
      <td>Very good</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>169</td>
      <td>11934</td>
      <td>66130</td>
      <td>8357</td>
      <td>1731</td>
      <td>63144</td>
      <td>72373</td>
      <td>47387</td>
      <td>91387</td>
      <td>71007</td>
      <td>155235</td>
      <td>32650</td>
      <td>33267</td>
    </tr>
  </tbody>
</table>
</div>

Check the first few rows of the dataset

```python
print(df.head())  
```

Output:


                                                    name      price  \
    0  Audemars Piguet Royal Oak Offshore Chronograph...   $43,500    
    1  Audemars Piguet Royal Oak Selfwinding\n39mm Bl...   $71,500    
    2  Audemars Piguet Royal Oak Chronograph\nBlue Di...   $79,191    
    3  Audemars Piguet Royal Oak Chronograph\nSelfwin...  $108,000    
    4  Audemars Piguet Royal Oak Offshore Chronograph...   $27,500    
    
                 brand                           model                   ref  \
    0  Audemars Piguet  Royal Oak Offshore Chronograph  26237ST.OO.1000ST.01   
    1  Audemars Piguet           Royal Oak Selfwinding  15300ST.OO.1220ST.02   
    2  Audemars Piguet           Royal Oak Chronograph               26331ST   
    3  Audemars Piguet           Royal Oak Chronograph  26715ST.OO.1356ST.01   
    4  Audemars Piguet  Royal Oak Offshore Chronograph  26170ST.OO.1000ST.01   
    
            mvmt  casem bracem                   yop       cond  \
    0        NaN    NaN    NaN                  2019     Unworn   
    1        NaN    NaN    NaN                  2012  Very good   
    2  Automatic  Steel  Steel               Unknown     Unworn   
    3  Automatic  Steel  Steel  2022 (Approximation)        New   
    4  Automatic  Steel  Steel               Unknown  Very good   
    
                      sex        size condition  
    0  Men's watch/Unisex       42 mm       NaN  
    1  Men's watch/Unisex       39 mm       NaN  
    2                 NaN       41 mm       NaN  
    3  Men's watch/Unisex       38 mm       NaN  
    4  Men's watch/Unisex  42 x 54 mm       NaN  

Remove Line Breaks (\n and \r) from Strings

```python
df = df.map(lambda x: x.replace('\n', '').replace('\r', '') if isinstance(x, str) else x)
```

Check all columns for \n or \r

```python
rows_with_new_lines = df.apply(lambda x: x.astype(str).str.contains('\n|\r', na=False)).any(axis=1)
```

Display rows with \n or \r

```python
df[rows_with_new_lines]
```

Output:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>price</th>
      <th>brand</th>
      <th>model</th>
      <th>ref</th>
      <th>mvmt</th>
      <th>casem</th>
      <th>bracem</th>
      <th>yop</th>
      <th>cond</th>
      <th>sex</th>
      <th>size</th>
      <th>condition</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>

Replace NaN values with "Unknown"

```python
df = df.fillna('Unknown') 
```

Convert data type of "price" column to string 

```python
df['price'] = df['price'].astype(str)
```

Remove "$" sign, commas ",", and convert cleaned data back to numeric data type. By using errors='coerce', any value that cannot be converted into a number (like 'Unknown') is converted to NaN.

```python
df['price'] = pd.to_numeric(df['price'].str.replace('$', '').str.replace(',', '').fillna('Unknown'), errors='coerce')
```

Create a New 'new_condition' Column by Combining 'cond' and 'condition'

```python
df['new_condition'] = df['cond'].fillna(df['condition'])
```
- The .fillna() method is used to replace missing values (NaN) in the 'cond' column with corresponding values from the 'condition' column.
- If a value is missing (NaN) in the 'cond' column, it will be filled with the value from the 'condition' column in the same row. If there is no missing value in 'cond', it will keep its original value.
- This ensures that the 'new_condition' column will have non-missing values by prioritizing data from 'cond', but falling back to 'condition' when necessary.

Update 'condition' Based on 'new_condition'

This code updates the values in the 'condition' column of the DataFrame df where the corresponding value in the 'new_condition' column is 'incomplete'. In this case, any row where 'new_condition' is 'incomplete' will have its corresponding 'condition' set to 'Unknown'.

```python
df.loc[df['new_condition'] == 'incomplete', 'condition'] = 'Unknown'
```

Drop Columns 'cond' and 'condition'

```python
df = df.drop(['cond', 'condition'], axis=1)
```

Extract Year of Production

This code extracts a 4-digit year (e.g., 2020) from the 'yop' column and stores it in a new column named 'Year of Production'.

```python
df['Year of Production'] = df['yop'].str.extract(r'(\d{4})').fillna('Unknown')
```

Verify output:

```python
print(df['Year of Production'].value_counts())
```
    Year of Production
    Unknown    91455
    2023       51209
    2022       23691
    2021       12144
    2020        6839
               ...  
    1878           1
    1690           1
    1741           1
    1885           1
    1650           1
    Name: count, Length: 170, dtype: int64

Drop "yop" Column

```python
df = df.drop('yop', axis=1)
```

Clean and Standardize "size" Column

```python
df['size'] = df['size'].apply(lambda x: str(x)
    .replace('Approximate ', '')
    .replace('weight ', '')
    .replace(': ', '')
    .replace('total ', '')
    .replace('product ', '')
    .split()[0]
    .rstrip('mm')
)
```

- Convert value into string
- Remove ('Approximate', 'weight', ': ', 'total', 'product', 'mm' suffix)
- split() splits strings into parts and extracts first part, e.g: "40 mm weight approx."

Group and Standardize "size" Column

This snippet processes the cleaned 'size' column to:

- Convert values to floats.
- Round them to the nearest whole number.
- Standardize invalid or non-numeric values by replacing them with 'Unknown'.

```python
def group_size(x):
    try:
        return str(round(float(x)))
    except:
        return 'Unknown'
df['size'] = df['size'].apply(group_size)
```

Convert 'size' Column to Numeric

```python
df['size'] = pd.to_numeric(df['size'], errors='coerce')
```

Filter Rows Based on Valid Size Range to Remove Outliers

```python
new_size = (df['size'] >= 20) & (df['size'] <= 70)  # Adjust range as needed, realistic example 20-70mm
df = df[new_size]  # Keep only rows within the valid range
```

Get Count of Each Size of Watches

```python
print(df['Diameter (mm)'].value_counts())
```

Output:

    Diameter (mm)
    40.0    39509
    41.0    29749
    42.0    29395
    36.0    21207
    44.0    17492
    39.0    12386
    38.0    10407
    43.0     9842
    34.0     9690
    45.0     7677
    35.0     6564
    26.0     5586
    37.0     5504
    31.0     5082
    33.0     4406
    46.0     4025
    28.0     3259
    32.0     2746
    30.0     2681
    29.0     2495
    27.0     2183
    47.0     2079
    24.0     2024
    25.0     1953
    48.0     1899
    22.0     1209
    20.0     1107
    23.0     1045
    50.0      698
    49.0      555
    21.0      446
    51.0      248
    52.0      182
    55.0      117
    54.0       83
    53.0       82
    56.0       25
    60.0       23
    57.0       22
    65.0       19
    58.0       15
    59.0       12
    69.0        5
    61.0        4
    64.0        4
    66.0        3
    70.0        3
    63.0        2
    68.0        1
    67.0        1
    62.0        1
    Name: count, dtype: int64

Get Average Size of Watches

```python
average_size = df['Diameter (mm)'].mean()
print(f"The average size of the watches is {average_size:.2f} mm.")
```

Output:

    The average size of the watches is 38.57 mm.


Rename Columns

This snippet renames the columns in the DataFrame to more descriptive and user-friendly names.

```python
new_columns = {
    'name': 'Name',
    'price': 'Price',
    'brand': 'Brand',
    'model': 'Model',
    'ref': 'Reference No.',
    'mvmt': 'Movement Type',
    'casem': 'Case Material',
    'bracem': 'Bracelet Material',
    'sex': 'Sex of Watch',
    'size': 'Diameter (mm)',
    'new_condition': 'Condition'
}
df = df.rename(columns=new_columns)
```

Preview First Few Rows

```python
print(df.head())
```

Output:


                                                    Name     Price  \
    0  Audemars Piguet Royal Oak Offshore Chronograph...   43500.0   
    1  Audemars Piguet Royal Oak Selfwinding39mm Blue...   71500.0   
    2  Audemars Piguet Royal Oak ChronographBlue Dial...   79191.0   
    3  Audemars Piguet Royal Oak ChronographSelfwindi...  108000.0   
    4  Audemars Piguet Royal Oak Offshore Chronograph...   27500.0   
    
                 Brand                           Model         Reference No.  \
    0  Audemars Piguet  Royal Oak Offshore Chronograph  26237ST.OO.1000ST.01   
    1  Audemars Piguet           Royal Oak Selfwinding  15300ST.OO.1220ST.02   
    2  Audemars Piguet           Royal Oak Chronograph               26331ST   
    3  Audemars Piguet           Royal Oak Chronograph  26715ST.OO.1356ST.01   
    4  Audemars Piguet  Royal Oak Offshore Chronograph  26170ST.OO.1000ST.01   
    
      Movement Type Case Material Bracelet Material        Sex of Watch  \
    0       Unknown       Unknown           Unknown  Men's watch/Unisex   
    1       Unknown       Unknown           Unknown  Men's watch/Unisex   
    2     Automatic         Steel             Steel             Unknown   
    3     Automatic         Steel             Steel  Men's watch/Unisex   
    4     Automatic         Steel             Steel  Men's watch/Unisex   
    
       Diameter (mm)  Condition Year of Production  
    0           42.0     Unworn               2019  
    1           39.0  Very good               2012  
    2           41.0     Unworn            Unknown  
    3           38.0        New               2022  
    4           42.0  Very good            Unknown  


Display First 100 Rows to Check Data

```python
df.head(100)
```
Output:

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Price</th>
      <th>Brand</th>
      <th>Model</th>
      <th>Reference No.</th>
      <th>Movement Type</th>
      <th>Case Material</th>
      <th>Bracelet Material</th>
      <th>Sex of Watch</th>
      <th>Diameter (mm)</th>
      <th>Condition</th>
      <th>Year of Production</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Audemars Piguet Royal Oak Offshore Chronograph...</td>
      <td>43500.0</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Offshore Chronograph</td>
      <td>26237ST.OO.1000ST.01</td>
      <td>Unknown</td>
      <td>Unknown</td>
      <td>Unknown</td>
      <td>Men's watch/Unisex</td>
      <td>42.0</td>
      <td>Unworn</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Audemars Piguet Royal Oak Selfwinding39mm Blue...</td>
      <td>71500.0</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Selfwinding</td>
      <td>15300ST.OO.1220ST.02</td>
      <td>Unknown</td>
      <td>Unknown</td>
      <td>Unknown</td>
      <td>Men's watch/Unisex</td>
      <td>39.0</td>
      <td>Very good</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Audemars Piguet Royal Oak ChronographBlue Dial...</td>
      <td>79191.0</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Chronograph</td>
      <td>26331ST</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Unknown</td>
      <td>41.0</td>
      <td>Unworn</td>
      <td>Unknown</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Audemars Piguet Royal Oak ChronographSelfwindi...</td>
      <td>108000.0</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Chronograph</td>
      <td>26715ST.OO.1356ST.01</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Men's watch/Unisex</td>
      <td>38.0</td>
      <td>New</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Audemars Piguet Royal Oak Offshore Chronograph...</td>
      <td>27500.0</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Offshore Chronograph</td>
      <td>26170ST.OO.1000ST.01</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Men's watch/Unisex</td>
      <td>42.0</td>
      <td>Very good</td>
      <td>Unknown</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Audemars Piguet Royal Oak Double Balance Wheel...</td>
      <td>NaN</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Double Balance Wheel Openworked</td>
      <td>15412BA.YG.1224BA.01</td>
      <td>Automatic</td>
      <td>Yellow gold</td>
      <td>Yellow gold</td>
      <td>Men's watch/Unisex</td>
      <td>41.0</td>
      <td>Unworn</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Audemars Piguet Royal Oak JumboSelfwinding Jum...</td>
      <td>NaN</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Jumbo</td>
      <td>15202ST.OO.1240ST.01</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Men's watch/Unisex</td>
      <td>39.0</td>
      <td>Unworn</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Audemars Piguet Royal Oak Double Balance Wheel...</td>
      <td>NaN</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Double Balance Wheel Openworked</td>
      <td>15407ST.OO.1220ST.01</td>
      <td>Automatic</td>
      <td>Steel</td>
      <td>Steel</td>
      <td>Men's watch/Unisex</td>
      <td>41.0</td>
      <td>Unworn</td>
      <td>2023</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Audemars Piguet Code 11.59Selfwinding Chronogr...</td>
      <td>NaN</td>
      <td>Audemars Piguet</td>
      <td>Code 11.59</td>
      <td>26393BC.OO.A002KB.01</td>
      <td>Automatic</td>
      <td>White gold</td>
      <td>Rubber</td>
      <td>Men's watch/Unisex</td>
      <td>41.0</td>
      <td>Unworn</td>
      <td>2022</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Audemars Piguet Royal Oak Offshore Chronograph...</td>
      <td>NaN</td>
      <td>Audemars Piguet</td>
      <td>Royal Oak Offshore Chronograph</td>
      <td>26420TI.OO.A027CA.01</td>
      <td>Automatic</td>
      <td>Titanium</td>
      <td>Rubber</td>
      <td>Men's watch/Unisex</td>
      <td>43.0</td>
      <td>Unworn</td>
      <td>2023</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 12 columns</p>
</div>

Save and Export csv File for Visualization

```python
luxury_watches = df 
```
```python
luxury_watches.to_csv(r"C:\Users\corvi\OneDrive\Desktop\Data Sets\Luxury_Watches_Final.csv", index=False)
```

## Key Findings

- Price Distribution:
    - The prices of luxury watches vary widely. The majority of watches fall within a certain range, but a few outliers represent extremely high-value watches.

- Size Insights:
    - The sizes of watches predominantly range between 34–45 mm, with 40 mm being the most popular, indicating this range is the most popular for luxury watches.

- Condition Insights:
    - Most watches are listed as 'New' or 'Very Good', suggesting that the majority of items are in premium condition.
 
- Popular Brands and Models:
    - Brands such as Rolex, Patek Philippe, and Omega dominate the dataset. Within these brands, certain models stand out for their popularity and frequency.

- Materials Used:
    - Case and bracelet materials such as stainless steel and gold are the most common. Rare materials like titanium and ceramic appear less frequently but are associated with higher prices.


## Business Insights

- Market Demand:
    - The prevalence of mid-sized watches (34–45 mm) indicates strong demand for standard sizes. Brands can consider focusing marketing efforts around this range.

- Target Pricing:
    - With a clearer understanding of price distribution, pricing strategies for luxury watches can be optimized to target the most frequent price ranges while leveraging the value of premium-priced items.

- Material Preferences:
    - Highlighting the most popular materials like stainless steel in marketing campaigns could attract more customers. Rare materials could be used to target high-net-worth individuals.

## Visualization

Interactive Tableau dashboard available here: https://public.tableau.com/views/LuxuryWatchesPriceAnalysis/PricingDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
