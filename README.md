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
