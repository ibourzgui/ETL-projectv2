

```python
import pandas as pd
from sqlalchemy import create_engine
import numpy as np

import pymysql
pymysql.install_as_MySQLdb()
```


```python
csv_file1 = "world-happiness-report-2019.csv"
world_happiness_df = pd.read_csv(csv_file1)
world_happiness_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country (region)</th>
      <th>Ladder</th>
      <th>SD of Ladder</th>
      <th>Positive affect</th>
      <th>Negative affect</th>
      <th>Social support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>Log of GDP
per capita</th>
      <th>Healthy life
expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Finland</td>
      <td>1</td>
      <td>4</td>
      <td>41.0</td>
      <td>10.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>47.0</td>
      <td>22.0</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denmark</td>
      <td>2</td>
      <td>13</td>
      <td>24.0</td>
      <td>26.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>3.0</td>
      <td>22.0</td>
      <td>14.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Norway</td>
      <td>3</td>
      <td>8</td>
      <td>16.0</td>
      <td>29.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Iceland</td>
      <td>4</td>
      <td>9</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>7.0</td>
      <td>45.0</td>
      <td>3.0</td>
      <td>15.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Netherlands</td>
      <td>5</td>
      <td>1</td>
      <td>12.0</td>
      <td>25.0</td>
      <td>15.0</td>
      <td>19.0</td>
      <td>12.0</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>18.0</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country (region)</th>
      <th>Ladder</th>
      <th>SD of Ladder</th>
      <th>Positive affect</th>
      <th>Negative affect</th>
      <th>Social support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>Log of GDP
per capita</th>
      <th>Healthy life
expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Finland</td>
      <td>1</td>
      <td>4</td>
      <td>41.0</td>
      <td>10.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>47.0</td>
      <td>22.0</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Denmark</td>
      <td>2</td>
      <td>13</td>
      <td>24.0</td>
      <td>26.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>3.0</td>
      <td>22.0</td>
      <td>14.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Norway</td>
      <td>3</td>
      <td>8</td>
      <td>16.0</td>
      <td>29.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>12.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Iceland</td>
      <td>4</td>
      <td>9</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>7.0</td>
      <td>45.0</td>
      <td>3.0</td>
      <td>15.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Netherlands</td>
      <td>5</td>
      <td>1</td>
      <td>12.0</td>
      <td>25.0</td>
      <td>15.0</td>
      <td>19.0</td>
      <td>12.0</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>18.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
csv_file2 = "economic_freedom_index2019_data.csv"
economic_freedom_df =pd.read_csv(csv_file2)


economic_freedom_df.columns
```




    Index(['CountryID', 'Country Name', 'WEBNAME', 'Region', 'World Rank',
           'Region Rank', '2019 Score', 'Property Rights', 'Judical Effectiveness',
           'Government Integrity', 'Tax Burden', 'Gov't Spending', 'Fiscal Health',
           'Business Freedom', 'Labor Freedom', 'Monetary Freedom',
           'Trade Freedom', 'Investment Freedom ', 'Financial Freedom',
           'Tariff Rate (%)', 'Income Tax Rate (%)', 'Corporate Tax Rate (%)',
           'Tax Burden % of GDP', 'Gov't Expenditure % of GDP ', 'Country',
           'Population (Millions)', 'GDP (Billions, PPP)', 'GDP Growth Rate (%)',
           '5 Year GDP Growth Rate (%)', 'GDP per Capita (PPP)',
           'Unemployment (%)', 'Inflation (%)', 'FDI Inflow (Millions)',
           'Public Debt (% of GDP)'],
          dtype='object')






    Index(['CountryID', 'Country Name', 'WEBNAME', 'Region', 'World Rank',
           'Region Rank', '2019 Score', 'Property Rights', 'Judical Effectiveness',
           'Government Integrity', 'Tax Burden', 'Gov't Spending', 'Fiscal Health',
           'Business Freedom', 'Labor Freedom', 'Monetary Freedom',
           'Trade Freedom', 'Investment Freedom ', 'Financial Freedom',
           'Tariff Rate (%)', 'Income Tax Rate (%)', 'Corporate Tax Rate (%)',
           'Tax Burden % of GDP', 'Gov't Expenditure % of GDP ', 'Country',
           'Population (Millions)', 'GDP (Billions, PPP)', 'GDP Growth Rate (%)',
           '5 Year GDP Growth Rate (%)', 'GDP per Capita (PPP)',
           'Unemployment (%)', 'Inflation (%)', 'FDI Inflow (Millions)',
           'Public Debt (% of GDP)'],
          dtype='object')




```python
new_economic_freedom_df=economic_freedom_df[['CountryID',
"Country Name",
"Region",
"World Rank",
"2019 Score",
"Financial Freedom",
"Income Tax Rate (%)",
"Corporate Tax Rate (%)",
"Tax Burden % of GDP",
"Population (Millions)",
"GDP Growth Rate (%)",
"5 Year GDP Growth Rate (%)",
"Unemployment (%)",
"Inflation (%)"]].copy()
```


```python
new_economic_freedom_df=new_economic_freedom_df.rename(index=str, columns={"Country Name": "Country_Name", \
                                                                           "World Rank": "World_Rank", \
                                                                           "2019 Score": "Score_2019", \
                                                                           "Financial Freedom": "Financial_Freedom",\
                                                                           "Income Tax Rate (%)":"Income_Tax_Rate_Pct",\
                                                                           "Corporate Tax Rate (%)":"Corporate_Tax_Rate_Pct", \
                                                                           "Tax Burden % of GDP":"Tax_Burden_Pct_of_GDP",\
                                                                           "Population (Millions)":"Population_in_Millions", \
                                                                           "GDP Growth Rate (%)": "GDP_Growth_Rate_Pct", \
                                                                           "5 Year GDP Growth Rate (%)": "Five_Year_GDP_Growth_Rate_Pct", \
                                                                           "Unemployment (%)":"Unemployment_Pct", \
                                                                           "Inflation (%)":"Inflation_Pct"})
new_economic_freedom_df['Country_Name'] = new_economic_freedom_df['Country_Name'].str.strip()
```


```python
new_economic_freedom_df.columns
```




    Index(['CountryID', 'Country_Name', 'Region', 'World_Rank', 'Score_2019',
           'Financial_Freedom', 'Income_Tax_Rate_Pct', 'Corporate_Tax_Rate_Pct',
           'Tax_Burden_Pct_of_GDP', 'Population_in_Millions',
           'GDP_Growth_Rate_Pct', 'Five_Year_GDP_Growth_Rate_Pct',
           'Unemployment_Pct', 'Inflation_Pct'],
          dtype='object')






    Index(['CountryID', 'Country_Name', 'Region', 'World_Rank', 'Score_2019',
           'Financial_Freedom', 'Income_Tax_Rate_Pct', 'Corporate_Tax_Rate_Pct',
           'Tax_Burden_Pct_of_GDP', 'Population_in_Millions',
           'GDP_Growth_Rate_Pct', 'Five_Year_GDP_Growth_Rate_Pct',
           'Unemployment_Pct', 'Inflation_Pct'],
          dtype='object')




```python
new_world_happiness_df=world_happiness_df[["Country (region)",
"Ladder",
"Positive affect",
"Negative affect",
"Social support",
"Freedom",
"Corruption",
"Generosity",
"Log of GDP\nper capita",
"Healthy life\nexpectancy"]]
```


```python
new_world_happiness_df = new_world_happiness_df.rename(index=str, columns={"Country (region)": "Country", 
                                                                           "Ladder": "Happiness_Rank", \
                                                                           "Positive affect":"Positive_Emotion",\
                                                                           "Negative affect":"Negative_Emotion", \
                                                                           "Social support": "Social_support",\
                                                                           "Log of GDP\nper capita": "GDP_Contribution",\
                                                                           "Healthy life\nexpectancy": "Healthy_life_expectancy" })
new_world_happiness_df['Country']=new_world_happiness_df['Country'].str.strip()
```


```python
new_economic_freedom_df  = new_economic_freedom_df[new_economic_freedom_df['Score_2019'].notnull()]
new_economic_freedom_df.count()
# pd.to_numeric(new_economic_freedom_df["Population_in_Millions"])
# pd.to_numeric(new_economic_freedom_df["Unemployment_Pct"])
```




    CountryID                        180
    Country_Name                     180
    Region                           180
    World_Rank                       180
    Score_2019                       180
    Financial_Freedom                180
    Income_Tax_Rate_Pct              179
    Corporate_Tax_Rate_Pct           179
    Tax_Burden_Pct_of_GDP            179
    Population_in_Millions           180
    GDP_Growth_Rate_Pct              180
    Five_Year_GDP_Growth_Rate_Pct    179
    Unemployment_Pct                 175
    Inflation_Pct                    179
    dtype: int64






    CountryID                        180
    Country_Name                     180
    Region                           180
    World_Rank                       180
    Score_2019                       180
    Financial_Freedom                180
    Income_Tax_Rate_Pct              179
    Corporate_Tax_Rate_Pct           179
    Tax_Burden_Pct_of_GDP            179
    Population_in_Millions           180
    GDP_Growth_Rate_Pct              180
    Five_Year_GDP_Growth_Rate_Pct    179
    Unemployment_Pct                 175
    Inflation_Pct                    179
    dtype: int64




```python
rds_connection_string = "root:mypassssss@127.0.0.1/happiness_db"
engine = create_engine(f'mysql://{rds_connection_string}')
```


```python
engine.table_names()
```


```python
#Use pandas to load csv converted DataFrame into database
new_economic_freedom_df.to_sql(name='economic_table', con=engine, if_exists='append', index=False)
```


```python
#Use pandas to load csv converted DataFrame into database
new_world_happiness_df.to_sql(name='happiness_table', con=engine, if_exists='append', index=False)
```


