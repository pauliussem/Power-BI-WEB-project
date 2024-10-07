 
## Declared plants by picked group by municipalities.

### Steps followed

### 1. Oracle sql database

### Step 1:
 Wrote a script to extract information from data base about declared plants by group.
Since every year has it’s own table and year isn’t provided in data set, made my own column [Metai].

### Step 2:
 Since we do not have classifiers in our database, had to create 2 excel tables:
* Plant, plant code and I’ve assigned group number to each group:
* Group name and group number.

### Step 3:
 Created new folder and saved script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.

### Step 4:
 Extracted required information from all tables from 2015 to 2024 and saved to folder “Year” so I could import all folder into power BI. Had to change only 2 numbers in a script (year value in column [Metai] and table name from database).

## 2. Power BI

### Step 1:
 Copied prepared template from earlier to dashboard folder and started to work on it (with picked font and etc.).

### Step 2:
 Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 3:
 In power query deleted unnecessary column Source.name. Renamed table.

### Step 4:
 Load data into Power BI Desktop, data is excel file – classifier from database (municipalities names and IDs) and 2 tables which I’ve created by myself. No further actions were needed.

### Step 5:
 Since I could use year information from main table, I deleted “METAI” table, which was in my template.

### Step 6:
 Made relationships between tables.

### Step 7:
 Set format to custom and custom format to ### ### ##0.00 for declared area in a table ‘Deklaruotas plotas‘.

### Step 8:
 Hid all not necessary columns.


## 3. Power BI report view

### Step 1:
 For data visualization took clustered column charts and matrix:
	* Matrix 2 levels (municipality and year) and values picked plant groups.
	* Clustered column charts for declared area by year and plant group and declared area by plant code and year.

### Step 2:
 Added shadows only on visuals.

### Step 3:
 Made 2 slicers to filter data by municipality and year. 
 
### Step 4:
 Edited interactions between matrix, slicers and clustered column chart from highlight to filter.

### Step 5:
 Turned on data labels for clustered column charts, set display units to none on both charts, orientation to vertical on one and horizontal on other and made transparency to 20%, so contrast wouldn’t be so big, if labels would appear on a bar. 

### Step 6:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

### Step 7:
 Fixed all titles, font, size, bold to picked standard.
### Step 8:
 Set bookmark to filter 2024 as default year.

# Insights

### 1 page report was created. Report was moved to Power BI service and published to web. HTML was provided to IT department.

### It was then published in our web page to simplify reading of data for end-user avoiding tons of excel or pdf files.

### It visualizes data of 10 years statistics of declared area of picked group of plants. You can check declared area of each group and compare declared plants by each group.

### You can sort plant by group very easily. You can see group or plants by group information in every municipality divided to each year from 2015 to 2024.
