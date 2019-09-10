
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.
* Observations are given for each data frame.


```python
# Dependencies and Setup
import pandas as pd

# File to Load 
purchase_csv = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(purchase_csv)

#Preview of the Data Frame
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
#Total Number of Players
Total_Players = purchase_data["SN"].nunique()
Player_Count_df = pd.DataFrame({"Total Players" : [Total_Players]})
Player_Count_df
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



### Observation

As per the Purchase Data CSV (purchase_data.csv), the total purchase ID count is 780 but the number of unique players is 576 only. From this we can come to conclusion that there are purchasers who buy the Heroes Of Pymoli Game repeatedly.


## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
#Number of Unique Items
Unique_Items = purchase_data["Item ID"].nunique()

#Average Purchase Price
Average_Price = purchase_data["Price"].mean()

#Total Number of Purchases
Total_Num_Purchases = purchase_data["Purchase ID"].count()

#Total Revenue
Total_Revenue = purchase_data["Price"].sum()

#Summary Data Frame to hold the results
Purchasing_Analysis_Total_df = pd.DataFrame({"Number of Unique Items" : [Unique_Items],
                                       "Average Price" : [Average_Price],
                                       "Total Number of Purchases" : [Total_Num_Purchases],
                                       "Total Revenue" : [Total_Revenue]
                                      })
#Formatting the Data Frame
Purchasing_Analysis_Total_df = Purchasing_Analysis_Total_df.style.format({"Average Price": "${:.2f}", 
                                                                          "Total Revenue": "${:,.2f}"})

#Displaying the Data Frame
Purchasing_Analysis_Total_df
```




<style  type="text/css" >
</style><table id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Number of Unique Items</th>        <th class="col_heading level0 col1" >Average Price</th>        <th class="col_heading level0 col2" >Total Number of Purchases</th>        <th class="col_heading level0 col3" >Total Revenue</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292level0_row0" class="row_heading level0 row0" >0</th>
                        <td id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292row0_col0" class="data row0 col0" >183</td>
                        <td id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292row0_col1" class="data row0 col1" >$3.05</td>
                        <td id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292row0_col2" class="data row0 col2" >780</td>
                        <td id="T_d91cc59c_d2db_11e9_b309_ccb0da51e292row0_col3" class="data row0 col3" >$2,379.77</td>
            </tr>
    </tbody></table>



### Observation

From the Purchasing Analysis Data, we can conclude that the Total Revenue of the 183 Unique items is $2379.77 of having 780 Total Number of Purchases with an average price of $3.05.

## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
#Group by Gender
purchase_data[""] = purchase_data["Gender"]
Gender_Group = purchase_data.groupby([""])

#Calculating the Player's Total Count and Percentage of Players based on Gender
Gender_Total_Count = Gender_Group["SN"].nunique()
Gender_Percentage_Players = round((Gender_Total_Count/Total_Players)*100,2)

#Summary Data Frame to hold the results
Gender_Demographics_df = pd.DataFrame({"Total Count": Gender_Total_Count, 
                                           "Percentage Of Players": Gender_Percentage_Players
                                        })

#Sorting the Values by Total Count in Descending Order
Gender_Demographics_df = Gender_Demographics_df.sort_values("Total Count", ascending=False) 

#Displaying the Data Frame
Gender_Demographics_df
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
      <th>Percentage Of Players</th>
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



### Observation

From the Gender Demographics, we can conclude that the Male Count and the Percentage of Male Players (84%) is higher than the Female Player and Other/Non-Disclosed Genders.


## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender

* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#Group by Gender
Gender_Group = purchase_data.groupby(["Gender"])

# Calculating Purchase Count, AverGender Purchase Price (PP) based on Gender.
# Calculating Total Purchase Value (PV), Avg Total Purchase Per Person (TPPP) based on Gender.
Gender_Purchase_Count = Gender_Group["Purchase ID"].nunique()
Gender_Avg_PP = Gender_Group["Price"].mean()
Gender_Total_PV = Gender_Group["Price"].sum()
Gender_Avg_TPPP = Gender_Total_PV/Gender_Group["SN"].nunique()