```python
combined_df = new_economic_freedom_df.merge(new_world_happiness_df, how='inner', \
                       left_on='Country_Name', right_on='Country')
combined_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>Population_in_Millions</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Afghanistan</td>
      <td>Asia-Pacific</td>
      <td>152.0</td>
      <td>51.5</td>
      <td>10.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>35.5</td>
      <td>...</td>
      <td>Afghanistan</td>
      <td>154</td>
      <td>152.0</td>
      <td>133.0</td>
      <td>151.0</td>
      <td>155.0</td>
      <td>136.0</td>
      <td>137.0</td>
      <td>134.0</td>
      <td>139.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Albania</td>
      <td>Europe</td>
      <td>52.0</td>
      <td>66.5</td>
      <td>70.0</td>
      <td>23.0</td>
      <td>15.0</td>
      <td>24.9</td>
      <td>2.9</td>
      <td>...</td>
      <td>Albania</td>
      <td>107</td>
      <td>90.0</td>
      <td>108.0</td>
      <td>133.0</td>
      <td>87.0</td>
      <td>134.0</td>
      <td>60.0</td>
      <td>81.0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Algeria</td>
      <td>Middle East and North Africa</td>
      <td>171.0</td>
      <td>46.2</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>24.5</td>
      <td>41.5</td>
      <td>...</td>
      <td>Algeria</td>
      <td>88</td>
      <td>113.0</td>
      <td>106.0</td>
      <td>101.0</td>
      <td>149.0</td>
      <td>46.0</td>
      <td>128.0</td>
      <td>72.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>Argentina</td>
      <td>Americas</td>
      <td>148.0</td>
      <td>52.2</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>30.8</td>
      <td>44.1</td>
      <td>...</td>
      <td>Argentina</td>
      <td>47</td>
      <td>28.0</td>
      <td>93.0</td>
      <td>46.0</td>
      <td>54.0</td>
      <td>109.0</td>
      <td>123.0</td>
      <td>55.0</td>
      <td>37.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>Armenia</td>
      <td>Europe</td>
      <td>47.0</td>
      <td>67.7</td>
      <td>70.0</td>
      <td>26.0</td>
      <td>20.0</td>
      <td>21.3</td>
      <td>3</td>
      <td>...</td>
      <td>Armenia</td>
      <td>116</td>
      <td>126.0</td>
      <td>145.0</td>
      <td>117.0</td>
      <td>123.0</td>
      <td>93.0</td>
      <td>129.0</td>
      <td>91.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>Australia</td>
      <td>Asia-Pacific</td>
      <td>5.0</td>
      <td>80.9</td>
      <td>90.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>28.2</td>
      <td>24.8</td>
      <td>...</td>
      <td>Australia</td>
      <td>11</td>
      <td>47.0</td>
      <td>37.0</td>
      <td>7.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>Austria</td>
      <td>Europe</td>
      <td>31.0</td>
      <td>72.0</td>
      <td>70.0</td>
      <td>50.0</td>
      <td>25.0</td>
      <td>42.7</td>
      <td>8.8</td>
      <td>...</td>
      <td>Austria</td>
      <td>10</td>
      <td>64.0</td>
      <td>24.0</td>
      <td>31.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>25.0</td>
      <td>16.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>9</td>
      <td>Azerbaijan</td>
      <td>Asia-Pacific</td>
      <td>60.0</td>
      <td>65.4</td>
      <td>60.0</td>
      <td>25.0</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>9.8</td>
      <td>...</td>
      <td>Azerbaijan</td>
      <td>90</td>
      <td>134.0</td>
      <td>20.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>22.0</td>
      <td>146.0</td>
      <td>65.0</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>11</td>
      <td>Bahrain</td>
      <td>Middle East and North Africa</td>
      <td>54.0</td>
      <td>66.4</td>
      <td>80.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.6</td>
      <td>1.5</td>
      <td>...</td>
      <td>Bahrain</td>
      <td>37</td>
      <td>39.0</td>
      <td>83.0</td>
      <td>59.0</td>
      <td>24.0</td>
      <td>NaN</td>
      <td>23.0</td>
      <td>20.0</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>12</td>
      <td>Bangladesh</td>
      <td>Asia-Pacific</td>
      <td>121.0</td>
      <td>55.6</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>8.8</td>
      <td>163.2</td>
      <td>...</td>
      <td>Bangladesh</td>
      <td>125</td>
      <td>145.0</td>
      <td>68.0</td>
      <td>126.0</td>
      <td>27.0</td>
      <td>36.0</td>
      <td>107.0</td>
      <td>119.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14</td>
      <td>Belarus</td>
      <td>Europe</td>
      <td>104.0</td>
      <td>57.9</td>
      <td>10.0</td>
      <td>13.0</td>
      <td>18.0</td>
      <td>23.8</td>
      <td>9.5</td>
      <td>...</td>
      <td>Belarus</td>
      <td>81</td>
      <td>149.0</td>
      <td>36.0</td>
      <td>33.0</td>
      <td>131.0</td>
      <td>37.0</td>
      <td>103.0</td>
      <td>58.0</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15</td>
      <td>Belgium</td>
      <td>Europe</td>
      <td>48.0</td>
      <td>67.3</td>
      <td>70.0</td>
      <td>50.0</td>
      <td>29.0</td>
      <td>44.2</td>
      <td>11.4</td>
      <td>...</td>
      <td>Belgium</td>
      <td>18</td>
      <td>57.0</td>
      <td>53.0</td>
      <td>22.0</td>
      <td>53.0</td>
      <td>20.0</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>17</td>
      <td>Benin</td>
      <td>Sub-Saharan Africa</td>
      <td>127.0</td>
      <td>55.3</td>
      <td>50.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>11.9</td>
      <td>11.1</td>
      <td>...</td>
      <td>Benin</td>
      <td>102</td>
      <td>118.0</td>
      <td>148.0</td>
      <td>153.0</td>
      <td>103.0</td>
      <td>75.0</td>
      <td>116.0</td>
      <td>128.0</td>
      <td>133.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>18</td>
      <td>Bhutan</td>
      <td>Asia-Pacific</td>
      <td>74.0</td>
      <td>62.9</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>30.0</td>
      <td>13.4</td>
      <td>0.8</td>
      <td>...</td>
      <td>Bhutan</td>
      <td>95</td>
      <td>37.0</td>
      <td>98.0</td>
      <td>68.0</td>
      <td>59.0</td>
      <td>25.0</td>
      <td>13.0</td>
      <td>95.0</td>
      <td>104.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>19</td>
      <td>Bolivia</td>
      <td>Americas</td>
      <td>173.0</td>
      <td>42.3</td>
      <td>40.0</td>
      <td>13.0</td>
      <td>25.0</td>
      <td>31.1</td>
      <td>11.1</td>
      <td>...</td>
      <td>Bolivia</td>
      <td>61</td>
      <td>70.0</td>
      <td>138.0</td>
      <td>93.0</td>
      <td>35.0</td>
      <td>91.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20</td>
      <td>Bosnia and Herzegovina</td>
      <td>Europe</td>
      <td>83.0</td>
      <td>61.9</td>
      <td>60.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>37.0</td>
      <td>3.5</td>
      <td>...</td>
      <td>Bosnia and Herzegovina</td>
      <td>78</td>
      <td>116.0</td>
      <td>79.0</td>
      <td>92.0</td>
      <td>137.0</td>
      <td>145.0</td>
      <td>32.0</td>
      <td>82.0</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>21</td>
      <td>Botswana</td>
      <td>Sub-Saharan Africa</td>
      <td>36.0</td>
      <td>69.5</td>
      <td>70.0</td>
      <td>25.0</td>
      <td>22.0</td>
      <td>24.9</td>
      <td>2.2</td>
      <td>...</td>
      <td>Botswana</td>
      <td>148</td>
      <td>87.0</td>
      <td>65.0</td>
      <td>105.0</td>
      <td>60.0</td>
      <td>54.0</td>
      <td>150.0</td>
      <td>66.0</td>
      <td>113.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Brazil</td>
      <td>Americas</td>
      <td>150.0</td>
      <td>51.9</td>
      <td>50.0</td>
      <td>27.5</td>
      <td>34.0</td>
      <td>32.2</td>
      <td>207.7</td>
      <td>...</td>
      <td>Brazil</td>
      <td>32</td>
      <td>69.0</td>
      <td>105.0</td>
      <td>43.0</td>
      <td>84.0</td>
      <td>71.0</td>
      <td>108.0</td>
      <td>70.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>23</td>
      <td>Bulgaria</td>
      <td>Europe</td>
      <td>37.0</td>
      <td>69.0</td>
      <td>60.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>28.0</td>
      <td>7.1</td>
      <td>...</td>
      <td>Bulgaria</td>
      <td>97</td>
      <td>117.0</td>
      <td>13.0</td>
      <td>18.0</td>
      <td>115.0</td>
      <td>147.0</td>
      <td>112.0</td>
      <td>56.0</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>24</td>
      <td>Burkina Faso</td>
      <td>Sub-Saharan Africa</td>
      <td>96.0</td>
      <td>59.4</td>
      <td>40.0</td>
      <td>27.5</td>
      <td>28.0</td>
      <td>16.3</td>
      <td>18.9</td>
      <td>...</td>
      <td>Burkina Faso</td>
      <td>115</td>
      <td>115.0</td>
      <td>117.0</td>
      <td>116.0</td>
      <td>127.0</td>
      <td>47.0</td>
      <td>125.0</td>
      <td>137.0</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>26</td>
      <td>Burundi</td>
      <td>Sub-Saharan Africa</td>
      <td>162.0</td>
      <td>48.9</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>12.3</td>
      <td>10.9</td>
      <td>...</td>
      <td>Burundi</td>
      <td>145</td>
      <td>98.0</td>
      <td>126.0</td>
      <td>152.0</td>
      <td>135.0</td>
      <td>23.0</td>
      <td>149.0</td>
      <td>151.0</td>
      <td>135.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>27</td>
      <td>Cambodia</td>
      <td>Asia-Pacific</td>
      <td>105.0</td>
      <td>57.8</td>
      <td>50.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>16</td>
      <td>...</td>
      <td>Cambodia</td>
      <td>109</td>
      <td>27.0</td>
      <td>142.0</td>
      <td>109.0</td>
      <td>2.0</td>
      <td>94.0</td>
      <td>61.0</td>
      <td>116.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>28</td>
      <td>Cameroon</td>
      <td>Sub-Saharan Africa</td>
      <td>145.0</td>
      <td>52.4</td>
      <td>50.0</td>
      <td>35.0</td>
      <td>33.0</td>
      <td>15.6</td>
      <td>24.3</td>
      <td>...</td>
      <td>Cameroon</td>
      <td>96</td>
      <td>106.0</td>
      <td>129.0</td>
      <td>129.0</td>
      <td>90.0</td>
      <td>120.0</td>
      <td>91.0</td>
      <td>121.0</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>29</td>
      <td>Canada</td>
      <td>Americas</td>
      <td>8.0</td>
      <td>77.7</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>15.0</td>
      <td>31.7</td>
      <td>36.7</td>
      <td>...</td>
      <td>Canada</td>
      <td>9</td>
      <td>18.0</td>
      <td>49.0</td>
      <td>20.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>31</td>
      <td>Central African Republic</td>
      <td>Sub-Saharan Africa</td>
      <td>161.0</td>
      <td>49.1</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>9.0</td>
      <td>5</td>
      <td>...</td>
      <td>Central African Republic</td>
      <td>155</td>
      <td>132.0</td>
      <td>153.0</td>
      <td>155.0</td>
      <td>133.0</td>
      <td>122.0</td>
      <td>113.0</td>
      <td>152.0</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>32</td>
      <td>Chad</td>
      <td>Sub-Saharan Africa</td>
      <td>159.0</td>
      <td>49.9</td>
      <td>40.0</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>5.3</td>
      <td>12.2</td>
      <td>...</td>
      <td>Chad</td>
      <td>132</td>
      <td>136.0</td>
      <td>151.0</td>
      <td>141.0</td>
      <td>142.0</td>
      <td>80.0</td>
      <td>106.0</td>
      <td>133.0</td>
      <td>148.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>33</td>
      <td>Chile</td>
      <td>Americas</td>
      <td>18.0</td>
      <td>75.4</td>
      <td>70.0</td>
      <td>35.0</td>
      <td>25.0</td>
      <td>20.4</td>
      <td>18.4</td>
      <td>...</td>
      <td>Chile</td>
      <td>26</td>
      <td>15.0</td>
      <td>78.0</td>
      <td>58.0</td>
      <td>98.0</td>
      <td>99.0</td>
      <td>45.0</td>
      <td>49.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>34</td>
      <td>China</td>
      <td>Asia-Pacific</td>
      <td>100.0</td>
      <td>58.4</td>
      <td>20.0</td>
      <td>45.0</td>
      <td>25.0</td>
      <td>17.5</td>
      <td>1390.1</td>
      <td>...</td>
      <td>China</td>
      <td>93</td>
      <td>21.0</td>
      <td>11.0</td>
      <td>108.0</td>
      <td>31.0</td>
      <td>NaN</td>
      <td>133.0</td>
      <td>68.0</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>35</td>
      <td>Colombia</td>
      <td>Americas</td>
      <td>49.0</td>
      <td>67.3</td>
      <td>70.0</td>
      <td>33.0</td>
      <td>33.0</td>
      <td>19.9</td>
      <td>49.3</td>
      <td>...</td>
      <td>Colombia</td>
      <td>43</td>
      <td>30.0</td>
      <td>88.0</td>
      <td>52.0</td>
      <td>56.0</td>
      <td>124.0</td>
      <td>111.0</td>
      <td>74.0</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>36</td>
      <td>Comoros</td>
      <td>Sub-Saharan Africa</td>
      <td>124.0</td>
      <td>55.4</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>14.5</td>
      <td>0.8</td>
      <td>...</td>
      <td>Comoros</td>
      <td>142</td>
      <td>67.0</td>
      <td>114.0</td>
      <td>143.0</td>
      <td>148.0</td>
      <td>81.0</td>
      <td>62.0</td>
      <td>143.0</td>
      <td>117.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>111</th>
      <td>144</td>
      <td>Serbia</td>
      <td>Europe</td>
      <td>69.0</td>
      <td>63.9</td>
      <td>50.0</td>
      <td>10.0</td>
      <td>15.0</td>
      <td>38.4</td>
      <td>7</td>
      <td>...</td>
      <td>Serbia</td>
      <td>70</td>
      <td>148.0</td>
      <td>92.0</td>
      <td>57.0</td>
      <td>124.0</td>
      <td>118.0</td>
      <td>84.0</td>
      <td>71.0</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>112</th>
      <td>146</td>
      <td>Sierra Leone</td>
      <td>Sub-Saharan Africa</td>
      <td>167.0</td>
      <td>47.5</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>30.0</td>
      <td>12.2</td>
      <td>7.4</td>
      <td>...</td>
      <td>Sierra Leone</td>
      <td>129</td>
      <td>139.0</td>
      <td>149.0</td>
      <td>135.0</td>
      <td>116.0</td>
      <td>112.0</td>
      <td>79.0</td>
      <td>145.0</td>
      <td>146.0</td>
    </tr>
    <tr>
      <th>113</th>
      <td>147</td>
      <td>Singapore</td>
      <td>Asia-Pacific</td>
      <td>2.0</td>
      <td>89.4</td>
      <td>80.0</td>
      <td>22.0</td>
      <td>17.0</td>
      <td>13.7</td>
      <td>5.6</td>
      <td>...</td>
      <td>Singapore</td>
      <td>34</td>
      <td>38.0</td>
      <td>2.0</td>
      <td>36.0</td>
      <td>20.0</td>
      <td>1.0</td>
      <td>21.0</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>114</th>
      <td>148</td>
      <td>Slovakia</td>
      <td>Europe</td>
      <td>65.0</td>
      <td>65.0</td>
      <td>70.0</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>32.7</td>
      <td>5.4</td>
      <td>...</td>
      <td>Slovakia</td>
      <td>38</td>
      <td>53.0</td>
      <td>47.0</td>
      <td>21.0</td>
      <td>108.0</td>
      <td>142.0</td>
      <td>70.0</td>
      <td>35.0</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>115</th>
      <td>149</td>
      <td>Slovenia</td>
      <td>Europe</td>
      <td>58.0</td>
      <td>65.5</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>17.0</td>
      <td>37.0</td>
      <td>2.1</td>
      <td>...</td>
      <td>Slovenia</td>
      <td>44</td>
      <td>114.0</td>
      <td>71.0</td>
      <td>14.0</td>
      <td>13.0</td>
      <td>97.0</td>
      <td>54.0</td>
      <td>34.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>151</td>
      <td>South Africa</td>
      <td>Sub-Saharan Africa</td>
      <td>102.0</td>
      <td>58.3</td>
      <td>50.0</td>
      <td>45.0</td>
      <td>28.0</td>
      <td>31.3</td>
      <td>56.5</td>
      <td>...</td>
      <td>South Africa</td>
      <td>106</td>
      <td>40.0</td>
      <td>80.0</td>
      <td>63.0</td>
      <td>85.0</td>
      <td>102.0</td>
      <td>89.0</td>
      <td>77.0</td>
      <td>123.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>152</td>
      <td>Spain</td>
      <td>Europe</td>
      <td>57.0</td>
      <td>65.7</td>
      <td>70.0</td>
      <td>45.0</td>
      <td>25.0</td>
      <td>33.5</td>
      <td>46.3</td>
      <td>...</td>
      <td>Spain</td>
      <td>30</td>
      <td>107.0</td>
      <td>107.0</td>
      <td>26.0</td>
      <td>95.0</td>
      <td>78.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>153</td>
      <td>Sri Lanka</td>
      <td>Asia-Pacific</td>
      <td>115.0</td>
      <td>56.4</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>28.0</td>
      <td>12.3</td>
      <td>21.4</td>
      <td>...</td>
      <td>Sri Lanka</td>
      <td>130</td>
      <td>32.0</td>
      <td>81.0</td>
      <td>80.0</td>
      <td>55.0</td>
      <td>111.0</td>
      <td>35.0</td>
      <td>79.0</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>157</td>
      <td>Sweden</td>
      <td>Europe</td>
      <td>19.0</td>
      <td>75.2</td>
      <td>80.0</td>
      <td>57.0</td>
      <td>22.0</td>
      <td>44.1</td>
      <td>10.1</td>
      <td>...</td>
      <td>Sweden</td>
      <td>7</td>
      <td>34.0</td>
      <td>8.0</td>
      <td>25.0</td>
      <td>10.0</td>
      <td>6.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>120</th>
      <td>158</td>
      <td>Switzerland</td>
      <td>Europe</td>
      <td>4.0</td>
      <td>81.9</td>
      <td>90.0</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>27.8</td>
      <td>8.4</td>
      <td>...</td>
      <td>Switzerland</td>
      <td>6</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>13.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>160</td>
      <td>Taiwan</td>
      <td>Asia-Pacific</td>
      <td>10.0</td>
      <td>77.3</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>8.9</td>
      <td>23.6</td>
      <td>...</td>
      <td>Taiwan</td>
      <td>25</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>48.0</td>
      <td>102.0</td>
      <td>56.0</td>
      <td>56.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>122</th>
      <td>161</td>
      <td>Tajikistan</td>
      <td>Asia-Pacific</td>
      <td>122.0</td>
      <td>55.6</td>
      <td>30.0</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>20.6</td>
      <td>8.8</td>
      <td>...</td>
      <td>Tajikistan</td>
      <td>74</td>
      <td>120.0</td>
      <td>54.0</td>
      <td>113.0</td>
      <td>86.0</td>
      <td>35.0</td>
      <td>72.0</td>
      <td>123.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>123</th>
      <td>162</td>
      <td>Tanzania</td>
      <td>Sub-Saharan Africa</td>
      <td>94.0</td>
      <td>60.2</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>12.4</td>
      <td>50</td>
      <td>...</td>
      <td>Tanzania</td>
      <td>153</td>
      <td>78.0</td>
      <td>50.0</td>
      <td>131.0</td>
      <td>78.0</td>
      <td>34.0</td>
      <td>49.0</td>
      <td>125.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>124</th>
      <td>163</td>
      <td>Thailand</td>
      <td>Asia-Pacific</td>
      <td>43.0</td>
      <td>68.3</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>20.0</td>
      <td>15.6</td>
      <td>69.1</td>
      <td>...</td>
      <td>Thailand</td>
      <td>52</td>
      <td>20.0</td>
      <td>35.0</td>
      <td>53.0</td>
      <td>18.0</td>
      <td>131.0</td>
      <td>10.0</td>
      <td>62.0</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>125</th>
      <td>165</td>
      <td>Togo</td>
      <td>Sub-Saharan Africa</td>
      <td>158.0</td>
      <td>50.3</td>
      <td>30.0</td>
      <td>45.0</td>
      <td>27.0</td>
      <td>21.5</td>
      <td>7.8</td>
      <td>...</td>
      <td>Togo</td>
      <td>139</td>
      <td>123.0</td>
      <td>147.0</td>
      <td>149.0</td>
      <td>120.0</td>
      <td>72.0</td>
      <td>131.0</td>
      <td>142.0</td>
      <td>132.0</td>
    </tr>
    <tr>
      <th>126</th>
      <td>167</td>
      <td>Trinidad and Tobago</td>
      <td>Americas</td>
      <td>112.0</td>
      <td>57.0</td>
      <td>50.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>22.8</td>
      <td>1.4</td>
      <td>...</td>
      <td>Trinidad and Tobago</td>
      <td>39</td>
      <td>14.0</td>
      <td>52.0</td>
      <td>29.0</td>
      <td>51.0</td>
      <td>141.0</td>
      <td>41.0</td>
      <td>38.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>127</th>
      <td>168</td>
      <td>Tunisia</td>
      <td>Middle East and North Africa</td>
      <td>125.0</td>
      <td>55.4</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>20.8</td>
      <td>11.5</td>
      <td>...</td>
      <td>Tunisia</td>
      <td>124</td>
      <td>147.0</td>
      <td>132.0</td>
      <td>121.0</td>
      <td>143.0</td>
      <td>101.0</td>
      <td>144.0</td>
      <td>84.0</td>
      <td>67.0</td>
    </tr>
    <tr>
      <th>128</th>
      <td>169</td>
      <td>Turkey</td>
      <td>Europe</td>
      <td>68.0</td>
      <td>64.6</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>22.0</td>
      <td>25.5</td>
      <td>80.8</td>
      <td>...</td>
      <td>Turkey</td>
      <td>79</td>
      <td>154.0</td>
      <td>121.0</td>
      <td>61.0</td>
      <td>140.0</td>
      <td>50.0</td>
      <td>98.0</td>
      <td>44.0</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>129</th>
      <td>170</td>
      <td>Turkmenistan</td>
      <td>Asia-Pacific</td>
      <td>164.0</td>
      <td>48.4</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>15.6</td>
      <td>5.7</td>
      <td>...</td>
      <td>Turkmenistan</td>
      <td>87</td>
      <td>135.0</td>
      <td>63.0</td>
      <td>8.0</td>
      <td>83.0</td>
      <td>NaN</td>
      <td>33.0</td>
      <td>60.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>130</th>
      <td>171</td>
      <td>Uganda</td>
      <td>Sub-Saharan Africa</td>
      <td>95.0</td>
      <td>59.7</td>
      <td>40.0</td>
      <td>40.0</td>
      <td>30.0</td>
      <td>12.9</td>
      <td>37.7</td>
      <td>...</td>
      <td>Uganda</td>
      <td>136</td>
      <td>91.0</td>
      <td>139.0</td>
      <td>114.0</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>74.0</td>
      <td>136.0</td>
      <td>127.0</td>
    </tr>
    <tr>
      <th>131</th>
      <td>172</td>
      <td>Ukraine</td>
      <td>Europe</td>
      <td>147.0</td>
      <td>52.3</td>
      <td>30.0</td>
      <td>20.0</td>
      <td>18.0</td>
      <td>33.1</td>
      <td>42.3</td>
      <td>...</td>
      <td>Ukraine</td>
      <td>133</td>
      <td>131.0</td>
      <td>44.0</td>
      <td>56.0</td>
      <td>141.0</td>
      <td>143.0</td>
      <td>66.0</td>
      <td>94.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>132</th>
      <td>173</td>
      <td>United Arab Emirates</td>
      <td>Middle East and North Africa</td>
      <td>9.0</td>
      <td>77.6</td>
      <td>60.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.9</td>
      <td>10.1</td>
      <td>...</td>
      <td>United Arab Emirates</td>
      <td>21</td>
      <td>43.0</td>
      <td>56.0</td>
      <td>72.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>133</th>
      <td>174</td>
      <td>United Kingdom</td>
      <td>Europe</td>
      <td>7.0</td>
      <td>78.9</td>
      <td>80.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>33.2</td>
      <td>66.1</td>
      <td>...</td>
      <td>United Kingdom</td>
      <td>15</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>9.0</td>
      <td>63.0</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>23.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>134</th>
      <td>175</td>
      <td>United States</td>
      <td>Americas</td>
      <td>12.0</td>
      <td>76.8</td>
      <td>80.0</td>
      <td>37.0</td>
      <td>21.0</td>
      <td>26.0</td>
      <td>325.9</td>
      <td>...</td>
      <td>United States</td>
      <td>19</td>
      <td>35.0</td>
      <td>70.0</td>
      <td>37.0</td>
      <td>62.0</td>
      <td>42.0</td>
      <td>12.0</td>
      <td>10.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>135</th>
      <td>176</td>
      <td>Uruguay</td>
      <td>Americas</td>
      <td>40.0</td>
      <td>68.6</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>27.4</td>
      <td>3.5</td>
      <td>...</td>
      <td>Uruguay</td>
      <td>33</td>
      <td>10.0</td>
      <td>76.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>33.0</td>
      <td>80.0</td>
      <td>52.0</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>136</th>
      <td>177</td>
      <td>Uzbekistan</td>
      <td>Asia-Pacific</td>
      <td>140.0</td>
      <td>53.3</td>
      <td>10.0</td>
      <td>22.0</td>
      <td>7.5</td>
      <td>18.2</td>
      <td>32.1</td>
      <td>...</td>
      <td>Uzbekistan</td>
      <td>41</td>
      <td>19.0</td>
      <td>15.0</td>
      <td>11.0</td>
      <td>1.0</td>
      <td>18.0</td>
      <td>29.0</td>
      <td>104.0</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>137</th>
      <td>179</td>
      <td>Venezuela</td>
      <td>Americas</td>
      <td>179.0</td>
      <td>25.9</td>
      <td>10.0</td>
      <td>34.0</td>
      <td>34.0</td>
      <td>14.9</td>
      <td>31.4</td>
      <td>...</td>
      <td>Venezuela</td>
      <td>108</td>
      <td>77.0</td>
      <td>135.0</td>
      <td>49.0</td>
      <td>145.0</td>
      <td>110.0</td>
      <td>139.0</td>
      <td>78.0</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>138</th>
      <td>180</td>
      <td>Vietnam</td>
      <td>Asia-Pacific</td>
      <td>128.0</td>
      <td>55.3</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>22.0</td>
      <td>18.0</td>
      <td>93.6</td>
      <td>...</td>
      <td>Vietnam</td>
      <td>94</td>
      <td>121.0</td>
      <td>27.0</td>
      <td>64.0</td>
      <td>23.0</td>
      <td>86.0</td>
      <td>97.0</td>
      <td>105.0</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>139</th>
      <td>182</td>
      <td>Zambia</td>
      <td>Sub-Saharan Africa</td>
      <td>138.0</td>
      <td>53.6</td>
      <td>50.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>17.9</td>
      <td>17.2</td>
      <td>...</td>
      <td>Zambia</td>
      <td>138</td>
      <td>84.0</td>
      <td>128.0</td>
      <td>115.0</td>
      <td>73.0</td>
      <td>69.0</td>
      <td>53.0</td>
      <td>115.0</td>
      <td>131.0</td>
    </tr>
    <tr>
      <th>140</th>
      <td>183</td>
      <td>Zimbabwe</td>
      <td>Sub-Saharan Africa</td>
      <td>175.0</td>
      <td>40.4</td>
      <td>10.0</td>
      <td>51.5</td>
      <td>25.0</td>
      <td>22.3</td>
      <td>14.9</td>
      <td>...</td>
      <td>Zimbabwe</td>
      <td>146</td>
      <td>63.0</td>
      <td>34.0</td>
      <td>110.0</td>
      <td>96.0</td>
      <td>63.0</td>
      <td>141.0</td>
      <td>131.0</td>
      <td>129.0</td>
    </tr>
  </tbody>
</table>
<p>141 rows × 24 columns</p>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>Population_in_Millions</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Afghanistan</td>
      <td>Asia-Pacific</td>
      <td>152.0</td>
      <td>51.5</td>
      <td>10.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>5.0</td>
      <td>35.5</td>
      <td>...</td>
      <td>Afghanistan</td>
      <td>154</td>
      <td>152.0</td>
      <td>133.0</td>
      <td>151.0</td>
      <td>155.0</td>
      <td>136.0</td>
      <td>137.0</td>
      <td>134.0</td>
      <td>139.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Albania</td>
      <td>Europe</td>
      <td>52.0</td>
      <td>66.5</td>
      <td>70.0</td>
      <td>23.0</td>
      <td>15.0</td>
      <td>24.9</td>
      <td>2.9</td>
      <td>...</td>
      <td>Albania</td>
      <td>107</td>
      <td>90.0</td>
      <td>108.0</td>
      <td>133.0</td>
      <td>87.0</td>
      <td>134.0</td>
      <td>60.0</td>
      <td>81.0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Algeria</td>
      <td>Middle East and North Africa</td>
      <td>171.0</td>
      <td>46.2</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>24.5</td>
      <td>41.5</td>
      <td>...</td>
      <td>Algeria</td>
      <td>88</td>
      <td>113.0</td>
      <td>106.0</td>
      <td>101.0</td>
      <td>149.0</td>
      <td>46.0</td>
      <td>128.0</td>
      <td>72.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>Argentina</td>
      <td>Americas</td>
      <td>148.0</td>
      <td>52.2</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>30.8</td>
      <td>44.1</td>
      <td>...</td>
      <td>Argentina</td>
      <td>47</td>
      <td>28.0</td>
      <td>93.0</td>
      <td>46.0</td>
      <td>54.0</td>
      <td>109.0</td>
      <td>123.0</td>
      <td>55.0</td>
      <td>37.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>Armenia</td>
      <td>Europe</td>
      <td>47.0</td>
      <td>67.7</td>
      <td>70.0</td>
      <td>26.0</td>
      <td>20.0</td>
      <td>21.3</td>
      <td>3</td>
      <td>...</td>
      <td>Armenia</td>
      <td>116</td>
      <td>126.0</td>
      <td>145.0</td>
      <td>117.0</td>
      <td>123.0</td>
      <td>93.0</td>
      <td>129.0</td>
      <td>91.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>Australia</td>
      <td>Asia-Pacific</td>
      <td>5.0</td>
      <td>80.9</td>
      <td>90.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>28.2</td>
      <td>24.8</td>
      <td>...</td>
      <td>Australia</td>
      <td>11</td>
      <td>47.0</td>
      <td>37.0</td>
      <td>7.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>Austria</td>
      <td>Europe</td>
      <td>31.0</td>
      <td>72.0</td>
      <td>70.0</td>
      <td>50.0</td>
      <td>25.0</td>
      <td>42.7</td>
      <td>8.8</td>
      <td>...</td>
      <td>Austria</td>
      <td>10</td>
      <td>64.0</td>
      <td>24.0</td>
      <td>31.0</td>
      <td>26.0</td>
      <td>19.0</td>
      <td>25.0</td>
      <td>16.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>9</td>
      <td>Azerbaijan</td>
      <td>Asia-Pacific</td>
      <td>60.0</td>
      <td>65.4</td>
      <td>60.0</td>
      <td>25.0</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>9.8</td>
      <td>...</td>
      <td>Azerbaijan</td>
      <td>90</td>
      <td>134.0</td>
      <td>20.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>22.0</td>
      <td>146.0</td>
      <td>65.0</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>11</td>
      <td>Bahrain</td>
      <td>Middle East and North Africa</td>
      <td>54.0</td>
      <td>66.4</td>
      <td>80.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.6</td>
      <td>1.5</td>
      <td>...</td>
      <td>Bahrain</td>
      <td>37</td>
      <td>39.0</td>
      <td>83.0</td>
      <td>59.0</td>
      <td>24.0</td>
      <td>NaN</td>
      <td>23.0</td>
      <td>20.0</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>12</td>
      <td>Bangladesh</td>
      <td>Asia-Pacific</td>
      <td>121.0</td>
      <td>55.6</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>8.8</td>
      <td>163.2</td>
      <td>...</td>
      <td>Bangladesh</td>
      <td>125</td>
      <td>145.0</td>
      <td>68.0</td>
      <td>126.0</td>
      <td>27.0</td>
      <td>36.0</td>
      <td>107.0</td>
      <td>119.0</td>
      <td>90.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>14</td>
      <td>Belarus</td>
      <td>Europe</td>
      <td>104.0</td>
      <td>57.9</td>
      <td>10.0</td>
      <td>13.0</td>
      <td>18.0</td>
      <td>23.8</td>
      <td>9.5</td>
      <td>...</td>
      <td>Belarus</td>
      <td>81</td>
      <td>149.0</td>
      <td>36.0</td>
      <td>33.0</td>
      <td>131.0</td>
      <td>37.0</td>
      <td>103.0</td>
      <td>58.0</td>
      <td>76.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15</td>
      <td>Belgium</td>
      <td>Europe</td>
      <td>48.0</td>
      <td>67.3</td>
      <td>70.0</td>
      <td>50.0</td>
      <td>29.0</td>
      <td>44.2</td>
      <td>11.4</td>
      <td>...</td>
      <td>Belgium</td>
      <td>18</td>
      <td>57.0</td>
      <td>53.0</td>
      <td>22.0</td>
      <td>53.0</td>
      <td>20.0</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>17</td>
      <td>Benin</td>
      <td>Sub-Saharan Africa</td>
      <td>127.0</td>
      <td>55.3</td>
      <td>50.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>11.9</td>
      <td>11.1</td>
      <td>...</td>
      <td>Benin</td>
      <td>102</td>
      <td>118.0</td>
      <td>148.0</td>
      <td>153.0</td>
      <td>103.0</td>
      <td>75.0</td>
      <td>116.0</td>
      <td>128.0</td>
      <td>133.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>18</td>
      <td>Bhutan</td>
      <td>Asia-Pacific</td>
      <td>74.0</td>
      <td>62.9</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>30.0</td>
      <td>13.4</td>
      <td>0.8</td>
      <td>...</td>
      <td>Bhutan</td>
      <td>95</td>
      <td>37.0</td>
      <td>98.0</td>
      <td>68.0</td>
      <td>59.0</td>
      <td>25.0</td>
      <td>13.0</td>
      <td>95.0</td>
      <td>104.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>19</td>
      <td>Bolivia</td>
      <td>Americas</td>
      <td>173.0</td>
      <td>42.3</td>
      <td>40.0</td>
      <td>13.0</td>
      <td>25.0</td>
      <td>31.1</td>
      <td>11.1</td>
      <td>...</td>
      <td>Bolivia</td>
      <td>61</td>
      <td>70.0</td>
      <td>138.0</td>
      <td>93.0</td>
      <td>35.0</td>
      <td>91.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20</td>
      <td>Bosnia and Herzegovina</td>
      <td>Europe</td>
      <td>83.0</td>
      <td>61.9</td>
      <td>60.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>37.0</td>
      <td>3.5</td>
      <td>...</td>
      <td>Bosnia and Herzegovina</td>
      <td>78</td>
      <td>116.0</td>
      <td>79.0</td>
      <td>92.0</td>
      <td>137.0</td>
      <td>145.0</td>
      <td>32.0</td>
      <td>82.0</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>21</td>
      <td>Botswana</td>
      <td>Sub-Saharan Africa</td>
      <td>36.0</td>
      <td>69.5</td>
      <td>70.0</td>
      <td>25.0</td>
      <td>22.0</td>
      <td>24.9</td>
      <td>2.2</td>
      <td>...</td>
      <td>Botswana</td>
      <td>148</td>
      <td>87.0</td>
      <td>65.0</td>
      <td>105.0</td>
      <td>60.0</td>
      <td>54.0</td>
      <td>150.0</td>
      <td>66.0</td>
      <td>113.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Brazil</td>
      <td>Americas</td>
      <td>150.0</td>
      <td>51.9</td>
      <td>50.0</td>
      <td>27.5</td>
      <td>34.0</td>
      <td>32.2</td>
      <td>207.7</td>
      <td>...</td>
      <td>Brazil</td>
      <td>32</td>
      <td>69.0</td>
      <td>105.0</td>
      <td>43.0</td>
      <td>84.0</td>
      <td>71.0</td>
      <td>108.0</td>
      <td>70.0</td>
      <td>72.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>23</td>
      <td>Bulgaria</td>
      <td>Europe</td>
      <td>37.0</td>
      <td>69.0</td>
      <td>60.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>28.0</td>
      <td>7.1</td>
      <td>...</td>
      <td>Bulgaria</td>
      <td>97</td>
      <td>117.0</td>
      <td>13.0</td>
      <td>18.0</td>
      <td>115.0</td>
      <td>147.0</td>
      <td>112.0</td>
      <td>56.0</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>24</td>
      <td>Burkina Faso</td>
      <td>Sub-Saharan Africa</td>
      <td>96.0</td>
      <td>59.4</td>
      <td>40.0</td>
      <td>27.5</td>
      <td>28.0</td>
      <td>16.3</td>
      <td>18.9</td>
      <td>...</td>
      <td>Burkina Faso</td>
      <td>115</td>
      <td>115.0</td>
      <td>117.0</td>
      <td>116.0</td>
      <td>127.0</td>
      <td>47.0</td>
      <td>125.0</td>
      <td>137.0</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>26</td>
      <td>Burundi</td>
      <td>Sub-Saharan Africa</td>
      <td>162.0</td>
      <td>48.9</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>12.3</td>
      <td>10.9</td>
      <td>...</td>
      <td>Burundi</td>
      <td>145</td>
      <td>98.0</td>
      <td>126.0</td>
      <td>152.0</td>
      <td>135.0</td>
      <td>23.0</td>
      <td>149.0</td>
      <td>151.0</td>
      <td>135.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>27</td>
      <td>Cambodia</td>
      <td>Asia-Pacific</td>
      <td>105.0</td>
      <td>57.8</td>
      <td>50.0</td>
      <td>20.0</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>16</td>
      <td>...</td>
      <td>Cambodia</td>
      <td>109</td>
      <td>27.0</td>
      <td>142.0</td>
      <td>109.0</td>
      <td>2.0</td>
      <td>94.0</td>
      <td>61.0</td>
      <td>116.0</td>
      <td>102.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>28</td>
      <td>Cameroon</td>
      <td>Sub-Saharan Africa</td>
      <td>145.0</td>
      <td>52.4</td>
      <td>50.0</td>
      <td>35.0</td>
      <td>33.0</td>
      <td>15.6</td>
      <td>24.3</td>
      <td>...</td>
      <td>Cameroon</td>
      <td>96</td>
      <td>106.0</td>
      <td>129.0</td>
      <td>129.0</td>
      <td>90.0</td>
      <td>120.0</td>
      <td>91.0</td>
      <td>121.0</td>
      <td>141.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>29</td>
      <td>Canada</td>
      <td>Americas</td>
      <td>8.0</td>
      <td>77.7</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>15.0</td>
      <td>31.7</td>
      <td>36.7</td>
      <td>...</td>
      <td>Canada</td>
      <td>9</td>
      <td>18.0</td>
      <td>49.0</td>
      <td>20.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>31</td>
      <td>Central African Republic</td>
      <td>Sub-Saharan Africa</td>
      <td>161.0</td>
      <td>49.1</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>9.0</td>
      <td>5</td>
      <td>...</td>
      <td>Central African Republic</td>
      <td>155</td>
      <td>132.0</td>
      <td>153.0</td>
      <td>155.0</td>
      <td>133.0</td>
      <td>122.0</td>
      <td>113.0</td>
      <td>152.0</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>32</td>
      <td>Chad</td>
      <td>Sub-Saharan Africa</td>
      <td>159.0</td>
      <td>49.9</td>
      <td>40.0</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>5.3</td>
      <td>12.2</td>
      <td>...</td>
      <td>Chad</td>
      <td>132</td>
      <td>136.0</td>
      <td>151.0</td>
      <td>141.0</td>
      <td>142.0</td>
      <td>80.0</td>
      <td>106.0</td>
      <td>133.0</td>
      <td>148.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>33</td>
      <td>Chile</td>
      <td>Americas</td>
      <td>18.0</td>
      <td>75.4</td>
      <td>70.0</td>
      <td>35.0</td>
      <td>25.0</td>
      <td>20.4</td>
      <td>18.4</td>
      <td>...</td>
      <td>Chile</td>
      <td>26</td>
      <td>15.0</td>
      <td>78.0</td>
      <td>58.0</td>
      <td>98.0</td>
      <td>99.0</td>
      <td>45.0</td>
      <td>49.0</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>34</td>
      <td>China</td>
      <td>Asia-Pacific</td>
      <td>100.0</td>
      <td>58.4</td>
      <td>20.0</td>
      <td>45.0</td>
      <td>25.0</td>
      <td>17.5</td>
      <td>1390.1</td>
      <td>...</td>
      <td>China</td>
      <td>93</td>
      <td>21.0</td>
      <td>11.0</td>
      <td>108.0</td>
      <td>31.0</td>
      <td>NaN</td>
      <td>133.0</td>
      <td>68.0</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>35</td>
      <td>Colombia</td>
      <td>Americas</td>
      <td>49.0</td>
      <td>67.3</td>
      <td>70.0</td>
      <td>33.0</td>
      <td>33.0</td>
      <td>19.9</td>
      <td>49.3</td>
      <td>...</td>
      <td>Colombia</td>
      <td>43</td>
      <td>30.0</td>
      <td>88.0</td>
      <td>52.0</td>
      <td>56.0</td>
      <td>124.0</td>
      <td>111.0</td>
      <td>74.0</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>36</td>
      <td>Comoros</td>
      <td>Sub-Saharan Africa</td>
      <td>124.0</td>
      <td>55.4</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>14.5</td>
      <td>0.8</td>
      <td>...</td>
      <td>Comoros</td>
      <td>142</td>
      <td>67.0</td>
      <td>114.0</td>
      <td>143.0</td>
      <td>148.0</td>
      <td>81.0</td>
      <td>62.0</td>
      <td>143.0</td>
      <td>117.0</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>111</th>
      <td>144</td>
      <td>Serbia</td>
      <td>Europe</td>
      <td>69.0</td>
      <td>63.9</td>
      <td>50.0</td>
      <td>10.0</td>
      <td>15.0</td>
      <td>38.4</td>
      <td>7</td>
      <td>...</td>
      <td>Serbia</td>
      <td>70</td>
      <td>148.0</td>
      <td>92.0</td>
      <td>57.0</td>
      <td>124.0</td>
      <td>118.0</td>
      <td>84.0</td>
      <td>71.0</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>112</th>
      <td>146</td>
      <td>Sierra Leone</td>
      <td>Sub-Saharan Africa</td>
      <td>167.0</td>
      <td>47.5</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>30.0</td>
      <td>12.2</td>
      <td>7.4</td>
      <td>...</td>
      <td>Sierra Leone</td>
      <td>129</td>
      <td>139.0</td>
      <td>149.0</td>
      <td>135.0</td>
      <td>116.0</td>
      <td>112.0</td>
      <td>79.0</td>
      <td>145.0</td>
      <td>146.0</td>
    </tr>
    <tr>
      <th>113</th>
      <td>147</td>
      <td>Singapore</td>
      <td>Asia-Pacific</td>
      <td>2.0</td>
      <td>89.4</td>
      <td>80.0</td>
      <td>22.0</td>
      <td>17.0</td>
      <td>13.7</td>
      <td>5.6</td>
      <td>...</td>
      <td>Singapore</td>
      <td>34</td>
      <td>38.0</td>
      <td>2.0</td>
      <td>36.0</td>
      <td>20.0</td>
      <td>1.0</td>
      <td>21.0</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>114</th>
      <td>148</td>
      <td>Slovakia</td>
      <td>Europe</td>
      <td>65.0</td>
      <td>65.0</td>
      <td>70.0</td>
      <td>25.0</td>
      <td>21.0</td>
      <td>32.7</td>
      <td>5.4</td>
      <td>...</td>
      <td>Slovakia</td>
      <td>38</td>
      <td>53.0</td>
      <td>47.0</td>
      <td>21.0</td>
      <td>108.0</td>
      <td>142.0</td>
      <td>70.0</td>
      <td>35.0</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>115</th>
      <td>149</td>
      <td>Slovenia</td>
      <td>Europe</td>
      <td>58.0</td>
      <td>65.5</td>
      <td>50.0</td>
      <td>50.0</td>
      <td>17.0</td>
      <td>37.0</td>
      <td>2.1</td>
      <td>...</td>
      <td>Slovenia</td>
      <td>44</td>
      <td>114.0</td>
      <td>71.0</td>
      <td>14.0</td>
      <td>13.0</td>
      <td>97.0</td>
      <td>54.0</td>
      <td>34.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>151</td>
      <td>South Africa</td>
      <td>Sub-Saharan Africa</td>
      <td>102.0</td>
      <td>58.3</td>
      <td>50.0</td>
      <td>45.0</td>
      <td>28.0</td>
      <td>31.3</td>
      <td>56.5</td>
      <td>...</td>
      <td>South Africa</td>
      <td>106</td>
      <td>40.0</td>
      <td>80.0</td>
      <td>63.0</td>
      <td>85.0</td>
      <td>102.0</td>
      <td>89.0</td>
      <td>77.0</td>
      <td>123.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>152</td>
      <td>Spain</td>
      <td>Europe</td>
      <td>57.0</td>
      <td>65.7</td>
      <td>70.0</td>
      <td>45.0</td>
      <td>25.0</td>
      <td>33.5</td>
      <td>46.3</td>
      <td>...</td>
      <td>Spain</td>
      <td>30</td>
      <td>107.0</td>
      <td>107.0</td>
      <td>26.0</td>
      <td>95.0</td>
      <td>78.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>153</td>
      <td>Sri Lanka</td>
      <td>Asia-Pacific</td>
      <td>115.0</td>
      <td>56.4</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>28.0</td>
      <td>12.3</td>
      <td>21.4</td>
      <td>...</td>
      <td>Sri Lanka</td>
      <td>130</td>
      <td>32.0</td>
      <td>81.0</td>
      <td>80.0</td>
      <td>55.0</td>
      <td>111.0</td>
      <td>35.0</td>
      <td>79.0</td>
      <td>54.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>157</td>
      <td>Sweden</td>
      <td>Europe</td>
      <td>19.0</td>
      <td>75.2</td>
      <td>80.0</td>
      <td>57.0</td>
      <td>22.0</td>
      <td>44.1</td>
      <td>10.1</td>
      <td>...</td>
      <td>Sweden</td>
      <td>7</td>
      <td>34.0</td>
      <td>8.0</td>
      <td>25.0</td>
      <td>10.0</td>
      <td>6.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>17.0</td>
    </tr>
    <tr>
      <th>120</th>
      <td>158</td>
      <td>Switzerland</td>
      <td>Europe</td>
      <td>4.0</td>
      <td>81.9</td>
      <td>90.0</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>27.8</td>
      <td>8.4</td>
      <td>...</td>
      <td>Switzerland</td>
      <td>6</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>13.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>160</td>
      <td>Taiwan</td>
      <td>Asia-Pacific</td>
      <td>10.0</td>
      <td>77.3</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>8.9</td>
      <td>23.6</td>
      <td>...</td>
      <td>Taiwan</td>
      <td>25</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>48.0</td>
      <td>102.0</td>
      <td>56.0</td>
      <td>56.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>122</th>
      <td>161</td>
      <td>Tajikistan</td>
      <td>Asia-Pacific</td>
      <td>122.0</td>
      <td>55.6</td>
      <td>30.0</td>
      <td>13.0</td>
      <td>15.0</td>
      <td>20.6</td>
      <td>8.8</td>
      <td>...</td>
      <td>Tajikistan</td>
      <td>74</td>
      <td>120.0</td>
      <td>54.0</td>
      <td>113.0</td>
      <td>86.0</td>
      <td>35.0</td>
      <td>72.0</td>
      <td>123.0</td>
      <td>92.0</td>
    </tr>
    <tr>
      <th>123</th>
      <td>162</td>
      <td>Tanzania</td>
      <td>Sub-Saharan Africa</td>
      <td>94.0</td>
      <td>60.2</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>12.4</td>
      <td>50</td>
      <td>...</td>
      <td>Tanzania</td>
      <td>153</td>
      <td>78.0</td>
      <td>50.0</td>
      <td>131.0</td>
      <td>78.0</td>
      <td>34.0</td>
      <td>49.0</td>
      <td>125.0</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>124</th>
      <td>163</td>
      <td>Thailand</td>
      <td>Asia-Pacific</td>
      <td>43.0</td>
      <td>68.3</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>20.0</td>
      <td>15.6</td>
      <td>69.1</td>
      <td>...</td>
      <td>Thailand</td>
      <td>52</td>
      <td>20.0</td>
      <td>35.0</td>
      <td>53.0</td>
      <td>18.0</td>
      <td>131.0</td>
      <td>10.0</td>
      <td>62.0</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>125</th>
      <td>165</td>
      <td>Togo</td>
      <td>Sub-Saharan Africa</td>
      <td>158.0</td>
      <td>50.3</td>
      <td>30.0</td>
      <td>45.0</td>
      <td>27.0</td>
      <td>21.5</td>
      <td>7.8</td>
      <td>...</td>
      <td>Togo</td>
      <td>139</td>
      <td>123.0</td>
      <td>147.0</td>
      <td>149.0</td>
      <td>120.0</td>
      <td>72.0</td>
      <td>131.0</td>
      <td>142.0</td>
      <td>132.0</td>
    </tr>
    <tr>
      <th>126</th>
      <td>167</td>
      <td>Trinidad and Tobago</td>
      <td>Americas</td>
      <td>112.0</td>
      <td>57.0</td>
      <td>50.0</td>
      <td>25.0</td>
      <td>25.0</td>
      <td>22.8</td>
      <td>1.4</td>
      <td>...</td>
      <td>Trinidad and Tobago</td>
      <td>39</td>
      <td>14.0</td>
      <td>52.0</td>
      <td>29.0</td>
      <td>51.0</td>
      <td>141.0</td>
      <td>41.0</td>
      <td>38.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>127</th>
      <td>168</td>
      <td>Tunisia</td>
      <td>Middle East and North Africa</td>
      <td>125.0</td>
      <td>55.4</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>20.8</td>
      <td>11.5</td>
      <td>...</td>
      <td>Tunisia</td>
      <td>124</td>
      <td>147.0</td>
      <td>132.0</td>
      <td>121.0</td>
      <td>143.0</td>
      <td>101.0</td>
      <td>144.0</td>
      <td>84.0</td>
      <td>67.0</td>
    </tr>
    <tr>
      <th>128</th>
      <td>169</td>
      <td>Turkey</td>
      <td>Europe</td>
      <td>68.0</td>
      <td>64.6</td>
      <td>60.0</td>
      <td>35.0</td>
      <td>22.0</td>
      <td>25.5</td>
      <td>80.8</td>
      <td>...</td>
      <td>Turkey</td>
      <td>79</td>
      <td>154.0</td>
      <td>121.0</td>
      <td>61.0</td>
      <td>140.0</td>
      <td>50.0</td>
      <td>98.0</td>
      <td>44.0</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>129</th>
      <td>170</td>
      <td>Turkmenistan</td>
      <td>Asia-Pacific</td>
      <td>164.0</td>
      <td>48.4</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>15.6</td>
      <td>5.7</td>
      <td>...</td>
      <td>Turkmenistan</td>
      <td>87</td>
      <td>135.0</td>
      <td>63.0</td>
      <td>8.0</td>
      <td>83.0</td>
      <td>NaN</td>
      <td>33.0</td>
      <td>60.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>130</th>
      <td>171</td>
      <td>Uganda</td>
      <td>Sub-Saharan Africa</td>
      <td>95.0</td>
      <td>59.7</td>
      <td>40.0</td>
      <td>40.0</td>
      <td>30.0</td>
      <td>12.9</td>
      <td>37.7</td>
      <td>...</td>
      <td>Uganda</td>
      <td>136</td>
      <td>91.0</td>
      <td>139.0</td>
      <td>114.0</td>
      <td>99.0</td>
      <td>95.0</td>
      <td>74.0</td>
      <td>136.0</td>
      <td>127.0</td>
    </tr>
    <tr>
      <th>131</th>
      <td>172</td>
      <td>Ukraine</td>
      <td>Europe</td>
      <td>147.0</td>
      <td>52.3</td>
      <td>30.0</td>
      <td>20.0</td>
      <td>18.0</td>
      <td>33.1</td>
      <td>42.3</td>
      <td>...</td>
      <td>Ukraine</td>
      <td>133</td>
      <td>131.0</td>
      <td>44.0</td>
      <td>56.0</td>
      <td>141.0</td>
      <td>143.0</td>
      <td>66.0</td>
      <td>94.0</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>132</th>
      <td>173</td>
      <td>United Arab Emirates</td>
      <td>Middle East and North Africa</td>
      <td>9.0</td>
      <td>77.6</td>
      <td>60.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.9</td>
      <td>10.1</td>
      <td>...</td>
      <td>United Arab Emirates</td>
      <td>21</td>
      <td>43.0</td>
      <td>56.0</td>
      <td>72.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>133</th>
      <td>174</td>
      <td>United Kingdom</td>
      <td>Europe</td>
      <td>7.0</td>
      <td>78.9</td>
      <td>80.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>33.2</td>
      <td>66.1</td>
      <td>...</td>
      <td>United Kingdom</td>
      <td>15</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>9.0</td>
      <td>63.0</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>23.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>134</th>
      <td>175</td>
      <td>United States</td>
      <td>Americas</td>
      <td>12.0</td>
      <td>76.8</td>
      <td>80.0</td>
      <td>37.0</td>
      <td>21.0</td>
      <td>26.0</td>
      <td>325.9</td>
      <td>...</td>
      <td>United States</td>
      <td>19</td>
      <td>35.0</td>
      <td>70.0</td>
      <td>37.0</td>
      <td>62.0</td>
      <td>42.0</td>
      <td>12.0</td>
      <td>10.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>135</th>
      <td>176</td>
      <td>Uruguay</td>
      <td>Americas</td>
      <td>40.0</td>
      <td>68.6</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>25.0</td>
      <td>27.4</td>
      <td>3.5</td>
      <td>...</td>
      <td>Uruguay</td>
      <td>33</td>
      <td>10.0</td>
      <td>76.0</td>
      <td>35.0</td>
      <td>30.0</td>
      <td>33.0</td>
      <td>80.0</td>
      <td>52.0</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>136</th>
      <td>177</td>
      <td>Uzbekistan</td>
      <td>Asia-Pacific</td>
      <td>140.0</td>
      <td>53.3</td>
      <td>10.0</td>
      <td>22.0</td>
      <td>7.5</td>
      <td>18.2</td>
      <td>32.1</td>
      <td>...</td>
      <td>Uzbekistan</td>
      <td>41</td>
      <td>19.0</td>
      <td>15.0</td>
      <td>11.0</td>
      <td>1.0</td>
      <td>18.0</td>
      <td>29.0</td>
      <td>104.0</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>137</th>
      <td>179</td>
      <td>Venezuela</td>
      <td>Americas</td>
      <td>179.0</td>
      <td>25.9</td>
      <td>10.0</td>
      <td>34.0</td>
      <td>34.0</td>
      <td>14.9</td>
      <td>31.4</td>
      <td>...</td>
      <td>Venezuela</td>
      <td>108</td>
      <td>77.0</td>
      <td>135.0</td>
      <td>49.0</td>
      <td>145.0</td>
      <td>110.0</td>
      <td>139.0</td>
      <td>78.0</td>
      <td>71.0</td>
    </tr>
    <tr>
      <th>138</th>
      <td>180</td>
      <td>Vietnam</td>
      <td>Asia-Pacific</td>
      <td>128.0</td>
      <td>55.3</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>22.0</td>
      <td>18.0</td>
      <td>93.6</td>
      <td>...</td>
      <td>Vietnam</td>
      <td>94</td>
      <td>121.0</td>
      <td>27.0</td>
      <td>64.0</td>
      <td>23.0</td>
      <td>86.0</td>
      <td>97.0</td>
      <td>105.0</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>139</th>
      <td>182</td>
      <td>Zambia</td>
      <td>Sub-Saharan Africa</td>
      <td>138.0</td>
      <td>53.6</td>
      <td>50.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>17.9</td>
      <td>17.2</td>
      <td>...</td>
      <td>Zambia</td>
      <td>138</td>
      <td>84.0</td>
      <td>128.0</td>
      <td>115.0</td>
      <td>73.0</td>
      <td>69.0</td>
      <td>53.0</td>
      <td>115.0</td>
      <td>131.0</td>
    </tr>
    <tr>
      <th>140</th>
      <td>183</td>
      <td>Zimbabwe</td>
      <td>Sub-Saharan Africa</td>
      <td>175.0</td>
      <td>40.4</td>
      <td>10.0</td>
      <td>51.5</td>
      <td>25.0</td>
      <td>22.3</td>
      <td>14.9</td>
      <td>...</td>
      <td>Zimbabwe</td>
      <td>146</td>
      <td>63.0</td>
      <td>34.0</td>
      <td>110.0</td>
      <td>96.0</td>
      <td>63.0</td>
      <td>141.0</td>
      <td>131.0</td>
      <td>129.0</td>
    </tr>
  </tbody>
</table>
<p>141 rows × 24 columns</p>
</div>




```python
combined_df_new = combined_df[["World_Rank", "Happiness_Rank", "Score_2019", "Positive_Emotion", "Negative_Emotion"]]
combined_df_new.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>World_Rank</th>
      <th>Happiness_Rank</th>
      <th>Score_2019</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>152.0</td>
      <td>154</td>
      <td>51.5</td>
      <td>152.0</td>
      <td>133.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>52.0</td>
      <td>107</td>
      <td>66.5</td>
      <td>90.0</td>
      <td>108.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>171.0</td>
      <td>88</td>
      <td>46.2</td>
      <td>113.0</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>148.0</td>
      <td>47</td>
      <td>52.2</td>
      <td>28.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>47.0</td>
      <td>116</td>
      <td>67.7</td>
      <td>126.0</td>
      <td>145.0</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>World_Rank</th>
      <th>Happiness_Rank</th>
      <th>Score_2019</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>152.0</td>
      <td>154</td>
      <td>51.5</td>
      <td>152.0</td>
      <td>133.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>52.0</td>
      <td>107</td>
      <td>66.5</td>
      <td>90.0</td>
      <td>108.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>171.0</td>
      <td>88</td>
      <td>46.2</td>
      <td>113.0</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>148.0</td>
      <td>47</td>
      <td>52.2</td>
      <td>28.0</td>
      <td>93.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>47.0</td>
      <td>116</td>
      <td>67.7</td>
      <td>126.0</td>
      <td>145.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
