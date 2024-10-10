# HR-Attrition-SQL-Analysis
This repository contains SQL queries and analysis of the HR Employee Attrition dataset. The analysis aims to explore various factors contributing to employee attrition.


![SQL](3161158.png)


## Project Overview

The purpose of this project is to clean, explore, and analyze the HR Employee Attrition dataset using SQL. By querying the data, we can identify patterns and derive insights about employee attrition.

## Dataset Description

The dataset contains the following columns:
- `Row`
- `Age`
- `Attrition`
- `BusinessTravel`
- `DailyRate`
- `Department`
- `DistanceFromHome`
- `Education`
- `EducationField`
- `EmployeeCount`
- `EmployeeNumber`
- `EnvironmentSatisfaction`
- `Gender`
- `HourlyRate`
- `JobInvolvement`
- `JobLevel`
- `JobRole`
- `JobSatisfaction`
- `MaritalStatus`
- `MonthlyIncome`
- `MonthlyRate`
- `NumCompaniesWorked`
- `Over18`
- `OverTime`
- `PercentSalaryHike`
- `PerformanceRating`
- `RelationshipSatisfaction`
- `StandardHours`
- `StockOptionLevel`
- `TotalWorkingYears`
- `TrainingTimesLastYear`
- `WorkLifeBalance`
- `YearsAtCompany`
- `YearsInCurrentRole`
- `YearsSinceLastPromotion`
- `YearsWithCurrManager`

## Example of Dataset

| Row | Age | Attrition | BusinessTravel   | DailyRate | Department           | DistanceFromHome | Education | EducationField   | Gender | JobRole | MaritalStatus | MonthlyIncome | OverTime | PerformanceRating | TotalWorkingYears | YearsAtCompany |
|-----|-----|-----------|------------------|-----------|----------------------|------------------|-----------|------------------|--------|---------|---------------|---------------|----------|-------------------|-------------------|----------------|
| 1   | 49  | false     | Travel_Rarely    | 1098      | Research & Development | 4                | 2         | Medical          | Male   | Manager | Married       | 18711         | false    | 3                 | 23                | 4              |
| 2   | 50  | false     | Travel_Rarely    | 264       | Sales                 | 9                | 3         | Marketing        | Male   | Manager | Married       | 19331         | true     | 3                 | 27                | 3              |
| 3   | 42  | false     | Travel_Rarely    | 1059      | Research & Development | 9                | 2         | Other            | Male   | Manager | Single        | 19613         | false    | 4                 | 24                | 3              |
| 4   | 58  | false     | Travel_Rarely    | 605       | Sales                 | 21               | 3         | Life Sciences    | Female | Manager | Married       | 17875         | true     | 3                 | 29                | 2              |
| 5   | 46  | false     | Travel_Rarely    | 705       | Sales                 | 2                | 4         | Marketing        | Female | Manager | Single        | 18947         | false    | 3                 | 22                | 2              |
| 6   | 44  | false     | Travel_Rarely    | 1315      | Research & Development | 3                | 4         | Other            | Male   | Manager | Married       | 19513         | true     | 3                 | 26                | 4              |
| 7   | 50  | false     | Travel_Frequently| 1421      | Research & Development | 2                | 3         | Medical          | Female | Manager | Married       | 17856         | false    | 4                 | 32                | 3              |
| 8   | 48  | false     | Travel_Frequently| 365       | Research & Development | 4                | 5         | Medical          | Male   | Manager | Married       | 15202         | false    | 4                 | 23                | 3              |
| 9   | 51  | false     | Travel_Rarely    | 942       | Research & Development | 3                | 3         | Technical Degree | Female | Manager | Married       | 13116         | false    | 3                 | 15                | 3              |
| 10  | 59  | false     | Non-Travel       | 1420      | Human Resources       | 2                | 4         | Human Resources  | Female | Manager | Married       | 18844         | false    | 4                 | 30                | 3              |
| 11  | 29  | false     | Travel_Rarely    | 900       | Research & Development | 10               | 3         | Life Sciences    | Male   | Sales   | Married       | 5000          | false    | 3                 | 10                | 7              |
| 12  | 31  | true      | Travel_Frequently| 900       | Sales                 | 20               | 2         | Marketing        | Female | Manager | Single        | 4500          | true     | 4                 | 8                 | 5              |
| 13  | 45  | false     | Travel_Rarely    | 1100      | Research & Development | 12               | 4         | Technical Degree | Female | Research Scientist | Divorced   | 12000         | false    | 3                 | 15                | 9              |
| 14  | 36  | true      | Travel_Rarely    | 850       | Sales                 | 15               | 3         | Marketing        | Male   | Sales Executive | Married   | 9000          | true     | 3                 | 7                 | 5              |
| 15  | 39  | false     | Travel_Rarely    | 950       | Research & Development | 8                | 2         | Life Sciences    | Female | Manager | Married       | 11000         | false    | 3                 | 12                | 6              |


