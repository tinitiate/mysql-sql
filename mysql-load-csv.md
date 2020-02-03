# MYSQL - Load data from external CSV file to a Table

* Here we create a table with various datatypes

```sql
-- Create Database
-- -----------------------------------------------------------------------------
create database csv_test;


-- Create a Test Table with various DataTypes
-- -----------------------------------------------------------------------------
create table csv_load_test (
    id              int            not null
   ,string_data     varchar(255)   not null
   ,text_data       text           null
   ,decimal_data    decimal(10,2)  null
   ,date_data       date           null
   ,datetime_data   datetime       null
   ,timestamp_data  timestamp      null
   ,primary key (id)
);


* CSV file to load
* Save the below contents to  `load_test.csv` file and place it in a directory.
```
1,'AAA','This is AAA',100.2,'01-01-2020','01-01-2020 16:20:23','01-01-2020 16:20:23 GMT'
2,'BBB','This is BBB',100.2,'01-01-2020','01-01-2020 16:20:23','01-01-2020 16:20:23 IST'
3,'CCC','This is CCC',100.2,'01-01-2020','01-01-2020 16:20:23','01-01-2020 16:20:23 EST'
```


* Load Data Statement from CSV file
```sql
load data infile 'c:/data/load_test.csv' into table csv_load_test
fields terminated by ',' enclosed by "'" lines terminated by '\n'
ignore 1 rows;
(id, string_data, text_data, decimal_data, @date_data, @datetime_data, @timestamp_data)
SET date_data = STR_TO_DATE(@date_data, '%m-%d-%Y');
SET datetime_data = STR_TO_DATE(@datetime_data, '%m-%d-%Y %h:%i%:s%');
SET timestamp_data = unix_timestamp(STR_TO_DATE(@timestamp_data, '%m-%d-%Y %h:%i%:s% GMT'));
```


* Run the Load Data Statement
* Check the Table for data
```sql
select * from csv_load_test;
```

