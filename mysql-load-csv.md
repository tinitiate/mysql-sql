# MYSQL - Load data from external CSV file to a Table

* Here we create a table with various datatypes

```sql
-- Create a Test Table with various DataTypes
-- -----------------------------------------------------------------------------
create table csv_load_test (
    id              int            not null
   ,string_data     varchar(255)   not null
   ,text_data       text           null
   ,decimal_data    decimal(10,2)  null,
   ,date_data       date           null,
   ,datetime_data   date           null,
   ,timestamp_data  date           null,
   ,primary key (id)
);

```

* Load Data from CSV file
```
load data infile 'c:/data/load_test.csv' into table csv_load_test
fields terminated by ',' enclosed by "'" lines terminated by '\n'
ignore 1 rows;
(id, string_data, text_data, decimal_data, @date_data, @datetime_data, @timestamp_data)
SET date_data = STR_TO_DATE(@date_data, '%m/%d/%Y');
SET datetime_data = STR_TO_DATE(@datetime_data, '%m/%d/%Y');
SET timestamp_data = STR_TO_DATE(@timestamp_data, '%m/%d/%Y');
```
