
# 自定义Pokemon数据 - 创建DataFrame

![](images/8.jpeg)

### 导入相关库


```python
import pandas as pd
```

### 创建一个数据字典


```python
raw_data = {"name": ['Bulbasaur', 'Charmander','Squirtle','Caterpie'],
            "evolution": ['Ivysaur','Charmeleon','Wartortle','Metapod'],
            "type": ['grass', 'fire', 'water', 'bug'],
            "hp": [45, 39, 44, 45],
            "pokedex": ['yes', 'no','yes','no']                        
            }
```

### 将数据字典存为一个名叫pokemon的数据框中


```python
pokemon = pd.DataFrame(raw_data)
pokemon.head()
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
      <th>evolution</th>
      <th>hp</th>
      <th>name</th>
      <th>pokedex</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ivysaur</td>
      <td>45</td>
      <td>Bulbasaur</td>
      <td>yes</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Charmeleon</td>
      <td>39</td>
      <td>Charmander</td>
      <td>no</td>
      <td>fire</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wartortle</td>
      <td>44</td>
      <td>Squirtle</td>
      <td>yes</td>
      <td>water</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Metapod</td>
      <td>45</td>
      <td>Caterpie</td>
      <td>no</td>
      <td>bug</td>
    </tr>
  </tbody>
</table>
</div>



### 数据框的列排序是字母顺序，请重新修改为name, type, hp, evolution, pokedex这个顺序


```python
pokemon = pokemon[['name', 'type', 'hp', 'evolution', 'pokedex']]
pokemon
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
      <th>name</th>
      <th>type</th>
      <th>hp</th>
      <th>evolution</th>
      <th>pokedex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>grass</td>
      <td>45</td>
      <td>Ivysaur</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Charmander</td>
      <td>fire</td>
      <td>39</td>
      <td>Charmeleon</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Squirtle</td>
      <td>water</td>
      <td>44</td>
      <td>Wartortle</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Caterpie</td>
      <td>bug</td>
      <td>45</td>
      <td>Metapod</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>



### 添加一个列place


```python
pokemon['place'] = ['park', 'street', 'lake', 'forest']
pokemon
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
      <th>name</th>
      <th>type</th>
      <th>hp</th>
      <th>evolution</th>
      <th>pokedex</th>
      <th>place</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bulbasaur</td>
      <td>grass</td>
      <td>45</td>
      <td>Ivysaur</td>
      <td>yes</td>
      <td>park</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Charmander</td>
      <td>fire</td>
      <td>39</td>
      <td>Charmeleon</td>
      <td>no</td>
      <td>street</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Squirtle</td>
      <td>water</td>
      <td>44</td>
      <td>Wartortle</td>
      <td>yes</td>
      <td>lake</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Caterpie</td>
      <td>bug</td>
      <td>45</td>
      <td>Metapod</td>
      <td>no</td>
      <td>forest</td>
    </tr>
  </tbody>
</table>
</div>



### 查看每个列的数据类型


```python
pokemon.dtypes
```




    name         object
    type         object
    hp            int64
    evolution    object
    pokedex      object
    place        object
    dtype: object


