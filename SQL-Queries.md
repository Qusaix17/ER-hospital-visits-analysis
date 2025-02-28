# SQL queries for ER visits 


## This query sum total visits for each hospital by the Year.

```
SELECT
  FACILITY_NAME,
    COUNT(CASE WHEN VISIT_DATE LIRE '%-20' THEN 1 END) AS visits_2020,
    COUNT(CASE WHEN VISIT_DATE LIRE '%-21' THEN 1 END) AS visits_2021,
    COUNT(CASE WHEN VISIT_DATE LIRE '%-22' THEN 1 END) AS visits_2022,
    COUNT(CASE WHEN VISIT_DATE LIRE '%-23' THEN 1 END) AS visits_2023

FROM Hospital data
GROUP BY FACILITY NAME;
```

- ```CASE``` statement returns 1 if the condition is meant.
- Condition is when ```VISIT_DATE``` ends with the respective year ( '-20' for 2020, '-21' for 2021...etc).
- All results are counted by ```COUNT()``` statement for each year and is returned in a specified column.
- ```GROUP BY``` statement so the results are grouped by the names of the facilities.

I had the visiters all together with dates scattered all over the Dataset, so i made this query to organize and sum each visits by the year.

## SQL query to calculate total number of revisits per hospital

```
SELECT DISTINCT FACILITY_NAME,           -- start main query
        SUM(re_visits) AS Total_revisits
  FROM (SELECT
          FACILITY_NAME                 -- start first subquery
          re_visits,
          AGE Y,
          AGE infant,
          VISIT_DATE
        FROM (SELECT                   -- start second subquery
                SERIAL_NO,
                VISIT_DATE
                COUNT(*) AS revisits,
                FACILITY_NAME,
                AGE Y,
                AGE infant
        FROM hospital data
        GROUP BY SERIAL_NO, FACILITY_NAME, AGE_Y, AGE_INFANT
        HAVING COUNT (*) > 1
        AS subquery
        GROUP BY FACILITY_NAME         -- end main query
```

### Main Query 
- ``` SELECT DISTINCT FACILITY_NAME ``` so each facility only apear once at teh result
- ``` SUM(re_visits) AS Total_revisits ``` To sum the total number of revisit for each facility
- ``` FROM ``` retrieves all data from the subquery
- ```GROUP BY``` statement so the results are grouped by the names of the facilities.

### First Subquery 
```
SELECT                    -- start first subquery
          FACILITY_NAME
          re_visits,
          AGE Y,
          AGE infant,
          VISIT_DATE
        FROM ( second quey )
```

- This is set to extract relevant columns from the second subquery.


  ### Second subquery
```
SELECT                   -- start second subquery
                SERIAL_NO,
                VISIT_DATE
                COUNT(*) AS revisits,
                FACILITY_NAME,
                AGE Y,
                AGE infant
        FROM hospital data
        GROUP BY SERIAL_NO, FACILITY_NAME, AGE_Y, AGE_INFANT
        HAVING COUNT (*) > 1
```

- ``` COUNT(*) AS revisits``` to count each visit as 1.
- ``` HAVING COUNT (*) > 1``` filters only the patients who have more than 1 visit.

Patients revisist count was possible since each patient is assigned a serial number, which used to identify any revisits.

## 


  

        

