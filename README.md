 
## Provided applications, declared area and number of fields by municipality.

### Steps followed

### 1. Oracle sql database

#### Step 1:
 Wrote a script to extract information from data base about applications, declared area and number of fields grouped by municipality.
Extracted information to indicate 5 groups of applications:

- General information;
- Natural person;
- Legal person;
- Applications which were applied through e-gov portal;
- Applications to get support for young farmer.

Since every year has it’s own table and year isn’t provided in data set, made my own column [Metai].

![1 1](https://github.com/user-attachments/assets/9fae0f4a-b318-4695-b80c-1004d20abae3)

#### Step 2: 
Created new folder and saved script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.

#### Step 3:
 Extracted required information from all tables from 2015 to 2024 and saved to folder “Year” so I could import all folder into power BI. Had to change only 2 numbers in a script (year value in column [Metai] and table name from database).

![1 2](https://github.com/user-attachments/assets/7af1b17b-f111-4445-bcee-5939f6a20026)

#### Step 4:
 Took municipalities ID classifier from database and saved as excel file.
  
### 2. Power BI

#### Step 1: 
Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

#### Step 2:
 In power query deleted unnecessary column Source.name. Renamed table.

#### Step 3:
 Load data into Power BI Desktop, data is excel file – municipalities ID classifier. None further actions were needed.

#### Step 4:
 Picked MIN and MAX values from main table column [Year]. 

    DAXs was written:
    • MIN metai = MIN('Pagrindine info'[METAI])
    • MAX metai = MAX('Pagrindine info'[METAI])

#### Step 5:
 Created new table “Metai” and wrote a DAX, so this table would refresh depending on relevant years from main table.

    DAX was written:
    • METAI = GENERATESERIES([METAI MIN],[METAI MAX],1)

#### Step 6:
 Created new table for measures. Had to SUM 3 values (applications, declared area and number of fields) of each group.

    15 DAXs were written:
    • Bendras paraisku = SUM('Pagrindine info'[PARAISKU_SK])
    • EVV paraiskos = SUM('Pagrindine info'[PER_EL_VALD_PARAISKU_SK])
    • And so on... 

#### Step 7:
 Made relationships between METAI[Metai] >  Pagrindine informacija[Metai] and Savivaldybiu ID[SAV_ID] > Pagrindine informacija[SAVIVALDYBES_ID].
#### Step 8:
 For calculations set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.

![1 3](https://github.com/user-attachments/assets/8f5fda6a-53c8-4fcf-ad56-ccce14e6880c)

#### Step 9:
 Hid all not necessary columns.

### 3. Power BI report View

#### Step 1:
 Picked Accessible City park theme as for all dashboards of this “Web project“ (green color seemed the best for data about agriculture).

#### Step 2:
 Picked light green color for wallpaper.

#### Step 3:
 Inserted company‘s logo.

#### Step 4:
 For data visualization took clustered column chart, matrix and line chart to compare data change every year:
- Matrix 2 levels (municipality and year) and values of 5 groups.
- Line chart only year and general information.
- Clustered column chart year and values of 5 groups.

#### Step 5:
 Added shadows on visuals.

#### Step 6:
 Made 2 slicers to filter data by municipality and year. 

#### Step 7:
 Edited interactions between matrix, slicers and clustered column chart from highlight to filer.

#### Step 8:
 Edited interactions of line chart between visuals and slicers so it responds to municipality filters, but not years (the only exception, if customer expand matrix > municipality by year).

#### Step 9:
 Took arial font for diagrams, since it’s standard in our company. Decided size of titles, legend, values, slicers and etc. whose will be used in all dashboards. 

#### Step 10:
 Turned on data labels for clustered column chart, set display units to none, orientation to vertical and made transparency to 20%, so contrast wouldn’t be so big when values is on top of a bar. Turned on data labels for line chart too, but left display units to thousands. 

![1 4](https://github.com/user-attachments/assets/e9f10775-9faa-4efe-b04d-c8069ac7997c)

#### Step 11:
 Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

#### Step 12:
 Duplicated first page 2 times, inserted page navigator. In selected state, made grey color of a button. Default state green color. Hover lighter green with black letters. Press darker green with white letters. 

![1 5](https://github.com/user-attachments/assets/a294590f-b6d4-458c-ab03-a0675aead12d)

#### Step 14:
 Filled visuals with required information. 2nd page > 2nd group (declared area), 3rd page > 3rd group (number of fields). Fixed titles, legends and etc. 

#### Step 15:
 Made additional bookmark buttons, divided into 3 groups. Assigned each group to each page to clear all the filters of current page.

![1 6](https://github.com/user-attachments/assets/9db04d81-1dda-454c-aff6-ad15bfd499d7)

#### Step 16:
 Set 2024 year as default, when bookmark button “Clear all selections” is used.

## Insights

### 3 pages report was created on Power BI desktop. 3 pages were picked to avoid overcrowding information. 
### I hid 2nd and 3rd pages so end-user wouldn’t see them after publishing to internet and use buttons instead.

![1 7](https://github.com/user-attachments/assets/e8227d3b-2415-4d90-997c-4671ad39e96e)


### Report was moved to Power BI service and published to web. HTML was provided to IT department.
### It was then published in our web page to simplify reading of data for end-user, avoiding tons of excel or pdf files.
### It shows data of 10 years of statistics of provided applications for support, about declared area and number of fields. 
### It provides additional information about legal and natural persons applications, which you can’t find in our web page.
### You can compare changes of applications and other groups over the year. You can check number of each group by year and municipality.
