
# 风速数据 - 统计

![](images/6.jpg)

### 加载数据


```python
import pandas as pd
import datetime
```


```python
data = pd.read_table('data/wind.data', sep='\s+', parse_dates=[[0, 1, 2]])
data.head()
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
      <th>Yr_Mo_Dy</th>
      <th>RPT</th>
      <th>VAL</th>
      <th>ROS</th>
      <th>KIL</th>
      <th>SHA</th>
      <th>BIR</th>
      <th>DUB</th>
      <th>CLA</th>
      <th>MUL</th>
      <th>CLO</th>
      <th>BEL</th>
      <th>MAL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2061-01-01</td>
      <td>15.04</td>
      <td>14.96</td>
      <td>13.17</td>
      <td>9.29</td>
      <td>NaN</td>
      <td>9.87</td>
      <td>13.67</td>
      <td>10.25</td>
      <td>10.83</td>
      <td>12.58</td>
      <td>18.50</td>
      <td>15.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2061-01-02</td>
      <td>14.71</td>
      <td>NaN</td>
      <td>10.83</td>
      <td>6.50</td>
      <td>12.62</td>
      <td>7.67</td>
      <td>11.50</td>
      <td>10.04</td>
      <td>9.79</td>
      <td>9.67</td>
      <td>17.54</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2061-01-03</td>
      <td>18.50</td>
      <td>16.88</td>
      <td>12.33</td>
      <td>10.13</td>
      <td>11.17</td>
      <td>6.17</td>
      <td>11.25</td>
      <td>NaN</td>
      <td>8.50</td>
      <td>7.67</td>
      <td>12.75</td>
      <td>12.71</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2061-01-04</td>
      <td>10.58</td>
      <td>6.63</td>
      <td>11.75</td>
      <td>4.58</td>
      <td>4.54</td>
      <td>2.88</td>
      <td>8.63</td>
      <td>1.79</td>
      <td>5.83</td>
      <td>5.88</td>
      <td>5.46</td>
      <td>10.88</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2061-01-05</td>
      <td>13.33</td>
      <td>13.25</td>
      <td>11.42</td>
      <td>6.17</td>
      <td>10.71</td>
      <td>8.21</td>
      <td>11.92</td>
      <td>6.54</td>
      <td>10.92</td>
      <td>10.34</td>
      <td>12.92</td>
      <td>11.83</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 6574 entries, 0 to 6573
    Data columns (total 13 columns):
    Yr_Mo_Dy    6574 non-null datetime64[ns]
    RPT         6568 non-null float64
    VAL         6571 non-null float64
    ROS         6572 non-null float64
    KIL         6569 non-null float64
    SHA         6572 non-null float64
    BIR         6574 non-null float64
    DUB         6571 non-null float64
    CLA         6572 non-null float64
    MUL         6571 non-null float64
    CLO         6573 non-null float64
    BEL         6574 non-null float64
    MAL         6570 non-null float64
    dtypes: datetime64[ns](1), float64(12)
    memory usage: 667.8 KB
    

### 对日期数据进行分析


```python
data.Yr_Mo_Dy.describe()
```




    count                    6574
    unique                   6574
    top       1968-11-10 00:00:00
    freq                        1
    first     1968-01-01 00:00:00
    last      2067-12-31 00:00:00
    Name: Yr_Mo_Dy, dtype: object



### 我们发现存在2067年？创建一个函数并用它去修复这个bug


```python
def fix_century(x):
    year = x.year - 100 if x.year > 1989 else x.year
    return datetime.date(year, x.month, x.day)
```


```python
data['Yr_Mo_Dy'] = data['Yr_Mo_Dy'].apply(fix_century)
data = data.set_index('Yr_Mo_Dy')
data.head(3)
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
      <th>RPT</th>
      <th>VAL</th>
      <th>ROS</th>
      <th>KIL</th>
      <th>SHA</th>
      <th>BIR</th>
      <th>DUB</th>
      <th>CLA</th>
      <th>MUL</th>
      <th>CLO</th>
      <th>BEL</th>
      <th>MAL</th>
    </tr>
    <tr>
      <th>Yr_Mo_Dy</th>
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
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1961-01-01</th>
      <td>15.04</td>
      <td>14.96</td>
      <td>13.17</td>
      <td>9.29</td>
      <td>NaN</td>
      <td>9.87</td>
      <td>13.67</td>
      <td>10.25</td>
      <td>10.83</td>
      <td>12.58</td>
      <td>18.50</td>
      <td>15.04</td>
    </tr>
    <tr>
      <th>1961-01-02</th>
      <td>14.71</td>
      <td>NaN</td>
      <td>10.83</td>
      <td>6.50</td>
      <td>12.62</td>
      <td>7.67</td>
      <td>11.50</td>
      <td>10.04</td>
      <td>9.79</td>
      <td>9.67</td>
      <td>17.54</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>1961-01-03</th>
      <td>18.50</td>
      <td>16.88</td>
      <td>12.33</td>
      <td>10.13</td>
      <td>11.17</td>
      <td>6.17</td>
      <td>11.25</td>
      <td>NaN</td>
      <td>8.50</td>
      <td>7.67</td>
      <td>12.75</td>
      <td>12.71</td>
    </tr>
  </tbody>
</table>
</div>



### 对应每一个location，一共有多少数据值缺失


