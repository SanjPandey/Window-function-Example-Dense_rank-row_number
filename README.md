select * from employees;

--Fourth Rank
select * from (
select first_name,
last_name,
salary ,
DENSE_RANK() over(order by salary desc) forth_rank from employees)
where forth_rank=3;

--record 25th 26th

select * from(
select first_name,salary,
row_number() over(order by salary desc) rank_bet_1st_to_11 
from employees)
where rank_bet_1st_to_11 in(25,26


--first highest salary and lowest salary

select * from (
select first_name,last_name,salary,
row_number()over(order by salary desc) highest_salary
from employees)
where highest_salary=1
union
select * from(
select first_name,last_name,salary,
row_number() over(order by salary) lowest_salary
from employees)
where lowest_salary=1;


--first highest salary and lowest salary
--or

with cte1 as 
(select * from employees order by salary fetch first row only),
cte2 as 
(
select * from employees order by salary desc fetch first row only)
select * from cte1 union select * from cte2;

--salary of each department

select employee_id,
first_name,
last_name,
salary,
department_id,
dense_rank() over(partition by department_id order by salary desc) salary from employees;

--first highest salary of each department
select * from(
select employee_id,
first_name,
last_name,
salary,
department_id,
dense_rank() over(partition by department_id order by salary desc) highest_sal from employees)
where highest_sal=1





