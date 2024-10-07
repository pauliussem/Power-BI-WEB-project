 
## Declared plant's groups and plants by municipality.

### Steps followed

### 1. Oracle sql database

### Step 1:
Wrote a script to extract information from database about declared plants by municipality divided into legal and natural persons.
Assigned IDs to natural and legal persons and used UNION function to merge information about both of them.
Since every year has it’s own table and year isn’t provided in data set, made my own column [Metai].

![2 1](https://github.com/user-attachments/assets/f622c91b-4316-4dff-8119-2870198c7952)

### Step 2:
Created new folder and saved script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.


### Step 3:
Extracted required information from all tables from 2015 to 2024 and saved to folder “Year” so I could import all folder into power BI. Had to change only 2 numbers in a script (year value in column [Metai] and table name from database).

![2 2](https://github.com/user-attachments/assets/cb63aac8-9831-493c-9b6f-e03d0f92cdc2)

### Step 4:
Extracted classifiers from data base:
- Plant code, name and validation.
- Group, group name and group number.


### Step 5:
Since I knew, which plant belongs to which group of area, created my own excel table with plant code and group number:

![2 3](https://github.com/user-attachments/assets/e59c295c-0c9e-4b5c-b89a-83c13aee060f)

However,  I had to assign every year to every plant code in my excel sheet, because supporting group for some plants has changed during the years.

![2 4](https://github.com/user-attachments/assets/74239370-d416-497a-8da6-31ed34f3ed9e)

### Step 6:
Created my own table for legal and netural persons names and IDs.


## 2. Power BI query

### Step 1:
Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

### Step 2:
In power query deleted unnecessary column Source.name. Renamed table.

### Step 3:
Load data into Power BI Desktop, data is excel files (classifiers from data base and my own created tables. 

### Step 4:
In table Naudmenu pavadinimai[GALIOJA_IKI] extracted text before delimeter “-”.

### Step 5:
Created custom  column in “Naudmenu pavadinimai“ to provide information about validation of plant code. Empty fields in [GALIOJA_IKI] were left empty, which means code is still valid. 

    DAX was written:
    = Table.AddColumn(#"Extracted Text Before Delimiter", "Galiojimas", each if [GALIOJA_IKI]="" then "" else "(Iki:"&" "&[GALIOJA_IKI]&")")

![2 5](https://github.com/user-attachments/assets/67648619-5529-4e61-9939-7f9a1b64bcc7)

## 3. Power BI Table/Model view.

### Step 1:
Because  of repetitive plant code every year in tables “Deklaruotos naudmenos“ and “Naudmenos grupės”, wrote 2 DAXs for merging plant code and year, so I could make relationship between these two tables.

    DAXs were written:
    • Pavadinimai su galiojimu = 'Naudmenu pavadinimai'[KODAS]&" ("&'Naudmenu pavadinimai'- [PAVADINIMAS]&") "&'Naudmenu pavadinimai'[Galiojimas]
    • Naudmenos pagal metus = 'Naudmenos grupės'[KODAS]&'Naudmenos grupės'[METAI]

### Step 2:
Now I can relate all of the tables:

![2 6](https://github.com/user-attachments/assets/0d1f31b5-d7fa-416d-8670-f9420ed60ac9)

### Step 3:
Merged [Kodas], [Pavadinimas] and [Galiojimas] from table ‘Naudmenu pavadinimai’, so I could use it in visual later.

    DAX was written:
    •Pavadinimai su galiojimu = 'Naudmenu pavadinimai'[KODAS]&" ("&'Naudmenu pavadinimai'[PAVADINIMAS]&") "&'Naudmenu pavadinimai'[Galiojimas]

### Step 4:
Merged [Pavadinimas] and [Galiojimas] from table ‘Naudmenu pavadinimai’, so I could use it in visual later.
The only difference from step 3, I removed [KODAS] from DAX, because I am not going to need it in page 2. 

### Step 5:
Picked ‘Naudmenos grupių pavadinimai‘ [EILE] and in column tools > ‘Sort by column’, picked sort by nr, so it would sort Roman Numerals in order.

![2 7](https://github.com/user-attachments/assets/b37473a9-41ce-4002-b0cb-98d4531be3f9)

### Step 6:
Made new column in table ‘Naudmenos grupių pavadinimai’. So I could use it in visuals later.

    DAX was written:
    • Grupė su pavadinimu = 'Naudmenos grupių pavadinimai'[EILE]&" ("&'Naudmenos grupių pavadinimai'[PAVADINIMAS]&")"
### Step 7:
 Created table for measures.

	DAX was written:
	• [ Skaiciavimai] = {Blank()} 

### Step 8:
 Wrote 2 DAXs to SUM general number of declared area and provided applications.

	DAXs were written:
	• Bendras paraiskos = SUM('Deklaruotos naudmenos'[PARAISKOS_FJ]);
	• Bendras plotas = SUM('Deklaruotos naudmenos'[PLOTAS_FJ]).

### Step 9:
 For calculations set format to custom and custom format to ### ### ##0. for whole numbers and ### ### ##0.00 for decimal numbers.
### Step 10:
 Hid all not necessary columns.

## 3. Power BI report view

### Step 1:
 Prepared template from previous dashboard. Left only my own created table “METAI”, bookmark button, slicer for year and company’s logo.
### Step 2:
 Customised current theme:
- Changed font to arial;
- Changed wallpaper color to #E0F1D3.

![2 8](https://github.com/user-attachments/assets/1dfc4022-0572-46ae-931a-f78e159b051d)

### Step 3:
 Saved it in folder “Template”, so I could take a copy of it and prepare new projects on top of it.

### Step 4:
 Since I could use year information from main table, I deleted “METAI” table.

### Step 5:
 For data visualization took clustered column chart and matrix:
- Matrix 2 levels (municipality and year) and values declared area of 9 plant groups.
- Used 3 clustered column charts to visualize declared area by plant code, by plant classifier group and by grouped areas.

### Step 6:
 Made 3 slicers to filter data by municipality, plant and year. Used my merged column [Pavadinimai su galiojimu] in slicer “Search by plant”. Added search possibility in 2 slicers, except for years.

### Step 7:
 Edited interactions between matrix, slicers and clustered column chart from highlight to filer.

### Step 8:
 Turned on data labels for clustered column chart, set display units to none, orientation to vertical and made transparency to 20%, so contrast wouldn’t be so big. 

### Step 9:
Made bookmark button to clear all the slicers and filters. Used bookmark button instead of clear all the slicers button, because end-user could filter data not only with slicers. Made same style for any state of a button.

### Step 10:
Fixed all titles, font, size, bold to picked standard.

### 4. Drill-through page

### Step 1:
Made second page to represent data about declared plants by municipality.

### Step 2:
 For data visualization took clustered column chart, matrix and line chart:
• Matrix:
• 2 levels (municipality and year). Values declared area and provided applications divided into legal and public persons by picked plant code.
• Informational matrix about picked plant code and description.
• Clustered column charts to visualize declared area by picked plant code and municipality.
• Line chart to visualize change of declared area by picked plant from 2015 to 2024.
### Step 3:

 Added [NAUDMENOS KODAS] in drill-through field.

### Step 4:
Added drill-through button on top of visual with data about declared area by plant code. Made inactive button grey and wrote a tip “For button activation, please press on plant code”.

### Step 5:
 When plant code is pressed, made it orange to stick to standard from previous dashboard. And left space in tool tip, so arrow would appear when mouse is on top of that.

### Step 6:
 In tool tip > enabled text, I have left space, so arrow without any text would appear when mouse is on top of that and it’s active.

![2 9](https://github.com/user-attachments/assets/702ac2fe-ba07-4811-b1a1-f6479e4b27fc)


# Insights

### 1 page report and 1 drill-through page was created. 

### I hid 2nd page so end-user wouldn’t see it after publishing to internet and use drill-through button instead.

![2 10](https://github.com/user-attachments/assets/cf04fe3d-33c8-4b4b-bd5f-d502d3865a5b)


### Report was moved to Power BI service and published to web. HTML was provided to IT department.
### It was then published in our web page to simplify reading of data for end-user avoiding tons of excel or pdf files. You would need 2000+ different excel tables to provide 10 years statistics of such information.
### It visualizes data of 10 years statistics of declared area of plants by municipality. You can check declared area by plant and by classified plant group in all municipalities.
### It provides additional information about declared area of plant by municipality. Which you can’t find in our website. It is pretty needful information, but it would be tons of excel tables. With help of this report you can easily filter it using visuals or slicer and then using drill-through button. 
### You can sort plant code by group or by area very easily, check statistics in every municipality and divide it by every year.
