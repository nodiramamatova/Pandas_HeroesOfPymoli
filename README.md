
## Unit 4 | Assignment - Pandas, Pandas, Pandas

## Option 1: Heroes of Pymoli

![title](Images/Fantasy.jpg)


```python
import os
import pandas as pd
import json
import numpy as np

file = "purchase_data2.json"
#file = "purchase_data.json"

with open(file) as data_file:
    data = json.load(data_file)
    
pymoli_pd = pd.DataFrame(data)
pymoli_pd.head()    
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>



**Player Count**

* Total Number of Players


```python
total = pymoli_pd['SN'].unique().size
total_players = pd.DataFrame({'Total Players': [total]})
total_players
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>



**Purchasing Analysis (Total)**

* Number of Unique Items
* Average Purchase Price
* Total Number of Purchases
* Total Revenue


```python
#Number of Unique Items
number_of_unique_items = pymoli_pd['Item Name'].value_counts()
number =len(number_of_unique_items)

# Average Purchase Price
avg_price = pymoli_pd['Price'].mean()

#Total Number of Purchases
total_num_purchase = pymoli_pd['Item Name'].count()

#Total Revenue
total_revenue = pymoli_pd['Price'].sum()

purchasing_analysis_total = pd.DataFrame({'Number of Unique Items': [number],
                                          'Average Purchase Price': [avg_price],
                                          'Total Number of Purchases': [total_num_purchase], 
                                          'Total Revenue': [total_revenue]
})
purchasing_analysis_total = purchasing_analysis_total[['Number of Unique Items',
                                                       'Average Purchase Price',
                                                       'Total Number of Purchases',
                                                        'Total Revenue']]
purchasing_analysis_total['Average Purchase Price'] = purchasing_analysis_total['Average Purchase Price'].map("${:.2f}".format)
purchasing_analysis_total['Total Revenue'] = purchasing_analysis_total['Total Revenue'].map("${:.2f}".format)

purchasing_analysis_total
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
      <th>Number of Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>63</td>
      <td>$2.92</td>
      <td>78</td>
      <td>$228.10</td>
    </tr>
  </tbody>
</table>
</div>



**Gender Demographics**

* Percentage and Count of Male Players
* Percentage and Count of Female Players
* Percentage and Count of Other / Non-Disclosed


```python
#Percentage and Count of Male Players
gender_male = pymoli_pd.loc[pymoli_pd['Gender']  == 'Male',:]
gender_male_count = gender_male['Gender'].count()

percentage_male = round((gender_male_count/total)* 100, 2)
percentage_male

#Percentage and Count of Female Players
gender_female = pymoli_pd.loc[pymoli_pd['Gender']  == 'Female',:]
gender_female_count = gender_female['Gender'].count()

percentage_female = round((gender_female_count/total)*100, 2)
percentage_female

# Percentage and Count of Other / Non-Disclosed
gender_other = pymoli_pd.loc[pymoli_pd['Gender']  == 'Other / Non-Disclosed',:]
other_nondisclosed_count = gender_other['Gender'].count()

pecentage_other = round((other_nondisclosed_count/total)*100,2)
pecentage_other


gender_demographics_pd = pd.DataFrame({'': ['Male', 'Female','Other / Non-Disclosed'],
                                       'Percentage Of Players':  [percentage_male, percentage_female,pecentage_other],
                                      'Total Count': [gender_male_count, gender_female_count, other_nondisclosed_count]})

gender_demographics_pd['Percentage Of Players'] = gender_demographics_pd['Percentage Of Players'].map("{:.2f}%".format)
gender_demographics_pd = gender_demographics_pd.set_index('')
gender_demographics_pd

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
      <th>Percentage Of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>86.49%</td>
      <td>64</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.57%</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.35%</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



**Purchasing Analysis (Gender)** 

* The below each broken by gender
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals


```python
male_purchase_avg = gender_male['Price'].mean()
male_purchase_total = gender_male['Price'].sum()

female_purchase_avg = gender_female['Price'].mean()
female_purchase_total = gender_female['Price'].sum()

other_purchase_avg = gender_other['Price'].mean()

#Normalized Totals
gender_male_SN = gender_male['SN'].unique()
gender_male_SN_len = len(gender_male_SN)
normalized_male_avg = male_purchase_total/gender_male_SN_len

gender_female_SN = gender_female['SN'].unique()
gender_female_SN_len = len(gender_female_SN)
normalized_female_avg = female_purchase_total/gender_female_SN_len


purchasing_analysis_gen_pd = pd.DataFrame({'Gender': ['Female','Male', 'Other / Non-Disclosed'],
                                           'Purchase Count': [gender_male_count, gender_female_count,other_nondisclosed_count],
                                          'Average Purchace Price': [female_purchase_avg, male_purchase_avg,other_purchase_avg],
                                          'Total Purchase Value': [female_purchase_total, male_purchase_total, other_purchase_avg],
                                          'Normalized Totals': [ normalized_female_avg, normalized_male_avg, other_purchase_avg]})
purchasing_analysis_gen_pd['Average Purchace Price'] = pd.to_numeric(purchasing_analysis_gen_pd['Average Purchace Price']).map("${:.2f}".format)
purchasing_analysis_gen_pd['Total Purchase Value'] = pd.to_numeric(purchasing_analysis_gen_pd['Total Purchase Value']).map("${:.2f}".format)
purchasing_analysis_gen_pd['Normalized Totals'] = pd.to_numeric(purchasing_analysis_gen_pd['Normalized Totals']).map("${:.2f}".format)
purchasing_analysis_gen_pd = purchasing_analysis_gen_pd[['Gender','Purchase Count',
                                                         'Average Purchace Price','Total Purchase Value', 'Normalized Totals']]
purchasing_analysis_gen_pd.set_index('Gender')

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
      <th>Purchase Count</th>
      <th>Average Purchace Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>64</td>
      <td>$3.18</td>
      <td>$41.38</td>
      <td>$3.18</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>13</td>
      <td>$2.88</td>
      <td>$184.60</td>
      <td>$3.08</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
      <td>$2.12</td>
      <td>$2.12</td>
      <td>$2.12</td>
    </tr>
  </tbody>
</table>
</div>



**Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals


```python
#The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
age_bins = [0,10,14,19,100]
age_bins_labels = ["<10", "10-14", "15-19", ">20"]
ages = np.array(pymoli_pd['Age'],dtype="int")
pymoli_pd['Age Levels'] = pd.cut(ages, age_bins, labels=age_bins_labels)
pymoli_pd.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Levels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>&gt;20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>&gt;20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>&gt;20</td>
    </tr>
  </tbody>
