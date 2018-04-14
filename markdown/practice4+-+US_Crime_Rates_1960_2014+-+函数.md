
# US_Crime_Rates_1960_2014数据 - 函数

![](images/4.jpeg)

### 导入数据


```python
import pandas as pd
```


```python
crime = pd.read_csv('data/US_Crime_Rates_1960_2014.csv')
crime.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 55 entries, 0 to 54
    Data columns (total 12 columns):
    Year                  55 non-null int64
    Population            55 non-null int64
    Total                 55 non-null int64
    Violent               55 non-null int64
    Property              55 non-null int64
    Murder                55 non-null int64
    Forcible_Rape         55 non-null int64
    Robbery               55 non-null int64
    Aggravated_assault    55 non-null int64
    Burglary              55 non-null int64
    Larceny_Theft         55 non-null int64
    Vehicle_Theft         55 non-null int64
    dtypes: int64(12)
    memory usage: 5.2 KB
    

### 将Year的数据类型转换为 datetime64  显示格式为年


```python
crime.Year = pd.to_datetime(crime.Year, format='%Y')
crime.Year.head(3)
```




    0   1960-01-01
    1   1961-01-01
    2   1962-01-01
    Name: Year, dtype: datetime64[ns]



### 将列Year设置为数据框的索引


```python
crime = crime.set_index('Year', drop=True) # drop 是否删除该列，默认为True
crime.head(3)
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
      <th>Population</th>
      <th>Total</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960-01-01</th>
      <td>179323175</td>
      <td>3384200</td>
      <td>288460</td>
      <td>3095700</td>
      <td>9110</td>
      <td>17190</td>
      <td>107840</td>
      <td>154320</td>
      <td>912100</td>
      <td>1855400</td>
      <td>328200</td>
    </tr>
    <tr>
      <th>1961-01-01</th>
      <td>182992000</td>
      <td>3488000</td>
      <td>289390</td>
      <td>3198600</td>
      <td>8740</td>
      <td>17220</td>
      <td>106670</td>
      <td>156760</td>
      <td>949600</td>
      <td>1913000</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>185771000</td>
      <td>3752200</td>
      <td>301510</td>
      <td>3450700</td>
      <td>8530</td>
      <td>17550</td>
      <td>110860</td>
      <td>164570</td>
      <td>994300</td>
      <td>2089600</td>
      <td>366800</td>
    </tr>
  </tbody>
</table>
</div>



### 删除名为Total的列


```python
del crime['Total']
crime.head(3)
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
      <th>Population</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960-01-01</th>
      <td>179323175</td>
      <td>288460</td>
      <td>3095700</td>
      <td>9110</td>
      <td>17190</td>
      <td>107840</td>
      <td>154320</td>
      <td>912100</td>
      <td>1855400</td>
      <td>328200</td>
    </tr>
    <tr>
      <th>1961-01-01</th>
      <td>182992000</td>
      <td>289390</td>
      <td>3198600</td>
      <td>8740</td>
      <td>17220</td>
      <td>106670</td>
      <td>156760</td>
      <td>949600</td>
      <td>1913000</td>
      <td>336000</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>185771000</td>
      <td>301510</td>
      <td>3450700</td>
      <td>8530</td>
      <td>17550</td>
      <td>110860</td>
      <td>164570</td>
      <td>994300</td>
      <td>2089600</td>
      <td>366800</td>
    </tr>
  </tbody>
</table>
</div>



### 按照Year对数据框进行分组并求和


```python
# 关于 .resample 的介绍
# https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.resample.html
# https://blog.csdn.net/wangshuang1631/article/details/52314944
# 更多关于 Offset Aliases的介绍 
# (http://pandas.pydata.org/pandas-docs/stable/timeseries.html#offset-aliases)

# AS = YS = year start
# 10AS = 以10年为周期执行重采样，获取每个10年的犯罪率
# 10年的重采样求和就是做10年数据的累加
crimes = crime.resample('10AS').sum()

# 10年的犯罪数可以累加，但是人口累加没有意义
# 用resample去得到“Population”列的最大值
population = crime['Population'].resample('10AS').max()

# 更新 "Population" 
crimes['Population'] = population

crimes
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
      <th>Population</th>
      <th>Violent</th>
      <th>Property</th>
      <th>Murder</th>
      <th>Forcible_Rape</th>
      <th>Robbery</th>
      <th>Aggravated_assault</th>
      <th>Burglary</th>
      <th>Larceny_Theft</th>
      <th>Vehicle_Theft</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1960-01-01</th>
      <td>201385000.0</td>
      <td>4134930</td>
      <td>45160900</td>
      <td>106180</td>
      <td>236720</td>
      <td>1633510</td>
      <td>2158520</td>
      <td>13321100</td>
      <td>26547700</td>
      <td>5292100</td>
    </tr>
    <tr>
      <th>1970-01-01</th>
      <td>220099000.0</td>
      <td>9607930</td>
      <td>91383800</td>
      <td>192230</td>
      <td>554570</td>
      <td>4159020</td>
      <td>4702120</td>
      <td>28486000</td>
      <td>53157800</td>
      <td>9739900</td>
    </tr>
    <tr>
      <th>1980-01-01</th>
      <td>248239000.0</td>
      <td>14074328</td>
      <td>117048900</td>
      <td>206439</td>
      <td>865639</td>
      <td>5383109</td>
      <td>7619130</td>
      <td>33073494</td>
      <td>72040253</td>
      <td>11935411</td>
    </tr>
    <tr>
      <th>1990-01-01</th>
      <td>272690813.0</td>
      <td>17527048</td>
      <td>119053499</td>
      <td>211664</td>
      <td>998827</td>
      <td>5748930</td>
      <td>10568963</td>
      <td>26750015</td>
      <td>77679366</td>
      <td>14624418</td>
    </tr>
    <tr>
      <th>2000-01-01</th>
      <td>307006550.0</td>
      <td>13968056</td>
      <td>100944369</td>
      <td>163068</td>
      <td>922499</td>
      <td>4230366</td>
      <td>8652124</td>
      <td>21565176</td>
      <td>67970291</td>
      <td>11412834</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>318857056.0</td>
      <td>6072017</td>
      <td>44095950</td>
      <td>72867</td>
      <td>421059</td>
      <td>1749809</td>
      <td>3764142</td>
      <td>10125170</td>
      <td>30401698</td>
      <td>3569080</td>
    </tr>
    <tr>
      <th>2020-01-01</th>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### 何时是美国历史上生存最危险的年代？


```python
crime = pd.read_csv('data/US_Crime_Rates_1960_2014.csv')
crime = crime.set_index('Year', drop=True)
crime.idxmax(0)
```




    Population            2014
    Total                 1991
    Violent               1992
    Property              1991
    Murder                1991
    Forcible_Rape         1992
    Robbery               1991
    Aggravated_assault    1993
    Burglary              1980
    Larceny_Theft         1991
    Vehicle_Theft         1991
    dtype: int64


