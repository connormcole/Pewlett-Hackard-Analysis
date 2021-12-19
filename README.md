# Pewlett-Hackard-Analysis

## Overview
The purpose of this analysis was to determine which employees were retiring soon from Pewlett Hackard, as well as who would be eligible to participate in the mentorship program.

## Results
- A significant number of employees are retiring from most title categories
- Only two managers are retiring
- The category with the highest number of retirees, Senior Engineer, will be the most difficult to fill since Engineers will have to be promoted, and their replacements trained 

![retiring_titles](https://user-images.githubusercontent.com/92554586/146694121-94bc275d-f2da-4d15-a1e7-47551546ccb9.png)

- 1,549 employees are eligible for the mentorship program

![mentorship_eligibility](https://user-images.githubusercontent.com/92554586/146694431-f1cc746d-9aa5-4cba-aae2-37809cc71ce7.png)

## Summary
90,398 employees will need to be replaced as a reult of the "silver tsunami." There are not enough employees from the mentorship program to train the next wave of employees.
To rectify this, the birthdate range could be expanded when determining eligibility for the program. Instead of only having employees born in 1965, the line in the query 
could be: AND e.birth_date BETWEEN '1960-01-01' AND '1965-12-31'. Another helpful query could be adding a salary column to the retiring titles table, that way the company
would know how much personnel expense they had to work with in filling the new roles. You would just need to add the salary column in the select statement, and left join
the salaries table onto the retirement_titles table:

SELECT e.emp_no, 
	e.first_name, 
	e.last_name,
	t.title,
	t.from_date,
	t.to_date,
  s.salary
INTO retirement_titles
FROM employees as e
-- Step 4
  LEFT JOIN titles as t
    ON e.emp_no = t.emp_no
  LEFT JOIN salaries as s
    ON t.emp_no = s.emp_no
-- Step 5
WHERE e.birth_date BETWEEN '1952-01-01' AND '1955-12-31'
ORDER BY e.emp_no;
