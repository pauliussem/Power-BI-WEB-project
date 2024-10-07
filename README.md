 
## Declared plants by picked group by municipalities.

### Steps followed

### 1. Oracle sql database

### Step 1:
 Since I had to count applications and declared area of declared plants by it’s code or by it’s indication, grouped by only by group or municipality or code, had to write 18 different scripts, divided into 3 groups. (Now I would use UNION and divide scripts into 3 groups instead, unfortunately after running script and saving different csv’s for 180 times I googled it later). 

### Step 2:
 Whereas I wanted to merge all .csv files of one group of scripts, I needed same column number and same columns names, so I wrote such a script and had to apply it to all 10 groups.

![6 1](https://github.com/user-attachments/assets/a9f3d3e3-c9c0-47b4-9651-86ca4a07b06a)

I wanted to get number of applications only by group and in other visuals I wanted to see number of applications only by plant code. Since some applications grouped by plant code, can be of the same farmer’s, I had to divide it into 2 different groups of scripts.
### Step 3:
 Had to create 7 different excel tables and take municipality and plant codes classifiers.

### Step 4:
Created 3 folders and saved scripts, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.

### Step 5:
 Extracted required information from all tables from 2015 to 2024 and saved to folders “Year” so I could import all folder into power BI. 

## 2. Power BI

### Step 1:
 Copied prepared template from earlier to dashboard folder and started to work on it.

### Step 2:
 Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 3:
 In power query deleted unnecessary column Source.name. Renamed tables.

### Step 4:
 Repeated everything for all 3 folders.

### Step 5:
 In all 3 tables replaced 0 to null values, so later in visuals, we won’t see unnecessary information with values of 0.

    = Table.ReplaceValue(#"Changed Type1",0,null,Replacer.ReplaceValue,{"SP_EKO_PLOTAS", "SP_EKO_PARAISKOS", "KPP_EKO_PLOTAS", "KPP_EKO_PARAISKOS", "AGRARINE_PLOTAS", "AGRARINE_PARAISKOS", "NEPALANKIOS_PLOTAS", "NEPALANKIOS_PARAISKOS", "NATURA_PLOTAS", "NATURA_PARAISKOS", "MISKO_PLETRA_PLOTAS", "MISKO_PLETRA_PARAISKOS", "NATURA_MISKUOSE_PLOTAS", "NATURA_MISKUOSE_PARAISKOS", "ZM_1_7_PLOTAS", "ZM_1_7_PARAISKOS", "AI_1_2_PLOTAS", "AI_1_2_PARAISKOS", "NM_1_7_PLOTAS", "NM_1_7_PARAISKOS"})

### Step 6:
 Load data into Power BI Desktop, data is excel files – classifiers from database and 7 tables which I’ve created by myself. 

### Step 7:
 Made relationships between tables.

![6 2](https://github.com/user-attachments/assets/b3b77755-f236-408e-b8e0-99d4ba9dc753)

### Step 8:
 Hid all not necessary columns.

### Step 9:
 Wrote a DAX to merge name and code for 4 my own created tables:
‘Agrarine aplinkosauga’, ‘Ekologinis lentele’, ‘Natura 2000’, ‘Nepalankios vietoves’

    DAXs were written:
    • Pavadinimas su kodu = 'Ekologinis lentele'[PAVADINIMAS]&" ("&'Ekologinis lentele'[KODAS]&")";
    • And so on fore ach table.

### Step 10:
 Created my own table for measures.

	DAX was written:
    • [ Skaiciavimai] = {Blank()} 

### Step 11:
 Wrote to sum all aplications and declaread area of each my own created group and picked MIN and MAX values of years, so ‘Metai’ table, automatically updates by relevant year.

	DAXs were written:
    • Agrarine paraiskos = SUM('Pozymiai pagal naudmenas'[AGRARINE_PARAISKOS]);
    • Agrarine plotas = SUM('Pozymiai pagal naudmenas'[AGRARINE_PLOTAS]);
    • And so on..;
    • MIN metai = MIN('Pozymiai pagal naudmenas'[METAI]);
    • MAX metai = MAX('Pozymiai pagal naudmenas'[METAI]);

### Step 12:
 Wrote a DAX to SUM all applications and declaread area of each group in table ‘Plotas ir paraiskos pagal savivaldybes’, so I could use it in matrix visual and divide each group into applications and declared area.

	DAXs were written:
    • Bendras paraiskos = 'Plotas ir paraiskos pagal savivaldybes'[AGRARINE_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[AI_1_2_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[KPP_EKO_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[MISKO_PLETRA_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[NATURA_MISKUOSE_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[NATURA_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[NEPALANKIOS_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[NM_1_7_PARAISKOS] + 'Plotas ir paraiskos pagal savivaldybes'[SP_EKO_PARAISKOS] +'Plotas ir paraiskos pagal savivaldybes'[ZM_1_7_PARAISKOS]
    • Bendras plotas = 'Plotas ir paraiskos pagal savivaldybes'[AGRARINE_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[AI_1_2_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[KPP_EKO_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[MISKO_PLETRA_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[NATURA_MISKUOSE_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[NATURA_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[NEPALANKIOS_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[NM_1_7_PLOTAS] + 'Plotas ir paraiskos pagal savivaldybes'[SP_EKO_PLOTAS] +'Plotas ir paraiskos pagal savivaldybes'[ZM_1_7_PLOTAS]

### Step 13:
 Set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.


## 3. Power BI report view

## Page 1

### Step 1:
 For data visualization took clustered column charts and matrix:

* Matrix 2 levels (municipality and year) and values (declared area and number of applications by support group).
* Clustered column charts were picked to visualize declared area by support group and other one, declared area by plant code of each group. 

### Step 2:
 Added shadows only on visuals.

### Step 3:
 Made 2 slicers to filter data by municipality and year. 
 
### Step 4:
 Edited interactions between matrix, slicers and clustered column chart from highlight to filer.

### Step 5:
 Turned on data labels for clustered column charts, set display units to none on both charts and made transparency to 20%, so contrast wouldn’t be so big, in case if numbers would appear on a bar.

### Step 6:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

## Page 1-4

### Step 7:
 Duplicated first page 4 times, inserted page navigator. In selected state, made grey color of a button. Default state green color. Hover lighter green with black letters and on press darker geen with white letters. 

### Step 8:
 Prepared 2nd page, pretty the same information as I the first page, except applications and declared area by codes from picked support groups.
### Step 9:
 Set filters to none, except year slicer for visual applications by supporting groups, because total number of applications differs from matrix.

### Step 10:
 Since page 2-5 provides exactly the same information, except supporting group, as soon as 2nd page seemed finished, duplicated it 3 times more and deleted 3 duplicates whose were created before to avoid as much as possible unnecessary work.

### Step 11:
 Fixed all titles, font, size, bold to picked standard.

### Step 12:
 Made additional bookmark buttons, divided into 5 groups. Assigned each group to each page to clear all the filters of current page.

![6 3](https://github.com/user-attachments/assets/ee1176c2-4520-4d3d-81e9-8c2bd7def642)

### Step 13:
 Set all bookmarks to filter 2024 as default.

### Step 14:
 Fixed mobile layout.

# Insights
### 5 pages report was created on Power BI desktop. 4 more pages were needed to provide detail information about picked groups.
### I hid 2nd, 3rd, 4th and 5th pages so end-user wouldn’t see them after publishing to internet and use page navigator buttons instead.

![6 4](https://github.com/user-attachments/assets/901c1dc9-d8c4-4cc8-9225-788ac0e79096)

### Report was moved to Power BI service and published to web. HTML was provided to IT department.
### It was then published in our web page to simplify reading of data for end-user, avoiding tons of excel or pdf files.


### It visualizes data of 10 years statistics of declared area of picked support groups. You can check declared area and number of applications of each group and compare declared plants by each group. 
### You can sort plant codes of each group very easily. You can see group or plants by groups information in every municipality divided to each year from 2015 to 2024.
