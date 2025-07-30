# Department Highest Salary

Return the highest salary for each departments, return duplicates if multiple people have the top salary 

```SQL
# Write your MySQL query statement below
SELECT d.name AS Department, e.name AS Employee, e.salary AS Salary
FROM Employee e
JOIN Department d ON e.departmentId = d.id
JOIN (
    -- #this is creating a shadowed table that we can 
    -- #refer to on the outside with the letter m
    -- #all we are doing here is just grabbing
    -- #dept ID's and then the max salary from those ID's
    -- #and then grouping then by dept it
    -- #so we end up with somehting like 90000 = id 1
    SELECT departmentId, MAX(salary) AS max_salary
    FROM Employee
    GROUP BY departmentId
-- then outside we just have naother join
-- and we want to join where the dept ID matches
-- and the salary value matches the max
-- we can alias the shadowed table with char m 
-- and ref its values as needed
-- again just ensure that 1. dept ID matches 2. match on same salary
) m ON e.departmentId = m.departmentId AND e.salary = m.max_salary

```

Notes: This problem requires us to shadow another table and to find the max salary and then join again to find the proper max salaries rather than just joining on a single table. 