## SQL Queries and Analysis

### Step 1: Data Cleaning

### Identifying Duplicated Employee Records by Department

In this step, I am using SQL to identify any duplicated employee records in the dataset. By grouping the data by `EmployeeNumber` and `Department`, I can locate any instances where an employee appears more than once in the same department.

```sql
SELECT 
  EmployeeNumber, 
  Department, 
  COUNT(*) AS DuplicateCount 
FROM 
  `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition2`
GROUP BY 
  EmployeeNumber, 
  Department 
HAVING 
  DuplicateCount > 1 
ORDER BY 
  DuplicateCount DESC;
```


## Step 2: Removing Irrelevant Columns

After verifying there were no duplicate records, the next step was to remove columns that do not provide meaningful insights or contribute to the analysis. The following columns were removed:

- `EmployeeCount`: This column had a constant value.
- `Over18`: Since all employees are over 18, this column does not provide any differentiating factor.
- `StandardHours`: This column had the same value for all employees.

### Updated Table Summary:
- **Number of Columns:** 33
- **Number of Rows:** 1470

By removing these columns, I ensure that my analysis focuses on the most relevant data.

save the new table as , fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3

## Step 3: Query for Summary Statistics

In this step, I used SQL to calculate some key summary statistics to better understand the dataset. These statistics include the average age of employees, the total Attrition number, and the average monthly income.

```sql
SELECT 
    AVG(Age) AS Average_Age,
    COUNT(CASE WHEN Attrition THEN 1 END) AS Total_Attrition, 
    AVG(MonthlyIncome) AS Average_Monthly_Income
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`;
```
### Summary Statistics Output

The following table presents the summary statistics obtained from the query:

| Row | Average_Age | Total_Attrition | Average_Monthly_Income |
|-----|-------------|-----------------|-------------------------|
| 1   | 36.92      | 237             | 6502.93                 |

## Step 4: Department Group wise Attrition

In this step, I performed a group-by analysis to evaluate attrition rates across different departments . The query calculates the number of employees who left the company (Attrition Count) , the total number of employees in each department, and the attrition rate for each department.

```sql
SELECT 
    Department AS Department_Name,
    COUNT(CASE WHEN Attrition THEN 1 END) AS Attrition_Count,  
    COUNT(*) AS Total_Employees,
    COUNT(CASE WHEN Attrition THEN 1 END) * 100.0 / COUNT(*) AS Attrition_Rate
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    Department;
```

the results of Attrition by Department is :

| Row | Department_Name           | Attrition_Count | Total_Employees | Attrition_Rate |
|-----|---------------------------|-----------------|-----------------|-----------------|
| 1   | Research & Development     | 133             | 961             | 13.84%          |
| 2   | Sales                      | 92              | 446             | 20.63%          |
| 3   | Human Resources            | 12              | 63              | 19.05%          |

so I noticed the highest department attrition rate was Research and department, sales and human resources 

commonly reason if there is a high attrition rate in a department is monthly income so let's check this one 

## Step 5: Average Monthly Income by Job Role

In this step, I calculated the average monthly income for each job role.

```sql
SELECT 
    JobRole,
    AVG(MonthlyIncome) AS Average_Monthly_Income
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    JobRole
ORDER BY 
    Average_Monthly_Income DESC;
