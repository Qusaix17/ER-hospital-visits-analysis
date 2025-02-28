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

## SQL query for visists by Gender

```
SELECT  FACILITY NAME, 
        LOCATION,
        COUNT(CASE WHEN GENDER = "Male" THEN 1 END) AS male,
        COUNT( CASE WHEN GENDER = "Female" THEN 1 END) AS Female,
        COUNT(GENDER) AS Total_visits_by_Gender 
FROM hospital_data
  GROUP BY FACILITY_NAME 
  ORDER BY Total_visits_by_Gender DESC
```

- ``` COUNT(CASE WHEN GENDER = "Male" THEN 1 END) AS male, ``` to count 1 everytime the case is meant, and palced in *male* column
- ``` COUNT( CASE WHEN GENDER = "Female" THEN 1 END) AS Female, ``` to count 1 everytime the case is meant, and palced in *female* column
- ``` COUNT(GENDER) AS Total_visits_by_Gender ``` aimed to sum up the total number of both females and males
- ``` GROUP BY FACILITY_NAME ``` to only include one time for each facility
- ``` ORDER BY Total_visits_by_Gender DESC ``` to list by descending order.


## SQL query to group ages into age groups by gender

```
WITH merged_ages AS (
    SELECT FACILITY_NAME,
           GENDER,
           coalesce(AGE_Y, AGE_infant) AS AGE
    FROM Hospital_data
)

SELECT FACILITY_NAME,
       GENDER,
       AGE,
       CASE
           WHEN AGE BETWEEN 1.0 AND 12.0 THEN 'Kids'
           WHEN AGE BETWEEN 13.0 AND 18.0 THEN 'Teen'
           WHEN AGE BETWEEN 19.0 AND 30.0 THEN 'Young_adults'
           WHEN AGE BETWEEN 31.0 AND 45.0 THEN 'Adults'
           WHEN AGE BETWEEN 46.0 AND 60.0 THEN 'Middle_age_adults'
           WHEN AGE BETWEEN 61.0 AND 120.0 THEN 'Elderly'
           ELSE 'Infants'
       END AS age_group
FROM merged_ages;
```
### First part (CTE)
```
WITH merged_ages AS (
    SELECT FACILITY_NAME,
           GENDER,
           coalesce(AGE_Y, AGE_infant) AS AGE
    FROM Hospital_data
```
- This part creates Common Table Expression (CTE) to merge both ages together in one column since theyre seperated into ```AGE_Y``` which are ages by year and ```AGE_INFANT``` which are ages under a year.

### Second part ( Main query )
```
SELECT FACILITY_NAME,
       GENDER,
       AGE,
       CASE
           WHEN AGE BETWEEN 1.0 AND 12.0 THEN 'Kids'
           WHEN AGE BETWEEN 13.0 AND 18.0 THEN 'Teen'
           WHEN AGE BETWEEN 19.0 AND 30.0 THEN 'Young_adults'
           WHEN AGE BETWEEN 31.0 AND 45.0 THEN 'Adults'
           WHEN AGE BETWEEN 46.0 AND 60.0 THEN 'Middle_age_adults'
           WHEN AGE BETWEEN 61.0 AND 120.0 THEN 'Elderly'
           ELSE 'Infants'
       END AS age_group
FROM merged_ages;
```
- After merging both ages into one column, ```CASE``` statement is used to group each age into a specified group
```
CASE
           WHEN AGE BETWEEN 1.0 AND 12.0 THEN 'Kids'
           WHEN AGE BETWEEN 13.0 AND 18.0 THEN 'Teen'
           WHEN AGE BETWEEN 19.0 AND 30.0 THEN 'Young_adults'
           WHEN AGE BETWEEN 31.0 AND 45.0 THEN 'Adults'
           WHEN AGE BETWEEN 46.0 AND 60.0 THEN 'Middle_age_adults'
           WHEN AGE BETWEEN 61.0 AND 120.0 THEN 'Elderly'
           ELSE 'Infants'
``` 

  

        

