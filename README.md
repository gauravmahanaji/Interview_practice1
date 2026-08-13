# Interview_practice1
-- “A window function in SQL is used to perform calculations across a set of related rows without reducing the number of rows in the result. It allows us to compare a row with other rows and calculate things like ranking, running totals, and averages.
create database window_function;
use window_function;
drop table employee;
create table employees (
name varchar(50) ,
department varchar(50),
salary decimal(10,2)
); 
create table salesdata (
month varchar(50),
sales int 
);
insert into employees values ('suhani''hr',55000);
insert into salesdata values ('april',18000);
select * from employees;
select * from salesdata;
SET SQL_SAFE_UPDATES = 0;
update employees set salary = 70000 where name = 'rohit';
select name,salary ,department, sum(salary) over() from employees;
select name ,department, salary, sum(salary) over(partition by department)as deptotal from employees;
select name,salary, row_number() over( order by salary desc ) as row_num from employees;
select name ,department,salary , row_number() over(partition by department order by salary desc ) as totalsalry from employees ;
select name ,department ,salary ,dense_rank() over( order by salary desc) from employees; 
select month,sales ,lag(sales) over(order by month) as previoussales from salesdata;
select month,sales ,lead(sales) over(order by month) as nextsales from salesdata;