```python
data.isnull().sum()
```




    RPT    6
    VAL    3
    ROS    2
    KIL    5
    SHA    2
    BIR    0
    DUB    3
    CLA    2
    MUL    3
    CLO    1
    BEL    0
    MAL    4
    dtype: int64



### 对应每一个location，一共有多少完整的数据值¶


```python
data.shape[1] - data.isnull().sum()
```




    RPT     6
    VAL     9
    ROS    10
    KIL     7
    SHA    10
    BIR    12
    DUB     9
    CLA    10
    MUL     9
    CLO    11
    BEL    12
    MAL     8
    dtype: int64



### 对于全体数据，计算风速的平均值


```python
data.mean().mean()
```




    10.227982360836924



### 创建一个名为loc_stats的数据框去计算并存储每个location的风速最小值，最大值，平均值和标准差


```python
loc_stats = pd.DataFrame()
loc_stats['min'] = data.min()
loc_stats['max'] = data.max()
loc_stats['mean'] = data.mean()
loc_stats['std'] = data.std()
loc_stats
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
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RPT</th>
      <td>0.67</td>
      <td>35.80</td>
      <td>12.362987</td>
      <td>5.618413</td>
    </tr>
    <tr>
      <th>VAL</th>
      <td>0.21</td>
      <td>33.37</td>
      <td>10.644314</td>
      <td>5.267356</td>
    </tr>
    <tr>
      <th>ROS</th>
      <td>1.50</td>
      <td>33.84</td>
      <td>11.660526</td>
      <td>5.008450</td>
    </tr>
    <tr>
      <th>KIL</th>
      <td>0.00</td>
      <td>28.46</td>
      <td>6.306468</td>
      <td>3.605811</td>
    </tr>
    <tr>
      <th>SHA</th>
      <td>0.13</td>
      <td>37.54</td>
      <td>10.455834</td>
      <td>4.936125</td>
    </tr>
    <tr>
      <th>BIR</th>
      <td>0.00</td>
      <td>26.16</td>
      <td>7.092254</td>
      <td>3.968683</td>
    </tr>
    <tr>
      <th>DUB</th>
      <td>0.00</td>
      <td>30.37</td>
      <td>9.797343</td>
      <td>4.977555</td>
    </tr>
    <tr>
      <th>CLA</th>
      <td>0.00</td>
      <td>31.08</td>
      <td>8.495053</td>
      <td>4.499449</td>
    </tr>
    <tr>
      <th>MUL</th>
      <td>0.00</td>
      <td>25.88</td>
      <td>8.493590</td>
      <td>4.166872</td>
    </tr>
    <tr>
      <th>CLO</th>
      <td>0.04</td>
      <td>28.21</td>
      <td>8.707332</td>
      <td>4.503954</td>
    </tr>
    <tr>
      <th>BEL</th>
      <td>0.13</td>
      <td>42.38</td>
      <td>13.121007</td>
      <td>5.835037</td>
    </tr>
    <tr>
      <th>MAL</th>
      <td>0.67</td>
      <td>42.54</td>
      <td>15.599079</td>
      <td>6.699794</td>
    </tr>
  </tbody>
</table>
</div>



### 创建一个名为day_stats的数据框去计算并存储所有location的风速最小值，最大值，平均值和标准差


```python
day_stats = pd.DataFrame()
day_stats['min'] = data.min(axis=1)
day_stats['max'] = data.max(axis=1)
day_stats['mean'] = data.mean(axis=1)
day_stats['std'] = data.std(axis=1)
day_stats.head()
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
      <th>min</th>
      <th>max</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>Yr_Mo_Dy</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1961-01-01</th>
      <td>9.29</td>
      <td>18.50</td>
      <td>13.018182</td>
      <td>2.808875</td>
    </tr>
    <tr>
      <th>1961-01-02</th>
      <td>6.50</td>
      <td>17.54</td>
      <td>11.336364</td>
      <td>3.188994</td>
    </tr>
    <tr>
      <th>1961-01-03</th>
      <td>6.17</td>
      <td>18.50</td>
      <td>11.641818</td>
      <td>3.681912</td>
    </tr>
    <tr>
      <th>1961-01-04</th>
      <td>1.79</td>
      <td>11.75</td>
      <td>6.619167</td>
      <td>3.198126</td>
    </tr>
    <tr>
      <th>1961-01-05</th>
      <td>6.17</td>
      <td>13.33</td>
      <td>10.630000</td>
      <td>2.445356</td>
    </tr>
  </tbody>
</table>
</div>



### 对于每一个location，计算一月份的平均风速


```python
data['date'] = data.index
data['year'] = data['date'].apply(lambda date: date.year)
data['month'] = data['date'].apply(lambda date: date.month)
data['day'] = data['date'].apply(lambda date: date.day)
january_winds = data.query('month == 1')
january_winds.loc[:, 'RPT':'MAL'].mean()
```




    RPT    14.847325
    VAL    12.914560
    ROS    13.299624
    KIL     7.199498
    SHA    11.667734
    BIR     8.054839
    DUB    11.819355
    CLA     9.512047
    MUL     9.543208
    CLO    10.053566
    BEL    14.550520
    MAL    18.028763
    dtype: float64



### 对于数据记录按照年为频率取样


