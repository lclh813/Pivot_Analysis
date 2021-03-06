# Pivot Analysis
## Notice
It is possible that GitHub fails to display Jupyter Notebooks. Should such circumstances arise, please refer to ***Part 4. Steps*** listed below for code samples.

## Part 1. Objective
Create a table on an ***annual*** basis to better know ***how many*** and ***from where*** the listed fruits are purchased from 2016 to 2017. 

## Part 2. Data
### 2.1. Background Information
> ***2.1.1. Info 1. Fruits Purchased by the Fruit Shop***

| Fruit_Type_ID  | Fruit_Type | Fruit_Name_ID | Fruit_Name        | 
| :---           | :---       | :---          | :---              | 
| APPL           | Apple      | APPL001       | Red Delicious     | 
| APPL           | Apple      | APPL002       | Royal Gala        | 
| GRAP           | Grape      | GRAP001       | Golden Muscat     | 
| KIWI           | Kiwifruit  | KIWI001       | Sungold Kiwifruit | 

> ***2.1.2. Info 2. Order History***

| Supplier | Purchase_Year | Supplier Type |
| :---     | :---          | :---          |
| Farm 1   | 2016, 2017    | Regular       | 
| Farm 2   | 2016, 2017    | Regular       |
| Farm 3-1 | 2016          | Non-Regular   | 
| Farm 3-2 | 2017          | Non-Regular   | 
| Farm 4   | 2016, 2017    | Regular       |

### 2.2. Original Data
- There are 24 xls files in sum, one file per month with a subtotal displayed in the last row, which represents total purchase for the entire month.

| Purchase_Date | Supplier | Total<br>Qty | APPL<br>001 Qty | APPL<br>001 % | APPL<br>002 Qty | APPL<br>002 % | GRAP<br>Qty | GRAP<br>%  | KIWI<br>Qty | KIWI<br>% |
| :---:         | :---:    | :---:  | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |  
| 2016/01/01    | Farm 1   | 100    | 10    | 10%   | 10    | 10%   | 70    | 70%   | 10    | 10%   |
| 2016/01/01    | Farm 2   | 200    | 10    | 5%    | 10    | 5%    | 120   | 60%   | 60    | 30%   |
| 2016/01/01    | Farm 3-1 | 300    | 30    | 10%   | 60    | 20%   | 105   | 35%   | 105   | 35%   |
| 2016/01/01    | Farm 4   | 400    | 40    | 10%   | 60    | 15%   | 200   | 50%   | 100   | 25%   |
| ...           | ...      | ...    | ...   | ...   | ...   | ...   | ....  | ...   | ...   | ...   |
| **Jan-2016** | **-** | **15,000** | **1,500** | **10%** | **1,500** | **10%** | **6,000** | **40%** | **6,000** | **40%** |
| ...           | ...      | ...    | ...   | ...   | ...   | ...   | ...   | ...   | ...   | ...   |
| 2017/12/31    | Farm 1   | 500    | 100   | 20%   | 200   | 40%   | 150   | 30%   | 50    | 10%   |
| 2017/12/31    | Farm 2   | 400    | 160   | 40%   | 80    | 20%   | 80    | 20%   | 80    | 20%   |
| 2017/12/31    | Farm 3-2 | 300    | 90    | 30%   | 30    | 10%   | 75    | 25%   | 105   | 35%   |
| 2017/12/31    | Farm 4   | 200    | 20    | 10%   | 30    | 15%   | 100   | 50%   | 50    | 25%   |
| **Dec-2017** | **-** | **18,000** | **9,000** | **50%** | **2,000** | **11%** | **3,000** | **17%** | **4,000** | **22%** |

### 2.3. Expected Result
- Convert original ***daily*** data to ***annual*** data and sum up the result of 2016 and 2017. 

### 2.3.1. Convert Daily Data to Monthly Data

> ***Table: Order History of the Fruit Shop***     
> ***Time: January, 2016***

| Fruit_Type | Farm 1  | Farm 2  | Farm 3-1 | Farm 4  |
| :---       | ---:    | ---:    | ---:     | ---:    |
| Apple      | 261     | 261     | 1,174    | 1,304   |
| Grape      | 848     | 1,455   | 1,273    | 2,424   |
| Kiwifruit  | 218     | 1,309   | 2,291    | 2,182   |

> ***Table: Order History of the Fruit Shop***   
> ***Time: December, 2017***

