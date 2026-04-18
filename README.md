# DSA3050A-Advanced-PowerBI-Exam
A complete Power BI healthcare analytics solution built on a 10,000-row synthetic patient dataset, covering data cleaning, star schema modeling, DAX measures, and a three-page interactive dashboard for monitoring admissions, billing performance, and clinical outcomes.
# Healthcare Analytics Dashboard

## Student Name and Admission Number
**Name:** Ilham Mohamed
**Admission Number:** 152

## Course Code and Class
**Course Code:** DSA3050
**Class:** A

## Project Overview
This project is an end-to-end healthcare analytics solution built in Microsoft Power BI. It transforms a synthetic hospital dataset of 10,000 patient admission records into a four-page interactive dashboard that supports decision making across executive, clinical, and financial audiences. The project covers the full analytics lifecycle: data acquisition, cleaning and transformation in Power Query, dimensional modelling using a star schema, DAX measure development, dashboard design, and the interpretation of findings into analytical insights and business recommendations.

The dashboard is organised using a progressive disclosure approach. Page 1 (Executive Summary) answers headline questions for senior leadership. Page 2 (Detailed Analysis) provides clinical and demographic breakdowns. Pages 3 and 4 (Performance Monitoring) surface operational, payer, and financial performance detail for analysts and contract owners.

## Problem Statement
Healthcare institutions generate large volumes of patient, clinical, and financial data every day, but administrators frequently lack a unified view of how admissions, clinical outcomes, and revenue interact. Without that integrated view, decisions about staffing, resource allocation, payer negotiation, and cost management are made reactively rather than strategically.

The core business question this project addresses is: **how can hospital administrators monitor patient admission patterns, understand the financial burden of different medical conditions, track clinical outcomes, and identify high-risk patient segments in order to improve resource allocation, reduce costs, and enhance quality of care?**

The dashboard answers specific decision-making questions including which medical conditions drive the highest billing costs, whether emergency admissions are significantly more expensive than elective ones, which hospitals and doctors carry the heaviest patient loads, whether admissions show seasonal patterns, and what proportion of patients have abnormal test results and how that correlates with length of stay.

## Dataset Description
The dataset is a synthetic hospital records dataset designed to mirror the structure of real-world healthcare data while protecting patient privacy. It contains 10,000 patient admission records with 15 columns spanning demographic, clinical, operational, and financial attributes.

Key fields include patient demographics (age, gender, blood type), clinical information (medical condition, medication, test results), operational data (admission type, hospital, doctor, admission date, discharge date, room number), and financial information (insurance provider, billing amount). The dataset includes both categorical and numerical variables as well as two date fields, which enables time-based analysis such as length-of-stay calculations and year-over-year trends.

The dataset is well-structured enough to support a star schema and has the volume and variety needed to demonstrate advanced Power BI capabilities including DAX measures, calculated columns, and time intelligence.

## Tools Used
The project was built using Microsoft Power BI Desktop as the primary analytics and visualisation platform. Power Query was used for data cleaning and transformation. DAX (Data Analysis Expressions) was used for all measures and calculated columns. The data modelling was done in Power BI's Model View using a star schema approach.

## Steps Followed
The project followed a structured analytics workflow beginning with data acquisition and understanding, where the business problem was defined and the dataset's structure was assessed for suitability.

Data cleaning and transformation was carried out in Power Query. This included checking for missing values (none found, as the dataset was synthetic), removing duplicate records using all columns to preserve legitimate repeat visits, verifying and correcting data types, standardising text fields by trimming whitespace and enforcing consistent casing, removing the Name column for privacy and analytical reasons, and validating date fields by confirming that discharge dates always fell after admission dates.

Data transformation included splitting the Blood Type column into separate Blood Group and Rh Factor columns for flexible analysis, creating conditional columns for Age Group (Minors, Young Adults, Middle Aged, Senior, Elderly), Billing Category (High and Low), and Length of Stay bands (short, medium, long), and filtering out negative billing values that were artefacts of synthetic data generation.

