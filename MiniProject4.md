## 1. Find the names of all employees who live in the same city and on the same street as do their managers
use company;  
select e.person_name, m.manager_name, street, city from employee e inner join manages m on e.person_name = m.person_name   
where (m.manager_name, street, city) in 
(select distinct m.manager_name, street, city from manages m inner join employee e on m.manager_name = e.person_name);

## 2. Find the names of all employees in this database who do not work for First Bank Corporation.
select person_name from works where company_name not like 'FBC%';


## 3. Find the names of all employees who earn more than every employee of Small Bank Corporation.

select person_name from works where salary > (select max(salary) from works where company_name = 'Small Bank Corporation');

## 4. Assume the companies may be located in several cities. Find all companies located in every city in which Small Bank Corporation is located.

select company_name from company where city in (select city from company where company_name = 'Small Bank Corporation');
