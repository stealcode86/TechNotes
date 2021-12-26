#TechNotes

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

F2 to edit a tab instead of starting all over again. ( fn+ F2 )
Ctrl + Z - undo, Ctrl Y - redo 
Ctrl + space bar -  Select entire column
Shift + space bar - Select entire row
Ctrl + + - Add column/ row 
Ctrl + - - Delete column / row
Alt + H + O + I - Fit to column Width
Alt + H + O + A - Fit to row Width
Alt + H + B + A - For border
Alt + H + B + N - To remove borders
$ - to look cells - $E$4 — locks Cell E4
Alt  + H + H +N - No fill
