
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import numpy as np

# File to Load (Remember to Change These)
Purchase_csv = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(Purchase_csv)
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
#player count 
#drop the duplicates name 
#select and count the SN 
Total_player_number =(purchase_data["SN"]).drop_duplicates().count() 

#create the table
pd.DataFrame({"Total Players":[Total_player_number]})


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
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
# unique items count 
Unique_Items =len(purchase_data["Item ID"].unique())
Unique_Items


```




    183




```python
# average price round to 2 decimal place

Average_Price = "${}".format(round(purchase_data["Price"].mean() , 2 ))

Average_Price
 
```




    '$3.05'




```python

# Total number of purchases
Total_Number = purchase_data["Price"].count()
Total_Number

```




    780




```python
# Total revenue
Total = purchase_data["Price"].sum()
Total_Revenue = "${}".format(Total)
Total_Revenue
```




    '$2379.77'




```python

#summary data frame 
d = { 
     "Number of Unique Items":[Unique_Items],
     "Average Price":[Average_Price],
     "Number of Purchases" : [Total_Number],
     "Total Revenue" : [Total_Revenue]
}

Summary_Table = pd.DataFrame ( d ,columns = ["Number of Unique Items","Average Price","Number of Purchases","Total Revenue"])

Summary_Table
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
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# total Gender count
Total_Gender_Count = purchase_data.groupby("Gender").nunique()["SN"]
Total_Gender_Count
```




    Gender
    Female                    81
    Male                     484
    Other / Non-Disclosed     11
    Name: SN, dtype: int64




```python
#total percentage count of Male
Total_Percentage = round( Total_Gender_Count / Total_player_number * 100 , 2)
Total_Percentage

```




    Gender
    Female                   14.06
    Male                     84.03
    Other / Non-Disclosed     1.91
    Name: SN, dtype: float64




```python
#create the DataFrame

Gender_Demographics = pd . DataFrame( { 
 
    "Total Count" : Total_Gender_Count,
    "Percentage of players":Total_Percentage
})

GenderDataFrame = Gender_Demographics.sort_values("Total Count" , ascending = False)

GenderDataFrame

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
      <th>Total Count</th>
      <th>Percentage of players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
## Purchasing Analysis (Gender)

# Run basic calculations to obtain purchase count
purchase_count =purchase_data.groupby("Gender")["Purchase ID"].count()
purchase_count

# Run basic calculations to obtain avg. purchase price and formatting
avgpurchaseprice=(purchase_data.groupby("Gender")["Price"].mean())
avg_purchase_price=avgpurchaseprice.map("${:,.2f}".format)
avg_purchase_price

# Run basic calculations to obtain average total purchase by gender and formatting

PvgPurchaseTotal = purchase_data.groupby("Gender")["Price"].sum()
avg_purchase_total = PvgPurchaseTotal.map("${:,.2f}".format)
avg_purchase_total


#Average purchase total by gender and formatting
AvgPurchasePerPerson = PvgPurchaseTotal / Total_Gender_Count
avg_purchase_per_person = AvgPurchasePerPerson.map("${:,.2f}".format)
avg_purchase_per_person

# Create a summary data frame to hold the result

x={
    "Purchase Count":purchase_count,
    "Average Purchase Price":avg_purchase_price,
    "Total Purchase Value":avg_purchase_total,
    "Avg Total Purchase per person":avg_purchase_per_person
}

Summary_Gender_Table= pd.DataFrame (x,columns = ["Purchase Count","Average Purchase Price","Total Purchase Value","Avg Total Purchase per person"])

Summary_Gender_Table    


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
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per person</th>
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
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$1,967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# Establish bins for ages define as 0 to 10,10 to 15
bins = [0, 10, 15, 20, 25, 30, 35, 40, 100]

#name of the group
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Categorize the existing players using the age bins. Hint: use pd.cut()
purchase_data["segment_age"] = pd.cut(purchase_data["Age"],bins,labels= group_names)

Interval_age = purchase_data.groupby("segment_age")

#total players by age category
total_count_age = Interval_age["SN"].nunique()

