# TechNotes

https://dev.mysql.com/doc/refman/5.7/en/alter-table.html#:~:text=1%20To%20use%20ALTER%20TABLE%2C%20you%20need%20ALTER,optional%20and%20can%20be%20omitted.%20More%20items...%20
1) Update using JOINS
update PADB.testowner.abc
set txtSAPCountryCode='IN'  FROM  PADB.testowner.abc Est 
				inner join PADB.testowner.def viw on Est.txtEstablishmentCode=viw.txtDevCentreCode
				where viw.txtEmpNo in ('912316','929800')

2) SELECT DATEADD(hh, 2, 
        DATEDIFF(dd, 0, GETDATE())) 'Date Part Only+2 hours'

i) SELECT DATEADD(dd, 2, 
        DATEDIFF(dd, 0, GETDATE())) 'Date Part Only+2 days'

3) To get Column, table name and schema in a DB
	use DBname
	SELECT COLUMN_NAME, TABLE_NAME, TABLE_SCHEMA
	FROM INFORMATION_SCHEMA.COLUMNS 
	WHERE COLUMN_NAME LIKE '%column_name%' AND TABLE_NAME LIKE '%CLX%'

4) Using where clause in UNION statement

(SELECT id, dpost FROM uid1088_qposts WHERE DATE(dpost)='2012-01-01')
UNION
(SELECT id, dpost FROM uid1091_qposts WHERE DATE(dpost)='2012-01-01')

5) If you want to check/get the list of SP’s/View’s/Function’s having a particular Table name. You can use below mentioned Query to get the complete List.

select 
   DISTINCT object.name
from 
   sysobjects Object, 
   syscomments comments 
where 
   Object.id = comments.id 
   and UPPER(text) like '%<TABLENAME>%'

6) IF EXISTS (SELECT count(*) FROM attendance.testowner.abc WHERE txtEventCode = 'PROGENSUSS' HAVING count(*) > N-1 )
BEGIN
   SET ROWCOUNT N-1 
   DELETE FROM attendance.testowner.abc WHERE txtEventCode = 'PROGENSUSS' 
   SET ROWCOUNT 0 
END

7) To convert Time to 24 hr format when given in number ( 1200 - 20:00 )
select distinct AL.intDeskID, E.intDeskCode, FORMAT(DATEADD(HH,(txtFromTime/60)%24,0),'HH:mm:ss') as txtCutOffTime, 
FORMAT(DATEADD(HH,(txtToTime/60)%24,0),'HH:mm:ss') as txtToTime

8) Select / Update ( Useful for writing where clause in kafka connector query )

update Attendance.testowner.abc set txtStatus='OS', fltOfficeHours='8' where txtEmpNo in 
( select txtEmpNo from 
( select HR.txtempno,HR.txtcompany as txtCompany, E.txtSAPCountryCode as txtSAPCountry, ats.txtstatus, ats.dtAttendance
from PADB.testowner.hr HR  WITH (NOLOCK) INNER JOIN  PADB.testowner.vie vie WITH (NOLOCK)     
on HR.txtempno=vie.txtEmpNo INNER JOIN  PADB.testowner.grn E with (Nolock)        
on vie.txtDevCentreCode=E.txtEstablishmentCode
INNER JOIN Attendance.testowner.ats ats on HR.txtEmpNo=ats.txtEmpNo where 
ats.dtLastModified>=cast ( getdate()-365 as date) and ats.txtEmpNoModifiedBy='StreamS' and ats.txtcompany='PROGEN' and txtstatus='' 
and E.txtSAPCountryCode IN ('NL','CR','AU' ) ) a )

select EmpNo,LeaveFormId,Status,FromDate,ToDate,NoOfDays,LeaveType,LeaveTypeID,CreatedOn,ModifiedOn,Country from 
( select EmpNo,LeaveFormId,Status,FromDate, ToDate,NoOfDays,LeaveType,LeaveTypeID,CreatedOn,ModifiedOn,Country 
from padb.testowner.vg (nolock) where LeaveFormId in ('26115272','388050','388052') ) a

9) Creating table with unique serial no

CREATE TABLE YourTable
(
    ID INT IDENTITY

)

10 ) Not Null constraint to tables

CREATE TABLE YourTable
(
	dtAttendance datetime not null

)

ALTER TABLE Persons
MODIFY Age int NOT NULL;

11) Alter table name, Column, column data type, add column

Alter table Stu_Table rename to Stu_Table_10

use Attendance

sp_rename 'TABLE_NAME.COLUMN_NAME','COLUMN_NAME','COLUMN';
sp_rename 'Attendance.misuser.abc.txtMonth', 'intMonth', 'column';

