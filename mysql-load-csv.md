# MYSQL - Load data from external CSV file to a Table

* Steps to load data in CSV file to a MYSQL Table
* **Check Server Parameter Settings**
```
SHOW VARIABLES LIKE "%version%";
SET GLOBAL local_infile = "ON";

SHOW VARIABLES LIKE 'local_infile';
SHOW VARIABLES LIKE "secure_file_priv";

-- ADD secure_file_priv LOCATION to the my.ini or my.cfg file
[mysqld]
secure_file_priv="c:/my_folder/"

Restart DB Server
```

After DB Restart, Run the following command in SQL WorkBench to make sure your CSV File Path is set
```
SHOW VARIABLES LIKE "secure_file_priv";
```



* **STEP 1.** Create the table
```sql
-- Create Database
-- -----------------------------------------------------------------------------
create database csv_test;

use datebase csv_test;

-- Create a Test Table with various DataTypes
-- -----------------------------------------------------------------------------
create table csv_load_test (
    id              int            not null
   ,string_data     varchar(255)   not null
   ,text_data       text           null
   ,decimal_data    decimal(10,2)  null
   ,date_data       date           null
   ,datetime_data   datetime       null
   ,primary key (id)
);
```


* **STEP 2.** Prepare the CSV file to load
* Save the below contents to `load_test.csv` file and place it in a directory,
  Here we save the file to c:\tinitiate\data\load_test.csv
```
1,'AAA','This is AAA',100.2,'01-01-2020','01-01-2020 16:20:23'
2,'BBB','This is BBB',100.2,'01-01-2020','01-01-2020 16:20:23'
3,'CCC','This is CCC',100.2,'01-01-2020','01-01-2020 16:20:23'
```


* **STEP 3.** Prepare the Load Data Statement from CSV file
* We specify the CSV file and its folder, make sure to have the same name.
* Run the following command in COMMAND PROMPT / Terminal, **DO NOT RUN IN SQL WORKBENCH**
```sql
load data local infile 'E:/code/CODING_DataAnalyst/data.csv' into table csv_load_test 
fields terminated by ',' enclosed by "'" lines terminated by '\r\n'
(id, string_data, text_data, decimal_data, @date_data, @datetime_data)
SET date_data = STR_TO_DATE(@date_data, '%m-%d-%Y'),
    datetime_data = STR_TO_DATE(@datetime_data, '%m-%d-%Y %H:%i:%s');
    
show warnings;
```


* **STEP 4.** Run the Load Data Statement
* Check the Table for data
```sql
select * from csv_load_test;
```