Data modelling used a star schema with Fact_Admissions as the central fact table and eleven dimension tables covering medical conditions, insurance, gender, admission types, test results, medications, blood type, age group, billing category, length of stay, and a custom date dimension built in Power Query. Relationships were created as many-to-one with single-direction filtering to ensure predictable, efficient query behaviour.

DAX measures were developed in a dedicated _Measures table to keep them centralised and easy to maintain. A Risk Category calculated column was created at row level to enable slicing and grouping.

Dashboard design followed an iterative process: initial layouts were built, then refined based on what the data actually revealed, with structural decisions made to respond to the limitations of synthetic data rather than forcing visuals that would not inform real decisions.

## Dashboard Features
The dashboard is organised across four pages, each targeting a different user type and level of analytical depth.

Page 1 (Executive Summary) presents the hospital's current state in four headline KPI cards (Total Billing Amount, Total Admissions, Average Billing per Admission, Admissions Growth %) supported by six charts answering the core what, when, and who questions: billing by medical condition, gender mix, monthly admission trends, billing by admission type and year, and patient distribution by billing category.

Page 2 (Detailed Analysis) offers clinical and demographic breakdowns including length of stay by condition and test results, admissions by age group with condition mix, medication mix, billing category mix by condition, and a blood type versus condition heatmap.

Page 3 (Performance Monitoring 1) focuses on provider and payer analysis, including admissions versus billing by insurance provider, insurer volume versus cost per admission scatter, and admissions by insurance provider broken down by admission type.

Page 4 (Performance Monitoring 2) handles financial and risk performance with quarterly billing comparisons, billing versus average length of stay by condition, and a risk segment scatter comparing cost, length of stay, and volume.

Interaction features include a consistent KPI strip anchored at the top of every page, page-specific slicers on the right for filtering (Year, Gender, Admission Type, Medical Condition, Age Group, Insurance Provider, Quarter), cross-filtering that turns every chart element into an interactive filter, a Year range slider on Page 4 for continuous temporal filtering, and tooltips on every visual for detail-on-demand access to underlying values.

## Key DAX Measures
Seventeen DAX measures were developed to support the dashboard, grouped into financial, operational, clinical, and comparative categories.

**Total Billing Amount** uses SUM on the Billing Amount column and serves as the primary financial KPI. **Average Billing per Admission** uses AVERAGE to enable fair cost comparison across conditions and hospitals regardless of volume. **Total Admissions** uses COUNTROWS on the fact table to measure patient volume.

Time intelligence measures include **YTD Billing** (TOTALYTD), **Previous Year Billing** (CALCULATE with SAMEPERIODLASTYEAR), **Prior Year YTD Billing** (CALCULATE with SAMEPERIODLASTYEAR wrapped around YTD Billing), **Previous Year Admissions**, **Billing Growth %**, **Admissions Growth %** (DIVIDE of current minus prior year over prior year), and **YTD vs Prior Year %**.

Clinical and operational measures include **Average Length of Stay** (AVERAGE on the Length of Stay column) and **% Abnormal Test Results** (CALCULATE filtered to abnormal results divided by total admissions using DIVIDE).

Ranking and comparative measures include **Top Hospital Rank** (RANKX with ALL for unfiltered ranking), **Billing % of Total** (DIVIDE with ALL inside CALCULATE to preserve totals), **Top Medication** (TOPN nested in MAXX to return the most-prescribed medication as text), **Top Insurance** (same pattern for top billing insurer), and **On Target Pace** (an IF statement on YTD vs Prior Year % returning "On Track" or "Behind" as a plain-text status flag).

A **Risk Category** calculated column was built using the SWITCH function to classify each admission as High Risk, Medium Risk, Monitor, or Low Risk based on test results and admission type. It was built as a calculated column rather than a measure because risk needed to exist at row level for slicing and grouping.

## Key Insights
Six analytical insights emerged from the dashboard.