corr = combined_df_new.corr()
corr
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>World_Rank</th>
      <th>Happiness_Rank</th>
      <th>Score_2019</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>World_Rank</th>
      <td>1.000000</td>
      <td>0.674575</td>
      <td>-0.967818</td>
      <td>0.371797</td>
      <td>0.586466</td>
    </tr>
    <tr>
      <th>Happiness_Rank</th>
      <td>0.674575</td>
      <td>1.000000</td>
      <td>-0.645458</td>
      <td>0.501577</td>
      <td>0.530415</td>
    </tr>
    <tr>
      <th>Score_2019</th>
      <td>-0.967818</td>
      <td>-0.645458</td>
      <td>1.000000</td>
      <td>-0.342618</td>
      <td>-0.590359</td>
    </tr>
    <tr>
      <th>Positive_Emotion</th>
      <td>0.371797</td>
      <td>0.501577</td>
      <td>-0.342618</td>
      <td>1.000000</td>
      <td>0.338993</td>
    </tr>
    <tr>
      <th>Negative_Emotion</th>
      <td>0.586466</td>
      <td>0.530415</td>
      <td>-0.590359</td>
      <td>0.338993</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>World_Rank</th>
      <th>Happiness_Rank</th>
      <th>Score_2019</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>World_Rank</th>
      <td>1.000000</td>
      <td>0.674575</td>
      <td>-0.967818</td>
      <td>0.371797</td>
      <td>0.586466</td>
    </tr>
    <tr>
      <th>Happiness_Rank</th>
      <td>0.674575</td>
      <td>1.000000</td>
      <td>-0.645458</td>
      <td>0.501577</td>
      <td>0.530415</td>
    </tr>
    <tr>
      <th>Score_2019</th>
      <td>-0.967818</td>
      <td>-0.645458</td>
      <td>1.000000</td>
      <td>-0.342618</td>
      <td>-0.590359</td>
    </tr>
    <tr>
      <th>Positive_Emotion</th>
      <td>0.371797</td>
      <td>0.501577</td>
      <td>-0.342618</td>
      <td>1.000000</td>
      <td>0.338993</td>
    </tr>
    <tr>
      <th>Negative_Emotion</th>
      <td>0.586466</td>
      <td>0.530415</td>
      <td>-0.590359</td>
      <td>0.338993</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