#Summary Data Frame to hold the results
Purchasing_Analysis_Gender_df = pd.DataFrame({"Purchase Count": Gender_Purchase_Count, 
                                           "Average Purchase Price": Gender_Avg_PP,
                                           "Total Purchase Value": Gender_Total_PV,
                                           "Avg Total Purchase per Person": Gender_Avg_TPPP})
#Sorting the Index
Purchasing_Analysis_Gender_df.sort_index()

#Formatting the Data Frame
Purchasing_Analysis_Gender_df = Purchasing_Analysis_Gender_df.style.format({"Average Purchase Price": "${:.2f}", 
                                                                            "Total Purchase Value": "${:,.2f}", 
                                                                            "Avg Total Purchase per Person": "${:.2f}"})

#Displaying the Data Frame
Purchasing_Analysis_Gender_df
```




<style  type="text/css" >
</style><table id="T_76d11736_d358_11e9_baa5_ccb0da51e292" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Gender</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_76d11736_d358_11e9_baa5_ccb0da51e292level0_row0" class="row_heading level0 row0" >Female</th>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row0_col0" class="data row0 col0" >113</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row0_col1" class="data row0 col1" >$3.20</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row0_col2" class="data row0 col2" >$361.94</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row0_col3" class="data row0 col3" >$4.47</td>
            </tr>
            <tr>
                        <th id="T_76d11736_d358_11e9_baa5_ccb0da51e292level0_row1" class="row_heading level0 row1" >Male</th>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row1_col0" class="data row1 col0" >652</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row1_col1" class="data row1 col1" >$3.02</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row1_col2" class="data row1 col2" >$1,967.64</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row1_col3" class="data row1 col3" >$4.07</td>
            </tr>
            <tr>
                        <th id="T_76d11736_d358_11e9_baa5_ccb0da51e292level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row2_col0" class="data row2 col0" >15</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row2_col1" class="data row2 col1" >$3.35</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row2_col2" class="data row2 col2" >$50.19</td>
                        <td id="T_76d11736_d358_11e9_baa5_ccb0da51e292row2_col3" class="data row2 col3" >$4.56</td>
            </tr>
    </tbody></table>



### Observation

From the Purchasing Analysis based on Gender, we can conclude three points, 
1)	Total Purchase Value is higher in males because the Purchase Count in Male Gender is higher. (It’s obvious since the Percentage of Male Players is 84%)
2)	The Average Purchase Price in the Other/Non-Disclosed Gender Category is higher than the Other Genders having a value of $3.35.
3)	The Average Total Purchase Per Person in the Female Gender Category is higher than the Other Genders having a value of $4.47.


## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
#Creating Bins & Groups by Age
Age_bins = [0,9,14,19,24,29,34,39,100]
Bin_Groups = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

#Categorizing the existing players using the age bins.
purchase_data[""] = pd.cut(purchase_data["Age"], Age_bins, labels=Bin_Groups)
Age_Group = purchase_data.groupby([""])

# Calculating Total Count, Percentage Of Players based on Age.
Total_Count = Age_Group["SN"].nunique()
Percentage_of_Players = round((Total_Count/Total_Players) * 100,2)

#Summary Data Frame to hold the results
Age_Demographics_df = pd.DataFrame({"Total Count": Total_Count, "Percentage of Players": Percentage_of_Players})

#Sorting the Index
Age_Demographics_df = Age_Demographics_df.sort_index()

#Displaying the Data Frame
Age_Demographics_df

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
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



### Observation

Based on the Age Demographics Data, we can conclude that,
1) The Age-Group between 20-24 is having the highest number of players (258) followed by Age-Group 15-19 having 107 players.
2) The Age-Group in the Group 40+ is having the least of 12 players followed by Ager-Group <10 having 17 players.

## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
#Creating Bins & Groups by Age
Age_bins = [0,9,14,19,24,29,34,39,100]
Bin_Groups = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

#Categorizing the existing players using the age bins.
purchase_data[""] = pd.cut(purchase_data["Age"], Age_bins, labels=Bin_Groups)
Age_Group = purchase_data.groupby([""])

# Calculating Purchase Count, Average Purchase Price (PP) based on Age.
# Calculating Total Purchase Value (PV), Avg Total Purchase Per Person (TPPP) based on Age.
Age_Purchase_Count = Age_Group["Purchase ID"].nunique()
Age_Avg_PP = Age_Group["Price"].mean()
Age_Total_PV = Age_Group["Price"].sum()
Age_Avg_TPPP = Age_Total_PV/Age_Group["SN"].nunique()

#Summary Data Frame to hold the results
Purchasing_Analysis_Age_df = pd.DataFrame({"Purchase Count": Age_Purchase_Count, 
                                           "Average Purchase Price": Age_Avg_PP,
                                           "Total Purchase Value": Age_Total_PV,
                                           "Avg Total Purchase per Person": Age_Avg_TPPP})
#Sorting the Index
Purchasing_Analysis_Age_df.sort_index()

#Formatting the Data Frame
Purchasing_Analysis_Age_df = Purchasing_Analysis_Age_df.style.format({"Average Purchase Price": "${:.2f}", 
                                                                      "Total Purchase Value": "${:,.2f}", 
                                                                      "Avg Total Purchase per Person": "${:.2f}"})

#Displaying the Data Frame
Purchasing_Analysis_Age_df
```




