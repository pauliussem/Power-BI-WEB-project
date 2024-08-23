## Steps followed

### Oracle sql database

- Step 1: Wrote a script to extract information from data base about applications, declared area and number of fields dividing information into 5 groups:
    • General information;
    • Natural person;
    • Legal person;
    • Applications which were applied through e-gov portal;
    • Applications to get support for young farmer.
  
Since every year has it’s own table and year isn’t provided in any column, made my own column [Metai].


- Step 2: Created new folder and saved script, so next year I could take exactly the same information from database (Same order, same column names and etc.)
Created one more folder (“Year”) in created folder to save .csv files by year.

- Step 3: Extracted required information from all tables from 2015 to 2024 and saved to folder “Year” so I could import all folder into power BI. Had to change only 2 numbers in a script (year value in column [Metai] and table name from database).

### Power BI

- Step 1: Load data into Power BI Desktop, dataset is folder “Year” with .csv files for each year.

- Step 2: In power query deleted unnecessary column Source.name. Renamed table.

- Step 3: Load data into Power BI Desktop, data is excel file – classifier from database (municipalities names and IDs). None further actions were needed.

- Step 4: Picked MIN and MAX values from main table column [Year]. 
DAXs was written:
	MIN metai = MIN('Pagrindine info'[METAI])
	MAX metai = MAX('Pagrindine info'[METAI])

- Step 5: Created new table “Metai” and wrote a DAX, so this table would refresh depending on relevant years from main table:
DAX was written:
METAI = GENERATESERIES([METAI MIN],[METAI MAX],1)

- Step 6: Created new table for measures. Had to SUM 3 values (applications, declared area and number of fields) of each group.
15 DAXs was written:
	Bendras paraisku = SUM('Pagrindine info'[PARAISKU_SK])
	EVV paraiskos = SUM('Pagrindine info'[PER_EL_VALD_PARAISKU_SK])
	And so on... 

Step 7: Made relationships between METAI[Metai] >  Pagrindine informacija[Metai] and Savivaldybiu ID[SAV_ID] > Pagrindine informacija[SAVIVALDYBES_ID].

- Step 8: Hid all not necessary columns.

### Power BI report View

- Step 1: Picked Accessible City park theme as for all dashboards of this “Web project“ (green color seemed the best for data about agriculture).

- Step 2: Picked light green color for wallpaper and saved Hex to use it in next dashboards.

- Step 3: Inserted company‘s logo.

- Step 4: For data visualization took clustered column chart, matrix and line chart to compare data change every year:
	* Matrix 2 levels (municipality and year) and values of 5 groups.
	* Line chart only year and general information.
	* Clustered column chart year and values of 5 groups.

- Step 5: Added shadows only on visuals.

- Step 6: Made 2 slicers to filter data by municipality and year. 

- Step 7: Edited interactions between matrix, slicers and clustered column chart from highlight to filer.

- Step 8: Edited interactions of line chart between visuals and slicers so it responds to municipality filters, but not years (the only exception, if customer expand matrix > municipality by year).

- Step 9: Took arial font for diagrams, since it’s standard in our company. Decided size of titles, legend, values, slicers and etc. whose will be used in all dashboards. 

- Step 10: Turned on data labels for clustered column chart, set display units to none, orientation to vertical and made transparency to 20%, so contrast wouldn’t be so big, when values is on top of a bar. Turned on data labels for line chart too, but left display units to thousands. 
