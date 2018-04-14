
# Chipotle快餐数据 - 了解数据

![](images/1.jpeg)

### 1. 从文件中加载数据，并查看数据前3行


```python
# 导入pandas库并命名为pd
import pandas as pd
```


```python
!ls data
```

    chipotle.tsv
    


```python
# 加载数据
chipo = pd.read_csv('data/chipotle.tsv', sep='\t')
```


```python
chipo.head(3)
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>NaN</td>
      <td>$2.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Izze</td>
      <td>[Clementine]</td>
      <td>$3.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1</td>
      <td>Nantucket Nectar</td>
      <td>[Apple]</td>
      <td>$3.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看各列的数据类型
chipo.dtypes
```




    order_id               int64
    quantity               int64
    item_name             object
    choice_description    object
    item_price            object
    dtype: object




```python
# 将item_price列转换为数字类型
chipo.item_price = chipo.item_price.apply(lambda x: float(x[1:]))
```


```python
chipo.dtypes
```




    order_id                int64
    quantity                int64
    item_name              object
    choice_description     object
    item_price            float64
    dtype: object




```python
chipo.head(10)
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>NaN</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>Izze</td>
      <td>[Clementine]</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1</td>
      <td>Nantucket Nectar</td>
      <td>[Apple]</td>
      <td>3.39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>Chips and Tomatillo-Green Chili Salsa</td>
      <td>NaN</td>
      <td>2.39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Tomatillo-Red Chili Salsa (Hot), [Black Beans...</td>
      <td>16.98</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa (Mild), [Rice, Cheese, Sou...</td>
      <td>10.98</td>
    </tr>
    <tr>
      <th>6</th>
      <td>3</td>
      <td>1</td>
      <td>Side of Chips</td>
      <td>NaN</td>
      <td>1.69</td>
    </tr>
    <tr>
      <th>7</th>
      <td>4</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Tomatillo Red Chili Salsa, [Fajita Vegetables...</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4</td>
      <td>1</td>
      <td>Steak Soft Tacos</td>
      <td>[Tomatillo Green Chili Salsa, [Pinto Beans, Ch...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>9</th>
      <td>5</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Pinto...</td>
      <td>9.25</td>
    </tr>
  </tbody>
</table>
</div>



### 2. 查看数据集的基本信息


```python
chipo.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4622 entries, 0 to 4621
    Data columns (total 5 columns):
    order_id              4622 non-null int64
    quantity              4622 non-null int64
    item_name             4622 non-null object
    choice_description    3376 non-null object
    item_price            4622 non-null float64
    dtypes: float64(1), int64(2), object(2)
    memory usage: 180.6+ KB
    

### 3. 查看数据的行列数和列名


```python
print ('(row, column) = ', chipo.shape)
```

    (row, column) =  (4622, 5)
    


```python
# 列名
print('columns = ', chipo.columns)
```

    columns =  Index(['order_id', 'quantity', 'item_name', 'choice_description',
           'item_price'],
          dtype='object')
    


```python
# 查看索引信息
chipo.index
```




    RangeIndex(start=0, stop=4622, step=1)



### 4. 查询商品种类的数量，以及下单最多的几种商品


```python
print ('Total items: ', len(chipo.item_name.unique()))
print ('--------------------------------------------------------------------------------')
print ('Total items: ', chipo.item_name.value_counts().count())
print ('--------------------------------------------------------------------------------')
print ('Total items = ', len(chipo.groupby(['item_name']).groups))
```

    Total items:  50
    --------------------------------------------------------------------------------
    Total items:  50
    --------------------------------------------------------------------------------
    Total items =  50
    


```python
# 获取销量最多的商品名
chipo.item_name.value_counts().head().index
```




    Index(['Chicken Bowl', 'Chicken Burrito', 'Chips and Guacamole',
           'Steak Burrito', 'Canned Soft Drink'],
          dtype='object')




```python
# 获取销量最多的商品销售量
chipo.item_name.value_counts().head()
```




    Chicken Bowl           726
    Chicken Burrito        553
    Chips and Guacamole    479
    Steak Burrito          368
    Canned Soft Drink      301
    Name: item_name, dtype: int64