corr.style.background_gradient()
```




<style  type="text/css" >
    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #0567a1;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #63a2cb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #0872b1;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #046198;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #e4e1ef;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #358fc0;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #167bb6;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #2081b9;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #197db7;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #b9c6e0;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #4a98c5;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #0569a4;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #1379b5;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #dddbec;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #71a8ce;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }</style>  
<table id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >World_Rank</th> 
        <th class="col_heading level0 col1" >Happiness_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Positive_Emotion</th> 
        <th class="col_heading level0 col4" >Negative_Emotion</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >World_Rank</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.674575</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.967818</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >0.371797</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >0.586466</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >Happiness_Rank</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.674575</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.645458</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >0.501577</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.530415</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.967818</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.645458</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >-0.342618</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.590359</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Positive_Emotion</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >0.371797</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >0.501577</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >-0.342618</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.338993</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Negative_Emotion</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >0.586466</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.530415</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.590359</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.338993</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
    </tr></tbody> 
</table> 






<style  type="text/css" >
    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #0567a1;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #63a2cb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #0872b1;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #046198;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #e4e1ef;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #358fc0;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #167bb6;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #fff7fb;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #2081b9;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #197db7;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #b9c6e0;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #4a98c5;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #0569a4;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #1379b5;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #dddbec;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #71a8ce;
        }    #T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }</style>  
<table id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >World_Rank</th> 
        <th class="col_heading level0 col1" >Happiness_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Positive_Emotion</th> 
        <th class="col_heading level0 col4" >Negative_Emotion</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >World_Rank</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.674575</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.967818</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >0.371797</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >0.586466</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >Happiness_Rank</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.674575</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.645458</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >0.501577</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.530415</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.967818</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.645458</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >-0.342618</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.590359</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Positive_Emotion</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >0.371797</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >0.501577</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >-0.342618</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.338993</td> 
    </tr>    <tr> 
        <th id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Negative_Emotion</th> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >0.586466</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.530415</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.590359</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.338993</td> 
        <td id="T_8c373c6c_5e09_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
    </tr></tbody> 
</table> 




```python
corr2 = combined_df.corr()
```


```python
corr2.style.background_gradient()
```




<style  type="text/css" >
    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #7bacd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #76aad0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #a8bedc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #d3d4e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #e6e2ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #b3c3de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #abbfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #dad9ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #c9cee4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #ced0e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #c1cae2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #9fbad9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #ede7f2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #0567a1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #63a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #0872b1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #0a73b2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #2d8abd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #8cb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #3b92c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #045f95;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #04629a;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #04588a;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #fdf5fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #f9f2f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #045585;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #d6d6e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #fdf5fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #fbf3f9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #eee8f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #f8f1f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f5eff6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #eee9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #f8f1f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #fbf3f9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #ede8f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #79abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #75a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #78abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #2383ba;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #a8bedc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #cacee5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #96b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #fef6fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #1e80b8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #bfc9e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #2685bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #c8cde4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #91b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #d4d4e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #4295c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #9ab8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #1c7fb8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #2987bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #2484ba;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #75a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #dedcec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #f4edf6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #efe9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #e5e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #e1dfed;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #d2d3e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #e8e4f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #f6eff7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #d5d5e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #d2d2e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045f95;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #c6cce3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #e3e0ee;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #73a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #6da6cd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #dfddec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #045c90;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #78abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #dcdaeb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #a5bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #79abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #cdd0e5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #c9cee4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #adc1dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #cacee5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #89b1d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #b3c3de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #97b7d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #046198;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #67a4cc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #f5eef6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #9ebad9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #167bb6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #1b7eb7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #2685bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #045687;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #045687;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #f3edf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #2081b9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #d2d2e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #a5bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #d5d5e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #a9bfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #197db7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #3f93c2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #056ba9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #4295c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #fef6fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #0569a4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #dad9ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #b1c2de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #c4cbe3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #8eb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #1379b5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #056dac;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #4496c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #96b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #5a9ec9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #0771b1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #197db7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #0569a4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #60a1ca;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #045585;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #60a1ca;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #056dab;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #04598c;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #046096;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #f6eff7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #0c74b2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #d7d6e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #c1cae2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #89b1d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #0f76b3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #056faf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #2f8bbe;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #2a88bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #2a88bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #2786bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #dedcec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #b5c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #b5c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #e0dded;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #c6cce3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #e9e5f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #9cb9d9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #69a5cc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #6fa7ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #157ab5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #d2d3e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #81aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #c2cbe2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #bfc9e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #8cb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #187cb6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #65a3cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #4897c4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #2c89bd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #2987bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #1b7eb7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #2786bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #eee9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #045b8f;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #ebe6f2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #f3edf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #cdd0e5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #3d93c2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #f4eef6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #83afd3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #a7bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #0d75b3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #045b8f;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #2f8bbe;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #03517e;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #045e93;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #e3e0ee;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #65a3cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #a9bfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #73a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #2182b9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #046299;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #3b92c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #03517e;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_8f460690_5e09_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >-0.0206702</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >0.00671645</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.118322</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.0259049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.156363</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.0432167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.0506146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >0.0600472</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >0.136872</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >-0.0478717</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >-0.0697628</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.156619</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >-0.163963</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >-0.091384</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.0556587</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >-0.153857</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.0366016</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.0080697</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >-0.0206702</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.967818</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.77339</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >-0.0105203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >0.381167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >-0.363998</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.0348896</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >0.0213793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.18049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >0.674575</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >0.371797</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >0.586466</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >0.589025</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.475981</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.249428</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.43031</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >0.733842</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >0.7084</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >0.00671645</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.967818</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.786203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >0.0147909</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >-0.367906</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >0.326261</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.115709</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.0427462</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.322128</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >-0.645458</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >-0.342618</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >-0.590359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >-0.546187</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.478494</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.318754</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.474299</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >-0.707808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >-0.676837</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.118322</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.77339</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.786203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.098425</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >-0.237107</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.412805</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >-0.0315743</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >-0.092443</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >-0.204136</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >-0.620995</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >-0.303905</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >-0.40705</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >-0.486576</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.382094</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.189173</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >-0.344861</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >-0.634026</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.626022</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.0259049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >-0.0105203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >0.0147909</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.098425</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.551451</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >0.326231</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >-0.0325808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >-0.122232</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >0.0234146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >-0.0599058</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.162722</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >0.0756269</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >-0.00560012</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >-0.08085</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >-0.340996</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >-0.00345361</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.00546833</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >-0.115938</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.156363</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >0.381167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >-0.367906</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >-0.237107</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.551451</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >-0.106681</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.0337579</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.00603359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.11341</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >0.348953</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.0326827</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >0.402751</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >0.372234</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.12205</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >-0.121789</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >0.270157</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.470123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >0.358374</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.0432167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >-0.363998</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >0.326261</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.412805</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >0.326231</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >-0.106681</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >-0.0753192</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >-0.287139</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >-0.0713769</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.467202</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.0511593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >-0.338623</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.563457</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.109889</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.108218</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >-0.118772</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >-0.463336</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.577098</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.0506146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.0348896</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.115709</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >-0.0315743</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >-0.0325808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.0337579</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >-0.0753192</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.784166</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.551965</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >0.137735</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >0.0337973</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.0200169</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >0.180182</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >-0.165601</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.116123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.0848562</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >0.231656</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >0.117185</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >0.0600472</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >0.0213793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.0427462</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >-0.092443</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >-0.122232</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.00603359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >-0.287139</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.784166</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.392123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >0.160908</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >-0.075447</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >0.00710676</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >0.19593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.259992</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.200435</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.0877737</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >0.253724</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.223333</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >0.136872</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.18049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.322128</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >-0.204136</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >0.0234146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.11341</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >-0.0713769</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.551965</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.392123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >0.081855</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >0.0148079</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.123715</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.0345359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >0.144917</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >0.0703507</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >0.127875</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >0.0263334</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >0.0169309</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >-0.0478717</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >0.674575</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >-0.645458</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >-0.620995</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >-0.0599058</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >0.348953</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.467202</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >0.137735</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >0.160908</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >0.081855</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.501577</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >0.530415</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.821257</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.545515</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.239255</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.506445</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >0.812544</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.812071</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >-0.0697628</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >0.371797</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >-0.342618</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >-0.303905</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.162722</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.0326827</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.0511593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >0.0337973</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >-0.075447</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >0.0148079</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.501577</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.338993</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.383946</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.665535</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >0.228592</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >0.368006</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >0.292793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.329788</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.156619</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >0.586466</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >-0.590359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >-0.40705</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >0.0756269</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >0.402751</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >-0.338623</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.0200169</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >0.00710676</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.123715</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >0.530415</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.338993</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.630168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >0.400225</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >0.215533</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >0.343125</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.566045</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.489324</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >-0.163963</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >0.589025</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >-0.546187</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >-0.486576</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >-0.00560012</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >0.372234</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.563457</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >0.180182</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >0.19593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.0345359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.821257</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.383946</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.630168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.440901</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >0.176392</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.450871</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >0.790329</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.734934</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >-0.091384</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.475981</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.478494</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.382094</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >-0.08085</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.12205</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.109889</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >-0.165601</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.259992</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >0.144917</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.545515</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.665535</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >0.400225</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.440901</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.415171</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.492129</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.41198</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >0.436088</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.0556587</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.249428</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.318754</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.189173</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >-0.340996</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >-0.121789</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.108218</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.116123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.200435</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >0.0703507</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.239255</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >0.228592</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >0.215533</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >0.176392</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.415171</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >0.292431</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >0.207756</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.176784</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >-0.153857</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.43031</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.474299</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >-0.344861</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >-0.00345361</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >0.270157</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >-0.118772</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.0848562</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.0877737</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >0.127875</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.506445</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >0.368006</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >0.343125</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.450871</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.492129</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >0.292431</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >0.475168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >0.430654</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.0366016</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >0.733842</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >-0.707808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >-0.634026</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.00546833</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.470123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >-0.463336</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >0.231656</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >0.253724</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >0.0263334</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >0.812544</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >0.292793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.566045</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >0.790329</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.41198</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >0.207756</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >0.475168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >0.844137</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.0080697</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >0.7084</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >-0.676837</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.626022</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >-0.115938</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >0.358374</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.577098</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >0.117185</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.223333</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >0.0169309</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.812071</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.329788</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.489324</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.734934</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >0.436088</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.176784</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >0.430654</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >0.844137</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 






<style  type="text/css" >
    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #7bacd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #76aad0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #a8bedc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #d3d4e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #e6e2ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #b3c3de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #abbfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #dad9ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #c9cee4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #ced0e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #c1cae2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #9fbad9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #ede7f2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #0567a1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #63a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #0872b1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #0a73b2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #2d8abd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #8cb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #3b92c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #045f95;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #04629a;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #04588a;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #fdf5fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #f9f2f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #045585;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #d6d6e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #fdf5fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #fbf3f9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #eee8f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #f8f1f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f5eff6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #eee9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #f8f1f8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #fbf3f9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #ede8f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #79abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #75a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #78abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #2383ba;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #a8bedc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #cacee5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #96b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #fef6fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #1e80b8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #bfc9e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #2685bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #c8cde4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #91b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #d4d4e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #4295c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #9ab8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #1c7fb8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #2987bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #2484ba;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #75a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #dedcec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #f4edf6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #efe9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #e5e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #e1dfed;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #d2d3e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #e8e4f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #f6eff7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #d5d5e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #d2d2e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045f95;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #c6cce3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #e3e0ee;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #5c9fc9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #73a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #6da6cd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #dfddec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #045c90;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #78abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #dcdaeb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #a5bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #79abd0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #cdd0e5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #b7c5df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #c9cee4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #adc1dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #b8c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #cacee5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #89b1d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #b3c3de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #94b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #bdc8e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #97b7d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #f0eaf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #046198;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #67a4cc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #f5eef6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #9ebad9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #167bb6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #1b7eb7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #2685bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #045687;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #045687;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #f3edf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #2081b9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #b9c6e0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #cccfe5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #eae6f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #d2d2e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #a5bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #d5d5e8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #a9bfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #197db7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #3f93c2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #056ba9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #509ac6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #4a98c5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #4295c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #fef6fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #0569a4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #dad9ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #bcc7e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #b1c2de;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #c4cbe3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #8eb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #1379b5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #056dac;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #4496c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #96b6d7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #5a9ec9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #0771b1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #197db7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #0569a4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #d9d8ea;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #e4e1ef;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #60a1ca;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #b4c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #045585;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #60a1ca;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #056dab;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #358fc0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #04598c;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #046096;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #f6eff7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #0c74b2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #d7d6e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #dddbec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #acc0dd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #c1cae2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #d1d2e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #f1ebf4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #89b1d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #0f76b3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #056faf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #3790c0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #2f8bbe;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #549cc7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #2a88bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #2a88bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #2786bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #dedcec;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #b5c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #b5c4df;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #e0dded;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #c0c9e2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #c6cce3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #e9e5f1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #9cb9d9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #93b5d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #69a5cc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #62a2cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #6fa7ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #fef6fa;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #157ab5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #d2d3e7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #d0d1e6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #81aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #c2cbe2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #bfc9e1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #d8d7e9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #8cb3d5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #187cb6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #65a3cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #4897c4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #2c89bd;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #2987bc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #80aed2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #1b7eb7;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #2786bb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #eee9f3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #045b8f;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #ebe6f2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #f3edf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #cdd0e5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #3d93c2;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #f4eef6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #71a8ce;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #83afd3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #a7bddb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #7eadd1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #0d75b3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #045b8f;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #4094c3;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #99b8d8;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #2f8bbe;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #03517e;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #045e93;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #e7e3f0;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #f2ecf5;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #e3e0ee;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #65a3cb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #fff7fb;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #8fb4d6;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #8bb2d4;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #a9bfdc;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #045788;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #73a9cf;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #2182b9;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #046299;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #3991c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #a2bcda;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #3b92c1;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #03517e;
        }    #T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_8f460690_5e09_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >-0.0206702</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >0.00671645</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.118322</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.0259049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.156363</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.0432167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.0506146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >0.0600472</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >0.136872</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >-0.0478717</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >-0.0697628</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.156619</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >-0.163963</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >-0.091384</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.0556587</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >-0.153857</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.0366016</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.0080697</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >-0.0206702</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.967818</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.77339</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >-0.0105203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >0.381167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >-0.363998</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.0348896</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >0.0213793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.18049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >0.674575</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >0.371797</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >0.586466</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >0.589025</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.475981</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.249428</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.43031</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >0.733842</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >0.7084</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >0.00671645</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.967818</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.786203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >0.0147909</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >-0.367906</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >0.326261</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.115709</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.0427462</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.322128</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >-0.645458</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >-0.342618</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >-0.590359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >-0.546187</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.478494</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.318754</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.474299</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >-0.707808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >-0.676837</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.118322</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.77339</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.786203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.098425</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >-0.237107</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.412805</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >-0.0315743</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >-0.092443</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >-0.204136</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >-0.620995</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >-0.303905</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >-0.40705</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >-0.486576</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.382094</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.189173</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >-0.344861</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >-0.634026</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.626022</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.0259049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >-0.0105203</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >0.0147909</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.098425</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.551451</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >0.326231</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >-0.0325808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >-0.122232</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >0.0234146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >-0.0599058</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.162722</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >0.0756269</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >-0.00560012</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >-0.08085</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >-0.340996</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >-0.00345361</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.00546833</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >-0.115938</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.156363</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >0.381167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >-0.367906</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >-0.237107</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.551451</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >-0.106681</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.0337579</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.00603359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.11341</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >0.348953</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.0326827</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >0.402751</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >0.372234</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.12205</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >-0.121789</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >0.270157</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.470123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >0.358374</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.0432167</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >-0.363998</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >0.326261</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.412805</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >0.326231</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >-0.106681</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >-0.0753192</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >-0.287139</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >-0.0713769</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.467202</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.0511593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >-0.338623</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.563457</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.109889</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.108218</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >-0.118772</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >-0.463336</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.577098</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.0506146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.0348896</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.115709</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >-0.0315743</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >-0.0325808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.0337579</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >-0.0753192</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.784166</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.551965</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >0.137735</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >0.0337973</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.0200169</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >0.180182</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >-0.165601</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.116123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.0848562</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >0.231656</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >0.117185</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >0.0600472</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >0.0213793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.0427462</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >-0.092443</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >-0.122232</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.00603359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >-0.287139</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.784166</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.392123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >0.160908</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >-0.075447</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >0.00710676</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >0.19593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.259992</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.200435</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.0877737</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >0.253724</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.223333</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >0.136872</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.18049</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.322128</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >-0.204136</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >0.0234146</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.11341</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >-0.0713769</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.551965</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.392123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >0.081855</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >0.0148079</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.123715</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.0345359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >0.144917</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >0.0703507</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >0.127875</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >0.0263334</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >0.0169309</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >-0.0478717</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >0.674575</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >-0.645458</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >-0.620995</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >-0.0599058</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >0.348953</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.467202</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >0.137735</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >0.160908</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >0.081855</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.501577</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >0.530415</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.821257</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.545515</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.239255</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.506445</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >0.812544</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.812071</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >-0.0697628</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >0.371797</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >-0.342618</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >-0.303905</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.162722</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.0326827</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.0511593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >0.0337973</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >-0.075447</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >0.0148079</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.501577</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.338993</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.383946</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.665535</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >0.228592</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >0.368006</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >0.292793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.329788</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.156619</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >0.586466</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >-0.590359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >-0.40705</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >0.0756269</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >0.402751</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >-0.338623</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.0200169</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >0.00710676</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.123715</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >0.530415</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.338993</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.630168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >0.400225</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >0.215533</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >0.343125</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.566045</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.489324</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >-0.163963</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >0.589025</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >-0.546187</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >-0.486576</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >-0.00560012</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >0.372234</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.563457</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >0.180182</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >0.19593</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.0345359</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.821257</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.383946</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.630168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.440901</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >0.176392</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.450871</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >0.790329</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.734934</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >-0.091384</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.475981</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.478494</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.382094</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >-0.08085</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.12205</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.109889</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >-0.165601</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.259992</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >0.144917</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.545515</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.665535</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >0.400225</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.440901</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.415171</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.492129</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.41198</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >0.436088</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.0556587</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.249428</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.318754</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.189173</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >-0.340996</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >-0.121789</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.108218</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.116123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.200435</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >0.0703507</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.239255</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >0.228592</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >0.215533</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >0.176392</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.415171</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >0.292431</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >0.207756</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.176784</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >-0.153857</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.43031</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.474299</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >-0.344861</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >-0.00345361</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >0.270157</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >-0.118772</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.0848562</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.0877737</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >0.127875</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.506445</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >0.368006</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >0.343125</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.450871</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.492129</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >0.292431</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >0.475168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >0.430654</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.0366016</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >0.733842</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >-0.707808</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >-0.634026</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.00546833</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.470123</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >-0.463336</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >0.231656</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >0.253724</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >0.0263334</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >0.812544</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >0.292793</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.566045</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >0.790329</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.41198</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >0.207756</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >0.475168</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >0.844137</td> 
    </tr>    <tr> 
        <th id="T_8f460690_5e09_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.0080697</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >0.7084</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >-0.676837</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.626022</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >-0.115938</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >0.358374</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.577098</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >0.117185</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.223333</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >0.0169309</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.812071</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.329788</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.489324</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.734934</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >0.436088</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.176784</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >0.430654</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >0.844137</td> 
        <td id="T_8f460690_5e09_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 



Happiness Rank, Economic World Rank, R2= 0.67  
Hapiness Health Life Expectancy, Economic World Rank, R2 = 0.71


```python
top10_new_economic_freedom_df = combined_df.sort_values(by=['World_Rank'])
top10_new_economic_freedom_df

