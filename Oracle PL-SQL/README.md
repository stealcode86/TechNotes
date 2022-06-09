1) Multiple Select in one CTE https://stackoverflow.com/questions/9682488/multiple-select-against-one-cte
2) Return value if no record is found https://stackoverflow.com/questions/8098795/return-a-value-if-no-record-is-found
3) Multiple Concat https://www.techonthenet.com/oracle/functions/concat.php

Select * from Dual 
select SYSDATE+10 from DUAL ( Today + 10 days )
Desc DUAL ( Table description )
SELECT NAME || 'AGED' || AGE from Table ( concatenation of table names )
SELECT NVL(DUMMY,0) from DUAL ( If dummy is null, it will be replaced by 0 ) --NVL - Null Value Logic
SELECT NVL2(DUMMY,26, 0) from DUAL ( If dummy is null, it will be replaced by 0 else replace it will 26 ) 
SELECT ADD_MONTHS('20-Feb-2022',7) from dual -- Adds 7 months to the date
SELECT NEXT_DAY('24-Feb-2022','Friday') from dual  -- Next Friday from 24-Feb-2022
SELECT TRUNC(some_date) from Dual -- returns the date only 
SELECT TO_CHAR (DUMMY,'dd/mm')-- to change data type from one to another
NATURAL JOIN IS similar to inner, left, right and full join ( Prefer natural over inner join, not sure why .. Natural join does the join on its own. We need not mention the columns to be joined )
CARTESIAN / CROSS JOIN is like matrix multiplication ( 2 tables with 4 rows each will produce 16 rows when cross joined )
SELF JOIN is joining the table with itself 
TRUNCATE removes all data from table but table view remains, whereas DROP removes data and table itself ( DDL ). DELETE removes all data or specific data ( DML ). TRUNCATE is faster than delete and drop.
Synonym - alternative name for an DB object ( table, view, sequence, procedure.
CURSOR - Oracle PL/SQL Cursor: Implicit, Explicit, For Loop with Example (guru99.com)
Line Number - How To Turn On Line Numbers in SQL Developer (databasestar.com)

TO_DATE(,'') - Converts char/ varchar etc. to required date type 
For concatenate and sub string  - CONCAT(SUBSTR(m.firstname, 1, 1), SUBSTR(m.surname, 1, 5))

Array.EXTEND ( Extends the internal size of the array / collection )

select * from TJURS_PRD where rownum<=100  -- Selects 100 rows 

EXCEPTION
 	WHEN NO_DATA_FOUND THEN -- Catches all no data found errors
     temp_apnt_state := FALSE;
WHEN OTHERS THEN  -- catches all the remaining exceptions
     temp_apnt_state := FALSE;
The TOO_MANY_ROWS exception is for ORA-01422 when you issue a SELECT .. INTO statement that returns more than one row. The exception you'll encounter in your case is ORA-01427, Single row subquery returns more than one row.

PL/SQL Tables and User-Defined Records (oracle.com)

LISTAGG - Oracle / PLSQL: LISTAGG Function (techonthenet.com)
REPLACE - Oracle / PLSQL: REPLACE Function (techonthenet.com)

TYPE ResponseLicDts IS REF CURSOR RETURN ResponseLicData; -- it is of ref cursor type and is returning the record
ORACLE-BASE - Using Ref Cursors To Return Recordsets
ORACLE-BASE - Complex Recordsets
DECODE function - Oracle / PLSQL: DECODE Function (techonthenet.com)
SELECT (oracle.com)


Select c.* from a,b,c inner join on a.id=b.id and b.id=c.id …… Displays all the rows of C Table.

CTE Commands
with cte( code )as  ( select distinct pers_org_unit_reltn_typ_Cd -- trandesc(pers_org_unit_reltn_typ_Cd) 
from TPERS_ORG_RELTN )
select trandesc(code),code from cte


![image](https://user-images.githubusercontent.com/49140843/172792251-8814100a-77f5-4c71-8da7-eb09c5c0d194.png)

