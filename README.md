# OCD-Patient-Analysis

### Project Overview

This project involved analyzing OCD patient data using complex SQL queries to uncover trends and support decision-making. Key analyses included examining demographic differences (gender and ethnicity) in obsession scores, tracking monthly diagnoses to identify emerging trends, and identifying the most prevalent obsession and compulsion types. The insights gained were used to inform resource planning, improve clinical initiatives, and develop targeted treatment strategies to enhance patient care.

### Data Sources

OCD Data: The primary dataset used for this analysis is the "Ocd_patient_dataset" file, containing detailed information about the ocd of every patient. 

### Tools

- Excel - Data Cleaning
- SQL Server - Data Analysis
- Power BI - Creating report

### Data Cleaning/Preparation

In the initial data preparation phase, we peformed the following task:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis (EDA)

EDA involved exploring the ocd data to answer key questions, such as:

 1. count & PCT of F vs M that have OCD & average obession score by Gender
 2. count & average obession score of ethnicities that have OCD
 3. Number of diagnosed with OCD MOM
 4. WHat is the most common obsession type (count) & it's respective average score
 5. what is the most common compulsion type (count) & it's respective Average obsession score

### Data Analysis

Include some interesting code/feature worked with

```SQL
Select 
	   gender,
	   count(patient_id) as patient_count,
		Round(AVG(y_bocs_score_obsessions),2)as avg_obsessions_score
From patient
	group by gender
	order by 2;

SELECT 
		gender,
		count(*) as Total_count,
		round((count(*) *100.0 / (Select count(*) from patient where ocd_diagnosis_date is not null)),2) as percentage,
		round(avg (y_bocs_score_obsessions),2) as avg_obsession_score
		from patient
		where ocd_diagnosis_date is not null
		group by gender;

    Select 
	     count(*) as patient_count,
		 ethnicity,
		 Round(AVG(y_bocs_score_obsessions),2)as avg_obsessions_score
from patient
Group by ethnicity
order by 3;

Select 
To_CHAR(ocd_diagnosis_date, 'YYYY-MM-01 00:00:00') as month,
count(patient_id) as patient_count
from patient
group by 1
order by 1;

Select
	obsession_type,
	count(patient_id) as patient_count,
	Round(avg (y_bocs_score_obsessions),2) as avg_obsessions_score
from patient
group by 1
order by 2 desc;

Select
	compulsion_type,
	count(patient_id) as patient_count,
	Round(avg (y_bocs_score_obsessions),2) as avg_obsessions_score
from patient
group by 1
order by 2;
```

### Results/Findings

The analysis reveals the following insights:

Compulsion Types:
A total of 5 types of compulsions were identified among patients.
The most prevalent compulsion is Washing, observed in 321 patients.
Counting is associated with the highest average obsession score of 20.41.

Ethnic Distribution:
Patients are grouped into 4 ethnic categories.
The largest group is Caucasian, comprising 398 patients.
Asian patients have the highest average obsession score of 20.32.

Monthly Trends:
The number of diagnosed patients shows a consistent increase over time.

Gender Distribution:
Males (50.23%) and females (49.77%) are nearly equally represented.
Females have a slightly higher average obsession score (20.2 vs. 19.9).

Obsession Types:
Most common: Harm-related (332 patients, score 20.66).
Least common but most severe: Hoarding (278 patients, score 21.01).