Admissions growth is outpacing billing growth, signalling margin compression per patient: admissions grew 7.48% year on year to 55,000 patients while average billing per admission remained flat at $25,590, indicating more patients are being served without proportional revenue growth.

The patient population is dominated by a single billing tier, with 91.98% of admissions falling into the High billing category and only 8.02% in Low, creating revenue concentration risk.

Monthly admission volumes are volatile but show no discernible seasonal pattern, with admissions fluctuating between 1,350 and 1,650 per month across admission types without any sustained quarterly peak, which has direct implications for staffing and capacity planning.

High-risk patients consume disproportionate resources relative to their population share: the risk segment scatter shows High Risk patients at approximately 15.6 days average length of stay versus 15.45 days for Low and Medium Risk segments, pointing toward the classic 80/20 distribution of hospital resource consumption.

Payer mix appears balanced across the five major insurers but admission-type composition reveals differentiated utilisation patterns, with some insurers showing disproportionately high emergency admissions that could indicate outpatient access gaps or prior-authorisation friction.

Clinical outcomes (abnormal test results) do not strongly differentiate length of stay across conditions, with stays clustered between 15 and 16 days regardless of test result category, a finding that either reflects synthetic data characteristics or, on real data, would suggest that test severity is not being used effectively to stratify care pathways.

These insights led to five actionable recommendations: launching a per-admission revenue diagnostic programme to address margin compression, building an insurer-level case management programme targeting high emergency-admission payers, implementing early risk stratification at admission, moving from seasonal forecasting to a rolling variability-based planning model, and reviewing billing categorisation granularity to enable more precise segmentation.

## Challenges Encountered
The most significant challenge was working with synthetic data in which several categorical variables (medication, blood type, insurance provider, hospital) were generated with uniform random assignment. This meant that patterns one would expect to see on real hospital data, such as payer concentration, condition-specific cost variance, seasonal admission peaks, and blood-type clinical correlations, did not appear in the data. This required two explicit design responses. First, the hospital-level ranking visual had to be removed entirely once it became clear the data generated only one admission per hospital, and was replaced with insurance-provider analysis which did show genuine variance. Second, scatter plots on Pages 3 and 4 were annotated to acknowledge that narrow axis ranges reflected uniform synthetic data rather than meaningful operational patterns.

Other challenges included sorting issues with the Age Group and Quarter columns, which defaulted to alphabetical rather than chronological order and required sort-by-column configuration against custom numeric fields. Negative billing values in the raw data had to be filtered out as they were synthetic-generation artefacts inconsistent with real healthcare billing. Several initial visuals used Average aggregations that produced visually flat bars on the uniform data; these were evaluated and in some cases retained (for clinically correct reasons) and in other cases replaced with more informative alternatives.

The overall challenge of the project was making honest design decisions in response to data limitations rather than forcing visuals that looked impressive but misrepresented what the data could support.

## Conclusion
This project delivered a complete four-page healthcare analytics dashboard grounded in a disciplined analytics workflow: from data acquisition through cleaning, modelling, measure development, and design, ending in interpretation. The dashboard successfully answers the business questions set out at the start of the project, with consistent KPI anchoring across all four pages, chart types selected to match the shape of each question, and interaction patterns designed to support both scanning and exploration.

The project also demonstrates analytical judgement in responding to data quality issues. Rather than forcing broken or misleading visuals, design decisions were made transparently, with limitations documented and acknowledged on the dashboard itself. The architecture, chart selection, and measure logic are all built to transfer directly to real operational hospital data, where the underlying patterns would surface more sharply and the recommendations would carry more quantified impact.

Beyond the technical deliverable, the project shows the full cycle of turning raw data into a decision-support tool: understanding the business problem, structuring the data to answer it, designing for the audience, and translating findings into specific, actionable recommendations for hospital administrators. That end-to-end arc, not just the final screenshots, is what makes this dashboard a genuine analytics solution rather than a static report.
