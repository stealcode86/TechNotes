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

3) SELECT COLUMN_NAME, TABLE_NAME, TABLE_SCHEMA
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