<style  type="text/css" >
</style><table id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row0_col0" class="data row0 col0" >23</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row0_col1" class="data row0 col1" >$3.35</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row0_col2" class="data row0 col2" >$77.13</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row0_col3" class="data row0 col3" >$4.54</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row1_col0" class="data row1 col0" >28</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row1_col1" class="data row1 col1" >$2.96</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row1_col2" class="data row1 col2" >$82.78</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row1_col3" class="data row1 col3" >$3.76</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row2_col0" class="data row2 col0" >136</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row2_col1" class="data row2 col1" >$3.04</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row2_col2" class="data row2 col2" >$412.89</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row2_col3" class="data row2 col3" >$3.86</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row3_col0" class="data row3 col0" >365</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row3_col1" class="data row3 col1" >$3.05</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row3_col2" class="data row3 col2" >$1,114.06</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row3_col3" class="data row3 col3" >$4.32</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row4_col0" class="data row4 col0" >101</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row4_col1" class="data row4 col1" >$2.90</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row4_col2" class="data row4 col2" >$293.00</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row4_col3" class="data row4 col3" >$3.81</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row5_col0" class="data row5 col0" >73</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row5_col1" class="data row5 col1" >$2.93</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row5_col2" class="data row5 col2" >$214.00</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row5_col3" class="data row5 col3" >$4.12</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row6_col0" class="data row6 col0" >41</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row6_col1" class="data row6 col1" >$3.60</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row6_col2" class="data row6 col2" >$147.67</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row6_col3" class="data row6 col3" >$4.76</td>
            </tr>
            <tr>
                        <th id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292level0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row7_col0" class="data row7 col0" >13</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row7_col1" class="data row7 col1" >$2.94</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row7_col2" class="data row7 col2" >$38.24</td>
                        <td id="T_7bfe6a76_d2a0_11e9_9560_ccb0da51e292row7_col3" class="data row7 col3" >$3.19</td>
            </tr>
    </tbody></table>



### Observation

From the Purchasing Analysis based on Age Group, we can conclude three points, 
1)	Total Purchase Value is higher in the Age Group 20-24 ($1114.06) followed by the Age Group (15-19) having $412.89 value since the Purchase count in these Age Groups are high and the Age Group 40+ having the least of $38.24.
2)	The Average Purchase Price is higher in the Age Group 35-39 of having $3.60 value and least in the Age Group 25-29 of having $2.90
3)	The Average Total Purchase Per Person is higher in the Age Group 35-39 of having $4.76 value and least in the Age Group 40+ of having $3.19

## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
#Group by Spenders
SN_Group = purchase_data.groupby(["SN"])

# Calculating Purchase Count, Average Purchase Price (PP) , Total Purchase Value (PV) based on Top Spenders
Spenders_Purchase_Count = SN_Group["Purchase ID"].nunique()
Spenders_Avg_PP = SN_Group["Price"].mean()
Spenders_Total_PV = SN_Group["Price"].sum()

