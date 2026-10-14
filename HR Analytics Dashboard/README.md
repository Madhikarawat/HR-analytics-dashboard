# HR Analytics Dashboard: Employee Attrition & Workforce Insights

An interactive, single-page Excel dashboard that cleans messy HR data from three source systems, models it with relationships, and answers the HR Director's core question: **"Has attrition increased, and where is it concentrated?"**



## Project Overview

**Scenario:** As a Junior HR Data Analyst, I received three raw tables exported from different systems (Employees, Departments, Cities). The data had duplicates, inconsistent text, mixed formats and invalid values. The task was to clean it, build relationships, create an interactive dashboard and present insights with recommendations.

**Outcome:** A refreshable Power Query pipeline, a three-table data model, 10 PivotTables and a one-page dashboard with KPI cards, 6 visuals and 4 slicers.

## Tools & Techniques

| Area | Used |
|---|---|
| Data cleaning | Excel Power Query (Trim, Clean, Proper Case, Replace Values, Remove Duplicates, type conversion, row filters) |
| Modelling | Excel Data Model (Power Pivot), one-to-many relationships |
| Analysis | PivotTables, calculated columns |
| Visualization | PivotCharts, funnel chart, filled map, doughnut chart, line chart, KPI cards |
| Interactivity | Slicers connected across PivotTables |

## Dataset

| Table | Role | Rows (clean) | Key columns |
|---|---|---|---|
| Employees | Fact | 9,975 (from 10,000 raw) | EmployeeID, DeptID, CityID, Age, Gender, Experience, HireDate, Salary, Performance, Satisfaction, Overtime, Attrition |
| Departments | Dimension | 8 | DeptID, Department, Manager, Budget |
| Cities | Dimension | 10 | CityID, City, State, Region |

**Relationships:** `Employees.DeptID → Departments.DeptID` and `Employees.CityID → Cities.CityID`



## Data Cleaning

| Issue | Treatment |
|---|---|
| Duplicate EmployeeIDs | Removed duplicates on EmployeeID (key column) |
| Invalid ages (17 and 67) | Records outside the allowed working-age range removed; cleaned ages range from 21 to 60 |
| Gender in mixed case and with extra spaces | Lowercased, trimmed, then proper-cased to `Male` / `Female` |
| Overtime as Y / N / YES / NO | Standardized to `Yes` / `No` |
| Attrition in mixed formats | Standardized to `Yes` / `No` and encoded as `Attrition_Flag` (1/0) |
| Mixed hire date formats | Converted to a single Date type |
| Salary stored as text/mixed formats | Converted to numeric; 16 missing salaries left as null (not guessed) |
| Performance / Satisfaction outside 1-5 | Validated to the 1-5 scale; 7 missing performance ratings left as null |
| Experience greater than Age - 18 | Flagged with a validation rule; invalid values reset to 17 years in a new `Exp (Cleaned)` column (original kept) |
| Department and city typos, casing, spaces | Trimmed, proper-cased and corrected (e.g. Finanace → Finance, Hydrabad → Hyderabad) |
| Duplicate DeptID / CityID | De-duplicated to unique keys |
| Region codes (N, S, north, NORTH) | Standardized to North / South / East / West |

**Derived columns:** `Exp (Cleaned)`, `Attrition_Flag` (1 = left, 0 = stayed), `Employee_Status` (Active / Inactive).

## Dashboard

**KPI cards:** Employee Count, Attrition Rate, Average Salary, Average Experience

**Visuals**
- Employees by Department (bar)
- Attrition Rate by Department (funnel)
- Employees by Gender (doughnut)
- Job Satisfaction by Department (bar)
- Hiring Trend by Year (line)
- Employees by State (filled map)

**Slicers:** Department, Region, Gender, Employee Status

The workbook also contains an **Analysis** sheet (10 PivotTables feeding the dashboard) and an **Insights** sheet with findings, recommendations and business impact.

## Key Findings

| Metric | Value |
|---|---|
| Total employee records | 9,975 (4,991 active, 4,984 inactive) |
| Overall attrition rate | **49.96%** |
| Average salary | ₹12,52,500 (about ₹12.5 LPA) |
| Average experience | 14.7 years (cleaned) |
| Average age | 40.5 years |
| Gender split | 50.5% male, 49.5% female |

**By department**

| Department | Employees | Attrition | Avg salary |
|---|---|---|---|
| Finance | 1,274 | 49.9% | ₹12.44 L |
| Customer Support | 1,271 | 50.8% | ₹12.42 L |
| R&D | 1,264 | 49.3% | ₹12.36 L |
| Sales | 1,254 | 50.4% | ₹12.91 L |
| Human Resources | 1,244 | **52.6%** | ₹12.47 L |
| Operations | 1,242 | 48.1% | ₹12.43 L |
| Marketing | 1,217 | 49.5% | ₹12.69 L |
| IT | 1,209 | 49.0% | ₹12.48 L |

**Insights**
- Nearly half of all employees in the dataset have left; **Human Resources (52.6%)** and **Customer Support (50.8%)** have the highest attrition, Operations the lowest (48.1%).
- By location, Kolkata (52.2%) and Chennai (51.6%) have the highest attrition; Maharashtra has the largest headcount (2,053, Mumbai + Pune).
- Sales has the highest average pay (₹12.91 L) and Finance the largest team (1,274).
- Attrition is almost identical for overtime vs non-overtime (49.6% vs 50.4%) and for male vs female (49.7% vs 50.3%), and shows no clear pattern across satisfaction scores, so no single factor explains it.
- Hiring is steady at roughly 850-895 per year from 2015 to 2025, peaking in 2020 (895). 2026 is a partial year (data runs to early July, 421 hires).

## Recommendations

1. **Target retention in the highest-attrition departments** (HR and Customer Support) with stay interviews and exit-reason tracking.
2. **Strengthen hiring and workforce planning** so replacement hiring keeps pace with exits.
3. **Invest in engagement and career development programs**, and capture richer exit data (reason for leaving, tenure, manager) so the real drivers can be identified.

**Business impact:** lower attrition reduces recruitment and onboarding cost, improves workforce planning and protects business continuity.

## Data Notes & Limitations

- Because the experience rule (Experience ≤ Age - 18) affected 3,639 records (about 36%), Average Experience depends on that cleaning choice; the original column is preserved for comparison.
- Employee Count includes former employees; current headcount is the **Active** count (4,991). Use the Employee Status slicer to switch views.
- Attrition is evenly high across every cut of the data, which suggests this dataset is simulated; conclusions are illustrative.

## Repository Structure

```
├── HR_Analytics_Dashboard.xlsx   # Final workbook: cleaned tables, Analysis, Dashboard, Insights
├── Employees.xlsx                # Raw employee export (10,000 rows)
├── Cities.xlsx   
├── Departments.xlsx   
├── Readmme.md   
├── Screenshots/
  └── dashboard.png    
  └── insight & recommendation.png            

```


## Skills Demonstrated

Data cleaning and validation · Power Query (ETL) · Data modelling · PivotTables · Dashboard design · KPI definition · Business insight and recommendation writing

