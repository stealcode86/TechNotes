# Tech Notes

1) [VLOOKUP](https://support.google.com/docs/answer/3093318?hl=en) 
2) [DATEDIF](https://support.google.com/docs/answer/6055612?hl=en)
3) Sorting using the function 
=SORT(A2:D6, 2, TRUE) 
4) To convert data using the CONVERT function
  =CONVERT(B2,"F","C") --converting from Farenheit to Celsius
  =CONVERT(D2,"mph","m/s") -- converting from Miles per hour to Metres per second
5) To join more than 2 strings
  =CONCATENATE(A3," ",B3)
6) String functions
 =LEN()
 =LEFT(,)
 =RIGHT(,)
 =FIND(,,)
 7) Value function 
  The VALUE function converts the text string to a numerical value.
=VALUE()
8) IFNA function is to replace the #N/A error with something more descriptive, like “Does not exist.”
IFNA(value, value_if_NA)
9) To generate sequence of number/ dates etc https://www.makeuseof.com/use-sequence-function-google-sheets/
10) To generate sequence of working days https://infoinspired.com/google-docs/spreadsheet/how-to-populate-sequential-dates-excluding-weekends-in-google-sheets/#:~:text=To%20autofill%20weekdays%20skipping%20weekends,formula%20will%20take%20care%20of!
*--*--* References *--*--*

[Google Sheets training and help](https://support.google.com/a/users/answer/9282959?visit_id=637361702049227170-1815413770&rd=1) <br/>
[Google Sheets cheat sheet](https://support.google.com/a/users/answer/9300022)
https://www.coursera.org/learn/visualize-data/quiz/spAfZ/hands-on-activity-creating-filtering-and-customizing-charts/attempt


=============()======== Notes =======()===============
1) VLOOKUP can return data only from the right and not in the left. For Eg: A:F.. can return values only from B:F. Also it returns the first match value. So if we mention TRUE in the conditions, we might get the first data that is the closest match to the data we are looking up and might not get the actually data. Hence it is preferred to use FALSE. You want the column that matches the search key in a VLOOKUP formula to be on the left side of the data. VLOOKUP only looks at data to the right after a match is found. In other words, the index for VLOOKUP indicates columns to the right only. This may require you to move columns around before you use VLOOKUP.
After you have populated data with the VLOOKUP formula, you may copy and paste the data as values only to remove the formulas so you can manipulate the data again. 