ALTER TABLE Attendance.misuser.abc 
ALTER COLUMN fltAmount decimal;

alter table Attendance.misuser.abc
add flgUpdate varchar(4)

12) To get int Month of the date

SELECT MONTH(CURRENT_TIMESTAMP);

SELECT DATEPART(month, CURRENT_TIMESTAMP);

13) Adding / Subtracting days, hours, minutes

Add 30 days to a date SELECT DATEADD(DD,30,cast(GETDATE() as date))
Add 3 hours to a date SELECT DATEADD(HOUR,-3,GETDATE())
Subtract 90 minutes from date SELECT DATEADD(MINUTE,-90,getdate())

14) To get number of days in current mont, previous month, next month

SELECT DAY(DATEADD(DD,-1,DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) + 1, 0)))

SELECT DAY(DATEADD(DD,-1,DATEADD(mm, DATEDIFF(mm, 0, GETDATE()), 0)))

SELECT DAY(DATEADD(DD,-1,DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) + 2, 0)))

15) Delete a Column

ALTER TABLE dbo.doc_exb DROP COLUMN column_b;

16) SELECT union XML

select (
    select id, name from (
        select id, name 
        from xmltest 
        UNION
        select id, name 
        from xmltest 
    ) A
    FOR XML PATH ('AccountDetails'), root ('Root')
) As XmlOutput

17) To get ip address and port listener in MS SQL for an instance

SELECT  
   CONNECTIONPROPERTY('net_transport') AS net_transport,
   CONNECTIONPROPERTY('protocol_type') AS protocol_type,
   CONNECTIONPROPERTY('auth_scheme') AS auth_scheme,
   CONNECTIONPROPERTY('local_net_address') AS local_net_address, -- ip address of current instance
   CONNECTIONPROPERTY('local_tcp_port') AS local_tcp_port,
   CONNECTIONPROPERTY('client_net_address') AS client_net_address 

18) To get current week Monday and Sunday 


SELECT DATEADD(wk, DATEDIFF(wk,0,GETDATE()), 0)
SELECT DATEADD(wk, DATEDIFF(wk,0,GETDATE()), 6)

19) To create CI and NCI

USE SQLShackDemo 
GO
set nocount on 
GO
DECLARE @StartTime AS DATETIME = GETDATE()
CREATE TABLE #TempWithNonClusterIndexBefore
([CountyCode] NVARCHAR(100),[RowVersion] DateTime)
CREATE NONCLUSTERED INDEX ix_tempNCIndexBef ON #TempWithNonClusterIndexBefore ([CountyCode],[RowVersion]);
INSERT INTO #TempWithNonClusterIndexBefore 
SELECT TOP 100000  * FROM [dbo].[CountryInfo] 
PRINT '#TempWithNonClusterIndexBefore'
PRINT DATEDIFF(ms,@StartTime,GETDATE())
DROP TABLE #TempWithNonClusterIndexBefore 
GO
DECLARE @StartTime AS DATETIME = GETDATE()
CREATE TABLE #TempWithNonClusterIndexAfter
([CountyCode] NVARCHAR(100),[RowVersion] DateTime)
INSERT INTO #TempWithNonClusterIndexAfter 
SELECT TOP 100000  * FROM [dbo].[CountryInfo] 
CREATE NONCLUSTERED INDEX ix_tempNCIndexAft ON #TempWithNonClusterIndexAfter ([CountyCode],[RowVersion]);
PRINT '#TempWithNonClusterIndexAfter'
PRINT DATEDIFF(ms,@StartTime,GETDATE())
DROP TABLE #TempWithNonClusterIndexAfter 
GO
DECLARE @StartTime AS DATETIME = GETDATE()
CREATE TABLE #TempWithClusterIndexBefore
([CountyCode] NVARCHAR(100),[RowVersion] DateTime)
CREATE CLUSTERED INDEX ix_tempCIndexBef ON #TempWithClusterIndexBefore ([CountyCode],[RowVersion]);
INSERT INTO #TempWithClusterIndexBefore 
SELECT TOP 100000  * FROM [dbo].[CountryInfo] 
PRINT '#TempWithClusterIndexBefore'
PRINT DATEDIFF(ms,@StartTime,GETDATE())
DROP TABLE #TempWithClusterIndexBefore
GO
DECLARE @StartTime AS DATETIME = GETDATE()
CREATE TABLE #TempWithClusterIndexAfter
([CountyCode] NVARCHAR(100),[RowVersion] DateTime)
INSERT INTO #TempWithClusterIndexAfter 
SELECT TOP 100000  CountyCode,RowVersion FROM [dbo].[CountryInfo] 
CREATE CLUSTERED INDEX ix_tempCIndexAft ON #TempWithClusterIndexAfter ([CountyCode],[RowVersion]);
PRINT '#TempWithClusterIndexAfter'
PRINT DATEDIFF(ms,@StartTime,GETDATE())
DROP TABLE #TempWithClusterIndexAfter
GO