top10_new_economic_freedom_df = top10_new_economic_freedom_df.iloc[:10]




```


```python
top10_new_economic_freedom_df
top10_new_economic_freedom_df.reset_index()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>53</td>
      <td>71</td>
      <td>Hong Kong</td>
      <td>Asia-Pacific</td>
      <td>1.0</td>
      <td>90.2</td>
      <td>90.0</td>
      <td>15.0</td>
      <td>16.5</td>
      <td>14.0</td>
      <td>...</td>
      <td>Hong Kong</td>
      <td>76</td>
      <td>105.0</td>
      <td>28.0</td>
      <td>76.0</td>
      <td>66.0</td>
      <td>14.0</td>
      <td>18.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>113</td>
      <td>147</td>
      <td>Singapore</td>
      <td>Asia-Pacific</td>
      <td>2.0</td>
      <td>89.4</td>
      <td>80.0</td>
      <td>22.0</td>
      <td>17.0</td>
      <td>13.7</td>
      <td>...</td>
      <td>Singapore</td>
      <td>34</td>
      <td>38.0</td>
      <td>2.0</td>
      <td>36.0</td>
      <td>20.0</td>
      <td>1.0</td>
      <td>21.0</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>93</td>
      <td>120</td>
      <td>New Zealand</td>
      <td>Asia-Pacific</td>
      <td>3.0</td>
      <td>84.4</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>28.0</td>
      <td>32.1</td>
      <td>...</td>
      <td>New Zealand</td>
      <td>8</td>
      <td>22.0</td>
      <td>12.0</td>
      <td>5.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>8.0</td>
      <td>26.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>120</td>
      <td>158</td>
      <td>Switzerland</td>
      <td>Europe</td>
      <td>4.0</td>
      <td>81.9</td>
      <td>90.0</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>27.8</td>
      <td>...</td>
      <td>Switzerland</td>
      <td>6</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>13.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>7</td>
      <td>Australia</td>
      <td>Asia-Pacific</td>
      <td>5.0</td>
      <td>80.9</td>
      <td>90.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>28.2</td>
      <td>...</td>
      <td>Australia</td>
      <td>11</td>
      <td>47.0</td>
      <td>37.0</td>
      <td>7.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>59</td>
      <td>78</td>
      <td>Ireland</td>
      <td>Europe</td>
      <td>6.0</td>
      <td>80.5</td>
      <td>70.0</td>
      <td>41.0</td>
      <td>12.5</td>
      <td>23.0</td>
      <td>...</td>
      <td>Ireland</td>
      <td>16</td>
      <td>33.0</td>
      <td>32.0</td>
      <td>6.0</td>
      <td>33.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>6.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>133</td>
      <td>174</td>
      <td>United Kingdom</td>
      <td>Europe</td>
      <td>7.0</td>
      <td>78.9</td>
      <td>80.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>33.2</td>
      <td>...</td>
      <td>United Kingdom</td>
      <td>15</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>9.0</td>
      <td>63.0</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>23.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>29</td>
      <td>Canada</td>
      <td>Americas</td>
      <td>8.0</td>
      <td>77.7</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>15.0</td>
      <td>31.7</td>
      <td>...</td>
      <td>Canada</td>
      <td>9</td>
      <td>18.0</td>
      <td>49.0</td>
      <td>20.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>132</td>
      <td>173</td>
      <td>United Arab Emirates</td>
      <td>Middle East and North Africa</td>
      <td>9.0</td>
      <td>77.6</td>
      <td>60.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.9</td>
      <td>...</td>
      <td>United Arab Emirates</td>
      <td>21</td>
      <td>43.0</td>
      <td>56.0</td>
      <td>72.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>121</td>
      <td>160</td>
      <td>Taiwan</td>
      <td>Asia-Pacific</td>
      <td>10.0</td>
      <td>77.3</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>8.9</td>
      <td>...</td>
      <td>Taiwan</td>
      <td>25</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>48.0</td>
      <td>102.0</td>
      <td>56.0</td>
      <td>56.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 25 columns</p>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>53</td>
      <td>71</td>
      <td>Hong Kong</td>
      <td>Asia-Pacific</td>
      <td>1.0</td>
      <td>90.2</td>
      <td>90.0</td>
      <td>15.0</td>
      <td>16.5</td>
      <td>14.0</td>
      <td>...</td>
      <td>Hong Kong</td>
      <td>76</td>
      <td>105.0</td>
      <td>28.0</td>
      <td>76.0</td>
      <td>66.0</td>
      <td>14.0</td>
      <td>18.0</td>
      <td>9.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>113</td>
      <td>147</td>
      <td>Singapore</td>
      <td>Asia-Pacific</td>
      <td>2.0</td>
      <td>89.4</td>
      <td>80.0</td>
      <td>22.0</td>
      <td>17.0</td>
      <td>13.7</td>
      <td>...</td>
      <td>Singapore</td>
      <td>34</td>
      <td>38.0</td>
      <td>2.0</td>
      <td>36.0</td>
      <td>20.0</td>
      <td>1.0</td>
      <td>21.0</td>
      <td>3.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>93</td>
      <td>120</td>
      <td>New Zealand</td>
      <td>Asia-Pacific</td>
      <td>3.0</td>
      <td>84.4</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>28.0</td>
      <td>32.1</td>
      <td>...</td>
      <td>New Zealand</td>
      <td>8</td>
      <td>22.0</td>
      <td>12.0</td>
      <td>5.0</td>
      <td>8.0</td>
      <td>5.0</td>
      <td>8.0</td>
      <td>26.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>120</td>
      <td>158</td>
      <td>Switzerland</td>
      <td>Europe</td>
      <td>4.0</td>
      <td>81.9</td>
      <td>90.0</td>
      <td>40.0</td>
      <td>24.0</td>
      <td>27.8</td>
      <td>...</td>
      <td>Switzerland</td>
      <td>6</td>
      <td>44.0</td>
      <td>21.0</td>
      <td>13.0</td>
      <td>11.0</td>
      <td>7.0</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>7</td>
      <td>Australia</td>
      <td>Asia-Pacific</td>
      <td>5.0</td>
      <td>80.9</td>
      <td>90.0</td>
      <td>45.0</td>
      <td>30.0</td>
      <td>28.2</td>
      <td>...</td>
      <td>Australia</td>
      <td>11</td>
      <td>47.0</td>
      <td>37.0</td>
      <td>7.0</td>
      <td>17.0</td>
      <td>13.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>59</td>
      <td>78</td>
      <td>Ireland</td>
      <td>Europe</td>
      <td>6.0</td>
      <td>80.5</td>
      <td>70.0</td>
      <td>41.0</td>
      <td>12.5</td>
      <td>23.0</td>
      <td>...</td>
      <td>Ireland</td>
      <td>16</td>
      <td>33.0</td>
      <td>32.0</td>
      <td>6.0</td>
      <td>33.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>6.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>133</td>
      <td>174</td>
      <td>United Kingdom</td>
      <td>Europe</td>
      <td>7.0</td>
      <td>78.9</td>
      <td>80.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>33.2</td>
      <td>...</td>
      <td>United Kingdom</td>
      <td>15</td>
      <td>52.0</td>
      <td>42.0</td>
      <td>9.0</td>
      <td>63.0</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>23.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>29</td>
      <td>Canada</td>
      <td>Americas</td>
      <td>8.0</td>
      <td>77.7</td>
      <td>80.0</td>
      <td>33.0</td>
      <td>15.0</td>
      <td>31.7</td>
      <td>...</td>
      <td>Canada</td>
      <td>9</td>
      <td>18.0</td>
      <td>49.0</td>
      <td>20.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>14.0</td>
      <td>19.0</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>132</td>
      <td>173</td>
      <td>United Arab Emirates</td>
      <td>Middle East and North Africa</td>
      <td>9.0</td>
      <td>77.6</td>
      <td>60.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.9</td>
      <td>...</td>
      <td>United Arab Emirates</td>
      <td>21</td>
      <td>43.0</td>
      <td>56.0</td>
      <td>72.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>4.0</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>121</td>
      <td>160</td>
      <td>Taiwan</td>
      <td>Asia-Pacific</td>
      <td>10.0</td>
      <td>77.3</td>
      <td>60.0</td>
      <td>45.0</td>
      <td>20.0</td>
      <td>8.9</td>
      <td>...</td>
      <td>Taiwan</td>
      <td>25</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>48.0</td>
      <td>102.0</td>
      <td>56.0</td>
      <td>56.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 25 columns</p>
</div>




```python
top10eco_corr = top10_new_economic_freedom_df.corr()
```


```python
top10eco_corr.style.background_gradient()
```




