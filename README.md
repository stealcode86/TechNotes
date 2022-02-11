# Tech Notes

1) [VLOOKUP](https://support.google.com/docs/answer/3093318?hl=en) VLOOKUP can return data only from the right and not in the left. For Eg: A:F.. can return values only from B:F
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


*--*--* References *--*--*

[Google Sheets training and help](https://support.google.com/a/users/answer/9282959?visit_id=637361702049227170-1815413770&rd=1) <br/>
[Google Sheets cheat sheet](https://support.google.com/a/users/answer/9300022)