# Calculate the numbers and percentages by age group and 
# round the percentage column to two decimal points
percentage_by_age_group = round((total_count_age/Total_player_number)*100,2)

# Create a summary data frame to hold the results and Display Age Demographics Table
Age_Demographics=pd.DataFrame({"Total Count":total_count_age,
                               "Percentage of players":percentage_by_age_group,
                                  
                                  })
Age_Demographics



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
      <th>Total Count</th>
      <th>Percentage of players</th>
    </tr>
    <tr>
      <th>segment_age</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>24</td>
      <td>4.17</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>41</td>
      <td>7.12</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>150</td>
      <td>26.04</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>232</td>
      <td>40.28</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>59</td>
      <td>10.24</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>37</td>
      <td>6.42</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>26</td>
      <td>4.51</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>7</td>
      <td>1.22</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#calculation to obtain purchase count
purchase_count_age = Interval_age["Purchase ID"].count()

#calculation obtain purchase and formatting with $ sign and round to 2 decimal
avg_purchase_price_age = (Interval_age["Price"].mean()).map("${:,.2f}".format)

#calculate total purchase value by age group and formatting with $ sign and round to 2 decimal
TotalPurchaseValueAge =Interval_age["Price"].sum()

total_purchase_value_age =TotalPurchaseValueAge.map("${:,.2f}".format)

#average purchase per person in the age group and formatting with $ sign and round to 2 decimal
avg_purchase_per_person_age_groupe =(TotalPurchaseValueAge/total_count_age).map("${:,.2f}".format)


#create DataFrame for Purchasing Analysis (Age)
z={
    "Purchase Count":purchase_count_age,
    "Average Purchase Price":avg_purchase_price_age,
    "Total Purchase Value":total_purchase_value_age,
    "Avg Total Purchase per person":avg_purchase_per_person_age_groupe
}

age_group_purchasing_analysis= pd.DataFrame (z,columns = ["Purchase Count",
                                                          "Average Purchase Price",
                                                          "Total Purchase Value",
                                                          "Avg Total Purchase per person"])

age_group_purchasing_analysis
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
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per person</th>
    </tr>
    <tr>
      <th>segment_age</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>$3.40</td>
      <td>$108.96</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>54</td>
      <td>$2.90</td>
      <td>$156.60</td>
      <td>$3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>200</td>
      <td>$3.11</td>
      <td>$621.56</td>
      <td>$4.14</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>325</td>
      <td>$3.02</td>
      <td>$981.64</td>
      <td>$4.23</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>$2.88</td>
      <td>$221.42</td>
      <td>$3.75</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>$2.99</td>
      <td>$155.71</td>
      <td>$4.21</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>33</td>
      <td>$3.40</td>
      <td>$112.35</td>
      <td>$4.32</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>7</td>
      <td>$3.08</td>
      <td>$21.53</td>
      <td>$3.08</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# group by spender
spender_purchase = purchase_data.groupby("SN")

# group total count per spender
purchase_count_spender = spender_purchase["Purchase ID"].count()

# group by average purchase price per spender
avg_purchase_price_spender = (spender_purchase["Price"].mean()).map("${:,.2f}".format)

#group by total purchase value per spender 
total_purchase_spender =spender_purchase["Price"].sum()



#create the summary DataFrame 

v={
    "Purchase Count":purchase_count_spender,
    "Average Purchase Price":avg_purchase_price_spender,
    "Total Purchase Value":total_purchase_spender
} 

summary_top_spender = pd.DataFrame (v,columns = ["Purchase Count",
                                                 "Average Purchase Price",
                                                 "Total Purchase Value"])

# sort value by highest total purchase top 5
summary_top_spender.sort_values("Total Purchase Value" , ascending = False).head()


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
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Create new data frame with new columns 
New_column_list = purchase_data[["Item ID", "Item Name", "Price"]]

# Group by item id and item name 
item1 = New_column_list.groupby(["Item ID","Item Name"])

# number of times an item has been purchased 
purchase_item = item1["Price"].count()

# purchase value per item 
purchase_per_items= item1["Price"].sum()

# Find individual item price
item_price = purchase_per_items/purchase_item

