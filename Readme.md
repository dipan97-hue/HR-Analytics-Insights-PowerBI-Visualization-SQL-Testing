# HR Analytics Insights: PowerBI Visualization & SQL Testing
----------------------

Functional Validation : To test each feature as per the requirement.To verify all the filters and action filters as per the requirement.

Data Validation: Check accuracy and quality of the data.

## Create Table ###
----
CREATE TABLE HRDATA(
EMPO INT8,
GENDER VARCHAR(50),
MARITAL_STATUS VARCHAR(50),
AGE INT8,
DEPARTMENT VARCHAR(50),
EDUCATION VARCHAR(50),
EDUCATION_FIELD VARCHAR(50),
JOB_ROLE VARCHAR(50),
BUSINESS_TRAVEL VARCHAR(50),
EMPLOYEE_COUNT INT8,
ATTRITION VARCHAR(50),
ATTRITION_LABEL VARCHAR(50),
JOB_SATISFACTION INT8,
ACTIVE_EMPLOYEE INT8);



## Test Report ##
---------

## 1.   KPI - Employee Count
----
select sum(employee_count) as Employee_Count from hrdata;


## 2. KPI- Attrition Count
----

select count(attrition) from hrdata where attrition='Yes';

----

## 3. KPI- Attrition Rate

----
select 
round (((select count(attrition) from hrdata where attrition='Yes')/ 
sum(employee_count)) * 100,2)
from hrdata;


 ## 4. KPI- Active Employee
 ----
 select sum(hr.employee_count) - (select count(attrition) from hrdata  where attrition='Yes') from hrdata;
 ----

 ## 5.KPI- Average Age
 ----
 select gender, count(attrition) as attrition_count from hrdata
where attrition='Yes'
group by gender
order by count(attrition) desc;

## 6. KPI - Attrition by Gender
---
select gender, count(attrition) as attrition_count from hrdata
where attrition='Yes'
group by gender
order by count(attrition) desc;

## 7. KPI - Department wise Attrition

----
select department, count(attrition), round((cast (count(attrition) as numeric) / 
(select count(attrition) from hrdata where attrition= 'Yes')) * 100, 2) as pct from hrdata
where attrition='Yes'
group by department 
order by count(attrition) desc;

## 8. KPI - No of Employee by Age Group
-----
select age_band, gender, sum(employee_count) from hrdata
group by age_band, gender
order by age_band, gender desc;


## 9. KPI - Education Field wise Attrition
----

select education_field, count(attrition) as attrition_count from hrdata
where attrition='Yes'
group by education_field
order by count(attrition) desc;


---

## 10. KPI - Attrition Rate by Gender for different Age group
---
select age_band, gender, count(attrition) as attrition, 
round((cast(count(attrition) as numeric) / (select count(attrition) from hrdata where attrition = 'Yes')) * 100,2) as pct
from hrdata
where attrition = 'Yes'
group by age_band, gender
order by age_band desc;

----


All the above test has been validated with the powerbi report shown in the github. 



