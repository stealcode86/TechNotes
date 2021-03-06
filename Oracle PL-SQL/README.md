-------------------------------- References ---------------------
https://docs.oracle.com/en/database/oracle/sql-developer/18.4/rptug/sql-developer-concepts-usage.html#GUID-7BE8E4DE-B2B6-4874-B3A0-B22D7001F146

1) Multiple Select in one CTE https://stackoverflow.com/questions/9682488/multiple-select-against-one-cte
2) Return value if no record is found https://stackoverflow.com/questions/8098795/return-a-value-if-no-record-is-found
3) Multiple Concat https://www.techonthenet.com/oracle/functions/concat.php
4) Select * from Dual 
5) select SYSDATE+10 from DUAL ( Today + 10 days )
6) Desc DUAL ( Table description )
7) SELECT NAME || 'AGED' || AGE from Table ( concatenation of table names )
8) SELECT NVL(DUMMY,0) from DUAL ( If dummy is null, it will be replaced by 0 ) --NVL - Null Value Logic
9) SELECT NVL2(DUMMY,26, 0) from DUAL ( If dummy is null, it will be replaced by 0 else replace it will 26 ) 
10) SELECT ADD_MONTHS('20-Feb-2022',7) from dual -- Adds 7 months to the date
11) SELECT NEXT_DAY('24-Feb-2022','Friday') from dual  -- Next Friday from 24-Feb-2022
12) SELECT TRUNC(some_date) from Dual -- returns the date only 
13) SELECT TO_CHAR (DUMMY,'dd/mm')-- to change data type from one to another
14) NATURAL JOIN IS similar to inner, left, right and full join ( Prefer natural over inner join, not sure why .. Natural join does the join on its own. We need not mention the columns to be joined )
15) CARTESIAN / CROSS JOIN is like matrix multiplication ( 2 tables with 4 rows each will produce 16 rows when cross joined )
16) SELF JOIN is joining the table with itself 
17) TRUNCATE removes all data from table but table view remains, whereas DROP removes data and table itself ( DDL ). DELETE removes all data or specific data ( DML ). TRUNCATE is faster than delete and drop.
18) Synonym - alternative name for an DB object ( table, view, sequence, procedure.
19) CURSOR - https://www.guru99.com/pl-sql-cursor.html#:~:text=Cursor%20Attributes%20%20%20%20Cursor%20Attribute%20,returns%20the%20numerical%20value.%20It%20gives%20...%20
20) Line Number - https://www.databasestar.com/sql-developer-line-numbers/#:~:text=So%2C%20the%20first%20step%20is%20to%20go%20to,Gutter.%20The%20Show%20Line%20Numbersoption%20is%20then%20shown.

21) TO_DATE(,'') - Converts char/ varchar etc. to required date type 
22) For concatenate and sub string  - CONCAT(SUBSTR(m.firstname, 1, 1), SUBSTR(m.surname, 1, 5))

23) Array.EXTEND ( Extends the internal size of the array / collection )

24) select * from TJURS_PRD where rownum<=100  -- Selects 100 rows 

25) EXCEPTION
 	WHEN NO_DATA_FOUND THEN -- Catches all no data found errors
     temp_apnt_state := FALSE;
WHEN OTHERS THEN  -- catches all the remaining exceptions
     temp_apnt_state := FALSE;
The TOO_MANY_ROWS exception is for ORA-01422 when you issue a SELECT .. INTO statement that returns more than one row. The exception you'll encounter in your case is ORA-01427, Single row subquery returns more than one row.

26) [PL/SQL Tables and User-Defined Records (oracle.com)](https://docs.oracle.com/cd/A57673_01/DOC/server/doc/PLS23/ch4.htm?msclkid=5996aa0ea5dc11ec91c5b2fce7843b67)

27) LISTAGG - [Oracle / PLSQL: LISTAGG Function (techonthenet.com)](https://www.techonthenet.com/oracle/functions/listagg.php#:~:text=Oracle%20%2F%20PLSQL%3A%20LISTAGG%20Function%201%20Description.%20The,LISTAGG%20function%20can%20be%20used%20in%20Oracle%2FPLSQL.%20?msclkid=03ca63dda5e211ecaab3f365dd916272)
28) REPLACE - https://www.techonthenet.com/oracle/functions/replace.php?msclkid=18d28b81a5ec11ec90f002ec11f144e8

29) TYPE ResponseLicDts IS REF CURSOR RETURN ResponseLicData; -- it is of ref cursor type and is returning the record
30) ORACLE-BASE - https://oracle-base.com/articles/misc/using-ref-cursors-to-return-recordsets
31) ORACLE-BASE - [Complex Recordsets](https://oracle-base.com/articles/8i/complex-recordsets)
32) DECODE function - [Oracle / PLSQL: DECODE Function (techonthenet.com)](https://www.techonthenet.com/oracle/functions/decode.php?msclkid=0ce0b892aaa711ecb6733b325a9ec974)
33) SELECT - https://docs.oracle.com/en/database/oracle/oracle-database/12.2/sqlrf/SELECT.html#GUID-CFA006CA-6FF1-4972-821E-6996142A51C6


34) Select c.* from a,b,c inner join on a.id=b.id and b.id=c.id ?????? Displays all the rows of C Table.

35) CTE Commands
with cte( code )as  ( select distinct pers_org_unit_reltn_typ_Cd -- trandesc(pers_org_unit_reltn_typ_Cd) 
from TPERS_ORG_RELTN )
select trandesc(code),code from cte

36) Increase font size - https://www.youtube.com/watch?time_continue=36&v=10pk-fPUPpc&feature=emb_logo
37) To Rename worksheet - https://www.thatjeffsmith.com/archive/2012/08/sql-developer-trick-renaming-your-worksheets/
38) To concatenate multiple columns https://stackoverflow.com/questions/1619259/oracle-sql-concatenate-multiple-columns-add-text
39) DECODE function like IF ELSE Condition https://www.techonthenet.com/oracle/functions/decode.php?msclkid=0ce0b892aaa711ecb6733b325a9ec974
40) Select inside a FOR LOOP https://stackoverflow.com/questions/50211782/pl-sql-select-inside-loop
41) ** Return a value if no record is return in SELECT https://stackoverflow.com/questions/8098795/return-a-value-if-no-record-is-found