<style  type="text/css" >
    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #4a98c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #8cb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #b4c4df;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #c8cde4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #f4edf6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #4a98c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #8fb4d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #4094c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #8bb2d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #67a4cc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #dcdaeb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #dedcec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #c9cee4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #99b8d8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #f3edf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #04649d;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #348ebf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #046097;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #d0d1e6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #056faf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #5ea0ca;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #a8bedc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #76aad0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #0569a5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #0c74b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #f5eff6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #4c99c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #d2d3e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #eee8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #b1c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #f0eaf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #056dab;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #589ec8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #056aa6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #056ead;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #c2cbe2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #f4edf6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #8fb4d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #86b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #2484ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #afc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #549cc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #b8c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #529bc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #046198;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #056dab;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #7bacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #eee8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #dedcec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #faf2f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #308cbe;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #88b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #0d75b3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #4697c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #0568a3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #046097;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #056dac;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #bdc8e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #a9bfdc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #f6eff7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #ede7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #a7bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #056caa;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #f3edf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #056fae;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #056ead;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #056faf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #b4c4df;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #d3d4e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #4897c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #69a5cc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #f0eaf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #faf3f9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #045280;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #e0deed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #a7bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #94b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #549cc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045382;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #a1bbda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #bfc9e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #d9d8ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #75a9cf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #86b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #d2d3e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #045280;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #acc0dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #c1cae2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #adc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #c1cae2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #5ea0ca;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #abbfdc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #88b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #76aad0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #0c74b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #89b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #ece7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #05659f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #1e80b8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #d0d1e6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #04629a;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #e5e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #e8e4f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #045b8f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #045b8f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #589ec8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #63a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #d3d4e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #dcdaeb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #0569a5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #d6d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #a4bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #afc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #d7d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #7eadd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #045b8e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #7eadd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #c9cee4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #4897c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #2383ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #8bb2d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #05659f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #71a8ce;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #4295c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #c8cde4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #e0dded;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #e6e2ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #b8c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #046096;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #2484ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #9ebad9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #358fc0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #1e80b8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #046299;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #8cb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #2987bc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #75a9cf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #eae6f1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #3991c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #045382;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #0568a3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #8eb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #046096;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #d4d4e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #2987bc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #e0deed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #cacee5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #e4e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #d4d4e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #d6d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #e1dfed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #045a8d;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #3b92c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #04649e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #2383ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #e1dfed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #a5bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #6ba5cd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #167bb6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #0872b1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #3991c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #0a73b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #056caa;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #d9d8ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #056aa6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #ede7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #e5e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #b1c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #509ac6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #045f95;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #a1bbda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #3b92c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #6da6cd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #056ba7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #046299;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #0567a2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.193087</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.0864071</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.453015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.185226</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.279617</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.337737</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.385199</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >-0.15145</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >-0.0730091</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >-0.0481732</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >-0.109463</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.2771</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >0.231828</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >0.223257</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.223256</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >0.316298</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.237387</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.378846</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.193087</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.938935</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.743484</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.153775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >-0.391885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >-0.131537</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.212346</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >-0.0291538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.114604</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >-0.452377</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >-0.55455</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >0.366242</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >0.041408</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.217423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.692025</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.366859</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >0.105331</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >0.703529</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.0864071</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.938935</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.548474</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.317749</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >0.208794</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >-0.164435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.240311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.0272032</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.190957</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >0.665801</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >0.586005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >-0.467215</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >0.224704</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.0372314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.488767</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.128728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >-0.266249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >-0.560643</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.453015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.743484</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.548474</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.211829</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >0.627058</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.554294</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >-0.0617775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >-0.305951</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >0.148621</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >0.137339</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >0.488981</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >-0.0206711</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >-0.3263</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.251609</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.681209</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >-0.511249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >0.302885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.832015</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.185226</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.153775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.317749</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.211829</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.710062</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >0.573634</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >0.224314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >0.0283671</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >-0.134955</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >-0.496786</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.376172</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >-0.272163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >-0.777055</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >0.301789</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >0.394519</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >0.0541435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.532538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >-0.656064</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.279617</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >-0.391885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >0.208794</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >0.627058</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.710062</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >0.566688</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.0372966</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.31622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.0509358</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >-0.237666</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.0743386</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >-0.470217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >-0.617217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.0717255</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >-0.0365394</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >-0.0803968</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.605633</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >-0.733395</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.337737</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >-0.131537</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >-0.164435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.554294</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >0.573634</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >0.566688</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >0.000198094</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >-0.0789075</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >0.37986</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.581411</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.198297</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >0.251029</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.84401</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.363628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.515279</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >-0.663977</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >0.833535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.505005</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.385199</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.212346</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.240311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >-0.0617775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >0.224314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.0372966</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >0.000198094</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.856728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.497554</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >0.187333</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >-0.026385</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.208092</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >-0.222941</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >0.160039</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.0977113</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.0482993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >-0.179319</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >-0.275045</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >-0.15145</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >-0.0291538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.0272032</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >-0.305951</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >0.0283671</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.31622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >-0.0789075</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.856728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.411758</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >-0.0135512</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >-0.0986799</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >0.033507</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >-0.191755</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.0689311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.185426</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.206423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >-0.348658</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.136367</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >-0.0730091</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.114604</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.190957</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >0.148621</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >-0.134955</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.0509358</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >0.37986</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.497554</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.411758</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >-0.0750053</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >0.211084</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.581259</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.0175324</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >-0.111536</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >-0.151354</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >-0.499119</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >0.673441</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >0.421177</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >-0.0481732</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >-0.452377</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >0.665801</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >0.137339</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >-0.496786</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >-0.237666</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.581411</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >0.187333</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >-0.0135512</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >-0.0750053</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.792592</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >-0.16325</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.751134</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.462201</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.0960019</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.238064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >-0.386171</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.147944</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >-0.109463</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >-0.55455</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >0.586005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >0.488981</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.376172</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.0743386</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.198297</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >-0.026385</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >-0.0986799</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >0.211084</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.792592</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.175228</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.487962</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.217278</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >-0.206404</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >-0.233797</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >-0.253622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.24628</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.2771</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >0.366242</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >-0.467215</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >-0.0206711</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >-0.272163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >-0.470217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >0.251029</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.208092</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >0.033507</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.581259</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >-0.16325</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.175228</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.0525313</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >-0.359383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >-0.296906</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >-0.567926</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.100383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.65641</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >0.231828</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >0.041408</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >0.224704</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >-0.3263</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >-0.777055</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >-0.617217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.84401</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >-0.222941</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >-0.191755</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.0175324</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.751134</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.487962</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.0525313</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.300993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >0.375602</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.456163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >-0.551652</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.688214</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >0.223257</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.217423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.0372314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.251609</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >0.301789</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.0717255</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.363628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >0.160039</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.0689311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >-0.111536</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.462201</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.217278</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >-0.359383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.300993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.829398</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.646104</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.0688535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >-0.0306896</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.223256</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.692025</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.488767</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.681209</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >0.394519</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >-0.0365394</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.515279</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.0977113</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.185426</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >-0.151354</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.0960019</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >-0.206404</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >-0.296906</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >0.375602</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.829398</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >0.842597</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >0.341648</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.659429</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >0.316298</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.366859</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.128728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >-0.511249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >0.0541435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >-0.0803968</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >-0.663977</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.0482993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.206423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >-0.499119</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.238064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >-0.233797</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >-0.567926</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.456163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.646104</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >0.842597</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >-0.71915</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >-0.123894</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.237387</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >0.105331</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >-0.266249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >0.302885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.532538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.605633</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >0.833535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >-0.179319</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >-0.348658</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >0.673441</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >-0.386171</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >-0.253622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.100383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >-0.551652</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.0688535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >0.341648</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >-0.71915</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >-0.20233</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.378846</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >0.703529</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >-0.560643</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.832015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >-0.656064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >-0.733395</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.505005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >-0.275045</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.136367</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >0.421177</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.147944</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.24628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.65641</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.688214</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >-0.0306896</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.659429</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >-0.123894</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >-0.20233</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 






<style  type="text/css" >
    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #4a98c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #8cb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #b4c4df;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #c8cde4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #f4edf6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #4a98c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #8fb4d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #4094c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #8bb2d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #67a4cc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #dcdaeb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #dedcec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #c9cee4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #99b8d8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #f3edf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #04649d;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #348ebf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #046097;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #d0d1e6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #056faf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #5ea0ca;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #a8bedc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #76aad0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #0569a5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #0c74b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #f5eff6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #4c99c5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #d2d3e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #eee8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #b1c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #f0eaf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #056dab;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #589ec8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #056aa6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #056ead;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #c2cbe2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #f4edf6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #8fb4d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #86b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #2484ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #afc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #549cc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #b8c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #529bc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #046198;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #056dab;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #7bacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #eee8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #dedcec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #faf2f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #308cbe;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #88b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #0d75b3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #4697c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #0568a3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #046097;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #056dac;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #bdc8e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #a9bfdc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #bcc7e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #f6eff7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #ede7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #a7bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #056caa;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #f3edf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #056fae;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #056ead;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #056faf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #b4c4df;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #d3d4e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #4897c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #69a5cc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #f0eaf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #faf3f9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #045280;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #e0deed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #a7bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #94b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #549cc7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045382;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #b3c3de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #a1bbda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #bfc9e1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #d9d8ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #75a9cf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #86b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #d2d3e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #045280;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #f7f0f7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #acc0dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #c1cae2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #adc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #c1cae2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #d8d7e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #5ea0ca;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #abbfdc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #88b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #76aad0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #0c74b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #89b1d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #ece7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #05659f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #1e80b8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #c6cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #d0d1e6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #04629a;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #e5e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #c4cbe3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #e8e4f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #045b8f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #045b8f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #589ec8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #63a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #d3d4e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #dcdaeb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #0569a5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #d6d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #a4bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #afc1dd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #d7d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #7eadd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #045b8e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #7eadd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #c9cee4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #4897c4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #ede8f3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #2383ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #8bb2d4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #c5cce3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #bbc7e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #1077b4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #cccfe5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #d5d5e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #7dacd1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #05659f;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #80aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #71a8ce;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #4295c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #c8cde4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #e0dded;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #e6e2ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #b8c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #046096;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #2484ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #9ebad9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #79abd0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #358fc0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #1e80b8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #046299;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #4496c3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #8cb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #cdd0e5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #2987bc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #75a9cf;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #eae6f1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #3991c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #045382;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #0568a3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #84b0d3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #8eb3d5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #046096;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #d4d4e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #f2ecf5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #2987bc;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #9cb9d9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #e0deed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #cacee5;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #e4e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #d4d4e8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #d6d6e9;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #e1dfed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #2786bb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #045a8d;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #3b92c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #04649e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #65a3cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #2383ba;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #96b6d7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #e1dfed;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #81aed2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #a5bddb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #f1ebf4;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #6ba5cd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #dad9ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #167bb6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #0872b1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #a2bcda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #62a2cb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #3991c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #0a73b2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #056caa;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #03517e;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #d9d8ea;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #f8f1f8;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #056aa6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #ede7f2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #91b5d6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #e5e1ef;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #b9c6e0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #3f93c2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #b1c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #509ac6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #045f95;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #dddbec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #f5eef6;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #fff7fb;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #dfddec;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #e7e3f0;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #a1bbda;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #3b92c1;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #83afd3;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #6da6cd;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #056ba7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #046299;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #d2d2e7;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #0567a2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #b0c2de;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #c0c9e2;
        }    #T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.193087</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.0864071</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.453015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.185226</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.279617</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.337737</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.385199</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >-0.15145</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >-0.0730091</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >-0.0481732</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >-0.109463</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.2771</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >0.231828</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >0.223257</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.223256</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >0.316298</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.237387</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.378846</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.193087</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.938935</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.743484</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.153775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >-0.391885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >-0.131537</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.212346</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >-0.0291538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.114604</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >-0.452377</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >-0.55455</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >0.366242</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >0.041408</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.217423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.692025</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.366859</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >0.105331</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >0.703529</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.0864071</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.938935</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.548474</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.317749</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >0.208794</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >-0.164435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.240311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.0272032</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.190957</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >0.665801</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >0.586005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >-0.467215</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >0.224704</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.0372314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.488767</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.128728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >-0.266249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >-0.560643</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.453015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.743484</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.548474</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >0.211829</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >0.627058</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.554294</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >-0.0617775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >-0.305951</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >0.148621</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >0.137339</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >0.488981</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >-0.0206711</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >-0.3263</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.251609</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.681209</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >-0.511249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >0.302885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.832015</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.185226</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.153775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.317749</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >0.211829</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.710062</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >0.573634</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >0.224314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >0.0283671</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >-0.134955</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >-0.496786</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.376172</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >-0.272163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >-0.777055</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >0.301789</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >0.394519</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >0.0541435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.532538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >-0.656064</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.279617</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >-0.391885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >0.208794</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >0.627058</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.710062</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >0.566688</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.0372966</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.31622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.0509358</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >-0.237666</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.0743386</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >-0.470217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >-0.617217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.0717255</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >-0.0365394</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >-0.0803968</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.605633</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >-0.733395</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.337737</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >-0.131537</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >-0.164435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.554294</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >0.573634</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >0.566688</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >0.000198094</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >-0.0789075</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >0.37986</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.581411</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.198297</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >0.251029</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.84401</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.363628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.515279</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >-0.663977</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >0.833535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.505005</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.385199</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.212346</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.240311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >-0.0617775</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >0.224314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.0372966</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >0.000198094</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.856728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.497554</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >0.187333</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >-0.026385</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.208092</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >-0.222941</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >0.160039</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.0977113</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.0482993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >-0.179319</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >-0.275045</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >-0.15145</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >-0.0291538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.0272032</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >-0.305951</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >0.0283671</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.31622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >-0.0789075</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.856728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.411758</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >-0.0135512</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >-0.0986799</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >0.033507</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >-0.191755</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.0689311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.185426</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.206423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >-0.348658</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.136367</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >-0.0730091</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.114604</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.190957</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >0.148621</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >-0.134955</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.0509358</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >0.37986</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.497554</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.411758</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >-0.0750053</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >0.211084</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.581259</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.0175324</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >-0.111536</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >-0.151354</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >-0.499119</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >0.673441</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >0.421177</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >-0.0481732</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >-0.452377</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >0.665801</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >0.137339</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >-0.496786</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >-0.237666</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.581411</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >0.187333</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >-0.0135512</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >-0.0750053</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.792592</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >-0.16325</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.751134</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.462201</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.0960019</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.238064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >-0.386171</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.147944</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >-0.109463</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >-0.55455</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >0.586005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >0.488981</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.376172</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.0743386</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.198297</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >-0.026385</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >-0.0986799</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >0.211084</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.792592</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.175228</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.487962</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.217278</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >-0.206404</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >-0.233797</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >-0.253622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.24628</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.2771</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >0.366242</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >-0.467215</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >-0.0206711</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >-0.272163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >-0.470217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >0.251029</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.208092</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >0.033507</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.581259</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >-0.16325</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.175228</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.0525313</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >-0.359383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >-0.296906</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >-0.567926</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.100383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.65641</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >0.231828</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >0.041408</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >0.224704</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >-0.3263</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >-0.777055</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >-0.617217</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.84401</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >-0.222941</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >-0.191755</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.0175324</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.751134</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.487962</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.0525313</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.300993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >0.375602</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.456163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >-0.551652</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.688214</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >0.223257</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.217423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.0372314</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.251609</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >0.301789</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.0717255</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.363628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >0.160039</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.0689311</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >-0.111536</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.462201</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.217278</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >-0.359383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.300993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.829398</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.646104</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.0688535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >-0.0306896</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.223256</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.692025</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.488767</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.681209</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >0.394519</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >-0.0365394</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.515279</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.0977113</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.185426</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >-0.151354</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.0960019</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >-0.206404</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >-0.296906</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >0.375602</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.829398</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >0.842597</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >0.341648</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.659429</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >0.316298</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.366859</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.128728</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >-0.511249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >0.0541435</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >-0.0803968</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >-0.663977</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.0482993</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.206423</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >-0.499119</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.238064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >-0.233797</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >-0.567926</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.456163</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.646104</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >0.842597</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >-0.71915</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >-0.123894</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.237387</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >0.105331</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >-0.266249</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >0.302885</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.532538</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.605633</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >0.833535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >-0.179319</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >-0.348658</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >0.673441</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >-0.386171</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >-0.253622</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.100383</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >-0.551652</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.0688535</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >0.341648</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >-0.71915</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >-0.20233</td> 
    </tr>    <tr> 
        <th id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.378846</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >0.703529</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >-0.560643</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.832015</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >-0.656064</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >-0.733395</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.505005</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >-0.275045</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.136367</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >0.421177</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.147944</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.24628</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.65641</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.688214</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >-0.0306896</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.659429</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >-0.123894</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >-0.20233</td> 
        <td id="T_52c7ea84_5e0a_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 



# top 10 Eco
Happiness Rank, Economic World Rank, R2= -0.45   
Happiness Health Life Expectancy, Economic World Rank, R2 = 0.70


