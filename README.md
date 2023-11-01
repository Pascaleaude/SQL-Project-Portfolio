# San Francisco Salary Analysis

## Project Overview

This data analysis projects aims to provide insights on how the government works by looking at who it employs and how the employees are compensated. By analyszing various aspects of the SF salaries data, we want to identify trends, make data driven recommendations, and get deeper understanding of bugdet salary allocations in the city of San Francisco between 2011 and 2014.

### Data Source

The primary dataset used for this analysis can be found on Kaggle. See [](https://www.kaggle.com/datasets/kaggle/sf-salaries/data)https://www.kaggle.com/datasets/kaggle/sf-salaries/data. 
I used the 'database.sqlite' version

### Tools

SQLite server

### Exploratory Data Analysis 

This involved exploring the salary data to answer key questions like:

- How has salaries changed over time between different groups?
- How are basepay, ovetimepay, and benefits allocated between different groups?
- Is there evidence of pay discrimination based on gender?
- How is budget allocated based on different groups and responsibilities?

### Data Analysis

ALTER Salaries
ADD COLUMN IncomeTreshold TEXT;

UPDATE Salaries
SET IncomeTreshold = 
CASE 
WHEN TotalPay < 100000 THEN 'LowIncome'
WHEN TotalPay >= 100000 AND TotalPay < 200000 THEN 'ModerateIncome'
WHEN TotalPay >= 200000 AND TotalPay < 300000 THEN 'HighIncome'
ELSE 'VeryHighIncome'
END;

Select Year, IncomeTreshold, AVG(TotalPay) as AvgIncome
From Salaries
GROUP BY year, IncomeTreshold
ORDER by year, IncomeTreshold;

Select JobTitle, BasePay, OvertimePay, Benefits, IncomeTreshold, Year
From SFSalaries.Salaries;

Select IncomeTreshold, SUM(BasePay) AS TotalBasePay, SUM(OvertimePay) AS TotalOvertimePay, SUM(Benefits) AS TotalBenefits
From Salaries
GROUP BY IncomeTreshold;

SELECT IncomeTreshold, COUNT(Id) AS EmployeeCount
FROM Salaries
GROUP By IncomeTreshold;

SELECT IncomeTreshold, SUM(Benefits)/ Count(Id) AS AverageBenefitsPE, SUM(BasePay)/ Count(Id) AS AverageBasePayPE, SUM(OvertimePay)/ Count(Id) AS AverageOvertimePayPE
From Salaries
GROUP BY IncomeTreshold;

SELECT JobTitle, EmployeeName, TotalPay, Benefits
FROM salaries
GROUP BY JobTitle
ORDER BY JobTitle;

SELECT JobTitle, AVG(TotalPay) AS AverageTotalPay, AVG(Benefits) AS AverageBenefits, COUNT(Id) AS EmployeeCount, AVG(TotalPay + Benefits) AS EstimatedBudgetAllocation
FROM Salaries
GROUP BY JobTitle
ORDER BY EstimatedBudgetAllocation DESC;


### Results/Findings

1. There is an overall increase in pay over time in low, moderate and high income groups. On the other hand, there is an overall decrease in pay in very high income groups over time.
2. Low income employees have the lowest base pay , overtime pay and even benefits compared to the employees in the other income groups as expected
3. Although we do not have a gender column, when the employee IDs were grouped by job title I noticed a discrepancy in salary based on genders for some job titles. For examples for firefighters
4. Sectors like public safety, health and social services were allocated a more significant amount of money than other sectors.

### Recomendations


### Limitations 

- No gender column
- 




