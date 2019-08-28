## Database Header
C:\Data> mysql –u <username> -p
create database

## Create Table
mysql -u <your username> -p --local-infile university
load data local infile <path to the csv file> into table <table name> fields terminated by ',' lines terminated by '\r\n';