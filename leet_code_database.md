# LeetCode Database Questions

## Combine Two Tables

### Problem:
SQL Schema
Table: Person


| Column Name | Type |
|---|---|
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |

PersonId is the primary key column for this table.


Table: Address

| Column Name | Type    |
|---|---|
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |

AddressId is the primary key column for this table.
 

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:

FirstName, LastName, City, State

### Solution
```mysql
SELECT FirstName, LastName, City, State
FROM Person
LEFT JOIN Address USING (PersonId)
```

## Employees Earning More Than Their Managers

### Problem
The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.

| Id | Name  | Salary | ManagerId |
|---|---|---|---|
| 1  | Joe   | 70000  | 3         |
| 2  | Henry | 80000  | 4         |
| 3  | Sam   | 60000  | NULL      |
| 4  | Max   | 90000  | NULL      |

Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.

| Employee |
|---|
| Joe |

### Solution

```mysql
SELECT e.Name as `Employee`
FROM Employee e
LEFT JOIN Employee e2 ON e.ManagerId = e2.Id
WHERE e.Salary > e2.Salary;
```

## Department Highest Salary

### Problem:

The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.


| Id | Name  | Salary | DepartmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |

The Department table holds all departments of the company.


| Id | Name     |
|----|----------|
| 1  | IT       |
| 2  | Sales    |

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, your SQL query should return the following rows (order of rows does not matter).


| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |

**Explanation:**

Max and Jim both have the highest salary in the IT department and Henry has the highest salary in the Sales department.

### Solution:

```mysql
SELECT d.Name Department, e.Name Employee, e.Salary Salary
FROM Employee e
JOIN Department d ON e.DepartmentId = d.Id
JOIN (
        SELECT d.Name dept_name, MAX(e.Salary) max_salary
        FROM Employee e
        JOIN Department d ON e.DepartmentId = d.Id
        GROUP BY d.Name 
    ) AS dept_max_salary
    ON dept_max_salary.dept_name = d.Name
WHERE e.Salary = dept_max_salary.max_salary