20) To search for a column named child in PADB DB 

use PADB
SELECT Table_Name,
Column_Name
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_CATALOG = 'PADB'
AND COLUMN_NAME LIKE '%CHILD%';
	
21) To select the 3rd record from the top 10 records in a table

select top 10 * from 
( select * , ROW_NUMBER() OVER (ORDER BY txtEmpNo) as SrNo from padb.testowner.Alcontrnallocations  ) as al
where SrNo=3

22) Varchar vs Char

DECLARE @myChar CHAR(100) , @myVarchar VARCHAR(100)
SET @myChar = 'SQL'
SET @myVarchar = 'SQL'
SELECT '[BEGIN]' + @myChar + '[END]' AS CHAR_Data
SELECT '[BEGIN]' + @myVarchar + '[END]' AS VARCHAR_Data

23) While Loop 

DECLARE @Counter INT 
SET @Counter=1
WHILE ( @Counter <= 10)
BEGIN
    PRINT 'The counter value is = ' + CONVERT(VARCHAR,@Counter)
    SET @Counter  = @Counter  + 1
END

24) Break Statement 

DECLARE @Counter INT 
SET @Counter=1
WHILE ( @Counter <= 10)
BEGIN
  PRINT 'The counter value is = ' + CONVERT(VARCHAR,@Counter)
  IF @Counter >=7
  BEGIN
  BREAK
  END
    SET @Counter  = @Counter  + 1
END

25) Continue Statement

DECLARE @Counter INT 
SET @Counter=1
WHILE ( @Counter <= 20)
BEGIN
 
  IF @Counter % 2 =1
  BEGIN
  SET @Counter  = @Counter  + 1
  CONTINUE   -- This means the loop with stop here and continue the while loop from the next number and the below condition will not be executed.
  END
    PRINT 'The counter value is = ' + CONVERT(VARCHAR,@Counter)
    SET @Counter  = @Counter  + 1
END

26) Example for running while loop in printing data from a table 

GO
DROP TABLE IF EXISTS #SampleTable
CREATE TABLE #SampleTable
(Id INT, CountryName NVARCHAR(100), ReadStatus TINYINT)
GO
INSERT INTO #SampleTable ( Id, CountryName, ReadStatus)
Values (1, 'Germany', 0),
        (2, 'France', 0),
        (3, 'Italy', 0),
    (4, 'Netherlands', 0) ,
       (5, 'Poland', 0)
 
 
 
  SELECT * FROM #SampleTable

GO
 
DECLARE @Counter INT , @MaxId INT, 
        @CountryName NVARCHAR(100)
SELECT @Counter = min(Id) , @MaxId = max(Id) 
FROM #SampleTable
 
WHILE(@Counter IS NOT NULL
      AND @Counter <= @MaxId)
BEGIN
   SELECT @CountryName = CountryName
   FROM #SampleTable WHERE Id = @Counter
    
   PRINT CONVERT(VARCHAR,@Counter) + '. country name is ' + @CountryName  
   SET @Counter  = @Counter  + 1        
END

27) IF ElSE loop 

DECLARE @num1 INTEGER;
DECLARE @num2 INTEGER;
 
SET @num1 = 20;
SET @num2 = 30;
 
IF (@num1 > @num2)
  PRINT '1st number is greater than 2nd number.'
ELSE IF (@num2 > @num1)
  PRINT '2nd number is greater than 1st number.'
ELSE 
  PRINT 'The numbers are equal.';

28) INTERSECT , EXCEPT ( Use it like Union , Union All )
The INTERSECT should return elements/rows which appear in both sets.
The EXCEPT operator returns all elements/rows from the first set, except those that are in the second set.

29) User Defined Functions ( Simple one )

CREATE FUNCTION east_or_west (
	@long DECIMAL(9,6)
)
RETURNS CHAR(4) AS
BEGIN
	DECLARE @return_value CHAR(4);
	SET @return_value = 'same';
    IF (@long > 0.00) SET @return_value = 'east';
    IF (@long < 0.00) SET @return_value = 'west';
 
    RETURN @return_value
END;

The first thing we should notice, after running this command, is that our function is now visible when 
we expand “Scalar valued functions” in the “Object Explorer” (for the database where we’ve created this function).

Our function takes a number as a parameter. The return value must be of the CHAR(4) type. The initial value (variable @return_value) is initially set to ‘same’. 
If the parameter (variable @long) is greater than 0, we’re ‘east’ from London, and if it’s less than 0, we’re ‘west’ of London. Notice that, in case of @long was 0, 
none of these two Ifs will change the value, so it will hold the initial value -> ‘same’.