```

### Average Monthly Income Output

The following table presents the average monthly income for each job role:

| Row | JobRole                     | Average_Monthly_Income |
|-----|-----------------------------|-------------------------|
| 1   | Manager                     | 17181.68                |
| 2   | Research Director            | 16033.55                |
| 3   | Healthcare Representative    | 7528.76                 |
| 4   | Manufacturing Director       | 7295.14                 |
| 5   | Sales Executive             | 6924.28                 |
| 6   | Human Resources             | 4235.75                 |
| 7   | Research Scientist           | 3239.97                 |
| 8   | Laboratory Technician       | 3237.17                 |
| 9   | Sales Representative         | 2626.00                 |

so i noticed the juniors on the sales department or sales representative, and also in the research departments have one of lowest monthly incomes in the organization, this may mean it can be a reason for high attrition 

## Step 6: Attrition Rates by Income Level

 to make sure and to check the attrition rate for all roles i will check the Attrition Rates by Income Level 

 ```sql
SELECT 
    CASE 
        WHEN MonthlyIncome < 4000 THEN 'Low Income'
        WHEN MonthlyIncome BETWEEN 4000 AND 7000 THEN 'Medium Income'
        ELSE 'High Income'
    END AS Income_Bracket,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition THEN 1 ELSE 0 END) AS Attrition_Count,
    (SUM(CASE WHEN Attrition THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS Attrition_Rate
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    Income_Bracket;

```
### Attrition Rates Output by Income 

| Income         | Total Employees | Attrition Count | Attrition Rate (%) |
|----------------|-----------------|------------------|---------------------|
| High Income    | 435             | 47               | 10.80               |
| Low Income     | 542             | 137              | 25.28               |
| Medium Income  | 493             | 53               | 10.75               |

### Insights

- **Low Income :** You may notice a higher attrition rate, increase with lower-paid employees.

- **Medium Income :** have moderate attrition rate.

- **High Income :** have low attrition rate.

## Step 7: Average Monthly Income by Education Level

this analysis to understand how the company deals with highly level of educated employees and highly skilled workers to make sure everyone is comforted to lower the attrition rate.

```sql
SELECT 
    Education,
    AVG(MonthlyIncome) AS Average_Monthly_Income
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    Education
ORDER BY 
    Average_Monthly_Income DESC;

```

### Average Monthly Income Output by Education Level

| Education | Average Monthly Income |
|-----------|-----------------------|
| 5         | 8277.65               |
| 4         | 6832.40               |
| 3         | 6517.26               |
| 2         | 6226.65               |
| 1         | 5640.57               |

So higher Education Levels Correspond to Higher Income Education Level 5 (representing advanced degrees such as Master's or PhD) It highlights organization value higher education in its hiring and promotion processes.

but The average income for those with Education Level 1 is significantly lower compared to higher levels ,This gap could raise concerns about equity,  particularly if the roles filled by these employees require significant responsibility or skill. It may be beneficial to explore whether these employees are adequately supported through training or the packages.

## Step 8: Attrition Rates by Job Level

This analysis examines if employees are more likely to leave the organization based on their job level.

```sql
SELECT 
    JobLevel,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = TRUE THEN 1 ELSE 0 END) AS Attrition_Count,
    (SUM(CASE WHEN Attrition = TRUE THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS Attrition_Rate
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    JobLevel
ORDER BY 
    JobLevel;


```

### Attrition Rates Output by Job Level

| Job Level | Total Employees | Attrition Count | Attrition Rate (%) |
|-----------|----------------|------------------|---------------------|
| 1         | 543            | 143              | 26.34               |
| 2         | 534            | 52               | 9.74                |
| 3         | 218            | 32               | 14.68               |
| 4         | 106            | 5                | 4.72                |
| 5         | 69             | 5                | 7.25                |


### For Attrition by Job Level:
High Attrition for Entry-Level Jobs: Job Level 1 has the highest attrition rate at 26.34%, meaning many entry-level employees leave. This might be due to dissatisfaction, limited growth opportunities, or better job offers elsewhere.

Moderate Attrition for Mid-Level Jobs: Job Levels 2 and 3 have lower attrition rates (9.74% and 14.68%, respectively). While mid-level employees leave less often, there is still a notable turnover, especially at Job Level 3.

Low Attrition for Senior Jobs: Job Levels 4 and 5 have the lowest attrition rates at 4.72% and 7.25%, suggesting that senior employees feel more secure and satisfied in their positions.

## Step 9: Attrition Rate by Gender

This query assesses if there are gender differences in attrition rates.

```sql
SELECT 
    Gender,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = True THEN 1 ELSE 0 END) AS Attrition_Count,
    (SUM(CASE WHEN Attrition = True THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS Attrition_Rate
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    Gender
ORDER BY 
    Attrition_Rate DESC;

```
### Attrition Rates Output by Gender


| Row | Gender | Total Employees | Attrition Count | Attrition Rate (%) |
|-----|--------|-----------------|------------------|---------------------|
| 1   | Male   | 882             | 150              | 17.01               |
| 2   | Female | 588             | 87               | 14.80               |

### For Attrition by Gender 

The attrition rate for males (17.01%) is only about 2.21 percentage points higher than that of females (14.80%). While this may seem small, it could still indicate different experiences or challenges faced by male employees. Even slight differences can have meaningful implications.


## Step 10: Attrition Rate by OverTime Status
This analysis explores whether employees who work overtime have different attrition rates compared to those who do not

```sql
SELECT 
    OverTime,
    COUNT(*) AS Total_Employees,
    SUM(CASE WHEN Attrition = True THEN 1 ELSE 0 END) AS Attrition_Count,
    (SUM(CASE WHEN Attrition = True THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS Attrition_Rate
FROM 
    `fair-yew-429113-a4.HR_Analytics.HR-Employee-Attrition3`
GROUP BY 
    OverTime
ORDER BY 
    Attrition_Rate DESC;
```
### Attrition Rates Output by OverTime Status

| Row | OverTime | Total Employees | Attrition Count | Attrition Rate (%) |
|-----|----------|-----------------|------------------|---------------------|
| 1   | True     | 416             | 127              | 30.53               |
| 2   | False    | 1054            | 110              | 10.44               |

### For Attrition by OverTime Status

#### Higher Attrition Rate for Overtime Workers
Employees who work overtime have an attrition rate of 30.53%, which is higher than the 10.44% attrition rate for those who do not work overtime.
This indicates that employees who put in extra hours may be more likely to leave the organization.

There are 416 employees who worked overtime, with 127 of them leaving, compared to 1,054 employees who did not work overtime, of whom 110 left.

Work-Life Balance Concerns:
The high attrition rate among employees who work overtime may suggest that they experience greater work-life balance issues, leading to burnout or dissatisfaction.
This is a critical area for organizations to address to retain talent.


## Conclusion

**●** Objective Achieved: The analysis successfully explored various factors contributing to employee attrition within the HR Employee Attrition dataset.

**●** Data Cleaning: Irrelevant columns were identified and removed, enhancing the dataset's clarity and focus for analysis.

**●** Attrition Insights: A total of 237 employees were identified as having left the organization, with an overall attrition rate of approximately 16.1%.

**●** Department Analysis: The highest attrition rates were observed in the Sales department (20.63%) and Research & Development (13.84%), indicating potential areas of concern for employee retention strategies.

**●** Income Correlation: There is a clear correlation between income levels and attrition rates:

Low Income: Employees with low incomes experienced the highest attrition rate of 25.28%.
Medium Income: This group had a moderate attrition rate of 10.75%.
High Income: Employees with high incomes had the lowest attrition rate at 10.80%.

**●** Job Role Impact: Job roles with lower average monthly incomes, particularly in sales and research departments, are associated with higher attrition rates, suggesting that compensation may be a significant factor influencing employees' decisions to leave.

**●** Actionable Recommendations: The findings suggest that improving compensation packages, especially for lower-paid roles, and addressing departmental challenges may enhance employee retention.

**●** Future Analysis: Further analysis is recommended to investigate other factors influencing attrition, such as work-life balance, and career advancement opportunities.

### Tableau Visualizations
I have presented all the findings through **Tableau visualizations**, offering a clearer view of the trends and insights drawn from the dataset. 
You can explore my **visualization work** on [GitHub](https://github.com/Israa-Idris/HR-Attrition-Tableau-Dashboard-Analysis) for more details.

If anyone wants to see the references, I have included the following resources:

- The Excel file can be found [here](HR-Employee-Attrition.csv).
- The dataset is sourced from Kaggle and can be accessed [here](https://www.kaggle.com/datasets/itssuru/hr-employee-attrition).

Feel free to ask about anything!
