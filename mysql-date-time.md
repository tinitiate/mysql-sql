---
YamlDesc: CONTENT-ARTICLE
Title: MySQL Date and Time
MetaDescription: MySQL, Date, DateTime, TimeStamp
MetaKeywords: MySQL, Date, DateTime, TimeStamp
Author: (c) Venkata Bhattaram / www.github.com/tinitiate
Contact: **syntaxboard@gmail.com**
ContentName: mysql-date-time
---

# MySQL Date, DateTime and TimeStamp
* Format and Its description
```sql
%Y      YYYY        4-digit year
%y      YY          2-digit year
%b      MON         Abbreviated month (Jan - Dec)
%M      MONTH       Month name (January - December)
%m      MM          Month (1 - 12)
%a      DY          Abbreviated day (Sun - Sat)
%d      DD          Day (1 - 31)
%H      HH24        Hour (0 - 23)
%h      HH / HH12   Hour (1 - 12)
%i      MI          Minutes (0 - 59)
%s      SS          Seconds (0 - 59)
```


## Create Test data
* Create Date Data Table
```sql
-- Create Table
-- -----------------------------------------------------------------------------
create table date_time_test (
    ,col_ts   timestamp
    ,col_dt   datetime
    ,col_date date
);

-- Insert Date Data
-- -----------------------------------------------------------------------------

-- Insert Current TimeStamp, Current DateTime, Current Date
insert into date_time_test values (current_timestamp(), now(), curdate());

-- Insert using String to Date /  DateTime / TimeStamp functions
insert into date_time_test values
   ( unix_timestamp(str_to_date('2020-01-01 01:10pm', '%Y-%m-%d %h:%i%p'))  -- TimeStamp
    ,str_to_date('2020-01-01 01:10pm', '%Y-%m-%d %h:%i%p')                  -- DateTime
    ,str_to_date('01-01-2020','%d-%m-%Y'));                                 -- Date

-- -----------------------------------------------------------------------------
```

* Select Data from Date Table
```sql
select   hour(col_dt)
        ,minute(col_dt)
        ,second(col_dt)
        ,day(col_dt)
        ,week(col_dt)
        ,month(col_dt)
        ,quarter(col_dt)
        ,year(col_dt)
from    date_time_test;

```

* **ADDDATE**
```sql
-- Add 15 Seconds
SELECT ADDDATE("2020-01-01 01:00:00", INTERVAL 15 SECOND);

-- Subtract 2 Months
SELECT ADDDATE("2020-01-01 01:00:00", INTERVAL -2 MONTH);

-- INTERVAL TYPES
-- -----------------------
    -- MICROSECOND
    -- SECOND
    -- MINUTE
    -- HOUR
    -- DAY
    -- WEEK
    -- MONTH
    -- QUARTER
    -- YEAR
    -- SECOND_MICROSECOND
    -- MINUTE_MICROSECOND
    -- MINUTE_SECOND
    -- HOUR_MICROSECOND
    -- HOUR_SECOND
    -- HOUR_MINUTE
    -- DAY_MICROSECOND
    -- DAY_SECOND
    -- DAY_MINUTE
    -- DAY_HOUR
    -- YEAR_MONTH
```

* DATEDIFF() function returns the number of days between two date values.
```sql
SELECT DATEDIFF("2020-01-01 01:00:00", "2020-01-01 00:30:00");

SELECT DATEDIFF("2020-02-01 01:00:00", "2020-01-01 01:00:00");
```

* TIMEDIFF() Returns the difference between two time expressions.
```sql
SELECT TIMEDIFF("15:10:10", "10:10:10");

SELECT TIMEDIFF("11:30:00", "09:10:10");
```