SELECT dbo.east_or_west(0) AS argument_0, dbo.east_or_west(-1) AS argument_minus_1, dbo.east_or_west(1) AS argument_plus_1;
O/P -- same, west, east

30) Partition By 

https://www.sqlshack.com/sql-partition-by-clause-overview/

SELECT Customercity, 
       CustomerName, 
       ROW_NUMBER() OVER(PARTITION BY Customercity
       ORDER BY OrderAmount DESC) AS "Row Number", 
       OrderAmount, 
       COUNT(OrderID) OVER(PARTITION BY Customercity) AS CountOfOrders, 
       AVG(Orderamount) OVER(PARTITION BY Customercity) AS AvgOrderAmount, 
       MIN(OrderAmount) OVER(PARTITION BY Customercity) AS MinOrderAmount, 
       SUM(Orderamount) OVER(PARTITION BY Customercity) TotalOrderAmount
FROM [dbo].[Orders];

PARTITION BY clause with Cumulative total value

In the following query, we specified ROWS clause to select the current row (using CURRENT ROW) and next row (using 1 FOLLOWING). 
It further calculates sum on those rows using sum(Orderamount) with a partition on CustomerCity ( using OVER(PARTITION BY Customercity ORDER BY OrderAmount DESC).


SELECT Customercity, 
       CustomerName, 
       OrderAmount, 
       ROW_NUMBER() OVER(PARTITION BY Customercity
       ORDER BY OrderAmount DESC) AS "Row Number", 
       CONVERT(VARCHAR(20), SUM(orderamount) OVER(PARTITION BY Customercity
       ORDER BY OrderAmount DESC ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING), 1) AS CumulativeTotal,

31) RANK() 

The RANK() function is used to give a unique rank to each record based on a specified value, for example salary, order amount etc.

If two records have the same value then the RANK() function will assign the same rank to both records by skipping the next rank. 
This means – if there are two identical values at rank 2, it will assign the same rank 2 to both records and then skip rank 3 and assign rank 4 to the next record.

SELECT order_id,order_date,customer_name,city, 
RANK() OVER(ORDER BY order_amount DESC) [Rank]
FROM [dbo].[Orders]

31) DENSE_RANK()

The DENSE_RANK() function is identical to the RANK() function except that it does not skip any rank. 
This means that if two identical records are found then DENSE_RANK() will assign the same rank to both records but not skip then skip the next rank.

SELECT order_id,order_date,customer_name,city, order_amount,
DENSE_RANK() OVER(ORDER BY order_amount DESC) [Rank]
FROM [dbo].[Orders]

32) COALESCE 

Return the first non-null value in a list.
SELECT COALESCE(NULL, NULL, NULL, 'W3Schools.com', NULL, 'Example.com');

33) Index

To create a clustered index in SQL Server, you can modify SQL CREATE INDEX. Here is the syntax:

CREATE CLUSTERED INDEX <index_name>
ON <table_name>(<column_name> ASC/DESC)

The SQL CREATE INDEX query can be modified as follows to create a non-clustered index:

CREATE NONCLUSTERED INDEX <index_name>
ON <table_name>(<column_name> ASC/DESC)

34) How to insert more than 1000 rows with hardcoded values in Sql

It’s very easy to get around this limitation by using what Microsoft refers to as a Derived Table:

DROP TABLE IF EXISTS #test;
CREATE TABLE #test(
    id integer identity(1,1) primary key,
    name varchar(48),
    etc varchar(255)
);

INSERT INTO #test(name,etc)
SELECT * FROM (     --  add this line
VALUES
    ('apple','Red round thing with a worm in it.'),
    ('banana','Long yellow thing to feed monkeys.'),
    ('cherry','Small black thing for cocktails.')
    --  thousands more rows
) AS whatever(a,b)  --  add this line
;

35) Add multiple columns to a table

Alter table #ShalitTemp 
add  fltWFHSubmitted varchar(25),
fltWFHApproved varchar(25),
fltOfficeHours varchar(25)


*-----* ---- References -----*-----* <br/>
[Learn SQL: Intro to SQL Server loops](https://www.sqlshack.com/learn-sql-intro-to-sql-server-loops/) <br/>
[How to use Window functions in SQL Server](https://www.sqlshack.com/use-window-functions-sql-server/) <br/>
[SQL Cheat Sheet](https://towardsdatascience.com/sql-cheat-sheet-776f8e3189fa) <br/>
[SQL Tuitorial](https://www.w3schools.com/sql/default.asp) 
	
