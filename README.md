


## Provided applications and declared area by supporting groups.

## Steps followed

### 1. Oracle sql database

### Step 1:
 Had to create 3 excel tables. One for groups, one for subgroups and for plant codes or indications. Assigned each subgroup to group and each plant code or indication to subgroup.

### Step 2:
 Wrote a script for each plant or indication, created 4 columns for groups, subgroups, plant or indication number and year. Year column was not necessary, because I had to take statistics only for 2024, however if statistics next year will be needed I could use the same script. Used UNION function to merge all statistics in the same columns.

![9 1](https://github.com/user-attachments/assets/4d6d8a4a-f41b-4964-9be1-daa33227afb5)

### Step 3:
 Created new folder and saved script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.

### Step 4:
 Extracted required statistics of 2024 and saved to folder “Year” so I could import all folder into power BI. 

## 2. Power BI

### Step 1:
 Copied prepared template from earlier to dashboard folder and started to work on it.

### Step 2:
 Load data into Power BI Desktop, dataset is folder “Year” with .csv file. Only one file was in a folder, but next year I could update information very easily.

### Step 3:
 In power query deleted unnecessary column Source.name. Renamed table.

### Step 4:
 Load data into Power BI Desktop, data is excel file – classifier from database (municipalities names and IDs) and 3 tables which I’ve created by myself. No further actions were needed.

### Step 5:
 Wrote a DAXs to take MIN and MAX values, so table ‘Metai’ could update automatically depending on provided information.

	DAXs were written:
    • MAX metai = MAX('Paraiskos ir plotas'[METAI]);
    • MIN metai = MIN('Paraiskos ir plotas'[METAI]).


### Step 6:
 Made relationships between tables. Assigned each subgroup to group and each plant code or indication to subgroup.

![9 2](https://github.com/user-attachments/assets/17fbc9fd-5b3e-4603-8889-bd0e872c9e5c)


### Step 7:
 For calculations, set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.

### Step 8:
 Hid all not necessary columns.

### Step 9:
 At ‘Pogrupiu kodai’ created new column with merged [Pavadinimas] and [Kodas]”.

    DAX was written:
    • Pavadinimas su kodu = 'Pogrupiu kodai'[Pavadinimas]&" ("&'Pogrupiu kodai'[Kodas]&")"

## 3. Power BI report view

### Step 1:

 For data visualization took clustered column charts and matrix:

* Matrix 2 levels (municipality and every plant code or indication excluded separately);
* 2 clustered columns charts. One for declared area and provided applications by group and other one declared area and provided applications by plant code or indication. 

### Step 2:
 Added shadows only on visuals.

### Step 3:
 Made 2 slicers to filter data by municipality and other one to filter data by plant code or indication.

### Step 4:
 ‘Pogrupiu kodai’ [Pavadinimas su kodu] made to sort by ‘Pogrupiu kodai’[Pogrupis].

### Step 5:
 Edited interactions between clustered column chart from highlight to filter.

### Step 6:
 Turned on data labels for clustered column charts, set display units to none orientation to vertical and made transparency to 20%, so contrast wouldn’t be so big, in case label appears on a bar. 

### Step 7:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

### Step 8:
 Set number format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.

### Step 9:
 Fixed all titles, font, size, bold to picked standard. 

# Insights

### 1 page report was created. Report was moved to Power BI service and published to web. HTML was provided to IT department.
### It was then published in our web page to simplify reading of data for end-user, avoiding tons of excel or pdf files.

### It visualizes data of declared area and provided applications of picked group of plants or indications. You can check declared area  and number of applications of each group and compare it be each plant code or indication.

### You can sort plant codes or indication by group. You can check this information divided in every municipality.