#Summary Data Frame to hold the results
Top_Spenders_df = pd.DataFrame({"Purchase Count": Spenders_Purchase_Count, 
                                           "Average Purchase Price": Spenders_Avg_PP,
                                           "Total Purchase Value": Spenders_Total_PV})

#Sorting the Data Frame by Total Purchase Value in Descending Order
Top_Spenders_df = Top_Spenders_df.sort_values("Total Purchase Value", ascending=False) 

#Displaying Priview of Data (head)
Top_Spenders_df = Top_Spenders_df.head()

#Formatting the Data Frame
Top_Spenders_df = Top_Spenders_df.style.format({"Average Purchase Price": "${:.2f}", "Total Purchase Value": "${:,.2f}"})

#Displaying the Data Frame
Top_Spenders_df

```




<style  type="text/css" >
</style><table id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >SN</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292level0_row0" class="row_heading level0 row0" >Lisosia93</th>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row0_col0" class="data row0 col0" >5</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row0_col1" class="data row0 col1" >$3.79</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row0_col2" class="data row0 col2" >$18.96</td>
            </tr>
            <tr>
                        <th id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292level0_row1" class="row_heading level0 row1" >Idastidru52</th>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row1_col0" class="data row1 col0" >4</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row1_col1" class="data row1 col1" >$3.86</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row1_col2" class="data row1 col2" >$15.45</td>
            </tr>
            <tr>
                        <th id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292level0_row2" class="row_heading level0 row2" >Chamjask73</th>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row2_col0" class="data row2 col0" >3</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row2_col1" class="data row2 col1" >$4.61</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row2_col2" class="data row2 col2" >$13.83</td>
            </tr>
            <tr>
                        <th id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292level0_row3" class="row_heading level0 row3" >Iral74</th>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row3_col0" class="data row3 col0" >4</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row3_col1" class="data row3 col1" >$3.40</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row3_col2" class="data row3 col2" >$13.62</td>
            </tr>
            <tr>
                        <th id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292level0_row4" class="row_heading level0 row4" >Iskadarya95</th>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row4_col0" class="data row4 col0" >3</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row4_col1" class="data row4 col1" >$4.37</td>
                        <td id="T_7d54ec90_d2a0_11e9_ac6a_ccb0da51e292row4_col2" class="data row4 col2" >$13.10</td>
            </tr>
    </tbody></table>



### Observation

Based on the Top Spenders data, we can conclude that Lisosia93 tops of purchasing 5 items with a highest Total Purchase Value of $18.96 followed by Idastidru52 having the purchase value of $15.45 The Average Purchase price of Lisosia93 is $3.79.

## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
#Group by Item ID and Item Name
Item_Group = purchase_data.groupby(["Item ID","Item Name"])

#Calculating Purchase Count, Item Price , Total Purchase Value based on Most Popular Items
Items_Purchase_Count = Item_Group["Purchase ID"].nunique()
Items_Price = Item_Group["Price"].mean()
Items_Total_PV = Item_Group["Price"].sum()

#Summary Data Frame to hold the results
Most_Popular_Item_df = pd.DataFrame({"Purchase Count": Items_Purchase_Count, 
                                           "Item Price": Items_Price,
                                           "Total Purchase Value": Items_Total_PV})

#Sorting the Data Frame by Purchase Count in Descending Order
Most_Popular_Item_df = Most_Popular_Item_df.sort_values("Purchase Count", ascending=False) 

#Displaying Priview of Data (head)
Most_Popular_Item_df = Most_Popular_Item_df.head()

#Formatting the Data Frame
Most_Popular_Item_df = Most_Popular_Item_df.style.format({"Item Price": "${:.2f}", "Total Purchase Value": "${:,.2f}"})

#Displaying the Data Frame
Most_Popular_Item_df
```




