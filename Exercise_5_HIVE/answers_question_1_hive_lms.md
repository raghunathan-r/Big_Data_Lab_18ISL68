## Creating a Database and a Table

show databases;

create database if not exists salesdb;

use salesdb;

create table sales (product string, price int, payment_type string, name string, city string, state string, country string);

## Q1. Insert 5 records using Insert command in HiveQL

create table sales (product string, price int, payment_type string, name string, city string, state string, country string)
row format delimited 
fields terminated by "," ;

insert into sales values ("product1", 1200, "mastercard", "carolina", "basildon", "england", "united kingdom");

Product1	1200	Mastercard	carolina	Basildon	England	United Kingdom
Product1	1200	Visa	Betina	Parkville	MO	United States
Product1	1200	Mastercard	Federica e Andrea	Astoria	OR	United States
Product1	1200	Visa	Gouya	Echuca	Victoria	Australia

## Q2. Import the dataset from the csv file
load data local inpath '/home/hadoop_user/Downloads/sales.csv' into table sales;

## Q3. Count the number of sales done by each country
select country, count(country) from sales group by country;

## Q4. Count the number of sales done by each state
select state, count(state) from sales group by state;

## Q5. Display (Product, name) grouped by product
select product, name from sales group by product;

## Q6. Create separate views for VISA and Mastercard
create view visa as select * from sales where payment_type = "visa";
select * from visa;

create view mastercard as select * from sales where payment_type = "Mastercard";
select * from mastercard;

## Q7. Show all the transactions done in Seattle
select * from sales where city = "Seattle";

## Q8. Find the max number of transactions done within the state of Ontario
select max(*) from sales group by city where state = "Ontario";
select max(count(*)) from sales where state = "Ontario" group by city;
select city, count(*) from sales where state = "Ontario" group by city;
select max(count(*)) from sales group by city where state = "Ontario";
select city, count(*) from sales where state = "Ontario" group by city;


## Q9. Find the number of transactions whose price is in between 1500-3600
select count(*) from sales where price between 15000 and 36000;

## Q10. List all the transactions done in the United States using Mastercard
select * from sales where country = "United States" and payment_type = "Mastercard";

# SEE Practice questions

## Q5.a. Create the following tables
    Bank(Bank_id:integer, Bname: string, blocation:string)
    Customer(Cust_id: integer, Cname: string, income:float, accid:int dob:date)
    Account(accid int, cust_id: int,bnk_id: int);

create table customer (cust_id integer, cname string, income float, accid int, dob date)
row format delimited 
fields terminated by ",";

load data local inpath "/file.csv" into table customer;

create table account(accid integer, cust_id integer, bnk_id integer);
