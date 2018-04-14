
# 自定义数据 - 合并

![](images/5.jpg)

### 导入相关库


```python
import pandas as pd
```

### 创建数据


```python
raw_data_1 = {
        'subject_id': ['1', '2', '3', '4', '5'],
        'first_name': ['Alex', 'Amy', 'Allen', 'Alice', 'Ayoung'], 
        'last_name': ['Anderson', 'Ackerman', 'Ali', 'Aoni', 'Atiches']}

raw_data_2 = {
        'subject_id': ['4', '5', '6', '7', '8'],
        'first_name': ['Billy', 'Brian', 'Bran', 'Bryce', 'Betty'], 
        'last_name': ['Bonder', 'Black', 'Balwner', 'Brice', 'Btisan']}

raw_data_3 = {
        'subject_id': ['1', '2', '3', '4', '5', '7', '8', '9', '10', '11'],
        'test_id': [51, 15, 15, 61, 16, 14, 15, 1, 61, 16]}
```

### 将上述的数据框分别命名为data1, data2, data3


```python
data1 = pd.DataFrame(raw_data_1, columns = ['subject_id', 'first_name', 'last_name'])
data2 = pd.DataFrame(raw_data_2, columns = ['subject_id', 'first_name', 'last_name'])
data3 = pd.DataFrame(raw_data_3, columns = ['subject_id', 'test_id'])
```

### 将data1和data2两个数据框按照行的维度进行合并，命名为all_data


```python
all_data = pd.concat([data1, data2], axis=0)
all_data
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
      <th>subject_id</th>
      <th>first_name</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Alex</td>
      <td>Anderson</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Amy</td>
      <td>Ackerman</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Allen</td>
      <td>Ali</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alice</td>
      <td>Aoni</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Ayoung</td>
      <td>Atiches</td>
    </tr>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>Billy</td>
      <td>Bonder</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>Brian</td>
      <td>Black</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>Bran</td>
      <td>Balwner</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>Bryce</td>
      <td>Brice</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>Betty</td>
      <td>Btisan</td>
    </tr>
  </tbody>
</table>
</div>



### 将data1和data2两个数据框按照列的维度进行合并，命名为all_data_col


```python
all_data_col = pd.concat([data1, data2], axis=1)
all_data_col
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
      <th>subject_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>subject_id</th>
      <th>first_name</th>
      <th>last_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Alex</td>
      <td>Anderson</td>
      <td>4</td>
      <td>Billy</td>
      <td>Bonder</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Amy</td>
      <td>Ackerman</td>
      <td>5</td>
      <td>Brian</td>
      <td>Black</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Allen</td>
      <td>Ali</td>
      <td>6</td>
      <td>Bran</td>
      <td>Balwner</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alice</td>
      <td>Aoni</td>
      <td>7</td>
      <td>Bryce</td>
      <td>Brice</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Ayoung</td>
      <td>Atiches</td>
      <td>8</td>
      <td>Betty</td>
      <td>Btisan</td>
    </tr>
  </tbody>
</table>
</div>



### 打印data3


```python
data3
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
      <th>subject_id</th>
      <th>test_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>16</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7</td>
      <td>14</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>9</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>10</td>
      <td>61</td>
    </tr>
    <tr>
      <th>9</th>
      <td>11</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



### 按照subject_id的值对all_data和data3作合并


```python
pd.merge(all_data, data3, on='subject_id')
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
      <th>subject_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>test_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Alex</td>
      <td>Anderson</td>
      <td>51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Amy</td>
      <td>Ackerman</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Allen</td>
      <td>Ali</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alice</td>
      <td>Aoni</td>
      <td>61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Billy</td>
      <td>Bonder</td>
      <td>61</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Ayoung</td>
      <td>Atiches</td>
      <td>16</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>Brian</td>
      <td>Black</td>
      <td>16</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bryce</td>
      <td>Brice</td>
      <td>14</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Betty</td>
      <td>Btisan</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>



### 对data1和data2按照subject_id作连接


```python
pd.merge(data1, data2, on='subject_id')
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
      <th>subject_id</th>
      <th>first_name_x</th>
      <th>last_name_x</th>
      <th>first_name_y</th>
      <th>last_name_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>Alice</td>
      <td>Aoni</td>
      <td>Billy</td>
      <td>Bonder</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>Ayoung</td>
      <td>Atiches</td>
      <td>Brian</td>
      <td>Black</td>
    </tr>
  </tbody>
</table>
</div>



### 找到 data1 和 data2 合并之后的所有匹配结果


```python
pd.merge(data1, data2, on='subject_id', how='outer')
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
      <th>subject_id</th>
      <th>first_name_x</th>
      <th>last_name_x</th>
      <th>first_name_y</th>
      <th>last_name_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Alex</td>
      <td>Anderson</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Amy</td>
      <td>Ackerman</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Allen</td>
      <td>Ali</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alice</td>
      <td>Aoni</td>
      <td>Billy</td>
      <td>Bonder</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Ayoung</td>
      <td>Atiches</td>
      <td>Brian</td>
      <td>Black</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bran</td>
      <td>Balwner</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bryce</td>
      <td>Brice</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Betty</td>
      <td>Btisan</td>
    </tr>
  </tbody>
</table>
</div>


