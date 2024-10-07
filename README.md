


## Provided applications by declared area intervals.

## Steps followed

### 1. Oracle sql database

### Step 1:
 Wrote 2 groups of scripts to extract information about legal person’s and public person’s provided applications and declared area by declared area’s intervals.
Since intervals were divided into 14 groups, applied group number to each group and used UNION function to merge all groups in one table and created one more group for legal and natural persons to used it in power BI later.

![8 1](https://github.com/user-attachments/assets/4267d01d-33e4-420c-be04-b982d0371c7e)

### Step 2:
 Since we do not have classifiers in our database, had to create 2 excel tables:
* Declared area interval’s groups;
* Public and legal person‘s groups.

### Step 3:
 Created new folder and saved each script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year and legal status.

### Step 4:
 Extracted required information from all tables from 2015 to 2024 and saved to folder “Year” so I could import all folder into power BI. Had to change year number in each place in a scripts.

![8 2](https://github.com/user-attachments/assets/9a6b737f-03d1-4423-89f0-4fe1f64c6a5c)

## 2. Power BI

### Step 1:
 Copied prepared template from earlier to dashboard folder and started to work on it.

### Step 2:
 Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year and public status.

### Step 3:
 In power query deleted unnecessary column Source.name. Renamed table to ‘Paraiskos ir deklaruotas plotas’.

### Step 4:
 Load data into Power BI Desktop, data is excel file – classifier from database (municipalities names and IDs) and 2 tables which I’ve created by myself. 

### Step 5:
 Added conditional column in table ‘Intervalu grupes’  and applied numbers to each interval, so I could sort intervals in order later.

    = Table.AddColumn(#"Promoted Headers", "Plotas sorted", each if [Plotas be grupiu] = "<1" then 1 else if [Plotas be grupiu] = "1,01 > 2" then 2 else if [Plotas be grupiu] = "2,01 > 3" then 3 else if [Plotas be grupiu] = "3,01 > 5" then 4 else if [Plotas be grupiu] = "5,01 > 10" then 5 else if [Plotas be grupiu] = "10,01 > 20" then 6 else if [Plotas be grupiu] = "20,01 > 30" then 7 else if [Plotas be grupiu] = "30,01 > 50" then 8 else if [Plotas be grupiu] = "50,01 > 100" then 9 else if [Plotas be grupiu] = "100,01 > 200" then 10 else if [Plotas be grupiu] = "200,01 > 300" then 11 else if [Plotas be grupiu] = "300,01 > 400" then 12 else if [Plotas be grupiu] = "400,01 > 500" then 13 else if [Plotas be grupiu] = "> 500" then 14 else null)


### Step 6:
 Since I could use year information from main table, I’ve deleted “METAI” tablem which was in a template.

### Step 7:
 Made relationships between tables.
### Step 8:
 For calculations, set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.
### Step 9:
 Hid all not necessary columns.

## 3. Power BI report view

### Step 1:
 For data visualization took 2 line charts and matrix:

* Matrix 2 levels (municipality and year) and values declared area intervals;
* Line charts to see changes by declared area intervals.

### Step 2:
 Added shadows only on visuals.

### Step 3:
 Made 2 slicers to filter data by municipality and year. 
### Step 4:
 Made slicer as tile, to filter data by public or legal person.

![8 3](https://github.com/user-attachments/assets/45de2a38-04b4-44aa-b07d-113ae5e9115c)

### Step 5:
 Removed interactions between line charts.

### Step 6:
 Turned on data labels on line charts and made transparency to 20% to stick to standard. 

### Step 7:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.
### Step 8:
 In column tools [Plotas] and [Plotas be grupiu] sorted by [Plotas sorted], because intervals are sorted in wrong order.
### Step 9:
 Fixed all titles, font, size, bold to picked standard.
### Step 10:
 Set bookmark to filter 2024 as default year.

# Insights

### 1 page report was created. Report was moved to Power BI service and published to web. HTML was provided to IT department.

### It was then published in our web page to simplify reading of data for end-user, avoiding tons of excel or pdf files.

### It visualizes data of 10 years statistics of declared area and provided applications by declared area intervals. You can check provided applications and declared area divided by these intervals in every municipality. 

### Declared area and provided applications divided into 2 groups (public and legal persons).

### You can easily see changes of declared area or provided applications by declared area intervals in line charts. You can check it by every municipality.
