# TechNotes

1) To get all tables in a DB

SELECT * FROM pg_catalog.pg_tables
WHERE schemaname != 'information_schema' AND
schemaname != 'pg_catalog';

2) To get top 5 rows from a table

SELECT * FROM testowner.attmstsysparams limit 5;

3) List 10 largest tables in postgres DB

select schemaname as table_schema,
    relname as table_name,
    pg_size_pretty(pg_total_relation_size(relid)) as total_size,
    pg_size_pretty(pg_relation_size(relid)) as data_size,
    pg_size_pretty(pg_total_relation_size(relid) - pg_relation_size(relid))
      as external_size
from pg_catalog.pg_statio_user_tables
order by pg_total_relation_size(relid) desc,
         pg_relation_size(relid) desc
limit 10;

4) To reduce 5 days from a given date/ time 

SELECT * FROM misuser.abc nolock
	
WHere Cast(dtAttendance as Date) >= Cast(now() - INTERVAL '5 DAY' AS Date)