</table>
</div>




```python
age_groups = pymoli_pd[['Age Levels', 'SN', 'Price']].groupby(['Age Levels'])
age_groups_stats = age_groups.agg({'Price': ['count', 'mean', 'sum']})
age_groups_stats.columns = ['Purchase Count', 'Average Spent', 'Total Spent']
age_groups_stats["Normalized Totals"] = age_groups_stats['Total Spent'] / age_groups_stats['Purchase Count']  
age_groups_stats["Normalized Totals"] = age_groups_stats["Normalized Totals"].map("${:.2f}".format)
age_groups_stats['Average Spent'] = age_groups_stats['Average Spent'].map("${:.2f}".format)
age_groups_stats['Total Spent'] = age_groups_stats['Total Spent'].map("${:.2f}".format)

age_groups_stats.reset_index()
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
      <th>Age Levels</th>
      <th>Purchase Count</th>
      <th>Average Spent</th>
      <th>Total Spent</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>$2.76</td>
      <td>$13.82</td>
      <td>$2.76</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>3</td>
      <td>$2.99</td>
      <td>$8.96</td>
      <td>$2.99</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>11</td>
      <td>$2.76</td>
      <td>$30.41</td>
      <td>$2.76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>&gt;20</td>
      <td>59</td>
      <td>$2.96</td>
      <td>$174.91</td>
      <td>$2.96</td>
    </tr>
  </tbody>
</table>
</div>



**Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value


```python
top_spenders = pymoli_pd[['SN', 'Price']].groupby(['SN'])
top_spenders_stats = top_spenders.agg({'Price': ['count', 'mean', 'sum']})
top_spenders_stats.columns = ['Purchase Count', 'Average Purchase Price', 'Total Purchase Value'] 
top_spenders_stats['Average Purchase Price'] = top_spenders_stats['Average Purchase Price'].map("${:.2f}".format)
top_spenders_stats['Total Purchase Value'] = top_spenders_stats['Total Purchase Value'].map("${:.2f}".format)  

top_spenders_stats = top_spenders_stats.sort_values(by=[('Total Purchase Value')],ascending=False)[:5]
top_spenders_stats.reset_index()
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
      <th>SN</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sundaky74</td>
      <td>2</td>
      <td>$3.71</td>
      <td>$7.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>$2.56</td>
      <td>$5.13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Eusty71</td>
      <td>1</td>
      <td>$4.81</td>
      <td>$4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chanirra64</td>
      <td>1</td>
      <td>$4.78</td>
      <td>$4.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alarap40</td>
      <td>1</td>
      <td>$4.71</td>
      <td>$4.71</td>
    </tr>
  </tbody>
</table>
</div>



**Most Popular Items**

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value


```python
most_popular = pymoli_pd[['Item ID', 'Item Name', 'Price']].groupby(['Item ID', 'Item Name', 'Price'])  
most_popular = most_popular.agg({'Price':['sum', 'count']})
most_popular.columns = ['Total Purchase Value', 'Purchase Count']
most_popular['Total Purchase Value'] = most_popular['Total Purchase Value'].map("${:.2f}".format)
#most_popular['Price'] = most_popular['Price'].map("${:.2f}".format)
most_popular = most_popular.sort_values(by=[('Purchase Count')], ascending=False)[:5]
most_popular.reset_index()
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
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>3.64</td>
      <td>$10.92</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>Betrayer</td>
      <td>4.12</td>
      <td>$8.24</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>111</td>
      <td>Misery's End</td>
      <td>1.79</td>
      <td>$3.58</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>64</td>
      <td>Fusion Pummel</td>
      <td>2.42</td>
      <td>$4.84</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>$8.22</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



**Most Profitable Items**

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value


```python
most_popular.sort_values(by=[('Total Purchase Value')], ascending=False)[:5]
most_popular.reset_index()
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
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>94</td>
      <td>Mourning Blade</td>
      <td>3.64</td>
      <td>$10.92</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>Betrayer</td>
      <td>4.12</td>
      <td>$8.24</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>111</td>
      <td>Misery's End</td>
      <td>1.79</td>
      <td>$3.58</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>64</td>
      <td>Fusion Pummel</td>
      <td>2.42</td>
      <td>$4.84</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>$8.22</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
