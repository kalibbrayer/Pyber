

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```


```python
city_data = "city_data.csv"
ride_data = "ride_data.csv"
```


```python
ride_data_df = pd.read_csv(ride_data)
city_data_df = pd.read_csv(city_data)
```


```python
ride_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
pyber_df = pd.merge(ride_data_df, city_data_df, how='inner', on='city')
pyber_df.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
pyber_info = pyber_df.groupby(["city", "type", "driver_count"]).agg({'fare': ['count', 'mean']}).rename(columns={'count': 'Total_Rides', 'mean': 'Average_Fare'})
pyber_info.columns = pyber_info.columns.droplevel(0)
```


```python
pyber_info = pyber_info.reset_index()
```


```python
pyber_info.head(5) 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>type</th>
      <th>driver_count</th>
      <th>Total_Rides</th>
      <th>Average_Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>Urban</td>
      <td>21</td>
      <td>31</td>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>Urban</td>
      <td>67</td>
      <td>26</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>Suburban</td>
      <td>16</td>
      <td>9</td>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>Urban</td>
      <td>21</td>
      <td>22</td>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>Urban</td>
      <td>49</td>
      <td>19</td>
      <td>21.981579</td>
    </tr>
  </tbody>
</table>
</div>




```python
#determine # of rows
pyber_info.shape
```




    (126, 5)




```python
% matplotlib inline 
```


```python
#determine number of unique cities to avoid duplicates
pyber_info['city'].nunique() 
```




    125




```python
#drop the duplicate city to clean the data
pyber_info = pyber_info.drop(pyber_info.index[72])
```


```python
#call rows where duplicate city was to make sure it was removed 
pyber_info.iloc[65:75,:]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>type</th>
      <th>driver_count</th>
      <th>Total_Rides</th>
      <th>Average_Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>65</th>
      <td>North Tracyfort</td>
      <td>Suburban</td>
      <td>18</td>
      <td>10</td>
      <td>26.856000</td>
    </tr>
    <tr>
      <th>66</th>
      <td>North Whitney</td>
      <td>Rural</td>
      <td>10</td>
      <td>10</td>
      <td>38.146000</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Pamelahaven</td>
      <td>Urban</td>
      <td>30</td>
      <td>15</td>
      <td>25.549333</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Paulfort</td>
      <td>Suburban</td>
      <td>13</td>
      <td>13</td>
      <td>31.144615</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Pearsonberg</td>
      <td>Urban</td>
      <td>43</td>
      <td>20</td>
      <td>23.307500</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Port Alexandria</td>
      <td>Suburban</td>
      <td>27</td>
      <td>15</td>
      <td>26.316667</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Port Guytown</td>
      <td>Suburban</td>
      <td>26</td>
      <td>15</td>
      <td>28.242000</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Port James</td>
      <td>Suburban</td>
      <td>15</td>
      <td>32</td>
      <td>31.806562</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Port Johnstad</td>
      <td>Urban</td>
      <td>22</td>
      <td>34</td>
      <td>25.882941</td>
    </tr>
    <tr>
      <th>75</th>
      <td>Port Jose</td>
      <td>Suburban</td>
      <td>11</td>
      <td>18</td>
      <td>31.193889</td>
    </tr>
  </tbody>
</table>
</div>




```python
#add colors to each city type for plots
city_type = np.unique(pyber_info['type'])
colors = ['gold', 'lightskyblue', 'lightcoral']
for i in range(len(city_type)):
    print(city_type[i]+colors[i])
explode = (0, 0, 0.05)
```

    Ruralgold
    Suburbanlightskyblue
    Urbanlightcoral



```python
#bubble plot displaying the average price of a pyber ride(x-axis) vs the driver count for each city(y-axis).
#the bubble size represents the total number of rides in each city and the color represents city type. 
for i in range(len(city_type)):
    plt.scatter(pyber_info[pyber_info['type']== city_type[i]]['driver_count'].values, 
                pyber_info[pyber_info['type']== city_type[i]]['Average_Fare'].values, 
                s = 10 * pyber_info[pyber_info['type']== city_type[i]]['Total_Rides'].values,
                c= colors[i], alpha=0.7, label= city_type[i])
plt.title('Driver Count vs Average Price With Bubble Size as Total Ride Count')
plt.xlabel('Driver Count')
plt.ylabel('Average Price')
plt.legend()
plt.show()
```


![png](output_15_0.png)



```python
#add additional column for 'Total_Fare'
pyber_info['Total_Fare'] = pyber_info['Total_Rides'] * pyber_info['Average_Fare'] 
pyber_info.head(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>type</th>
      <th>driver_count</th>
      <th>Total_Rides</th>
      <th>Average_Fare</th>
      <th>Total_Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>Urban</td>
      <td>21</td>
      <td>31</td>
      <td>23.928710</td>
      <td>741.79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>Urban</td>
      <td>67</td>
      <td>26</td>
      <td>20.609615</td>
      <td>535.85</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>Suburban</td>
      <td>16</td>
      <td>9</td>
      <td>37.315556</td>
      <td>335.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_table = pyber_info.groupby(['type']).agg({'Total_Fare': 'sum', 'driver_count': 'sum', 'Total_Rides': 'sum'})
sum_table.apply(lambda x: round (100* x/x.sum(),2)) 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total_Fare</th>
      <th>driver_count</th>
      <th>Total_Rides</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>6.68</td>
      <td>3.11</td>
      <td>5.26</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>30.35</td>
      <td>18.98</td>
      <td>26.32</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>62.97</td>
      <td>77.91</td>
      <td>68.42</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_table.plot.pie(subplots=True, colors=colors, explode=explode, autopct='%1.1f%%', figsize=(10,3)) 
plt.title("% Total Fares, Driver Counts and Rides by Type")
plt.show()
```


![png](output_18_0.png)



```python

```