### 5. 查询最受欢迎的食物及其销量，销售额


```python
# 查询最受欢迎的食物
favoriteItems = chipo.groupby(['item_name']).sum().sort_values('quantity', ascending=False)
# 删除order_id列
favoriteItems=favoriteItems.drop('order_id', axis=1)
favoriteItems.head()
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_price</th>
    </tr>
    <tr>
      <th>item_name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Chicken Bowl</th>
      <td>713926</td>
      <td>761</td>
      <td>7342.73</td>
    </tr>
    <tr>
      <th>Chicken Burrito</th>
      <td>497303</td>
      <td>591</td>
      <td>5575.82</td>
    </tr>
    <tr>
      <th>Chips and Guacamole</th>
      <td>449959</td>
      <td>506</td>
      <td>2201.04</td>
    </tr>
    <tr>
      <th>Steak Burrito</th>
      <td>328437</td>
      <td>386</td>
      <td>3851.43</td>
    </tr>
    <tr>
      <th>Canned Soft Drink</th>
      <td>304753</td>
      <td>351</td>
      <td>438.75</td>
    </tr>
  </tbody>
</table>
</div>



### 6. 查询最受欢迎食物（下单数，销量，销售额）


```python
favoriteItems = chipo.groupby(['item_name']).agg({'order_id' : 'count', 'quantity' : 'sum', 'item_price' : 'sum'}).sort_values('quantity', ascending=False)
favoriteItems.head()
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_price</th>
    </tr>
    <tr>
      <th>item_name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Chicken Bowl</th>
      <td>726</td>
      <td>761</td>
      <td>7342.73</td>
    </tr>
    <tr>
      <th>Chicken Burrito</th>
      <td>553</td>
      <td>591</td>
      <td>5575.82</td>
    </tr>
    <tr>
      <th>Chips and Guacamole</th>
      <td>479</td>
      <td>506</td>
      <td>2201.04</td>
    </tr>
    <tr>
      <th>Steak Burrito</th>
      <td>368</td>
      <td>386</td>
      <td>3851.43</td>
    </tr>
    <tr>
      <th>Canned Soft Drink</th>
      <td>301</td>
      <td>351</td>
      <td>438.75</td>
    </tr>
  </tbody>
</table>
</div>



###  7. 查询订单的商品总数量


```python
chipo.quantity.sum()
```




    4972



### 8. 统计总收入


```python
chipo.item_price.sum()
```




    34500.160000000003



### 9. 统计订单总数


```python
chipo.order_id.value_counts().count()
```




    1834



### 10. 订单平均消费


```python
chipo.item_price.sum() / chipo.order_id.value_counts().count()
# chipo.groupby(by=['order_id']).sum()['item_price'].mean()
```




    18.811428571428575



### 11. 按商品名称过滤查询数据


```python
chipo[(chipo['item_name'] == 'Chicken Bowl') & (chipo['quantity'] > 1)].head()
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Tomatillo-Red Chili Salsa (Hot), [Black Beans...</td>
      <td>16.98</td>
    </tr>
    <tr>
      <th>154</th>
      <td>70</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...</td>
      <td>17.50</td>
    </tr>
    <tr>
      <th>282</th>
      <td>124</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>17.50</td>
    </tr>
    <tr>
      <th>409</th>
      <td>178</td>
      <td>3</td>
      <td>Chicken Bowl</td>
      <td>[[Fresh Tomato Salsa (Mild), Tomatillo-Green C...</td>
      <td>32.94</td>
    </tr>
    <tr>
      <th>415</th>
      <td>181</td>
      <td>2</td>
      <td>Chicken Bowl</td>
      <td>[Tomatillo Red Chili Salsa]</td>
      <td>17.50</td>
    </tr>
  </tbody>
</table>
</div>



### 12. 查询消费金额最大的订单信息 (3个)


```python
maxOrder = chipo.groupby(['order_id']).sum().sort_values('item_price', ascending=False)
maxOrder.head(3)
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
      <th>quantity</th>
      <th>item_price</th>
    </tr>
    <tr>
      <th>order_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>926</th>
      <td>23</td>
      <td>205.25</td>
    </tr>
    <tr>
      <th>1443</th>
      <td>35</td>
      <td>160.74</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>14</td>
      <td>139.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