```python
data.query('month == 1 and day == 1')
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
      <th>RPT</th>
      <th>VAL</th>
      <th>ROS</th>
      <th>KIL</th>
      <th>SHA</th>
      <th>BIR</th>
      <th>DUB</th>
      <th>CLA</th>
      <th>MUL</th>
      <th>CLO</th>
      <th>BEL</th>
      <th>MAL</th>
      <th>date</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Yr_Mo_Dy</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1961-01-01</th>
      <td>15.04</td>
      <td>14.96</td>
      <td>13.17</td>
      <td>9.29</td>
      <td>NaN</td>
      <td>9.87</td>
      <td>13.67</td>
      <td>10.25</td>
      <td>10.83</td>
      <td>12.58</td>
      <td>18.50</td>
      <td>15.04</td>
      <td>1961-01-01</td>
      <td>1961</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>9.29</td>
      <td>3.42</td>
      <td>11.54</td>
      <td>3.50</td>
      <td>2.21</td>
      <td>1.96</td>
      <td>10.41</td>
      <td>2.79</td>
      <td>3.54</td>
      <td>5.17</td>
      <td>4.38</td>
      <td>7.92</td>
      <td>1962-01-01</td>
      <td>1962</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-01-01</th>
      <td>15.59</td>
      <td>13.62</td>
      <td>19.79</td>
      <td>8.38</td>
      <td>12.25</td>
      <td>10.00</td>
      <td>23.45</td>
      <td>15.71</td>
      <td>13.59</td>
      <td>14.37</td>
      <td>17.58</td>
      <td>34.13</td>
      <td>1963-01-01</td>
      <td>1963</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1964-01-01</th>
      <td>25.80</td>
      <td>22.13</td>
      <td>18.21</td>
      <td>13.25</td>
      <td>21.29</td>
      <td>14.79</td>
      <td>14.12</td>
      <td>19.58</td>
      <td>13.25</td>
      <td>16.75</td>
      <td>28.96</td>
      <td>21.00</td>
      <td>1964-01-01</td>
      <td>1964</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1965-01-01</th>
      <td>9.54</td>
      <td>11.92</td>
      <td>9.00</td>
      <td>4.38</td>
      <td>6.08</td>
      <td>5.21</td>
      <td>10.25</td>
      <td>6.08</td>
      <td>5.71</td>
      <td>8.63</td>
      <td>12.04</td>
      <td>17.41</td>
      <td>1965-01-01</td>
      <td>1965</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1966-01-01</th>
      <td>22.04</td>
      <td>21.50</td>
      <td>17.08</td>
      <td>12.75</td>
      <td>22.17</td>
      <td>15.59</td>
      <td>21.79</td>
      <td>18.12</td>
      <td>16.66</td>
      <td>17.83</td>
      <td>28.33</td>
      <td>23.79</td>
      <td>1966-01-01</td>
      <td>1966</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1967-01-01</th>
      <td>6.46</td>
      <td>4.46</td>
      <td>6.50</td>
      <td>3.21</td>
      <td>6.67</td>
      <td>3.79</td>
      <td>11.38</td>
      <td>3.83</td>
      <td>7.71</td>
      <td>9.08</td>
      <td>10.67</td>
      <td>20.91</td>
      <td>1967-01-01</td>
      <td>1967</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1968-01-01</th>
      <td>30.04</td>
      <td>17.88</td>
      <td>16.25</td>
      <td>16.25</td>
      <td>21.79</td>
      <td>12.54</td>
      <td>18.16</td>
      <td>16.62</td>
      <td>18.75</td>
      <td>17.62</td>
      <td>22.25</td>
      <td>27.29</td>
      <td>1968-01-01</td>
      <td>1968</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1969-01-01</th>
      <td>6.13</td>
      <td>1.63</td>
      <td>5.41</td>
      <td>1.08</td>
      <td>2.54</td>
      <td>1.00</td>
      <td>8.50</td>
      <td>2.42</td>
      <td>4.58</td>
      <td>6.34</td>
      <td>9.17</td>
      <td>16.71</td>
      <td>1969-01-01</td>
      <td>1969</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1970-01-01</th>
      <td>9.59</td>
      <td>2.96</td>
      <td>11.79</td>
      <td>3.42</td>
      <td>6.13</td>
      <td>4.08</td>
      <td>9.00</td>
      <td>4.46</td>
      <td>7.29</td>
      <td>3.50</td>
      <td>7.33</td>
      <td>13.00</td>
      <td>1970-01-01</td>
      <td>1970</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1971-01-01</th>
      <td>3.71</td>
      <td>0.79</td>
      <td>4.71</td>
      <td>0.17</td>
      <td>1.42</td>
      <td>1.04</td>
      <td>4.63</td>
      <td>0.75</td>
      <td>1.54</td>
      <td>1.08</td>
      <td>4.21</td>
      <td>9.54</td>
      <td>1971-01-01</td>
      <td>1971</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1972-01-01</th>
      <td>9.29</td>
      <td>3.63</td>
      <td>14.54</td>
      <td>4.25</td>
      <td>6.75</td>
      <td>4.42</td>
      <td>13.00</td>
      <td>5.33</td>
      <td>10.04</td>
      <td>8.54</td>
      <td>8.71</td>
      <td>19.17</td>
      <td>1972-01-01</td>
      <td>1972</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1973-01-01</th>
      <td>16.50</td>
      <td>15.92</td>
      <td>14.62</td>
      <td>7.41</td>
      <td>8.29</td>
      <td>11.21</td>
      <td>13.54</td>
      <td>7.79</td>
      <td>10.46</td>
      <td>10.79</td>
      <td>13.37</td>
      <td>9.71</td>
      <td>1973-01-01</td>
      <td>1973</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1974-01-01</th>
      <td>23.21</td>
      <td>16.54</td>
      <td>16.08</td>
      <td>9.75</td>
      <td>15.83</td>
      <td>11.46</td>
      <td>9.54</td>
      <td>13.54</td>
      <td>13.83</td>
      <td>16.66</td>
      <td>17.21</td>
      <td>25.29</td>
      <td>1974-01-01</td>
      <td>1974</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1975-01-01</th>
      <td>14.04</td>
      <td>13.54</td>
      <td>11.29</td>
      <td>5.46</td>
      <td>12.58</td>
      <td>5.58</td>
      <td>8.12</td>
      <td>8.96</td>
      <td>9.29</td>
      <td>5.17</td>
      <td>7.71</td>
      <td>11.63</td>
      <td>1975-01-01</td>
      <td>1975</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-01-01</th>
      <td>18.34</td>
      <td>17.67</td>
      <td>14.83</td>
      <td>8.00</td>
      <td>16.62</td>
      <td>10.13</td>
      <td>13.17</td>
      <td>9.04</td>
      <td>13.13</td>
      <td>5.75</td>
      <td>11.38</td>
      <td>14.96</td>
      <td>1976-01-01</td>
      <td>1976</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-01-01</th>
      <td>20.04</td>
      <td>11.92</td>
      <td>20.25</td>
      <td>9.13</td>
      <td>9.29</td>
      <td>8.04</td>
      <td>10.75</td>
      <td>5.88</td>
      <td>9.00</td>
      <td>9.00</td>
      <td>14.88</td>
      <td>25.70</td>
      <td>1977-01-01</td>
      <td>1977</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-01-01</th>
      <td>8.33</td>
      <td>7.12</td>
      <td>7.71</td>
      <td>3.54</td>
      <td>8.50</td>
      <td>7.50</td>
      <td>14.71</td>
      <td>10.00</td>
      <td>11.83</td>
      <td>10.00</td>
      <td>15.09</td>
      <td>20.46</td>
      <td>1978-01-01</td>
      <td>1978</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### 对于数据记录按照月为频率取样


```python
data.query('day == 1')
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
      <th>RPT</th>
      <th>VAL</th>
      <th>ROS</th>
      <th>KIL</th>
      <th>SHA</th>
      <th>BIR</th>
      <th>DUB</th>
      <th>CLA</th>
      <th>MUL</th>
      <th>CLO</th>
      <th>BEL</th>
      <th>MAL</th>
      <th>date</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Yr_Mo_Dy</th>
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
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1961-01-01</th>
      <td>15.04</td>
      <td>14.96</td>
      <td>13.17</td>
      <td>9.29</td>
      <td>NaN</td>
      <td>9.87</td>
      <td>13.67</td>
      <td>10.25</td>
      <td>10.83</td>
      <td>12.58</td>
      <td>18.50</td>
      <td>15.04</td>
      <td>1961-01-01</td>
      <td>1961</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-02-01</th>
      <td>14.25</td>
      <td>15.12</td>
      <td>9.04</td>
      <td>5.88</td>
      <td>12.08</td>
      <td>7.17</td>
      <td>10.17</td>
      <td>3.63</td>
      <td>6.50</td>
      <td>5.50</td>
      <td>9.17</td>
      <td>8.00</td>
      <td>1961-02-01</td>
      <td>1961</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-03-01</th>
      <td>12.67</td>
      <td>13.13</td>
      <td>11.79</td>
      <td>6.42</td>
      <td>9.79</td>
      <td>8.54</td>
      <td>10.25</td>
      <td>13.29</td>
      <td>NaN</td>
      <td>12.21</td>
      <td>20.62</td>
      <td>NaN</td>
      <td>1961-03-01</td>
      <td>1961</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-04-01</th>
      <td>8.38</td>
      <td>6.34</td>
      <td>8.33</td>
      <td>6.75</td>
      <td>9.33</td>
      <td>9.54</td>
      <td>11.67</td>
      <td>8.21</td>
      <td>11.21</td>
      <td>6.46</td>
      <td>11.96</td>
      <td>7.17</td>
      <td>1961-04-01</td>
      <td>1961</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-05-01</th>
      <td>15.87</td>
      <td>13.88</td>
      <td>15.37</td>
      <td>9.79</td>
      <td>13.46</td>
      <td>10.17</td>
      <td>9.96</td>
      <td>14.04</td>
      <td>9.75</td>
      <td>9.92</td>
      <td>18.63</td>
      <td>11.12</td>
      <td>1961-05-01</td>
      <td>1961</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-06-01</th>
      <td>15.92</td>
      <td>9.59</td>
      <td>12.04</td>
      <td>8.79</td>
      <td>11.54</td>
      <td>6.04</td>
      <td>9.75</td>
      <td>8.29</td>
      <td>9.33</td>
      <td>10.34</td>
      <td>10.67</td>
      <td>12.12</td>
      <td>1961-06-01</td>
      <td>1961</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-07-01</th>
      <td>7.21</td>
      <td>6.83</td>
      <td>7.71</td>
      <td>4.42</td>
      <td>8.46</td>
      <td>4.79</td>
      <td>6.71</td>
      <td>6.00</td>
      <td>5.79</td>
      <td>7.96</td>
      <td>6.96</td>
      <td>8.71</td>
      <td>1961-07-01</td>
      <td>1961</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-08-01</th>
      <td>9.59</td>
      <td>5.09</td>
      <td>5.54</td>
      <td>4.63</td>
      <td>8.29</td>
      <td>5.25</td>
      <td>4.21</td>
      <td>5.25</td>
      <td>5.37</td>
      <td>5.41</td>
      <td>8.38</td>
      <td>9.08</td>
      <td>1961-08-01</td>
      <td>1961</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-09-01</th>
      <td>5.58</td>
      <td>1.13</td>
      <td>4.96</td>
      <td>3.04</td>
      <td>4.25</td>
      <td>2.25</td>
      <td>4.63</td>
      <td>2.71</td>
      <td>3.67</td>
      <td>6.00</td>
      <td>4.79</td>
      <td>5.41</td>
      <td>1961-09-01</td>
      <td>1961</td>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-10-01</th>
      <td>14.25</td>
      <td>12.87</td>
      <td>7.87</td>
      <td>8.00</td>
      <td>13.00</td>
      <td>7.75</td>
      <td>5.83</td>
      <td>9.00</td>
      <td>7.08</td>
      <td>5.29</td>
      <td>11.79</td>
      <td>4.04</td>
      <td>1961-10-01</td>
      <td>1961</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-11-01</th>
      <td>13.21</td>
      <td>13.13</td>
      <td>14.33</td>
      <td>8.54</td>
      <td>12.17</td>
      <td>10.21</td>
      <td>13.08</td>
      <td>12.17</td>
      <td>10.92</td>
      <td>13.54</td>
      <td>20.17</td>
      <td>20.04</td>
      <td>1961-11-01</td>
      <td>1961</td>
      <td>11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1961-12-01</th>
      <td>9.67</td>
      <td>7.75</td>
      <td>8.00</td>
      <td>3.96</td>
      <td>6.00</td>
      <td>2.75</td>
      <td>7.25</td>
      <td>2.50</td>
      <td>5.58</td>
      <td>5.58</td>
      <td>7.79</td>
      <td>11.17</td>
      <td>1961-12-01</td>
      <td>1961</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-01-01</th>
      <td>9.29</td>
      <td>3.42</td>
      <td>11.54</td>
      <td>3.50</td>
      <td>2.21</td>
      <td>1.96</td>
      <td>10.41</td>
      <td>2.79</td>
      <td>3.54</td>
      <td>5.17</td>
      <td>4.38</td>
      <td>7.92</td>
      <td>1962-01-01</td>
      <td>1962</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-02-01</th>
      <td>19.12</td>
      <td>13.96</td>
      <td>12.21</td>
      <td>10.58</td>
      <td>15.71</td>
      <td>10.63</td>
      <td>15.71</td>
      <td>11.08</td>
      <td>13.17</td>
      <td>12.62</td>
      <td>17.67</td>
      <td>22.71</td>
      <td>1962-02-01</td>
      <td>1962</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-03-01</th>
      <td>8.21</td>
      <td>4.83</td>
      <td>9.00</td>
      <td>4.83</td>
      <td>6.00</td>
      <td>2.21</td>
      <td>7.96</td>
      <td>1.87</td>
      <td>4.08</td>
      <td>3.92</td>
      <td>4.08</td>
      <td>5.41</td>
      <td>1962-03-01</td>
      <td>1962</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-04-01</th>
      <td>14.33</td>
      <td>12.25</td>
      <td>11.87</td>
      <td>10.37</td>
      <td>14.92</td>
      <td>11.00</td>
      <td>19.79</td>
      <td>11.67</td>
      <td>14.09</td>
      <td>15.46</td>
      <td>16.62</td>
      <td>23.58</td>
      <td>1962-04-01</td>
      <td>1962</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-05-01</th>
      <td>9.62</td>
      <td>9.54</td>
      <td>3.58</td>
      <td>3.33</td>
      <td>8.75</td>
      <td>3.75</td>
      <td>2.25</td>
      <td>2.58</td>
      <td>1.67</td>
      <td>2.37</td>
      <td>7.29</td>
      <td>3.25</td>
      <td>1962-05-01</td>
      <td>1962</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-06-01</th>
      <td>5.88</td>
      <td>6.29</td>
      <td>8.67</td>
      <td>5.21</td>
      <td>5.00</td>
      <td>4.25</td>
      <td>5.91</td>
      <td>5.41</td>
      <td>4.79</td>
      <td>9.25</td>
      <td>5.25</td>
      <td>10.71</td>
      <td>1962-06-01</td>
      <td>1962</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-07-01</th>
      <td>8.67</td>
      <td>4.17</td>
      <td>6.92</td>
      <td>6.71</td>
      <td>8.17</td>
      <td>5.66</td>
      <td>11.17</td>
      <td>9.38</td>
      <td>8.75</td>
      <td>11.12</td>
      <td>10.25</td>
      <td>17.08</td>
      <td>1962-07-01</td>
      <td>1962</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-08-01</th>
      <td>4.58</td>
      <td>5.37</td>
      <td>6.04</td>
      <td>2.29</td>
      <td>7.87</td>
      <td>3.71</td>
      <td>4.46</td>
      <td>2.58</td>
      <td>4.00</td>
      <td>4.79</td>
      <td>7.21</td>
      <td>7.46</td>
      <td>1962-08-01</td>
      <td>1962</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-09-01</th>
      <td>10.00</td>
      <td>12.08</td>
      <td>10.96</td>
      <td>9.25</td>
      <td>9.29</td>
      <td>7.62</td>
      <td>7.41</td>
      <td>8.75</td>
      <td>7.67</td>
      <td>9.62</td>
      <td>14.58</td>
      <td>11.92</td>
      <td>1962-09-01</td>
      <td>1962</td>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-10-01</th>
      <td>14.58</td>
      <td>7.83</td>
      <td>19.21</td>
      <td>10.08</td>
      <td>11.54</td>
      <td>8.38</td>
      <td>13.29</td>
      <td>10.63</td>
      <td>8.21</td>
      <td>12.92</td>
      <td>18.05</td>
      <td>18.12</td>
      <td>1962-10-01</td>
      <td>1962</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-11-01</th>
      <td>16.88</td>
      <td>13.25</td>
      <td>16.00</td>
      <td>8.96</td>
      <td>13.46</td>
      <td>11.46</td>
      <td>10.46</td>
      <td>10.17</td>
      <td>10.37</td>
      <td>13.21</td>
      <td>14.83</td>
      <td>15.16</td>
      <td>1962-11-01</td>
      <td>1962</td>
      <td>11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1962-12-01</th>
      <td>18.38</td>
      <td>15.41</td>
      <td>11.75</td>
      <td>6.79</td>
      <td>12.21</td>
      <td>8.04</td>
      <td>8.42</td>
      <td>10.83</td>
      <td>5.66</td>
      <td>9.08</td>
      <td>11.50</td>
      <td>11.50</td>
      <td>1962-12-01</td>
      <td>1962</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-01-01</th>
      <td>15.59</td>
      <td>13.62</td>
      <td>19.79</td>
      <td>8.38</td>
      <td>12.25</td>
      <td>10.00</td>
      <td>23.45</td>
      <td>15.71</td>
      <td>13.59</td>
      <td>14.37</td>
      <td>17.58</td>
      <td>34.13</td>
      <td>1963-01-01</td>
      <td>1963</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-02-01</th>
      <td>15.41</td>
      <td>7.62</td>
      <td>24.67</td>
      <td>11.42</td>
      <td>9.21</td>
      <td>8.17</td>
      <td>14.04</td>
      <td>7.54</td>
      <td>7.54</td>
      <td>10.08</td>
      <td>10.17</td>
      <td>17.67</td>
      <td>1963-02-01</td>
      <td>1963</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-03-01</th>
      <td>16.75</td>
      <td>19.67</td>
      <td>17.67</td>
      <td>8.87</td>
      <td>19.08</td>
      <td>15.37</td>
      <td>16.21</td>
      <td>14.29</td>
      <td>11.29</td>
      <td>9.21</td>
      <td>19.92</td>
      <td>19.79</td>
      <td>1963-03-01</td>
      <td>1963</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-04-01</th>
      <td>10.54</td>
      <td>9.59</td>
      <td>12.46</td>
      <td>7.33</td>
      <td>9.46</td>
      <td>9.59</td>
      <td>11.79</td>
      <td>11.87</td>
      <td>9.79</td>
      <td>10.71</td>
      <td>13.37</td>
      <td>18.21</td>
      <td>1963-04-01</td>
      <td>1963</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-05-01</th>
      <td>18.79</td>
      <td>14.17</td>
      <td>13.59</td>
      <td>11.63</td>
      <td>14.17</td>
      <td>11.96</td>
      <td>14.46</td>
      <td>12.46</td>
      <td>12.87</td>
      <td>13.96</td>
      <td>15.29</td>
      <td>21.62</td>
      <td>1963-05-01</td>
      <td>1963</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1963-06-01</th>
      <td>13.37</td>
      <td>6.87</td>
      <td>12.00</td>
      <td>8.50</td>
      <td>10.04</td>
      <td>9.42</td>
      <td>10.92</td>
      <td>12.96</td>
      <td>11.79</td>
      <td>11.04</td>
      <td>10.92</td>
      <td>13.67</td>
      <td>1963-06-01</td>
      <td>1963</td>
      <td>6</td>
      <td>1</td>
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
    </tr>
    <tr>
      <th>1976-07-01</th>
      <td>8.50</td>
      <td>1.75</td>
      <td>6.58</td>
      <td>2.13</td>
      <td>2.75</td>
      <td>2.21</td>
      <td>5.37</td>
      <td>2.04</td>
      <td>5.88</td>
      <td>4.50</td>
      <td>4.96</td>
      <td>10.63</td>
      <td>1976-07-01</td>
      <td>1976</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-08-01</th>
      <td>13.00</td>
      <td>8.38</td>
      <td>8.63</td>
      <td>5.83</td>
      <td>12.92</td>
      <td>8.25</td>
      <td>13.00</td>
      <td>9.42</td>
      <td>10.58</td>
      <td>11.34</td>
      <td>14.21</td>
      <td>20.25</td>
      <td>1976-08-01</td>
      <td>1976</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-09-01</th>
      <td>11.87</td>
      <td>11.00</td>
      <td>7.38</td>
      <td>6.87</td>
      <td>7.75</td>
      <td>8.33</td>
      <td>10.34</td>
      <td>6.46</td>
      <td>10.17</td>
      <td>9.29</td>
      <td>12.75</td>
      <td>19.55</td>
      <td>1976-09-01</td>
      <td>1976</td>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-10-01</th>
      <td>10.96</td>
      <td>6.71</td>
      <td>10.41</td>
      <td>4.63</td>
      <td>7.58</td>
      <td>5.04</td>
      <td>5.04</td>
      <td>5.54</td>
      <td>6.50</td>
      <td>3.92</td>
      <td>6.79</td>
      <td>5.00</td>
      <td>1976-10-01</td>
      <td>1976</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-11-01</th>
      <td>13.96</td>
      <td>15.67</td>
      <td>10.29</td>
      <td>6.46</td>
      <td>12.79</td>
      <td>9.08</td>
      <td>10.00</td>
      <td>9.67</td>
      <td>10.21</td>
      <td>11.63</td>
      <td>23.09</td>
      <td>21.96</td>
      <td>1976-11-01</td>
      <td>1976</td>
      <td>11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1976-12-01</th>
      <td>13.46</td>
      <td>16.42</td>
      <td>9.21</td>
      <td>4.54</td>
      <td>10.75</td>
      <td>8.67</td>
      <td>10.88</td>
      <td>4.83</td>
      <td>8.79</td>
      <td>5.91</td>
      <td>8.83</td>
      <td>13.67</td>
      <td>1976-12-01</td>
      <td>1976</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-01-01</th>
      <td>20.04</td>
      <td>11.92</td>
      <td>20.25</td>
      <td>9.13</td>
      <td>9.29</td>
      <td>8.04</td>
      <td>10.75</td>
      <td>5.88</td>
      <td>9.00</td>
      <td>9.00</td>
      <td>14.88</td>
      <td>25.70</td>
      <td>1977-01-01</td>
      <td>1977</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-02-01</th>
      <td>11.83</td>
      <td>9.71</td>
      <td>11.00</td>
      <td>4.25</td>
      <td>8.58</td>
      <td>8.71</td>
      <td>6.17</td>
      <td>5.66</td>
      <td>8.29</td>
      <td>7.58</td>
      <td>11.71</td>
      <td>16.50</td>
      <td>1977-02-01</td>
      <td>1977</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-03-01</th>
      <td>8.63</td>
      <td>14.83</td>
      <td>10.29</td>
      <td>3.75</td>
      <td>6.63</td>
      <td>8.79</td>
      <td>5.00</td>
      <td>8.12</td>
      <td>7.87</td>
      <td>6.42</td>
      <td>13.54</td>
      <td>13.67</td>
      <td>1977-03-01</td>
      <td>1977</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-04-01</th>
      <td>21.67</td>
      <td>16.00</td>
      <td>17.33</td>
      <td>13.59</td>
      <td>20.83</td>
      <td>15.96</td>
      <td>25.62</td>
      <td>17.62</td>
      <td>19.41</td>
      <td>20.67</td>
      <td>24.37</td>
      <td>30.09</td>
      <td>1977-04-01</td>
      <td>1977</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-05-01</th>
      <td>6.42</td>
      <td>7.12</td>
      <td>8.67</td>
      <td>3.58</td>
      <td>4.58</td>
      <td>4.00</td>
      <td>6.75</td>
      <td>6.13</td>
      <td>3.33</td>
      <td>4.50</td>
      <td>19.21</td>
      <td>12.38</td>
      <td>1977-05-01</td>
      <td>1977</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-06-01</th>
      <td>7.08</td>
      <td>5.25</td>
      <td>9.71</td>
      <td>2.83</td>
      <td>2.21</td>
      <td>3.50</td>
      <td>5.29</td>
      <td>1.42</td>
      <td>2.00</td>
      <td>0.92</td>
      <td>5.21</td>
      <td>5.63</td>
      <td>1977-06-01</td>
      <td>1977</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-07-01</th>
      <td>15.41</td>
      <td>16.29</td>
      <td>17.08</td>
      <td>6.25</td>
      <td>11.83</td>
      <td>11.83</td>
      <td>12.29</td>
      <td>10.58</td>
      <td>10.41</td>
      <td>7.21</td>
      <td>17.37</td>
      <td>7.83</td>
      <td>1977-07-01</td>
      <td>1977</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-08-01</th>
      <td>4.33</td>
      <td>2.96</td>
      <td>4.42</td>
      <td>2.33</td>
      <td>0.96</td>
      <td>1.08</td>
      <td>4.96</td>
      <td>1.87</td>
      <td>2.33</td>
      <td>2.04</td>
      <td>10.50</td>
      <td>9.83</td>
      <td>1977-08-01</td>
      <td>1977</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-09-01</th>
      <td>17.37</td>
      <td>16.33</td>
      <td>16.83</td>
      <td>8.58</td>
      <td>14.46</td>
      <td>11.83</td>
      <td>15.09</td>
      <td>13.92</td>
      <td>13.29</td>
      <td>13.88</td>
      <td>23.29</td>
      <td>25.17</td>
      <td>1977-09-01</td>
      <td>1977</td>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-10-01</th>
      <td>16.75</td>
      <td>15.34</td>
      <td>12.25</td>
      <td>9.42</td>
      <td>16.38</td>
      <td>11.38</td>
      <td>18.50</td>
      <td>13.92</td>
      <td>14.09</td>
      <td>14.46</td>
      <td>22.34</td>
      <td>29.67</td>
      <td>1977-10-01</td>
      <td>1977</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-11-01</th>
      <td>16.71</td>
      <td>11.54</td>
      <td>12.17</td>
      <td>4.17</td>
      <td>8.54</td>
      <td>7.17</td>
      <td>11.12</td>
      <td>6.46</td>
      <td>8.25</td>
      <td>6.21</td>
      <td>11.04</td>
      <td>15.63</td>
      <td>1977-11-01</td>
      <td>1977</td>
      <td>11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1977-12-01</th>
      <td>13.37</td>
      <td>10.92</td>
      <td>12.42</td>
      <td>2.37</td>
      <td>5.79</td>
      <td>6.13</td>
      <td>8.96</td>
      <td>7.38</td>
      <td>6.29</td>
      <td>5.71</td>
      <td>8.54</td>
      <td>12.42</td>
      <td>1977-12-01</td>
      <td>1977</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-01-01</th>
      <td>8.33</td>
      <td>7.12</td>
      <td>7.71</td>
      <td>3.54</td>
      <td>8.50</td>
      <td>7.50</td>
      <td>14.71</td>
      <td>10.00</td>
      <td>11.83</td>
      <td>10.00</td>
      <td>15.09</td>
      <td>20.46</td>
      <td>1978-01-01</td>
      <td>1978</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-02-01</th>
      <td>27.25</td>
      <td>24.21</td>
      <td>18.16</td>
      <td>17.46</td>
      <td>27.54</td>
      <td>18.05</td>
      <td>20.96</td>
      <td>25.04</td>
      <td>20.04</td>
      <td>17.50</td>
      <td>27.71</td>
      <td>21.12</td>
      <td>1978-02-01</td>
      <td>1978</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-03-01</th>
      <td>15.04</td>
      <td>6.21</td>
      <td>16.04</td>
      <td>7.87</td>
      <td>6.42</td>
      <td>6.67</td>
      <td>12.29</td>
      <td>8.00</td>
      <td>10.58</td>
      <td>9.33</td>
      <td>5.41</td>
      <td>17.00</td>
      <td>1978-03-01</td>
      <td>1978</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-04-01</th>
      <td>3.42</td>
      <td>7.58</td>
      <td>2.71</td>
      <td>1.38</td>
      <td>3.46</td>
      <td>2.08</td>
      <td>2.67</td>
      <td>4.75</td>
      <td>4.83</td>
      <td>1.67</td>
      <td>7.33</td>
      <td>13.67</td>
      <td>1978-04-01</td>
      <td>1978</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-05-01</th>
      <td>10.54</td>
      <td>12.21</td>
      <td>9.08</td>
      <td>5.29</td>
      <td>11.00</td>
      <td>10.08</td>
      <td>11.17</td>
      <td>13.75</td>
      <td>11.87</td>
      <td>11.79</td>
      <td>12.87</td>
      <td>27.16</td>
      <td>1978-05-01</td>
      <td>1978</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-06-01</th>
      <td>10.37</td>
      <td>11.42</td>
      <td>6.46</td>
      <td>6.04</td>
      <td>11.25</td>
      <td>7.50</td>
      <td>6.46</td>
      <td>5.96</td>
      <td>7.79</td>
      <td>5.46</td>
      <td>5.50</td>
      <td>10.41</td>
      <td>1978-06-01</td>
      <td>1978</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-07-01</th>
      <td>12.46</td>
      <td>10.63</td>
      <td>11.17</td>
      <td>6.75</td>
      <td>12.92</td>
      <td>9.04</td>
      <td>12.42</td>
      <td>9.62</td>
      <td>12.08</td>
      <td>8.04</td>
      <td>14.04</td>
      <td>16.17</td>
      <td>1978-07-01</td>
      <td>1978</td>
      <td>7</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-08-01</th>
      <td>19.33</td>
      <td>15.09</td>
      <td>20.17</td>
      <td>8.83</td>
      <td>12.62</td>
      <td>10.41</td>
      <td>9.33</td>
      <td>12.33</td>
      <td>9.50</td>
      <td>9.92</td>
      <td>15.75</td>
      <td>18.00</td>
      <td>1978-08-01</td>
      <td>1978</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-09-01</th>
      <td>8.42</td>
      <td>6.13</td>
      <td>9.87</td>
      <td>5.25</td>
      <td>3.21</td>
      <td>5.71</td>
      <td>7.25</td>
      <td>3.50</td>
      <td>7.33</td>
      <td>6.50</td>
      <td>7.62</td>
      <td>15.96</td>
      <td>1978-09-01</td>
      <td>1978</td>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-10-01</th>
      <td>9.50</td>
      <td>6.83</td>
      <td>10.50</td>
      <td>3.88</td>
      <td>6.13</td>
      <td>4.58</td>
      <td>4.21</td>
      <td>6.50</td>
      <td>6.38</td>
      <td>6.54</td>
      <td>10.63</td>
      <td>14.09</td>
      <td>1978-10-01</td>
      <td>1978</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-11-01</th>
      <td>13.59</td>
      <td>16.75</td>
      <td>11.25</td>
      <td>7.08</td>
      <td>11.04</td>
      <td>8.33</td>
      <td>8.17</td>
      <td>11.29</td>
      <td>10.75</td>
      <td>11.25</td>
      <td>23.13</td>
      <td>25.00</td>
      <td>1978-11-01</td>
      <td>1978</td>
      <td>11</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1978-12-01</th>
      <td>21.29</td>
      <td>16.29</td>
      <td>24.04</td>
      <td>12.79</td>
      <td>18.21</td>
      <td>19.29</td>
      <td>21.54</td>
      <td>17.21</td>
      <td>16.71</td>
      <td>17.83</td>
      <td>17.75</td>
      <td>25.70</td>
      <td>1978-12-01</td>
      <td>1978</td>
      <td>12</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>216 rows × 16 columns</p>
</div>


