# HR Attrition Analysis

## About this project
This project is about finding out why employees are leaving a company. I used the IBM HR Attrition dataset for this. The whole flow is built using Microsoft Fabric, from data upload to final dashboard.

## Tools Used
- Microsoft Fabric (Lakehouse)
- Dataflow Gen2 (for data cleaning and loading)
- Power BI (HR Semantic Model + Dashboard)
- Fabric Publishing (to publish the report online)

## How I built it
1. First, I uploaded the raw IBM HR dataset into a Lakehouse in Fabric.
2. Then I created a Dataflow Gen2 to clean the data, fix column types, and load it properly into tables.
3. After that, I built a HR Semantic Model on top of this data. Since I had only one single table (all columns like Department, JobRole, Salary Band were part of the same table), there was no need to create relationships between multiple tables. I directly used this one table to build measures and the semantic model.
4. On top of the semantic model, I created a Power BI dashboard.
5. In the end, I published the whole report on Fabric so it can be shared and viewed by others.

## Data Security (Column Level Security)
Monthly Salary is sensitive information, so I applied **CLS (Column Level Security)** on the salary column. This means normal users cannot see exact salary numbers, only people with proper access can view this data. This keeps employee salary details private and safe.

## Dashboard Pages
The dashboard has 2 pages:

**Page 1 - Overview**
This page shows the overall attrition numbers like Attrition Rate, Average Monthly Income, Average Tenure of Leavers, Employees Left, Employees Stayed and Total Headcount. It also has Attrition Rate by Department, an Attrition Decomposition tree, and tables for Attrition by Job Role and Attrition by Salary Band.

**Page 2 - Deep Dive**
This page shows attrition rate broken down by different factors: OverTime, Education Field, Gender, Marital Status, Age Group and Business Travel. This helps to understand which type of employees are leaving more.

## Why I used Table instead of Card
Normally for showing numbers like Attrition Rate or Headcount, we use Card or Matrix visuals. But in my case, Card and Matrix visuals were not working properly (they were not refreshing / showing correct values with the semantic model). So instead, I used Table visuals to show this same information. It still shows the same numbers clearly, just in table form instead of card form.

## Key Data Points
- Total Headcount: 1470
- Employees Left: 237
- Employees Stayed: 1233
- Overall Attrition Rate: 16.1%
- Average Monthly Income: 6502.9
- Average Tenure of Leavers: 5.1 years

## Problems Faced and Solutions

**Problem 1:** Card and KPI visuals were not working correctly with the semantic model data.
**Solution:** Used Table visuals instead of Cards, which displayed the correct numbers without any issue.

**Problem 2:** Salary is sensitive data and should not be visible to everyone.
**Solution:** Applied Column Level Security (CLS) on the Monthly Salary column so only authorized users can see actual salary values.

**Problem 3:** Attrition rate was different for different departments and roles, hard to find the main reason.
**Solution:** Built a Deep Dive page with multiple breakdowns (OverTime, Age Group, Marital Status, etc.) to find the exact reasons behind attrition instead of just looking at one number.

## Main Insights
- Attrition Rate is highest in Sales department (20.6%) compared to Research & Development (13.8%).
- Employees who do OverTime have a much higher attrition rate (30.5%) compared to those who don't (10.4%).
- Younger employees (18 to 25 age group) leave the most, with 35.8% attrition rate.
- Single employees have higher attrition (25.5%) compared to Married or Divorced employees.
- Employees who travel frequently for business also show higher attrition (24.9%).
- Attrition is higher in the lowest salary band (under 3k) at 28.6%, compared to higher salary bands.

## Conclusion
This dashboard helps HR team to understand which employees are at higher risk of leaving, based on department, role, salary, age and other factors. Using this, HR can take action early, like reducing overtime pressure or focusing more on younger and single employees, to reduce attrition rate.