arrOrderId = maxOrder.head(3).index[0:3].values
arrOrderId
```




    array([ 926, 1443, 1483], dtype=int64)




```python
chipo[chipo['order_id'].isin(arrOrderId)]
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
      <th>order_id</th>
      <th>quantity</th>
      <th>item_name</th>
      <th>choice_description</th>
      <th>item_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2304</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Sour Cream, Lettuce]]</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2305</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2306</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2307</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2308</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Lettu...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2309</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2310</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Cheese, Sour...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2311</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2312</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Lettuce]]</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2313</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Cheese, Sour Cream...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2314</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Sour Cream]]</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2315</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2316</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Burrito</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2317</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2318</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2319</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Cheese]]</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2320</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Cheese, Lettuce]]</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2321</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Pinto Beans,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2322</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Cheese]]</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2323</th>
      <td>926</td>
      <td>1</td>
      <td>Barbacoa Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2324</th>
      <td>926</td>
      <td>1</td>
      <td>Chicken Burrito</td>
      <td>[Tomatillo Red Chili Salsa, [Rice, Cheese, Sou...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>2325</th>
      <td>926</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Tomatillo Red Chili Salsa, [Rice, Black Beans...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>2326</th>
      <td>926</td>
      <td>1</td>
      <td>Veggie Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3598</th>
      <td>1443</td>
      <td>15</td>
      <td>Chips and Fresh Tomato Salsa</td>
      <td>NaN</td>
      <td>44.25</td>
    </tr>
    <tr>
      <th>3599</th>
      <td>1443</td>
      <td>7</td>
      <td>Bottled Water</td>
      <td>NaN</td>
      <td>10.50</td>
    </tr>
    <tr>
      <th>3600</th>
      <td>1443</td>
      <td>1</td>
      <td>6 Pack Soft Drink</td>
      <td>[Coke]</td>
      <td>6.49</td>
    </tr>
    <tr>
      <th>3601</th>
      <td>1443</td>
      <td>3</td>
      <td>Veggie Burrito</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...</td>
      <td>33.75</td>
    </tr>
    <tr>
      <th>3602</th>
      <td>1443</td>
      <td>4</td>
      <td>Chicken Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>35.00</td>
    </tr>
    <tr>
      <th>3603</th>
      <td>1443</td>
      <td>3</td>
      <td>Steak Burrito</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Chees...</td>
      <td>27.75</td>
    </tr>
    <tr>
      <th>3604</th>
      <td>1443</td>
      <td>2</td>
      <td>Bottled Water</td>
      <td>NaN</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>3700</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3701</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>3702</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Burrito</td>
      <td>[Tomatillo Red Chili Salsa, [Fajita Vegetables...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3703</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Fajita Vegetables,...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>3704</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Burrito</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>3705</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Soft Tacos</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Black...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>3706</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Pinto Beans, Chees...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3707</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Black Beans, Chees...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>3708</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Fresh Tomato Salsa, [Rice, Black Beans, Sour ...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3709</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>11.25</td>
    </tr>
    <tr>
      <th>3710</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Soft Tacos</td>
      <td>[Fresh Tomato Salsa, Guacamole]</td>
      <td>11.75</td>
    </tr>
    <tr>
      <th>3711</th>
      <td>1483</td>
      <td>1</td>
      <td>Carnitas Bowl</td>
      <td>[Fresh Tomato Salsa, [Fajita Vegetables, Rice,...</td>
      <td>9.25</td>
    </tr>
    <tr>
      <th>3712</th>
      <td>1483</td>
      <td>1</td>
      <td>Chicken Salad Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Black Beans, Chees...</td>
      <td>8.75</td>
    </tr>
    <tr>
      <th>3713</th>
      <td>1483</td>
      <td>1</td>
      <td>Steak Bowl</td>
      <td>[Roasted Chili Corn Salsa, [Rice, Black Beans,...</td>
      <td>11.75</td>
    </tr>
  </tbody>
</table>
</div>


