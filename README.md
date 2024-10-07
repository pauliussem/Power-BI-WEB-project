


## Provided applications to get linked support.

## Steps followed

### 1. Oracle sql database

### Step 1:
 Had to write 2 different scripts, to get information about proposed applications for linked support. One for general applications by municipality, other one grouped by applications by plant code (it’s because one farmer can apply with different plant codes).

### Step 2:
 Took 2 classifiers from data base:

* Plant codes and it’s names;
* Municipality ID’s and names.

### Step 3:
 Created 2 new folders and saved scripts, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created folder (“Year”) for each created folder to save .csv files by year.

### Step 4:
 Extracted required information from all tables from 2015 to 2024 and saved to created folders “Year” so I could import both folders into power BI. Had to change only 2 numbers in a script (year value in column [Metai] and table name from database).

## 2. Power BI

### Step 1:
 Copied prepared template from earlier to dashboard folder and started to work on it.

### Step 2:
 Load data into Power BI Desktop, dataset is 2 folders “Year” with .csv files for each year.

### Step 3:
 In power query deleted unnecessary columns Source.name. Renamed tables.

### Step 4:
 Load data into Power BI Desktop, data is excel file – classifier from database (municipalities names and IDs) and 2 tables which I’ve created by myself. No further actions were needed.

### Step 5:
 Wrote a DAXs to take MIN and MAX years. So table metai would refresh according provided dataset.

	DAXs were written:
    • MAX metai = MAX('Susietoji parama pagal kodus'[METAI]);
    • MIN metai = MIN('Susietoji parama pagal kodus'[METAI]).

### Step 6: Made relationships between tables.

### Step 7:
 Set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.

### Step 8:
 Hid all not necessary columns.

### Step 9:
 At ‘Naudmenu pavadinimai’ created new column with merged [Pavadinimas] and [Kodas], so I could use it in matrix later.

    DAX was written:
    • Pavadinimas su kodu = 'Naudmenu pavadinimai'[KODAS]&" ("&'Naudmenu pavadinimai'[PAVADINIMAS]&")"

## Power BI report view

### Step 1:
 For data visualization took clustered column charts, matrixs and line charts:

* Matrixs for applications and declared area by municipality and other one by plant code.
* Clustered column charts to provide information about applications and declared area by plant code.
* Line charts to provide changes of declared area and provided applications during the year.

### Step 2:
 Added shadows only on visuals.

### Step 3:
 Made 3 slicers to filter data by municipality, plant code and year. 
 
### Step 4:
 Edited interactions between matrix, slicers and clustered column chart from highlight to filer.

### Step 5:
 For line charts, made filters only by municipality, so I could see change even if year filter is on. 

### Step 6:
 Turned on data labels for clustered column charts and line charts, set display units to none except for declared area by municipality and made transparency to 20%, so contrast wouldn’t be so big.

### Step 7:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

### Step 8:
 Fixed all titles, font, size, bold to picked standard.

### Step 9:
 Set bookmark to filter 2024 as default year.

### Step 10:
 Fixed mobile layout. 


# Insights

### 1 page report was created. Report was moved to Power BI service and published to web. HTML was provided to IT department.
### It was then published in our web page to simplify reading of data for end-user, avoiding tons of excel or pdf files.

### It visualizes data of 10 years statistics of declared area and provided application for linked support to get. You can check declared area and provided applications by municipality and plant code.

### You could see change of declared area and provided applications during the years.