<style  type="text/css" >
</style><table id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row0_col0" class="data row0 col0" >12</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level0_row1" class="row_heading level0 row1" >145</th>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level1_row1" class="row_heading level1 row1" >Fiery Glass Crusader</th>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row1_col0" class="data row1 col0" >9</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row1_col1" class="data row1 col1" >$4.58</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row1_col2" class="data row1 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level0_row2" class="row_heading level0 row2" >108</th>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level1_row2" class="row_heading level1 row2" >Extraction, Quickblade Of Trembling Hands</th>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row2_col0" class="data row2 col0" >9</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row2_col1" class="data row2 col1" >$3.53</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row2_col2" class="data row2 col2" >$31.77</td>
            </tr>
            <tr>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level0_row3" class="row_heading level0 row3" >82</th>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level1_row3" class="row_heading level1 row3" >Nirvana</th>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row3_col0" class="data row3 col0" >9</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row3_col1" class="data row3 col1" >$4.90</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row3_col2" class="data row3 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level0_row4" class="row_heading level0 row4" >19</th>
                        <th id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292level1_row4" class="row_heading level1 row4" >Pursuit, Cudgel of Necromancy</th>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row4_col0" class="data row4 col0" >8</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row4_col1" class="data row4 col1" >$1.02</td>
                        <td id="T_7eb0e740_d2a0_11e9_bbec_ccb0da51e292row4_col2" class="data row4 col2" >$8.16</td>
            </tr>
    </tbody></table>



### Observation

From the Most Popular Data Frame, we can conclude that "Oathbreaker, Last Hope of the Breaking Storm" item is the most popular item of having 12 Purchase Count of $50.76 Total Purchase Value followed by "Fiery Glass Crusader" having 9 purchase count and $41.22 Total Purchase Value.

## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
#Group by Item ID and Item Name
Item_Group = purchase_data.groupby(["Item ID","Item Name"])

#Calculating Purchase Count, Item Price , Total Purchase Value based on Most Profitable Items
Items_Purchase_Count = Item_Group["Purchase ID"].nunique()
Items_Price = Item_Group["Price"].mean()
Items_Total_PV = Item_Group["Price"].sum()

#Summary Data Frame to hold the results
Most_Profitable_Item_df = pd.DataFrame({"Purchase Count": Items_Purchase_Count, 
                                           "Item Price": Items_Price,
                                           "Total Purchase Value": Items_Total_PV})

#Sorting the Data Frame by Total Purchase Value in Descending Order
Most_Profitable_Item_df = Most_Profitable_Item_df.sort_values("Total Purchase Value", ascending=False) 

#Displaying Priview of Data (head)
Most_Profitable_Item_df = Most_Profitable_Item_df.head()

#Formatting the Data Frame
Most_Profitable_Item_df = Most_Profitable_Item_df.style.format({"Item Price": "${:.2f}", "Total Purchase Value": "${:,.2f}"})

#Displaying the Data Frame
Most_Profitable_Item_df
```




<style  type="text/css" >
</style><table id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row0_col0" class="data row0 col0" >12</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level0_row1" class="row_heading level0 row1" >82</th>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level1_row1" class="row_heading level1 row1" >Nirvana</th>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row1_col0" class="data row1 col0" >9</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row1_col1" class="data row1 col1" >$4.90</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row1_col2" class="data row1 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level0_row2" class="row_heading level0 row2" >145</th>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row2_col0" class="data row2 col0" >9</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row2_col1" class="data row2 col1" >$4.58</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row2_col2" class="data row2 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level0_row3" class="row_heading level0 row3" >92</th>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level1_row3" class="row_heading level1 row3" >Final Critic</th>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row3_col0" class="data row3 col0" >8</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row3_col1" class="data row3 col1" >$4.88</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row3_col2" class="data row3 col2" >$39.04</td>
            </tr>
            <tr>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level0_row4" class="row_heading level0 row4" >103</th>
                        <th id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292level1_row4" class="row_heading level1 row4" >Singed Scalpel</th>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row4_col0" class="data row4 col0" >8</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row4_col1" class="data row4 col1" >$4.35</td>
                        <td id="T_801f3f9c_d2a0_11e9_a37b_ccb0da51e292row4_col2" class="data row4 col2" >$34.80</td>
            </tr>
    </tbody></table>



### Observation

From the Most Profitable Data Frame, we can conclude that "Oathbreaker, Last Hope of the Breaking Storm" item is the most Profitable item of having $50.76 Total Purchase Value followed by "Nirvana" having $44.10 Total Purchase Value.