| Fruit_Type | Farm 1  | Farm 2  | Farm 3-2 | Farm 4  |
| :---       | ---:    | ---:    | ---:     | ---:    |
| Apple      | 4,648   | 3,718   | 1,859    | 775     |
| Grape      | 1,110   | 593     | 556      | 741     |
| Kiwifruit  | 702     | 1,123   | 1,473    | 702     |

### 2.3.2. Convert Monthly Data to Annual Data and Sum up

> ***Table: Order History of the Fruit Shop***   
> ***Time: 2016-2017***

| Fruit_Type | Farm 1  | Farm 2  | Farm 3   | Farm 4  |
| :---       | ---:    | ---:    | ---:     | ---:    |
| Apple      | 120,000 | 100,000 | 130,000  | 80,000  |
| Grape      | 90,000  | 110,000 | 80,000   | 90,000  |
| Kiwifruit  | 125,000 | 100,000 | 60,000   | 50,000  |

## Part 3. Outline
### 3.1. Clean Dataset
### 3.1.1. Drop Columns 
- Drop columns that are not needed for further analysis which include ***Total Qty*** and those containing ***%***
- Tool: Python ```drop```

| Purchase_Date | Supplier  | APPL001 | APPL002 | GRAP | KIWI | 
|:---:          |:---       | ---:    | ---:    | ---: | ---: | 
| 2016/01/01    | Farm 1    | 10      | 10      | 70   | 10   |
| 2016/01/01    | Farm 2    | 10      | 10      | 120  | 60   |
| ...           | ...       | ...     | ...     | ...  | ...  |
| 2017/12/31    | Farm 3    | 90      | 30      | 75   | 105  |
| 2017/12/31    | Farm 4    | 20      | 30      | 100  | 50   |

### 3.1.2. Reshape Dataframe
- Prepare to move ***Fruit_Name_ID*** to the row axis while ***Purchase_Date*** and ***Supplier*** remain at the header. 
- Tool: Python ```melt``` 
 
| Purchase_Date | Supplier  | Fruit_Name_ID | Qty |
| :---:         | ---       | :---          | ---:| 
| 2016/01/01    | Farm 1    | APPL001       | 10  |
| 2016/01/01    | Farm 1    | APPL002       | 10  |
| 2016/01/01    | Farm 1    | GRAP          | 70  |
| 2016/01/01    | Farm 1    | KIWI          | 10  | 
| ...           | ...       | ...           | ... |
| 2017/12/31    | Farm 4    | APPL001       | 20  | 
| 2017/12/31    | Farm 4    | APPL002       | 30  |
| 2017/12/31    | Farm 4    | GRAP          | 100 |  
| 2017/12/31    | Farm 4    | KIWI          | 50  | 

### 3.1.3. Data Type Conversion
- Records in Column ***Qty*** turned out to be string objects rather than numeric values because they are formatted with thousand separator. It is necessary to convert strings to numbers before proceed further calculation.
#### 3.1.3.1. Conversion to String
- Tool: Python ```astype```
#### 3.1.3.2. Remove Thousand Separator
- Tool: Python ```apply``` ```lambda```
#### 3.1.3.3. Conversion to Integer
- Tool: Python ```astype```
#### 3.1.4. Export Dataset for Analysis
- Tool: Python ```groupby``` ```to_csv```

### 3.2. Pivot Analysis
#### 3.2.1. Drop Column
- Drop ***Purchase_Date*** which is of no use for pivot analysis.
- Tool: Python ```drop```
#### 3.2.2. Create Pivot Table
- Set ***Fruit_Type_ID*** at row axis and ***Supplier*** at column axis. 
#### 3.2.3. Rename Columns
- ***Apple*** purchased in 2016 is ***Red Delicious*** and ***Royal Gala*** in 2017. 
#### 3.2.4. Sum up Rows
- Add ***Farm 3-1*** and ***Farm 3-2*** together to get ***Farm3***.
- Tool: Python ```if``` ```pivot_table```

## Part 4. Steps
> [***Complete Code***](https://nbviewer.jupyter.org/github/lclh813/Pivot/blob/master/5_CompleteCode.ipynb)
#### [Step 1. Import Library](https://nbviewer.jupyter.org/github/lclh813/Pivot/blob/master/1_ImportLibrary.ipynb)
#### [Step 2. Import Data](https://nbviewer.jupyter.org/github/lclh813/Pivot/blob/master/2_ImportData.ipynb)
#### [Step 3. Clean Dataset](https://nbviewer.jupyter.org/github/lclh813/Pivot/blob/master/3_CleanDataset.ipynb)
#### [Step 4. Pivot Analysis](https://nbviewer.jupyter.org/github/lclh813/Pivot_Analysis/blob/master/4_PivotAnalysis.ipynb)