# Create data frame with new column
MostPopularItems = pd.DataFrame({"Purchase Count": purchase_item, 
                                   "Item Price": item_price,
                                   "Total Purchase Value":purchase_per_items})

# Sort in descending to have the top 5
most_popular_items= MostPopularItems.sort_values(["Purchase Count"], ascending=False).head()

#formatting with $ sign
most_popular_items.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})


```




<style  type="text/css" >
</style>  
<table id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Item Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level0_row0" class="row_heading level0 row0" >178</th> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row0_col0" class="data row0 col0" >12</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row0_col1" class="data row0 col1" >$4.23</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row0_col2" class="data row0 col2" >$50.76</td> 
    </tr>    <tr> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level0_row1" class="row_heading level0 row1" >145</th> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level1_row1" class="row_heading level1 row1" >Fiery Glass Crusader</th> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row1_col0" class="data row1 col0" >9</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row1_col1" class="data row1 col1" >$4.58</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row1_col2" class="data row1 col2" >$41.22</td> 
    </tr>    <tr> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level0_row2" class="row_heading level0 row2" >108</th> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level1_row2" class="row_heading level1 row2" >Extraction, Quickblade Of Trembling Hands</th> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row2_col0" class="data row2 col0" >9</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row2_col1" class="data row2 col1" >$3.53</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row2_col2" class="data row2 col2" >$31.77</td> 
    </tr>    <tr> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level0_row3" class="row_heading level0 row3" >82</th> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level1_row3" class="row_heading level1 row3" >Nirvana</th> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row3_col0" class="data row3 col0" >9</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row3_col1" class="data row3 col1" >$4.90</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row3_col2" class="data row3 col2" >$44.10</td> 
    </tr>    <tr> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level0_row4" class="row_heading level0 row4" >19</th> 
        <th id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824level1_row4" class="row_heading level1 row4" >Pursuit, Cudgel of Necromancy</th> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row4_col0" class="data row4 col0" >8</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row4_col1" class="data row4 col1" >$1.02</td> 
        <td id="T_c231ecf0_4e7a_11e9_a625_505bc2d07824row4_col2" class="data row4 col2" >$8.16</td> 
    </tr></tbody> 
</table> 



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# sort the previous table by Total purchase value  to have the most profitable items
most_popular_items = MostPopularItems.sort_values(["Total Purchase Value"],
                                                   ascending=False).head()
# Formatting
most_popular_items.style.format({"Item Price":"${:,.2f}",
                                "Total Purchase Value":"${:,.2f}"})


```




<style  type="text/css" >
</style>  
<table id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Item Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level0_row0" class="row_heading level0 row0" >178</th> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row0_col0" class="data row0 col0" >12</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row0_col1" class="data row0 col1" >$4.23</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row0_col2" class="data row0 col2" >$50.76</td> 
    </tr>    <tr> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level0_row1" class="row_heading level0 row1" >82</th> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level1_row1" class="row_heading level1 row1" >Nirvana</th> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row1_col0" class="data row1 col0" >9</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row1_col1" class="data row1 col1" >$4.90</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row1_col2" class="data row1 col2" >$44.10</td> 
    </tr>    <tr> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level0_row2" class="row_heading level0 row2" >145</th> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row2_col0" class="data row2 col0" >9</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row2_col1" class="data row2 col1" >$4.58</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row2_col2" class="data row2 col2" >$41.22</td> 
    </tr>    <tr> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level0_row3" class="row_heading level0 row3" >92</th> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level1_row3" class="row_heading level1 row3" >Final Critic</th> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row3_col0" class="data row3 col0" >8</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row3_col1" class="data row3 col1" >$4.88</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row3_col2" class="data row3 col2" >$39.04</td> 
    </tr>    <tr> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level0_row4" class="row_heading level0 row4" >103</th> 
        <th id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824level1_row4" class="row_heading level1 row4" >Singed Scalpel</th> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row4_col0" class="data row4 col0" >8</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row4_col1" class="data row4 col1" >$4.35</td> 
        <td id="T_c2345c58_4e7a_11e9_88bb_505bc2d07824row4_col2" class="data row4 col2" >$34.80</td> 
    </tr></tbody> 
</table> 