```python
bot10_new_economic_freedom_df = combined_df.sort_values(by=['World_Rank'])
bot10_new_economic_freedom_df

bot10_new_economic_freedom_df = bot10_new_economic_freedom_df.iloc[-10:]
bot10_new_economic_freedom_df
bot10_new_economic_freedom_df.reset_index()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24</td>
      <td>31</td>
      <td>Central African Republic</td>
      <td>Sub-Saharan Africa</td>
      <td>161.0</td>
      <td>49.1</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>9.0</td>
      <td>...</td>
      <td>Central African Republic</td>
      <td>155</td>
      <td>132.0</td>
      <td>153.0</td>
      <td>155.0</td>
      <td>133.0</td>
      <td>122.0</td>
      <td>113.0</td>
      <td>152.0</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>26</td>
      <td>Burundi</td>
      <td>Sub-Saharan Africa</td>
      <td>162.0</td>
      <td>48.9</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>12.3</td>
      <td>...</td>
      <td>Burundi</td>
      <td>145</td>
      <td>98.0</td>
      <td>126.0</td>
      <td>152.0</td>
      <td>135.0</td>
      <td>23.0</td>
      <td>149.0</td>
      <td>151.0</td>
      <td>135.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89</td>
      <td>116</td>
      <td>Mozambique</td>
      <td>Sub-Saharan Africa</td>
      <td>163.0</td>
      <td>48.6</td>
      <td>50.0</td>
      <td>32.0</td>
      <td>32.0</td>
      <td>20.2</td>
      <td>...</td>
      <td>Mozambique</td>
      <td>123</td>
      <td>108.0</td>
      <td>131.0</td>
      <td>122.0</td>
      <td>46.0</td>
      <td>40.0</td>
      <td>121.0</td>
      <td>146.0</td>
      <td>134.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>129</td>
      <td>170</td>
      <td>Turkmenistan</td>
      <td>Asia-Pacific</td>
      <td>164.0</td>
      <td>48.4</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>15.6</td>
      <td>...</td>
      <td>Turkmenistan</td>
      <td>87</td>
      <td>135.0</td>
      <td>63.0</td>
      <td>8.0</td>
      <td>83.0</td>
      <td>NaN</td>
      <td>33.0</td>
      <td>60.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>112</td>
      <td>146</td>
      <td>Sierra Leone</td>
      <td>Sub-Saharan Africa</td>
      <td>167.0</td>
      <td>47.5</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>30.0</td>
      <td>12.2</td>
      <td>...</td>
      <td>Sierra Leone</td>
      <td>129</td>
      <td>139.0</td>
      <td>149.0</td>
      <td>135.0</td>
      <td>116.0</td>
      <td>112.0</td>
      <td>79.0</td>
      <td>145.0</td>
      <td>146.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>36</td>
      <td>49</td>
      <td>Ecuador</td>
      <td>Americas</td>
      <td>170.0</td>
      <td>46.9</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>25.0</td>
      <td>21.2</td>
      <td>...</td>
      <td>Ecuador</td>
      <td>50</td>
      <td>11.0</td>
      <td>113.0</td>
      <td>71.0</td>
      <td>42.0</td>
      <td>68.0</td>
      <td>95.0</td>
      <td>86.0</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>3</td>
      <td>Algeria</td>
      <td>Middle East and North Africa</td>
      <td>171.0</td>
      <td>46.2</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>24.5</td>
      <td>...</td>
      <td>Algeria</td>
      <td>88</td>
      <td>113.0</td>
      <td>106.0</td>
      <td>101.0</td>
      <td>149.0</td>
      <td>46.0</td>
      <td>128.0</td>
      <td>72.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>14</td>
      <td>19</td>
      <td>Bolivia</td>
      <td>Americas</td>
      <td>173.0</td>
      <td>42.3</td>
      <td>40.0</td>
      <td>13.0</td>
      <td>25.0</td>
      <td>31.1</td>
      <td>...</td>
      <td>Bolivia</td>
      <td>61</td>
      <td>70.0</td>
      <td>138.0</td>
      <td>93.0</td>
      <td>35.0</td>
      <td>91.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>140</td>
      <td>183</td>
      <td>Zimbabwe</td>
      <td>Sub-Saharan Africa</td>
      <td>175.0</td>
      <td>40.4</td>
      <td>10.0</td>
      <td>51.5</td>
      <td>25.0</td>
      <td>22.3</td>
      <td>...</td>
      <td>Zimbabwe</td>
      <td>146</td>
      <td>63.0</td>
      <td>34.0</td>
      <td>110.0</td>
      <td>96.0</td>
      <td>63.0</td>
      <td>141.0</td>
      <td>131.0</td>
      <td>129.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>137</td>
      <td>179</td>
      <td>Venezuela</td>
      <td>Americas</td>
      <td>179.0</td>
      <td>25.9</td>
      <td>10.0</td>
      <td>34.0</td>
      <td>34.0</td>
      <td>14.9</td>
      <td>...</td>
      <td>Venezuela</td>
      <td>108</td>
      <td>77.0</td>
      <td>135.0</td>
      <td>49.0</td>
      <td>145.0</td>
      <td>110.0</td>
      <td>139.0</td>
      <td>78.0</td>
      <td>71.0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 25 columns</p>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CountryID</th>
      <th>Country_Name</th>
      <th>Region</th>
      <th>World_Rank</th>
      <th>Score_2019</th>
      <th>Financial_Freedom</th>
      <th>Income_Tax_Rate_Pct</th>
      <th>Corporate_Tax_Rate_Pct</th>
      <th>Tax_Burden_Pct_of_GDP</th>
      <th>...</th>
      <th>Country</th>
      <th>Happiness_Rank</th>
      <th>Positive_Emotion</th>
      <th>Negative_Emotion</th>
      <th>Social_support</th>
      <th>Freedom</th>
      <th>Corruption</th>
      <th>Generosity</th>
      <th>GDP_Contribution</th>
      <th>Healthy_life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24</td>
      <td>31</td>
      <td>Central African Republic</td>
      <td>Sub-Saharan Africa</td>
      <td>161.0</td>
      <td>49.1</td>
      <td>30.0</td>
      <td>50.0</td>
      <td>30.0</td>
      <td>9.0</td>
      <td>...</td>
      <td>Central African Republic</td>
      <td>155</td>
      <td>132.0</td>
      <td>153.0</td>
      <td>155.0</td>
      <td>133.0</td>
      <td>122.0</td>
      <td>113.0</td>
      <td>152.0</td>
      <td>150.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>26</td>
      <td>Burundi</td>
      <td>Sub-Saharan Africa</td>
      <td>162.0</td>
      <td>48.9</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>12.3</td>
      <td>...</td>
      <td>Burundi</td>
      <td>145</td>
      <td>98.0</td>
      <td>126.0</td>
      <td>152.0</td>
      <td>135.0</td>
      <td>23.0</td>
      <td>149.0</td>
      <td>151.0</td>
      <td>135.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89</td>
      <td>116</td>
      <td>Mozambique</td>
      <td>Sub-Saharan Africa</td>
      <td>163.0</td>
      <td>48.6</td>
      <td>50.0</td>
      <td>32.0</td>
      <td>32.0</td>
      <td>20.2</td>
      <td>...</td>
      <td>Mozambique</td>
      <td>123</td>
      <td>108.0</td>
      <td>131.0</td>
      <td>122.0</td>
      <td>46.0</td>
      <td>40.0</td>
      <td>121.0</td>
      <td>146.0</td>
      <td>134.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>129</td>
      <td>170</td>
      <td>Turkmenistan</td>
      <td>Asia-Pacific</td>
      <td>164.0</td>
      <td>48.4</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>8.0</td>
      <td>15.6</td>
      <td>...</td>
      <td>Turkmenistan</td>
      <td>87</td>
      <td>135.0</td>
      <td>63.0</td>
      <td>8.0</td>
      <td>83.0</td>
      <td>NaN</td>
      <td>33.0</td>
      <td>60.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>112</td>
      <td>146</td>
      <td>Sierra Leone</td>
      <td>Sub-Saharan Africa</td>
      <td>167.0</td>
      <td>47.5</td>
      <td>20.0</td>
      <td>15.0</td>
      <td>30.0</td>
      <td>12.2</td>
      <td>...</td>
      <td>Sierra Leone</td>
      <td>129</td>
      <td>139.0</td>
      <td>149.0</td>
      <td>135.0</td>
      <td>116.0</td>
      <td>112.0</td>
      <td>79.0</td>
      <td>145.0</td>
      <td>146.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>36</td>
      <td>49</td>
      <td>Ecuador</td>
      <td>Americas</td>
      <td>170.0</td>
      <td>46.9</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>25.0</td>
      <td>21.2</td>
      <td>...</td>
      <td>Ecuador</td>
      <td>50</td>
      <td>11.0</td>
      <td>113.0</td>
      <td>71.0</td>
      <td>42.0</td>
      <td>68.0</td>
      <td>95.0</td>
      <td>86.0</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>3</td>
      <td>Algeria</td>
      <td>Middle East and North Africa</td>
      <td>171.0</td>
      <td>46.2</td>
      <td>30.0</td>
      <td>35.0</td>
      <td>23.0</td>
      <td>24.5</td>
      <td>...</td>
      <td>Algeria</td>
      <td>88</td>
      <td>113.0</td>
      <td>106.0</td>
      <td>101.0</td>
      <td>149.0</td>
      <td>46.0</td>
      <td>128.0</td>
      <td>72.0</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>14</td>
      <td>19</td>
      <td>Bolivia</td>
      <td>Americas</td>
      <td>173.0</td>
      <td>42.3</td>
      <td>40.0</td>
      <td>13.0</td>
      <td>25.0</td>
      <td>31.1</td>
      <td>...</td>
      <td>Bolivia</td>
      <td>61</td>
      <td>70.0</td>
      <td>138.0</td>
      <td>93.0</td>
      <td>35.0</td>
      <td>91.0</td>
      <td>104.0</td>
      <td>101.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>140</td>
      <td>183</td>
      <td>Zimbabwe</td>
      <td>Sub-Saharan Africa</td>
      <td>175.0</td>
      <td>40.4</td>
      <td>10.0</td>
      <td>51.5</td>
      <td>25.0</td>
      <td>22.3</td>
      <td>...</td>
      <td>Zimbabwe</td>
      <td>146</td>
      <td>63.0</td>
      <td>34.0</td>
      <td>110.0</td>
      <td>96.0</td>
      <td>63.0</td>
      <td>141.0</td>
      <td>131.0</td>
      <td>129.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>137</td>
      <td>179</td>
      <td>Venezuela</td>
      <td>Americas</td>
      <td>179.0</td>
      <td>25.9</td>
      <td>10.0</td>
      <td>34.0</td>
      <td>34.0</td>
      <td>14.9</td>
      <td>...</td>
      <td>Venezuela</td>
      <td>108</td>
      <td>77.0</td>
      <td>135.0</td>
      <td>49.0</td>
      <td>145.0</td>
      <td>110.0</td>
      <td>139.0</td>
      <td>78.0</td>
      <td>71.0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 25 columns</p>
</div>




```python
bot10eco_corr = bot10_new_economic_freedom_df.corr()
```


```python
bot10eco_corr.style.background_gradient()
```




<style  type="text/css" >
    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #d2d2e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #c5cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #62a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #94b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #a4bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #dedcec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #dddbec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #0568a3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #e0deed;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #fdf5fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #63a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #d7d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #b9c6e0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #034a74;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #056dab;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #fbf4f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #ede7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #529bc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #1077b4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #549cc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #4094c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #2c89bd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #529bc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f9f2f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #eee9f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #b0c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #b1c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #96b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #2d8abd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #a2bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #157ab5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #dedcec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #dad9ea;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #3991c1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #0566a0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #7bacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #b0c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #328dbf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #d3d4e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #d6d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #f5eff6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #2383ba;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #0a73b2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #5ea0ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #a8bedc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #046096;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #056dac;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #5c9fc9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #0c74b2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #ece7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #ebe6f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #fdf5fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #e3e0ee;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #f5eff6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #f6eff7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #d2d3e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #e7e3f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #034a74;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #f7f0f7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #71a8ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045c90;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #adc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #8eb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #f1ebf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #d6d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #fef6fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #4c99c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #bfc9e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #0569a4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #589ec8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #04588a;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #ede7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #93b5d6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #fbf4f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #e0deed;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #e6e2ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #f9f2f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #63a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #eee8f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #5ea0ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #d2d3e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #2685bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #86b0d3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #79abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #056faf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #1278b4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #a7bddb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #046097;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #045280;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #e4e1ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #f2ecf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #96b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #197db7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #88b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #76aad0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #ced0e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #056dac;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #d4d4e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #a8bedc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #e0dded;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #7bacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #94b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #589ec8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #88b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #d3d4e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #0567a1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #d2d2e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #bbc7e0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #034b76;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #0567a1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #7eadd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #adc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #f2ecf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #5c9fc9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #f8f1f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #f5eef6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #0f76b3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #2c89bd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #a4bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #81aed2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #a7bddb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #569dc8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #c2cbe2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #e0dded;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #4496c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #dad9ea;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #84b0d3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #fef6fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #bfc9e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #3991c1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #c5cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #76aad0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #05659f;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #045e93;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #eee8f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #308cbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #e5e1ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #2383ba;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #4295c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #93b5d6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #dddbec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #509ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #e6e2ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #b7c5df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #045e93;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #6fa7ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #60a1ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #034c78;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #b7c5df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #045382;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #7eadd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #e7e3f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #a2bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #89b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #5a9ec9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #89b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #bdc8e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #03517e;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #056ba9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #71a8ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #045483;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.301496</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.443417</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.675326</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.103971</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.174122</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.240905</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.272361</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >-0.0227645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >0.418103</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >0.235482</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >0.102346</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.445301</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >-0.43543</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >0.0119791</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.263104</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >-0.232079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.0920052</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.118197</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.301496</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.850241</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.367375</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.0562645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >0.0411437</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >0.508137</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.580209</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >-0.293521</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.598079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >-0.35615</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >-0.550037</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >-0.238163</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >-0.413618</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.0263323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.227503</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.292736</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >-0.489947</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >-0.581175</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.443417</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.850241</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.469776</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.113366</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >-0.250554</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >-0.124864</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.866811</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.601591</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.907936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >0.0837337</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >0.340168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >0.031357</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >0.392691</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.234598</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.356244</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.367243</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >0.358511</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >0.405423</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.675326</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.367375</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.469776</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >-0.0046323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >0.303311</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.347464</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >0.314999</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >0.256948</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >-0.419936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >-0.270233</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >-0.211684</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >0.498956</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >0.40035</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.530802</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.372781</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >0.149752</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >0.284715</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.0314921</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.103971</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.0562645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.113366</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >-0.0046323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.434519</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >-0.191168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >-0.205893</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >-0.543448</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >0.0657031</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >0.521605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.258558</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >-0.146686</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >0.450574</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >0.348246</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >-0.139093</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >0.70518</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.367556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >0.149151</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.174122</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >0.0411437</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >-0.250554</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >0.303311</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.434519</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >-0.257205</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.520841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.605892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.336985</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >0.464645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.123178</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >0.62087</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >0.685918</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.272426</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >0.0224253</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >0.761817</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.645236</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >0.283841</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.240905</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >0.508137</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >-0.124864</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.347464</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >-0.191168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >-0.257205</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >0.181832</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >0.468846</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >-0.187946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.649633</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.507345</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >-0.264239</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.24824</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.569927</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.289279</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >0.0816774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >-0.395291</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.483878</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.272361</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.580209</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.866811</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >0.314999</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >-0.205893</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.520841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >0.181832</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.763277</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.958125</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >-0.0681578</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >0.22785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.237083</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >0.190868</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >-0.452072</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.198946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.509928</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >0.199727</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >0.335913</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >-0.0227645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >-0.293521</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.601591</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >0.256948</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >-0.543448</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.605892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >0.468846</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.763277</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.715949</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >-0.343677</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >0.105109</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >-0.406364</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >-0.178967</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.59716</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.545012</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.516892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >-0.1186</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.0544874</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >0.418103</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.598079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.907936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >-0.419936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >0.0657031</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.336985</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >-0.187946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.958125</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.715949</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >-0.00334108</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >-0.143457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.192124</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.37556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >0.376126</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >0.366723</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >0.290232</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >-0.320605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >-0.354696</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >0.235482</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >-0.35615</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >0.0837337</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >-0.270233</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >0.521605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >0.464645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.649633</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >-0.0681578</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >-0.343677</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >-0.00334108</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.500023</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >0.0298938</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.643774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.548645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.0292907</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.407432</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >0.761299</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.849367</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >0.102346</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >-0.550037</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >0.340168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >-0.211684</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.258558</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.123178</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.507345</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >0.22785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >0.105109</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >-0.143457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.500023</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.197015</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.212379</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.458168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >0.19348</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >-0.306724</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >0.239872</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.652206</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.445301</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >-0.238163</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >0.031357</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >0.498956</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >-0.146686</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >0.62087</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >-0.264239</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.237083</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >-0.406364</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.192124</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >0.0298938</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.197015</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.438289</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >0.104457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >0.416563</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >0.122006</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.337952</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.133373</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >-0.43543</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >-0.413618</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >0.392691</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >0.40035</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >0.450574</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >0.685918</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.24824</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >0.190868</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >-0.178967</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.37556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.643774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.212379</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.438289</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.237195</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >-0.142341</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.531755</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >0.891857</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.689395</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >0.0119791</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.0263323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.234598</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.530802</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >0.348246</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.272426</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.569927</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >-0.452072</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.59716</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >0.376126</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.548645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.458168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >0.104457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.237195</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.134422</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.359568</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.0631891</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >0.21081</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.263104</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.227503</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.356244</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.372781</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >-0.139093</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >0.0224253</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.289279</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.198946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.545012</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >0.366723</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.0292907</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >0.19348</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >0.416563</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >-0.142341</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.134422</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >-0.500694</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >-0.0389486</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.0565045</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >-0.232079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.292736</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.367243</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >0.149752</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >0.70518</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >0.761817</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >0.0816774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.509928</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.516892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >0.290232</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.407432</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >-0.306724</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >0.122006</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.531755</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.359568</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >-0.500694</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >0.378785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >0.0862997</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.0920052</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >-0.489947</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >0.358511</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >0.284715</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.367556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.645236</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >-0.395291</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >0.199727</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >-0.1186</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >-0.320605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >0.761299</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >0.239872</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.337952</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >0.891857</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.0631891</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >-0.0389486</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >0.378785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >0.844461</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.118197</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >-0.581175</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >0.405423</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.0314921</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >0.149151</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >0.283841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.483878</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >0.335913</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.0544874</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >-0.354696</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.849367</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.652206</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.133373</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.689395</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >0.21081</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.0565045</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >0.0862997</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >0.844461</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 






<style  type="text/css" >
    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col0 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col1 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col2 {
            background-color:  #d2d2e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col3 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col4 {
            background-color:  #c5cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col5 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col6 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col7 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col8 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col9 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col10 {
            background-color:  #62a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col11 {
            background-color:  #94b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col12 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col13 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col14 {
            background-color:  #a4bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col15 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col16 {
            background-color:  #dedcec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col17 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col18 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col0 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col1 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col2 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col3 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col4 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col5 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col6 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col7 {
            background-color:  #dddbec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col8 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col9 {
            background-color:  #0568a3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col10 {
            background-color:  #e0deed;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col11 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col12 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col13 {
            background-color:  #fdf5fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col14 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col15 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col16 {
            background-color:  #63a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col17 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col18 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col0 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col1 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col2 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col3 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col4 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col5 {
            background-color:  #d7d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col6 {
            background-color:  #b9c6e0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col7 {
            background-color:  #034a74;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col8 {
            background-color:  #056dab;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col9 {
            background-color:  #fbf4f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col10 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col11 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col12 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col13 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col14 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col15 {
            background-color:  #ede7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col16 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col17 {
            background-color:  #529bc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col18 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col0 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col1 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col2 {
            background-color:  #1077b4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col3 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col4 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col5 {
            background-color:  #549cc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col6 {
            background-color:  #4094c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col7 {
            background-color:  #2c89bd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col8 {
            background-color:  #529bc7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col9 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col10 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col11 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col12 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col13 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col14 {
            background-color:  #f9f2f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col15 {
            background-color:  #eee9f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col16 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col17 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col18 {
            background-color:  #b0c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col0 {
            background-color:  #b1c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col1 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col2 {
            background-color:  #96b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col3 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col4 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col5 {
            background-color:  #2d8abd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col6 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col7 {
            background-color:  #a2bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col8 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col9 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col10 {
            background-color:  #157ab5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col11 {
            background-color:  #dedcec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col12 {
            background-color:  #dad9ea;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col13 {
            background-color:  #3991c1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col14 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col15 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col16 {
            background-color:  #0566a0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col17 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col18 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col0 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col1 {
            background-color:  #7bacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col2 {
            background-color:  #b0c2de;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col3 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col4 {
            background-color:  #328dbf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col5 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col6 {
            background-color:  #d3d4e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col7 {
            background-color:  #d6d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col8 {
            background-color:  #f5eff6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col9 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col10 {
            background-color:  #2383ba;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col11 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col12 {
            background-color:  #0a73b2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col13 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col14 {
            background-color:  #5ea0ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col15 {
            background-color:  #a8bedc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col16 {
            background-color:  #046096;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col17 {
            background-color:  #056dac;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col18 {
            background-color:  #5c9fc9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col0 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col1 {
            background-color:  #0c74b2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col2 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col3 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col4 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col5 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col6 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col7 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col8 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col9 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col10 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col11 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col12 {
            background-color:  #ece7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col13 {
            background-color:  #ebe6f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col14 {
            background-color:  #fdf5fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col15 {
            background-color:  #e3e0ee;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col16 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col17 {
            background-color:  #f5eff6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col18 {
            background-color:  #f6eff7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col0 {
            background-color:  #d2d3e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col1 {
            background-color:  #e7e3f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col2 {
            background-color:  #034a74;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col3 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col4 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col5 {
            background-color:  #f7f0f7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col6 {
            background-color:  #71a8ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col7 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col8 {
            background-color:  #045c90;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col9 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col10 {
            background-color:  #adc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col11 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col12 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col13 {
            background-color:  #8eb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col14 {
            background-color:  #f1ebf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col15 {
            background-color:  #d6d6e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col16 {
            background-color:  #fef6fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col17 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col18 {
            background-color:  #4c99c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col0 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col1 {
            background-color:  #bfc9e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col2 {
            background-color:  #0569a4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col3 {
            background-color:  #589ec8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col4 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col5 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col6 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col7 {
            background-color:  #04588a;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col8 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col9 {
            background-color:  #ede7f2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col10 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col11 {
            background-color:  #93b5d6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col12 {
            background-color:  #fbf4f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col13 {
            background-color:  #e0deed;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col14 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col15 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col16 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col17 {
            background-color:  #d1d2e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col18 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col0 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col1 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col2 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col3 {
            background-color:  #e6e2ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col4 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col5 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col6 {
            background-color:  #c6cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col7 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col8 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col9 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col10 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col11 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col12 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col13 {
            background-color:  #f9f2f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col14 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col15 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col16 {
            background-color:  #63a2cb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col17 {
            background-color:  #eee8f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col18 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col0 {
            background-color:  #5ea0ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col1 {
            background-color:  #cacee5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col2 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col3 {
            background-color:  #d2d3e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col4 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col5 {
            background-color:  #2685bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col6 {
            background-color:  #fff7fb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col7 {
            background-color:  #86b0d3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col8 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col9 {
            background-color:  #79abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col10 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col11 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col12 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col13 {
            background-color:  #056faf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col14 {
            background-color:  #1278b4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col15 {
            background-color:  #a7bddb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col16 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col17 {
            background-color:  #046097;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col18 {
            background-color:  #045280;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col0 {
            background-color:  #83afd3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col1 {
            background-color:  #e4e1ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col2 {
            background-color:  #2a88bc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col3 {
            background-color:  #c8cde4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col4 {
            background-color:  #dfddec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col5 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col6 {
            background-color:  #f2ecf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col7 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col8 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col9 {
            background-color:  #96b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col10 {
            background-color:  #197db7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col11 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col12 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col13 {
            background-color:  #88b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col14 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col15 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col16 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col17 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col18 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col0 {
            background-color:  #e9e5f1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col1 {
            background-color:  #b5c4df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col2 {
            background-color:  #76aad0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col3 {
            background-color:  #187cb6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col4 {
            background-color:  #ced0e6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col5 {
            background-color:  #056dac;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col6 {
            background-color:  #d4d4e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col7 {
            background-color:  #a8bedc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col8 {
            background-color:  #e0dded;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col9 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col10 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col11 {
            background-color:  #7bacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col12 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col13 {
            background-color:  #3f93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col14 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col15 {
            background-color:  #3790c0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col16 {
            background-color:  #94b6d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col17 {
            background-color:  #589ec8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col18 {
            background-color:  #88b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col0 {
            background-color:  #e8e4f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col1 {
            background-color:  #d3d4e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col2 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col3 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col4 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col5 {
            background-color:  #0567a1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col6 {
            background-color:  #d2d2e7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col7 {
            background-color:  #4897c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col8 {
            background-color:  #bbc7e0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col9 {
            background-color:  #c0c9e2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col10 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col11 {
            background-color:  #78abd0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col12 {
            background-color:  #3d93c2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col13 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col14 {
            background-color:  #69a5cc;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col15 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col16 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col17 {
            background-color:  #034b76;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col18 {
            background-color:  #0567a1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col0 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col1 {
            background-color:  #7eadd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col2 {
            background-color:  #adc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col3 {
            background-color:  #f2ecf5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col4 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col5 {
            background-color:  #5c9fc9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col6 {
            background-color:  #f8f1f8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col7 {
            background-color:  #cdd0e5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col8 {
            background-color:  #f5eef6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col9 {
            background-color:  #2081b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col10 {
            background-color:  #0f76b3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col11 {
            background-color:  #2c89bd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col12 {
            background-color:  #a4bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col13 {
            background-color:  #81aed2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col14 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col15 {
            background-color:  #8cb3d5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col16 {
            background-color:  #4e9ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col17 {
            background-color:  #a7bddb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col18 {
            background-color:  #73a9cf;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col0 {
            background-color:  #569dc8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col1 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col2 {
            background-color:  #c2cbe2;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col3 {
            background-color:  #e0dded;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col4 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col5 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col6 {
            background-color:  #d8d7e9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col7 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col8 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col9 {
            background-color:  #2182b9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col10 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col11 {
            background-color:  #7dacd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col12 {
            background-color:  #4496c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col13 {
            background-color:  #dad9ea;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col14 {
            background-color:  #84b0d3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col15 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col16 {
            background-color:  #fef6fa;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col17 {
            background-color:  #bfc9e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col18 {
            background-color:  #9ab8d8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col0 {
            background-color:  #cccfe5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col1 {
            background-color:  #3991c1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col2 {
            background-color:  #c5cce3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col3 {
            background-color:  #76aad0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col4 {
            background-color:  #05659f;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col5 {
            background-color:  #045e93;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col6 {
            background-color:  #8bb2d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col7 {
            background-color:  #d5d5e8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col8 {
            background-color:  #eee8f3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col9 {
            background-color:  #308cbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col10 {
            background-color:  #2f8bbe;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col11 {
            background-color:  #e5e1ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col12 {
            background-color:  #9fbad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col13 {
            background-color:  #2383ba;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col14 {
            background-color:  #4295c3;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col15 {
            background-color:  #fbf3f9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col16 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col17 {
            background-color:  #4a98c5;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col18 {
            background-color:  #93b5d6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col0 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col1 {
            background-color:  #dddbec;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col2 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col3 {
            background-color:  #509ac6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col4 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col5 {
            background-color:  #056ba7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col6 {
            background-color:  #e6e2ef;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col7 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col8 {
            background-color:  #afc1dd;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col9 {
            background-color:  #b7c5df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col10 {
            background-color:  #045e93;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col11 {
            background-color:  #6fa7ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col12 {
            background-color:  #60a1ca;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col13 {
            background-color:  #034c78;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col14 {
            background-color:  #97b7d7;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col15 {
            background-color:  #b7c5df;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col16 {
            background-color:  #4697c4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col17 {
            background-color:  #023858;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col18 {
            background-color:  #045382;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col0 {
            background-color:  #7eadd1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col1 {
            background-color:  #e7e3f0;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col2 {
            background-color:  #1c7fb8;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col3 {
            background-color:  #a2bcda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col4 {
            background-color:  #89b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col5 {
            background-color:  #5a9ec9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col6 {
            background-color:  #f0eaf4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col7 {
            background-color:  #2786bb;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col8 {
            background-color:  #89b1d4;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col9 {
            background-color:  #bdc8e1;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col10 {
            background-color:  #03517e;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col11 {
            background-color:  #056ba9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col12 {
            background-color:  #9cb9d9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col13 {
            background-color:  #056aa6;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col14 {
            background-color:  #71a8ce;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col15 {
            background-color:  #a1bbda;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col16 {
            background-color:  #9ebad9;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col17 {
            background-color:  #045483;
        }    #T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col18 {
            background-color:  #023858;
        }</style>  
<table id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >CountryID</th> 
        <th class="col_heading level0 col1" >World_Rank</th> 
        <th class="col_heading level0 col2" >Score_2019</th> 
        <th class="col_heading level0 col3" >Financial_Freedom</th> 
        <th class="col_heading level0 col4" >Income_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col5" >Corporate_Tax_Rate_Pct</th> 
        <th class="col_heading level0 col6" >Tax_Burden_Pct_of_GDP</th> 
        <th class="col_heading level0 col7" >GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <th class="col_heading level0 col9" >Inflation_Pct</th> 
        <th class="col_heading level0 col10" >Happiness_Rank</th> 
        <th class="col_heading level0 col11" >Positive_Emotion</th> 
        <th class="col_heading level0 col12" >Negative_Emotion</th> 
        <th class="col_heading level0 col13" >Social_support</th> 
        <th class="col_heading level0 col14" >Freedom</th> 
        <th class="col_heading level0 col15" >Corruption</th> 
        <th class="col_heading level0 col16" >Generosity</th> 
        <th class="col_heading level0 col17" >GDP_Contribution</th> 
        <th class="col_heading level0 col18" >Healthy_life_expectancy</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row0" class="row_heading level0 row0" >CountryID</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col0" class="data row0 col0" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col1" class="data row0 col1" >0.301496</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col2" class="data row0 col2" >-0.443417</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col3" class="data row0 col3" >-0.675326</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col4" class="data row0 col4" >-0.103971</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col5" class="data row0 col5" >-0.174122</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col6" class="data row0 col6" >-0.240905</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col7" class="data row0 col7" >-0.272361</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col8" class="data row0 col8" >-0.0227645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col9" class="data row0 col9" >0.418103</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col10" class="data row0 col10" >0.235482</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col11" class="data row0 col11" >0.102346</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col12" class="data row0 col12" >-0.445301</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col13" class="data row0 col13" >-0.43543</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col14" class="data row0 col14" >0.0119791</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col15" class="data row0 col15" >0.263104</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col16" class="data row0 col16" >-0.232079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col17" class="data row0 col17" >-0.0920052</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row0_col18" class="data row0 col18" >0.118197</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row1" class="row_heading level0 row1" >World_Rank</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col0" class="data row1 col0" >0.301496</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col1" class="data row1 col1" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col2" class="data row1 col2" >-0.850241</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col3" class="data row1 col3" >-0.367375</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col4" class="data row1 col4" >0.0562645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col5" class="data row1 col5" >0.0411437</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col6" class="data row1 col6" >0.508137</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col7" class="data row1 col7" >-0.580209</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col8" class="data row1 col8" >-0.293521</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col9" class="data row1 col9" >0.598079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col10" class="data row1 col10" >-0.35615</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col11" class="data row1 col11" >-0.550037</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col12" class="data row1 col12" >-0.238163</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col13" class="data row1 col13" >-0.413618</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col14" class="data row1 col14" >0.0263323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col15" class="data row1 col15" >0.227503</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col16" class="data row1 col16" >0.292736</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col17" class="data row1 col17" >-0.489947</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row1_col18" class="data row1 col18" >-0.581175</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row2" class="row_heading level0 row2" >Score_2019</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col0" class="data row2 col0" >-0.443417</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col1" class="data row2 col1" >-0.850241</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col2" class="data row2 col2" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col3" class="data row2 col3" >0.469776</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col4" class="data row2 col4" >-0.113366</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col5" class="data row2 col5" >-0.250554</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col6" class="data row2 col6" >-0.124864</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col7" class="data row2 col7" >0.866811</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col8" class="data row2 col8" >0.601591</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col9" class="data row2 col9" >-0.907936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col10" class="data row2 col10" >0.0837337</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col11" class="data row2 col11" >0.340168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col12" class="data row2 col12" >0.031357</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col13" class="data row2 col13" >0.392691</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col14" class="data row2 col14" >-0.234598</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col15" class="data row2 col15" >-0.356244</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col16" class="data row2 col16" >-0.367243</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col17" class="data row2 col17" >0.358511</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row2_col18" class="data row2 col18" >0.405423</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row3" class="row_heading level0 row3" >Financial_Freedom</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col0" class="data row3 col0" >-0.675326</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col1" class="data row3 col1" >-0.367375</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col2" class="data row3 col2" >0.469776</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col3" class="data row3 col3" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col4" class="data row3 col4" >-0.0046323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col5" class="data row3 col5" >0.303311</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col6" class="data row3 col6" >0.347464</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col7" class="data row3 col7" >0.314999</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col8" class="data row3 col8" >0.256948</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col9" class="data row3 col9" >-0.419936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col10" class="data row3 col10" >-0.270233</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col11" class="data row3 col11" >-0.211684</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col12" class="data row3 col12" >0.498956</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col13" class="data row3 col13" >0.40035</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col14" class="data row3 col14" >-0.530802</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col15" class="data row3 col15" >-0.372781</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col16" class="data row3 col16" >0.149752</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col17" class="data row3 col17" >0.284715</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row3_col18" class="data row3 col18" >-0.0314921</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row4" class="row_heading level0 row4" >Income_Tax_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col0" class="data row4 col0" >-0.103971</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col1" class="data row4 col1" >0.0562645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col2" class="data row4 col2" >-0.113366</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col3" class="data row4 col3" >-0.0046323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col4" class="data row4 col4" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col5" class="data row4 col5" >0.434519</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col6" class="data row4 col6" >-0.191168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col7" class="data row4 col7" >-0.205893</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col8" class="data row4 col8" >-0.543448</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col9" class="data row4 col9" >0.0657031</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col10" class="data row4 col10" >0.521605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col11" class="data row4 col11" >-0.258558</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col12" class="data row4 col12" >-0.146686</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col13" class="data row4 col13" >0.450574</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col14" class="data row4 col14" >0.348246</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col15" class="data row4 col15" >-0.139093</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col16" class="data row4 col16" >0.70518</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col17" class="data row4 col17" >0.367556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row4_col18" class="data row4 col18" >0.149151</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row5" class="row_heading level0 row5" >Corporate_Tax_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col0" class="data row5 col0" >-0.174122</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col1" class="data row5 col1" >0.0411437</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col2" class="data row5 col2" >-0.250554</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col3" class="data row5 col3" >0.303311</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col4" class="data row5 col4" >0.434519</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col5" class="data row5 col5" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col6" class="data row5 col6" >-0.257205</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col7" class="data row5 col7" >-0.520841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col8" class="data row5 col8" >-0.605892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col9" class="data row5 col9" >0.336985</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col10" class="data row5 col10" >0.464645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col11" class="data row5 col11" >-0.123178</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col12" class="data row5 col12" >0.62087</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col13" class="data row5 col13" >0.685918</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col14" class="data row5 col14" >0.272426</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col15" class="data row5 col15" >0.0224253</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col16" class="data row5 col16" >0.761817</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col17" class="data row5 col17" >0.645236</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row5_col18" class="data row5 col18" >0.283841</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row6" class="row_heading level0 row6" >Tax_Burden_Pct_of_GDP</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col0" class="data row6 col0" >-0.240905</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col1" class="data row6 col1" >0.508137</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col2" class="data row6 col2" >-0.124864</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col3" class="data row6 col3" >0.347464</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col4" class="data row6 col4" >-0.191168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col5" class="data row6 col5" >-0.257205</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col6" class="data row6 col6" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col7" class="data row6 col7" >0.181832</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col8" class="data row6 col8" >0.468846</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col9" class="data row6 col9" >-0.187946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col10" class="data row6 col10" >-0.649633</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col11" class="data row6 col11" >-0.507345</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col12" class="data row6 col12" >-0.264239</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col13" class="data row6 col13" >-0.24824</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col14" class="data row6 col14" >-0.569927</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col15" class="data row6 col15" >-0.289279</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col16" class="data row6 col16" >0.0816774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col17" class="data row6 col17" >-0.395291</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row6_col18" class="data row6 col18" >-0.483878</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row7" class="row_heading level0 row7" >GDP_Growth_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col0" class="data row7 col0" >-0.272361</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col1" class="data row7 col1" >-0.580209</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col2" class="data row7 col2" >0.866811</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col3" class="data row7 col3" >0.314999</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col4" class="data row7 col4" >-0.205893</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col5" class="data row7 col5" >-0.520841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col6" class="data row7 col6" >0.181832</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col7" class="data row7 col7" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col8" class="data row7 col8" >0.763277</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col9" class="data row7 col9" >-0.958125</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col10" class="data row7 col10" >-0.0681578</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col11" class="data row7 col11" >0.22785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col12" class="data row7 col12" >-0.237083</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col13" class="data row7 col13" >0.190868</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col14" class="data row7 col14" >-0.452072</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col15" class="data row7 col15" >-0.198946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col16" class="data row7 col16" >-0.509928</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col17" class="data row7 col17" >0.199727</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row7_col18" class="data row7 col18" >0.335913</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row8" class="row_heading level0 row8" >Five_Year_GDP_Growth_Rate_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col0" class="data row8 col0" >-0.0227645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col1" class="data row8 col1" >-0.293521</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col2" class="data row8 col2" >0.601591</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col3" class="data row8 col3" >0.256948</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col4" class="data row8 col4" >-0.543448</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col5" class="data row8 col5" >-0.605892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col6" class="data row8 col6" >0.468846</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col7" class="data row8 col7" >0.763277</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col8" class="data row8 col8" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col9" class="data row8 col9" >-0.715949</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col10" class="data row8 col10" >-0.343677</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col11" class="data row8 col11" >0.105109</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col12" class="data row8 col12" >-0.406364</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col13" class="data row8 col13" >-0.178967</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col14" class="data row8 col14" >-0.59716</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col15" class="data row8 col15" >-0.545012</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col16" class="data row8 col16" >-0.516892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col17" class="data row8 col17" >-0.1186</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row8_col18" class="data row8 col18" >0.0544874</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row9" class="row_heading level0 row9" >Inflation_Pct</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col0" class="data row9 col0" >0.418103</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col1" class="data row9 col1" >0.598079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col2" class="data row9 col2" >-0.907936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col3" class="data row9 col3" >-0.419936</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col4" class="data row9 col4" >0.0657031</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col5" class="data row9 col5" >0.336985</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col6" class="data row9 col6" >-0.187946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col7" class="data row9 col7" >-0.958125</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col8" class="data row9 col8" >-0.715949</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col9" class="data row9 col9" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col10" class="data row9 col10" >-0.00334108</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col11" class="data row9 col11" >-0.143457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col12" class="data row9 col12" >0.192124</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col13" class="data row9 col13" >-0.37556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col14" class="data row9 col14" >0.376126</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col15" class="data row9 col15" >0.366723</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col16" class="data row9 col16" >0.290232</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col17" class="data row9 col17" >-0.320605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row9_col18" class="data row9 col18" >-0.354696</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row10" class="row_heading level0 row10" >Happiness_Rank</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col0" class="data row10 col0" >0.235482</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col1" class="data row10 col1" >-0.35615</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col2" class="data row10 col2" >0.0837337</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col3" class="data row10 col3" >-0.270233</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col4" class="data row10 col4" >0.521605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col5" class="data row10 col5" >0.464645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col6" class="data row10 col6" >-0.649633</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col7" class="data row10 col7" >-0.0681578</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col8" class="data row10 col8" >-0.343677</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col9" class="data row10 col9" >-0.00334108</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col10" class="data row10 col10" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col11" class="data row10 col11" >0.500023</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col12" class="data row10 col12" >0.0298938</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col13" class="data row10 col13" >0.643774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col14" class="data row10 col14" >0.548645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col15" class="data row10 col15" >0.0292907</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col16" class="data row10 col16" >0.407432</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col17" class="data row10 col17" >0.761299</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row10_col18" class="data row10 col18" >0.849367</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row11" class="row_heading level0 row11" >Positive_Emotion</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col0" class="data row11 col0" >0.102346</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col1" class="data row11 col1" >-0.550037</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col2" class="data row11 col2" >0.340168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col3" class="data row11 col3" >-0.211684</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col4" class="data row11 col4" >-0.258558</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col5" class="data row11 col5" >-0.123178</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col6" class="data row11 col6" >-0.507345</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col7" class="data row11 col7" >0.22785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col8" class="data row11 col8" >0.105109</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col9" class="data row11 col9" >-0.143457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col10" class="data row11 col10" >0.500023</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col11" class="data row11 col11" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col12" class="data row11 col12" >0.197015</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col13" class="data row11 col13" >0.212379</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col14" class="data row11 col14" >0.458168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col15" class="data row11 col15" >0.19348</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col16" class="data row11 col16" >-0.306724</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col17" class="data row11 col17" >0.239872</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row11_col18" class="data row11 col18" >0.652206</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row12" class="row_heading level0 row12" >Negative_Emotion</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col0" class="data row12 col0" >-0.445301</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col1" class="data row12 col1" >-0.238163</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col2" class="data row12 col2" >0.031357</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col3" class="data row12 col3" >0.498956</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col4" class="data row12 col4" >-0.146686</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col5" class="data row12 col5" >0.62087</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col6" class="data row12 col6" >-0.264239</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col7" class="data row12 col7" >-0.237083</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col8" class="data row12 col8" >-0.406364</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col9" class="data row12 col9" >0.192124</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col10" class="data row12 col10" >0.0298938</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col11" class="data row12 col11" >0.197015</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col12" class="data row12 col12" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col13" class="data row12 col13" >0.438289</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col14" class="data row12 col14" >0.104457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col15" class="data row12 col15" >0.416563</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col16" class="data row12 col16" >0.122006</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col17" class="data row12 col17" >0.337952</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row12_col18" class="data row12 col18" >0.133373</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row13" class="row_heading level0 row13" >Social_support</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col0" class="data row13 col0" >-0.43543</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col1" class="data row13 col1" >-0.413618</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col2" class="data row13 col2" >0.392691</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col3" class="data row13 col3" >0.40035</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col4" class="data row13 col4" >0.450574</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col5" class="data row13 col5" >0.685918</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col6" class="data row13 col6" >-0.24824</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col7" class="data row13 col7" >0.190868</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col8" class="data row13 col8" >-0.178967</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col9" class="data row13 col9" >-0.37556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col10" class="data row13 col10" >0.643774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col11" class="data row13 col11" >0.212379</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col12" class="data row13 col12" >0.438289</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col13" class="data row13 col13" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col14" class="data row13 col14" >0.237195</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col15" class="data row13 col15" >-0.142341</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col16" class="data row13 col16" >0.531755</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col17" class="data row13 col17" >0.891857</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row13_col18" class="data row13 col18" >0.689395</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row14" class="row_heading level0 row14" >Freedom</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col0" class="data row14 col0" >0.0119791</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col1" class="data row14 col1" >0.0263323</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col2" class="data row14 col2" >-0.234598</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col3" class="data row14 col3" >-0.530802</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col4" class="data row14 col4" >0.348246</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col5" class="data row14 col5" >0.272426</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col6" class="data row14 col6" >-0.569927</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col7" class="data row14 col7" >-0.452072</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col8" class="data row14 col8" >-0.59716</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col9" class="data row14 col9" >0.376126</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col10" class="data row14 col10" >0.548645</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col11" class="data row14 col11" >0.458168</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col12" class="data row14 col12" >0.104457</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col13" class="data row14 col13" >0.237195</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col14" class="data row14 col14" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col15" class="data row14 col15" >0.134422</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col16" class="data row14 col16" >0.359568</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col17" class="data row14 col17" >0.0631891</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row14_col18" class="data row14 col18" >0.21081</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row15" class="row_heading level0 row15" >Corruption</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col0" class="data row15 col0" >0.263104</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col1" class="data row15 col1" >0.227503</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col2" class="data row15 col2" >-0.356244</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col3" class="data row15 col3" >-0.372781</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col4" class="data row15 col4" >-0.139093</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col5" class="data row15 col5" >0.0224253</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col6" class="data row15 col6" >-0.289279</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col7" class="data row15 col7" >-0.198946</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col8" class="data row15 col8" >-0.545012</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col9" class="data row15 col9" >0.366723</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col10" class="data row15 col10" >0.0292907</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col11" class="data row15 col11" >0.19348</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col12" class="data row15 col12" >0.416563</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col13" class="data row15 col13" >-0.142341</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col14" class="data row15 col14" >0.134422</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col15" class="data row15 col15" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col16" class="data row15 col16" >-0.500694</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col17" class="data row15 col17" >-0.0389486</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row15_col18" class="data row15 col18" >0.0565045</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row16" class="row_heading level0 row16" >Generosity</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col0" class="data row16 col0" >-0.232079</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col1" class="data row16 col1" >0.292736</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col2" class="data row16 col2" >-0.367243</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col3" class="data row16 col3" >0.149752</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col4" class="data row16 col4" >0.70518</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col5" class="data row16 col5" >0.761817</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col6" class="data row16 col6" >0.0816774</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col7" class="data row16 col7" >-0.509928</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col8" class="data row16 col8" >-0.516892</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col9" class="data row16 col9" >0.290232</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col10" class="data row16 col10" >0.407432</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col11" class="data row16 col11" >-0.306724</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col12" class="data row16 col12" >0.122006</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col13" class="data row16 col13" >0.531755</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col14" class="data row16 col14" >0.359568</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col15" class="data row16 col15" >-0.500694</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col16" class="data row16 col16" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col17" class="data row16 col17" >0.378785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row16_col18" class="data row16 col18" >0.0862997</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row17" class="row_heading level0 row17" >GDP_Contribution</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col0" class="data row17 col0" >-0.0920052</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col1" class="data row17 col1" >-0.489947</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col2" class="data row17 col2" >0.358511</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col3" class="data row17 col3" >0.284715</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col4" class="data row17 col4" >0.367556</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col5" class="data row17 col5" >0.645236</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col6" class="data row17 col6" >-0.395291</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col7" class="data row17 col7" >0.199727</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col8" class="data row17 col8" >-0.1186</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col9" class="data row17 col9" >-0.320605</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col10" class="data row17 col10" >0.761299</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col11" class="data row17 col11" >0.239872</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col12" class="data row17 col12" >0.337952</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col13" class="data row17 col13" >0.891857</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col14" class="data row17 col14" >0.0631891</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col15" class="data row17 col15" >-0.0389486</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col16" class="data row17 col16" >0.378785</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col17" class="data row17 col17" >1</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row17_col18" class="data row17 col18" >0.844461</td> 
    </tr>    <tr> 
        <th id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763level0_row18" class="row_heading level0 row18" >Healthy_life_expectancy</th> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col0" class="data row18 col0" >0.118197</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col1" class="data row18 col1" >-0.581175</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col2" class="data row18 col2" >0.405423</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col3" class="data row18 col3" >-0.0314921</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col4" class="data row18 col4" >0.149151</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col5" class="data row18 col5" >0.283841</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col6" class="data row18 col6" >-0.483878</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col7" class="data row18 col7" >0.335913</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col8" class="data row18 col8" >0.0544874</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col9" class="data row18 col9" >-0.354696</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col10" class="data row18 col10" >0.849367</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col11" class="data row18 col11" >0.652206</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col12" class="data row18 col12" >0.133373</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col13" class="data row18 col13" >0.689395</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col14" class="data row18 col14" >0.21081</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col15" class="data row18 col15" >0.0565045</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col16" class="data row18 col16" >0.0862997</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col17" class="data row18 col17" >0.844461</td> 
        <td id="T_b89ce43a_5e0b_11e9_94ec_98e0d97e0763row18_col18" class="data row18 col18" >1</td> 
    </tr></tbody> 
</table> 



# Bottom 10 Eco
Happiness Rank, Economic World Rank, R2= -0.35  
Happiness Health Life Expectancy, Economic World Rank, R2 = -0.58


```python

```
