# Predicting Data Science Salaries with Linear Mixed Models

**Author:** Shuxin Qian  
**Tools:** R, tidyverse, lme4, ggplot2  

---

## 📌 Overview

This project investigates the factors influencing data science salaries using a **Linear Mixed-Effects Model (LMM)**.  
Using a dataset of **15,000 AI-related job postings (2024–2025)**, the analysis explores how job characteristics, company attributes, and employee factors contribute to salary variation.

The study finds that **experience level**, **company location**, and **company size** are the strongest predictors of salary, while many individual-level variables (skills, education, job title) have weak or insignificant effects.

---

## 📂 Dataset Description

The dataset includes job postings with variables such as:

- `job_title`
- `salary_usd`, `salary_currency`
- `experience_level`
- `employment_type`
- `company_location`, `employee_residence`
- `company_size`
- `remote_ratio`
- `required_skills`
- `education_required`
- `years_experience`
- `industry`
- `benefits_score`

A key focus of this project is understanding **group-level variation** in salary.

---

## 🧹 Data Cleaning & Preparation

### **1. Exploratory Data Analysis (EDA)**
- Distribution plots, histograms, and box/violin plots  
- Salary comparisons across:
  - industries  
  - education levels  
  - job titles  
  - experience levels  
- Trend plots for top skills and job titles (2024–2025)

### **2. Data Cleaning Steps**
- Convert `posting_date` to Date format  
- Split `required_skills` into long/wide formats  
- Create binary skill indicators:
  - `program`, `version`, `bigdata`, `cloud`, `deployment`, `MLprogram`, `MLknowledge`, `math`
- Log-transform salary: `log(salary_usd)`  
- Remove multicollinearity and prepare modeling dataset

---

## 🧠 Modeling Approach: Linear Mixed-Effects Model

To capture **group-level salary variation**, the model includes:

### **Random Effects**
- **Company location**
- **Experience level**

These were selected using **Intraclass Correlation Coefficient (ICC)**:

| Group | Variance | SD | ICC |
|-------|----------|------|------|
| company_location | 0.139 | 0.373 | 0.368 |
| experience_level | 0.219 | 0.467 | 0.579 |
| Residual | 0.0197 | 0.141 | 0.052 |

### **Fixed Effects**
- employment type  
- employee residence  
- industry  
- company size  
- job title  
- education level  
- skill indicators  

Model assumptions were checked using residual plots and random-effect error-bar plots.

---

## 📈 Key Results

### **1. Salary Distribution**
- Raw salary is strongly right-skewed  
- Most salaries fall between **80k–160k USD**  
- Extreme values reach **400k USD**  
- Log transformation improves model fit

### **2. EDA Findings**
- Education levels show similar salary distributions  
- Industries differ slightly (Automotive, Tech higher)  
- Job titles show limited separation  
- **Experience level** shows the clearest differences:
  - Executive > Senior > Mid > Entry

### **3. Mixed-Effects Model Findings**

#### **Strongest Predictors**
- **Experience level** (largest ICC)
- **Company location**
- **Company size** (large companies pay significantly more)

#### **Moderate Predictors**
- Industry (tech slightly higher)
- Employment type (freelancers, full-time slightly higher)

#### **Weak or Non-Significant Predictors**
- Job titles  
- Education levels (Bachelor/Master/PhD)  
- Skill indicators (binary skill presence too coarse)  
- Remote ratio  
- Currency type  

### **Random Effects Interpretation**
- Executive roles have positive random intercepts  
- Entry-level roles cluster below zero  
- High-paying countries: US, Norway, Denmark  
- Lower-paying countries: China, India  

### **Model Limitations**
- Skill variables lack proficiency levels  
- Job title and skills may be correlated  
- Employee residence and company location may overlap  
- Synthetic dataset may reduce residual variance  

---

## 🗣️ Discussion

The analysis shows that **group-level factors dominate salary variation**:

- Experience level explains **58%** of variation  
- Company location explains **37%**  
- Residual variance is only **5%**

This suggests that **where you work** and **your seniority** matter far more than individual skills or degrees.

---
