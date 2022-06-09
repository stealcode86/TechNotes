# TechNotes

1) Find for a text in range and return value 

	=VLOOKUP() or 
	=INDEX(,MATCH(),)

2) Get cell value by giving address

	=INDIRECT(ADDRESS(3,4)) or
	=INDIRECT(G4)

3) To concatenate Date and Time with text 

	=CONCATENATE("'",TEXT(Sheet1!C2,"dd-MMM-yyyy"),"'",",")
	You can get date in the required format.

4) Automatically update data in Sheet 2 from Sheet 1

https://www.got-it.ai/solutions/excel-chat/excel-tutorial/data-entry/automatically-update-data-in-another-sheet

5) Replace #N/A error with String 

=IFNA(Sheet2!J1,CONCATENATE("'"," ","'",","))

6) Excel - Shortcuts 

F2 to edit a tab instead of starting all over again. ( fn+ F2 ) <br/>
Ctrl + Z - undo, Ctrl Y - redo <br/>
Ctrl + space bar -  Select entire column <br/>
Shift + space bar - Select entire row <br/>
Ctrl + + - Add column/ row <br/>
Ctrl + - - Delete column / row <br/>
Alt + H + O + I - Fit to column Width <br/>
Alt + H + O + A - Fit to row Width <br/>
Alt + H + B + A - For border <br/>
Alt + H + B + N - To remove borders <br/>
$ - to look cells - $E$4 — locks Cell E4 <br/>
Alt  + H + H +N - No fill
Ctrl + Shift + L — to add or remove filters in table columns 
Ctrl + Shift + down arrow - to select data from that cell and below 
Ctrl + Shift + 4 - Apply currency formatting 

7) How to get data from another excel file in local

='[beginner-DA-course.xlsx]Data’!L12
=‘File name’TableName/SheetName!RowColumnNo:

8) Statistics Formulas

Average - AVERAGE(data[Amount]) ——  data - table name , amount - col name <br/>
Median - MEDIAN(data[Amount]) <br/>
Min - MIN(data[Amount]) <br/>
Max -MAX(data[Amount]) <br/>
UNIQUE(data[Products]) - To get distinct data in any column <br/>
COUNTA(data[Products]) - To check no: of distinct products <br/>
SUMIFS (sum range, criteria range, criteria) <br/>

9) [VLOOKUP Tutorial](https://www.youtube.com/watch?v=aJXgqNhRWMM) <BR/>
   [VLOOKUP function](https://support.microsoft.com/en-us/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1)

10) [Web scraping made easy: import HTML tables or lists using Google Sheets and Excel](https://www.thedataschool.co.uk/anna-prosvetova/web-scraping-made-easy-import-html-tables-or-lists-using-google-sheets-and-excel)
11) [DATEDIF function](https://support.microsoft.com/en-us/office/datedif-function-25dba1a4-2812-480b-84dd-8b32a451b35c)
12) [DAYS360 function](https://support.microsoft.com/en-us/office/days360-function-b9a509fd-49ef-407e-94df-0cbda5718c2a)
13) [XLOOKUP function](https://support.microsoft.com/en-us/office/xlookup-function-b7fd680e-6d10-43e6-84f9-88eae8bf5929)
14) Deleting blank Cells https://www.automateexcel.com/how-to/delete-rows-blank-cells/
15) Remove first / last Characters https://www.ablebits.com/office-addins-blog/remove-first-last-characters-excel/
16) Autofill A-Z https://www.addictivetips.com/microsoft-office/autofill-letters-from-a-z-in-excel/#:~:text=Select%20both%20and%20move%20the,also%20useful%20for%20filling%20formulas.
17) Remove characters from left and right in a string https://www.extendoffice.com/documents/excel/560-excel-remove-character-from-string.html


## References 

[Excel Functions](https://excelfind.com/excel-functions/) <br/>
[Excel Shortcuts](https://excelfind.com/excel-shortcuts/) <br/>
[Excel Video Training](https://support.microsoft.com/en-us/office/excel-video-training-9bc05390-e94c-46af-a5b3-d7c22f6990bb) <br/>
[Formulas and functions](https://support.microsoft.com/en-us/office/formulas-and-functions-294d9486-b332-48ed-b489-abe7d0f9eda9?ui=en-US&rs=en-US&ad=US#id0eaabaaa=errors) <br/>
https://www.coursera.org/learn/visualize-data/quiz/spAfZ/hands-on-activity-creating-filtering-and-customizing-charts/attempt

