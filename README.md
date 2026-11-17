<a id="top"></a>

# **SKYLITE GROUP: HR WORKFORCE PULSE ANALYSIS**

*Where is the business at risk of losing good people, and what is driving it?*

**Prepared by:** Daniel Diala 

**Tools:** Microsoft Excel (Pivot Tables, Slicers, Interactive Dashboard)

---

## Table of Contents

1. [Project Background](#1-project-background)
   - [Company Overview](#company-overview)
   - [Problem Statement](#problem-statement)
   - [Objectives](#objectives)
   - [Analysis Focus Areas](#analysis-focus-areas)
2. [Data Structure & Initial Checks](#2-data-structure--initial-checks)
3. [Executive Summary](#3-executive-summary)
4. [Insights Deep Dive](#4-insights-deep-dive)
5. [Takeaway](#5-takeaway)
6. [Recommendations](#6-recommendations)
7. [Assumptions & Caveats](#7-assumptions--caveats)
   - [Data Quality Issues](#data-quality-issues)
   - [Analytical Assumptions](#analytical-assumptions)
8. [Skills Demonstrated](#8-skills-demonstrated)

---

## 1. Project Background

### Company Overview

Skylite Group is a mid-sized, production-led organisation with **311 employee records** spread across six departments: Production, IT/IS, Sales, Software Engineering, Admin Offices and the Executive Office. Production alone accounts for 209 employees (67%), and the workforce is concentrated in Massachusetts (276 employees, 89%). Over the period covered by the data, 207 employees remain active and **104 have left (33.4% attrition)**, with the first recorded departure in 2010 and the most recent in October 2018.

The HR dataset records one row per employee and covers demographics, employment and termination details, compensation, recruitment source, performance, engagement and satisfaction scores, and direct manager, which makes it possible to look at turnover from several angles at once.

### Problem Statement

One in three employees at Skylite Group has left the company, yet leadership has no clear picture of **where** the losses are concentrated or **why** people leave. Without that, retention spending is likely to be spread thinly or aimed at the wrong cause (pay, engagement, management or career growth) when the real drivers sit elsewhere.

> **Central question:** Where is the business at risk of losing good people, and what is driving it (pay, management, satisfaction, or something else) so that leadership knows where to focus retention efforts?

### Objectives

- **Size the problem:** establish the workforce profile, headcount by department and the overall attrition rate.
- **Diagnose attrition:** identify when people leave, why they leave, how satisfied they were, and whether early leavers differ from long-serving ones.
- **Test the pay question:** compare the best- and worst-paid positions against the company average salary.
- **Assess performance:** compare departments and recruitment sources to see where strong performers come from and where underperformance sits.
- **Evaluate management effectiveness:** compare managers on retention, attrition and team performance.
- **Turn the findings into action:** give HR leadership clear, prioritised recommendations.

### Analysis Focus Areas

| Focus Area | Question Answered | 
| --- | --- |
| **Workforce Overview** | Who works here and where is headcount concentrated? |
| **Attrition Analysis** | When, why and after how long do people leave? | 
| **Compensation Analysis** | Is pay a visible driver of turnover? | 
| **Performance Analysis** | Which departments and hiring channels deliver the strongest performers? | 
| **Manager Effectiveness** | Do retention and performance depend on who leads the team? | 



---

## 2. Data Structure & Initial Checks

The dataset is a single employee-level table, so no joins were needed. The raw export was kept untouched as an audit trail and every analysis sheet was built from the cleaned copy.

| Attribute | Detail |
| --- | --- |
| **Domain** | Human Resources / Workforce Analytics |
| **Grain** | One row = one employee |
| **Raw data (Origin_Data)** | 311 employees × 36 columns |
| **Cleaned data (Clean_Data)** | 311 employees × 42 columns (6 calculated columns added) |
| **Employment status** | 207 Active, 104 Terminated |
| **Departments** | Admin Offices, Executive Office, IT/IS, Production, Sales, Software Engineering |
| **Time coverage** | Hires from 2006 to 2018; terminations from August 2010 to October 2018 |
| **Duplicate check** | None found on Employee_ID or Employee_Name |


### Key Fields in Clean_Data

| Theme | Fields |
| --- | --- |
| **Identity & demographics** | Employee_Name, Employee_ID, Date_of_Birth, Sex, Marital_Description, Citizen_Description, HispanicLatino, Race_Description, State, Zip |
| **Employment** | Position, Department, Employment_Status, Termination_Reason, Date_of_Hire, Date_of_Termination, From_Diversity_JobFair_ID |
| **Compensation** | Salary (annual, USD) |
| **Recruitment & management** | ManagerName, ManagerID, Recruitment_Source |
| **Performance & engagement** | Performance_Score, Perfect_Score_ID (1 to 4), Engagement_Survey, Employee_Satisfaction (1 to 5), Special_Projects_Count, DaysLateLast30, Absences |

### Calculated Columns

Six columns were created because the raw data could not answer the business questions directly.

| Column | How It Was Built | Why It Was Needed |
| --- | --- | --- |
| **Salary Group** | Salary compared with the company average (about $69,021): High pay (at or above) or Low pay (below) | Turns a continuous salary into two tiers that pivots can compare quickly |
| **Tenure (Years) / Tenure (Months)** | Date_of_Termination minus Date_of_Hire; blank for Active employees | The raw data had no "how long did they stay" field, which the attrition analysis depends on |
| **Tenure Group** | Short Tenure (left before 3 years) or Long Tenure (3+ years); N/A for Active | Separates early exits (onboarding or fit) from later exits (advancement or burnout) |
| **Employment_Status_Group** | Collapses three statuses into Active or Terminated | Keeps headcount and retention KPIs simple |
| **Satisfication_Category** | Maps the 1 to 5 satisfaction score to Very low, Low, Moderate, High, Very High | Makes satisfaction readable on dashboard charts |

[View Worksheet](./Skylite_Group_HR_Workforce_Analysis_Worksheet.xlsx)

### Headline KPIs

| Metric | Value | Definition |
| --- | --- | --- |
| **Total headcount** | 311 | All employee records in Clean_Data |
| **Active / Terminated** | 207 (66.6%) / 104 (33.4%) | Employment_Status_Group; terminated share is the attrition rate |
| **Average salary** | $69,020.68 | Mean annual salary; also the High/Low pay cut-off |
| **Average performance score** | 2.98 | Mean of Perfect_Score_ID (1 = Pip, 2 = Needs Improvement, 3 = Fully Meets, 4 = Exceeds) |
| **Average engagement / satisfaction** | 4.11 / 3.89 (of 5) | Mean survey and self-reported satisfaction scores |
| **Average tenure before attrition** | 40 months (2.93 whole years) | Mean tenure of the 104 leavers |


---

## 3. Executive Summary

Skylite Group lost 104 of its 311 employees (33.4%), and the analysis shows the loss is **concentrated rather than evenly spread**:

- **Production** accounts for 83 of the 104 departures.
- **2015 and 2016** account for 45 of all departures.
- Among larger teams, attrition ranges from about **7% to 62%** depending on the manager.

Leavers were not unhappy on the way out (96% rated their satisfaction Moderate or higher) and most cited a better position, more money or a career change. The problem is therefore opportunity and retention rather than engagement alone, with early-tenure exits as the one exception.

The recommendations focus on structured early check-ins for new hires, internal career pathways, management audits in the highest-attrition teams, smarter recruitment spend, and a root-cause review of the 2015 to 2016 spike.

<img width="1800" height="520" alt="figure-01-headline-metrics" src="https://github.com/user-attachments/assets/a9ad049e-5473-49af-a12c-1ac61619d39c" />


***Headline metrics for Skylite Group***

[View Interactive Dashboard](https://drive.google.com/file/d/1wrQqZxmopnmWeH_ZvjqDRG0JBGlO2iOb/view?usp=sharing)


---

## 4. Insights Deep Dive

The dashboard has five analysis pages, each built from pivot tables in the analysis sheets and linked together with navigation buttons and slicers. Each page below shows the page itself, then every chart on it with the key insights it supports. Figures are taken directly from the pivot tables.

> **Reading note:** some charts are filtered to the top 5 or top 10 items. Where a percentage is calculated on that filtered group rather than on all employees, this is stated next to the chart.

---

### Workforce Overview

**Objective:** understand who makes up the workforce and where headcount and attrition sit, so the size of the retention problem is clear before diving into causes.

<img width="1307" height="568" alt="Skylite 1" src="https://github.com/user-attachments/assets/5bcba5c9-8b4b-4abd-beb7-309784e64d46" />



***Workforce Overview Dashboard***


**KPI cards:** Total headcount 311, Active employees 207, Terminated employees 104, Attrition rate 33%.

#### 1.1 Department Headcount 

<img width="1240" height="600" alt="chart-1-1-department-headcount" src="https://github.com/user-attachments/assets/90c99623-820c-4199-a73c-e18b90c03b49" />


- Production is by far the largest department with **209 employees (67%)**, followed by IT/IS (50), Sales (31), Software Engineering (11), Admin Offices (9) and the Executive Office (1).
- Production and IT/IS together make up 83% of the workforce, so retention in these two departments moves the company-wide numbers more than anywhere else.

#### 1.2 Department Headcount by Employment Status 

<img width="1240" height="640" alt="chart-1-2-headcount-by-employment-status" src="https://github.com/user-attachments/assets/a93798ae-6216-4f3e-9515-e340e48257f6" />


- Production has **126 active and 83 terminated** employees, an attrition rate of about **40%**, and accounts for 80% of all 104 departures.
- Software Engineering also loses a high share (4 of 11, 36%), although the team is small. IT/IS (20%), Admin Offices (22%) and Sales (16%) sit well below Production, and the single Executive Office employee is still active.
- **Takeaway:** attrition is a Production problem first, which directs the later pages to look at what is different there.

#### 1.3 Gender Distribution 

<img width="1040" height="660" alt="chart-1-3-gender-distribution" src="https://github.com/user-attachments/assets/aefe0365-7577-4df6-8073-31346ad54269" />


- The workforce is **57% female (176) and 43% male (135)**. This gives the demographic context for the rest of the analysis; attrition was not split by gender.

#### 1.4 Marital Status 

<img width="1120" height="600" alt="chart-1-4-marital-status" src="https://github.com/user-attachments/assets/9e8fb4d5-eac0-410b-92c3-00cd487b761b" />


- Employees are mostly **Single (44.05%) or Married (39.87%)**, with Divorced (9.65%), Separated (3.86%) and Widowed (2.57%) making up the remaining 16%.

#### 1.5 Workforce Analysis by State (top 5 states)

<img width="1120" height="600" alt="chart-1-5-workforce-by-state" src="https://github.com/user-attachments/assets/3e4e1d68-3384-439f-a508-5db7ae1f89c9" />


- **Massachusetts holds 276 employees (89% of the workforce)**, followed by Connecticut (6), Texas (3), Vermont (2) and Alabama (1). The data contains 28 states, but the chart shows the five largest.
- With nearly all staff in one state, geography is unlikely to explain turnover, which fits the small number of departures for Relocation Out Of Area (5 of 104).


---

### Attrition Analysis

**Objective:** find out when employees leave, why they leave, how satisfied they were at the time, and whether early leavers behave differently from long-serving ones.


<img width="1309" height="569" alt="Skylite 2" src="https://github.com/user-attachments/assets/a4cc3905-5990-476b-a9e1-93f9bfea1e26" />


***Attrition Analysis Dashboard***

**KPI cards:** average tenure before attrition 40 months, average satisfaction of leavers 3.88, long-tenure leavers 50% and short-tenure leavers 50% (52 employees each).

#### 2.1 Attrition Trend, 2010 to 2018 

<img width="1320" height="600" alt="chart-2-1-attrition-trend" src="https://github.com/user-attachments/assets/34dd0375-e89c-42e2-a759-adc653066878" />


- Departures rose from **1 in 2010 to a peak of 23 in 2015**, stayed almost as high at 22 in 2016, then dropped to 8 in 2017.
- **2015 and 2016 together account for 45 of the 104 departures (43%)**, which makes this a spike with a likely specific cause rather than a steady background rate.
- 2018 shows 13 departures but the data ends in October 2018, so it is a partial year and should not be read as a full-year figure.

#### 2.2 Top Attrition Reasons

<img width="1480" height="700" alt="chart-2-2-top-attrition-reasons" src="https://github.com/user-attachments/assets/e15118e9-5c0d-4bdb-8d4e-400a657879f1" />


- **Another Position (22.99%)** is the leading reason, followed by Unhappy (16.09%), More Money (12.64%), Career Change (10.34%) and Hours (9.20%). Attendance (8.05%) is the first clearly negative reason on the list.
- Another Position, More Money and Career Change together make up 40 of the 104 departures (38%): people mostly leave for something better rather than because they were pushed out.
- Percentages are calculated on the ten reasons shown (87 of 104 leavers). On all 104 leavers, Another Position is 19.2% and Unhappy is 13.5%, so the ranking holds.

#### 2.3 Satisfaction Level by Attrition 

<img width="1200" height="660" alt="chart-2-3-satisfaction-by-attrition" src="https://github.com/user-attachments/assets/1c5d9537-0157-4e3c-b9d3-9d13d3606c0e" />


- **High (36.54%) and Very High (27.88%) satisfaction** cover almost two thirds of leavers, and Moderate adds another 31.73%. Only **3.85% (4 people) rated their satisfaction Low**, so 96% of leavers were at least moderately satisfied.
- Leavers averaged 3.88 out of 5 against 3.89 for the company overall, so people who left were no less satisfied than the rest. "Fix engagement to fix turnover" would not address the main driver here.

#### 2.4 Short-Tenure Employee Attrition Reason

<img width="1200" height="680" alt="chart-2-4-short-tenure-reasons" src="https://github.com/user-attachments/assets/3654d4d6-87ee-4cc1-b0e8-d720986a99ef" />


- Among employees who left within three years, **Unhappy is the top reason (24.24%)**, ahead of Another Position and Career Change (21.21% each), Hours (18.18%) and More Money (15.15%).
- Percentages are calculated on the five reasons shown (33 of the 52 short-tenure leavers). Hours is the clearest early-tenure signal: 6 of the 8 departures for hours happened within three years.
- Long-tenure leavers show a different pattern, with Another Position as the leading reason (13 of 52). Early exits point to fit and onboarding, while later exits point to a lack of advancement.


---

###  Compensation Analysis

**Objective:** test whether pay is a visible driver of turnover by comparing the best- and worst-paid positions against the company average.

<img width="1320" height="569" alt="Skylite 3" src="https://github.com/user-attachments/assets/3ade8ac1-9bb8-480c-a9e1-0bde5d5f1cab" />


***Compensation Analysis***

**KPI cards:** average individual salary $69.02K, highest paid position President & CEO, lowest paid position Administrative Assistant.

#### 3.1 Top Earning Positions (top 10 positions)

<img width="1680" height="720" alt="chart-3-1-top-earning-positions" src="https://github.com/user-attachments/assets/951a903b-ce42-46cc-8d9c-d1a684339aa0" />


- Leadership and technical specialist roles lead: President & CEO ($250.00K), CIO ($220.45K), Director of Sales ($180.00K), IT Manager - Infra ($157.00K) and Data Architect ($150.29K).
- Even the tenth position on the list (Software Engineer, $96.28K) pays well above the company average of $69.02K.

#### 3.2 Bottom Earning Positions (bottom 10 positions)

<img width="1680" height="720" alt="chart-3-2-bottom-earning-positions" src="https://github.com/user-attachments/assets/0c93fde6-d5cc-4d67-aa0e-0ce5e45360a1" />


- The lowest paid roles are **Administrative Assistant ($52.28K)**, **Production Technician I ($54.78K)** and IT Support ($63.57K). The CEO earns about 4.8 times the lowest paid role.
- Production Technician I, Production Technician II and Production Manager all appear in the bottom 10, which links the lowest pay levels to the department with the highest attrition (about 40%).
- Because a few high-paying executive roles pull the average up, 221 of 311 employees (71%) fall in the Low pay group below the $69.02K average. Even so, only 11 of the 104 leavers cited More Money, so pay on its own does not explain the turnover.


---

### Performance Analysis

**Objective:** find out where strong performers come from, which hiring channels deliver the best hires, and where underperformance is concentrated.

<img width="1311" height="570" alt="Skylite 4" src="https://github.com/user-attachments/assets/a9f2402d-b3f5-4bec-b301-7d0cdada8ae3" />



***Performance Analysis Dashboard***

**KPI cards:** average performance score 2.98 (scale 1 to 4), best performing department Software Engineering, lowest performing department Sales.

#### 4.1 Recruitment Source Performance Analysis 

<img width="1400" height="680" alt="chart-4-1-recruitment-source-performance" src="https://github.com/user-attachments/assets/b8ec91a7-e5cc-461b-88b3-f2d90301715a" />

- **Indeed (87) and LinkedIn (76) supply 52% of all hires**, followed by Google Search (49), Employee Referral (31), Diversity Job Fair (29), Careerbuilder (23) and the company Website (13).
- **Employee Referral hires perform best (3.16)**, the only major channel clearly above the 2.98 company average. LinkedIn and Diversity Job Fair hires score 3.00, while Indeed (2.95) is slightly below average despite being the biggest source.
- **Website hires perform worst (2.77)** and bring in few people, so the channel is weak on both quality and volume. On Online Web Application (1 hire) and Other (2 hires) the sample is too small to judge.

#### 4.2 Departmental Performance Overview (rating counts)

<img width="1400" height="720" alt="chart-4-2-departmental-performance" src="https://github.com/user-attachments/assets/65abb185-0f7f-443b-a116-eb00041c1059" />


- Across the company, 243 employees (78%) are rated Fully Meets, 37 (12%) Exceeds, 18 (6%) Needs Improvement and 13 (4%) Pip.
- Production has the most underperformers in absolute terms (**15 Needs Improvement and 8 Pip out of 209**), but **Sales has the highest rate (5 of 31, 16%)**, which fits it being the lowest performing department (average 2.84).
- Software Engineering (3.09) and IT/IS (3.06) have the highest average scores. Sales is not the lowest paid department, so its gap points to role fit, management or work environment rather than pay alone.


---

###  Manager Effectiveness Analysis

**Objective:** test whether retention and team performance depend on who leads the team.

<img width="1321" height="568" alt="Skylite 5" src="https://github.com/user-attachments/assets/84dd0693-5107-4ab3-9ac2-97a3cbbbb40f" />


***Manager Effectiveness Analysis Dashboard***

**KPI cards:** 21 managers, highest retention managers Brian Champaigne and Eric Dougall, highest attrition managers Webster Butler and Amy Dunn, average performance score 2.98.

#### 5.1 Managers Attrition & Retention Analysis (top 10 managers by team size)

<img width="1800" height="760" alt="chart-5-1-manager-attrition-retention" src="https://github.com/user-attachments/assets/25808fed-525d-418c-a61c-97add6f75771" />


- **Webster Butler and Amy Dunn each lost 13 of their 21 employees (61.9% attrition)**, and Kissy Sullivan lost 12 of 22 (55%): these are the only three of the ten largest teams where more employees left than stayed.
- Other large teams retain much better: Ketsia Liebig lost 5 of 21 (24%), and Kelley Spirea and Brannon Miller lost 6 of 22 (27% each). Teams of similar size and in the same company show a gap of more than 35 percentage points.
- Percentages on this chart are shares of the 213 employees under these ten managers, not of the whole company.

#### 5.2 Managers with Highest Performers (average team performance score)
<img width="1040" height="640" alt="chart-5-2-managers-highest-performers" src="https://github.com/user-attachments/assets/1114b0b8-a96a-414d-8773-2e35b63bb275" />


- **Eric Dougall (3.25)**, Jennifer Zamora (3.14), Simon Roup (3.12), Alex Sweetwater (3.11) and Janet King (3.11) lead the strongest teams, all above the 2.98 company average.
- Strong performance does not guarantee retention: Simon Roup's team scores well but 8 of 17 employees (47%) have left. Eric Dougall and Jennifer Zamora lead small teams (4 and 7 employees).

#### 5.3 Managers with Lowest Performers (average team performance score)

<img width="1040" height="640" alt="chart-5-3-managers-lowest-performers" src="https://github.com/user-attachments/assets/47b7ee50-b5fb-4e84-acd4-e5d25da1899e" />


- Michael Albert (2.86), Peter Monroe (2.86), Brannon Miller (2.82), John Smith (2.71) and Debra Houlihan (2.67) lead the lowest scoring teams. Debra Houlihan's team has only 3 people, so her score should be read with caution.
- Low performance and low retention do not always go together. Peter Monroe's team retains 93% of its employees despite a below-average score, while Michael Albert's team combines a low score with 41% attrition. Cross-reading the two measures is what identifies the managers who need support first.


---

## 5. Takeaway

The analysis set out to answer where Skylite Group is at risk of losing good people and what is driving it. The picture that emerges is specific rather than general:

- **Where:** attrition is concentrated in Production (83 of 104 leavers, about 40% of the department), with Software Engineering also high on a small base. It was not constant over time: 45 of the 104 departures fell in 2015 and 2016.
- **Why:** people mostly leave for something better. Another Position, More Money and Career Change account for 38% of departures, 96% of leavers were at least moderately satisfied, and their average satisfaction (3.88) matches the company (3.89). Pay matters less than expected, with only 11 leavers citing money.
- **Who leaves early:** half of all leavers go within three years, and this group is the one where dissatisfaction (Unhappy) and working hours stand out, pointing to an onboarding and fit gap.
- **What management changes:** among teams of 13 or more employees, attrition ranges from about 7% to 62%, and two large teams (Webster Butler and Amy Dunn) lost three in five employees. Management is the biggest lever visible in the data.
- **Where good people come from:** employee referrals produce the strongest performers (3.16) while the company website produces the weakest (2.77). Sales is the weakest department (2.84) without being the lowest paid.

> **In short:** the standard approach of raising engagement or pay across the board would miss the real causes. Retention effort is better targeted at career growth for experienced staff, a stronger first year for new hires, and the specific teams and departments where losses are concentrated.


---

## 6. Recommendations

| Observation | Recommendation |
| --- | --- |
| Short-tenure leavers cite Unhappy and Hours most often; half of all leavers go within three years | Introduce structured 90-day and 12-month check-ins for new hires to catch dissatisfaction before it turns into early attrition |
| Long-tenure leavers mainly depart for Another Position (13 of 52); 38% of all leavers go for a better position, money or a career change | Build internal mobility pathways (internal job postings, career ladders) so experienced staff can grow without leaving |
| Production loses about 40% of its staff (83 leavers) and Software Engineering 36% | Investigate the rising attrition in Production and Software Engineering and develop a more targeted retention approach for each |
| Webster Butler and Amy Dunn lose 62% of their teams; Kissy Sullivan 55%; low-performing teams cluster under a few managers | Audit management practices in these teams (and review Debra Houlihan's small team) and use coaching or restructuring where needed |
| 2015 and 2016 hold 45 of the 104 departures (43%) | Run a root-cause review of that period (exit interviews, organisational changes) to see whether it was a one-off or a warning sign to monitor |
| Employee Referral hires score 3.16 and the Website 2.77; Indeed is the biggest source but scores below average (2.95) | Shift recruitment effort towards referrals and diversity job fairs, and reassess the careers website |
| Sales is the lowest performing department (2.84; 16% underperformers) without being the lowest paid | Compare Sales with Software Engineering (management style, tooling, incentives, workload) to find a transferable fix rather than assuming a pay problem |


---

## 7. Assumptions & Caveats

The dataset was not free of errors. The tables below show what was found, how it was handled so the analysis stays reliable, and what would prevent it happening again.

### Data Quality Issues

| Issue Found | Mitigation | Recommendation |
| --- | --- | --- |
| Inconsistent capitalisation in Employment_Status, Performance_Score, Recruitment_Source and Termination_Reason (e.g. "PIP", "attendance", "CareerBuilder") | Standardised each field to consistent title case so categories group correctly in pivot tables | Use dropdown lists or validated reference values at the point of data entry |
| Trailing spaces in Sex ("M ") and Department (the whole Production label, 209 rows) | Trimmed the text and expanded Sex to Female and Male | Trim text on import and enforce clean values in the source system |
| State stored as two-letter codes (MA, CT, TX) | Converted to full state names for cleaner labels and filters | Agree one standard format for geographic fields |
| Perfect_Score_ID does not match Performance_Score in 2 of 311 records | Flagged as a raw data-entry inconsistency and left as is, since it affects under 1% of records and does not move department averages materially | Derive the numeric score from the rating automatically instead of keying both |
| ZIP codes stored as numbers (leading zero lost, e.g. 01960 became 1960) | Left unchanged because ZIP is not used in this analysis | Store ZIP as text if postal-level mapping is ever needed |
| Blank Date_of_Termination (207 rows) and blank ManagerID (8 rows) | Checked and confirmed as expected: active employees have no termination date and top-level roles have no manager | Document expected blanks in the data dictionary so they are not mistaken for errors |
| Possible duplicate employee records | Checked Employee_ID and Employee_Name; all 311 records are unique | Keep a duplicate check in the standard data preparation steps |

### Analytical Assumptions

| Issue Found | Mitigation | Recommendation |
| --- | --- | --- |
| Salary is continuous and hard to compare across groups | Created Salary Group using the company average ($69,021) as the High/Low pay cut-off | Review the cut-off against market benchmarks, as an average is pulled up by executive salaries |
| No tenure field in the raw data | Calculated tenure from hire and termination dates; Short Tenure means under 3 years. Whole-year tenure averages 2.93 years while months give 40 (3.3 years), so months are used for the KPI | Capture tenure directly in the HR system and agree one tenure definition |
| Several charts show only the top 5 or top 10 items, so percentages use the filtered group as the base (reasons: 87 of 104 leavers; short-tenure reasons: 33 of 52; manager chart: 213 employees) | Stated the base next to each chart and checked that rankings hold on the full data | Show the base (n) on every filtered chart and label "% of top-N" |
| Several teams are small (e.g. Eric Dougall 4, Debra Houlihan 3), so their averages and rates are volatile | Reported team sizes beside manager findings and avoided strong conclusions on small teams | Set a minimum team size before ranking managers |
| 2018 is a partial year (terminations only recorded to October 2018) | Flagged on the trend insight and not read as a full-year decline or rise | Refresh the data for a full year before trend comparisons |
| The dashboard does not split satisfaction or attrition by gender, race or age | Demographic charts are used for context only; no conclusions are drawn on them | Add these cuts if leadership wants a diversity and fairness view of attrition |
| The data is a snapshot and shows associations, not causes | Wording stays at "suggests" and "points to"; recommendations include root-cause reviews before action | Pair this analysis with exit interviews and engagement data over time |


---

## 8. Skills Demonstrated

| Skill Area | How It Was Applied in This Project |
| --- | --- |
| **Data cleaning & validation** | Standardised text, trimmed whitespace, converted codes to labels, tested for duplicates, and logged every decision while keeping the raw data untouched as an audit trail |
| **Feature engineering** | Built six calculated columns (salary group, tenure in years and months, tenure group, status group, satisfaction category) to answer questions the raw data could not |
| **Pivot tables & pivot charts** | Built five analysis sheets of pivot tables and converted them to charts for attrition, compensation, performance and management analysis |
| **Dashboard design** | Designed a seven-page interactive dashboard with KPI cards, slicers, navigation buttons and a consistent visual style |
| **Data modelling in Excel** | Used the Excel Data Model and time-grouped date fields to produce the yearly attrition trend |
| **KPI definition** | Defined attrition rate, tenure before attrition, retention by manager, average salary and performance score in a consistent way |
| **HR / workforce analytics** | Applied domain concepts such as attrition drivers, tenure bands, retention, pay positioning, performance distribution and manager effectiveness |
| **Critical thinking & data quality awareness** | Separated expected blanks from real errors, flagged small samples and partial years, and stated the base behind every percentage |
| **Insight-driven storytelling** | Linked each chart to a business question, moved from findings to a takeaway, and turned them into prioritised recommendations |
| **Documentation** | Produced a data dictionary, a cleaning log and a structured report for non-technical readers |

[Back to top](#top)

---

*Skylite Group | HR Workforce Pulse Analysis | Prepared by Daniel Diala*

