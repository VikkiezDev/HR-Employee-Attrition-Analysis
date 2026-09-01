# HR-Employee-Attrition-Analysis

## List of columns to discard
- DailyRate
- DistanceFromHome
- EducationField
- EmployeeCount
- HourlyRate
- JobLevel
- MonthlyRate
- Over18
- RelationshipSatisfaction
- StandardHours
- StockOptionLevel
- TrainingTimesLastYear

## 1. Feature Engineering (Grouping & Bins)
- Raw continuous numbers are hard to slice in Pivot Tables.
- Create custom grouped categories using Add Column → Conditional Column:
    - Age Group: Group Age into readable brackets:< 25 | 25-34 | 35-49 | 50+
    - Income Level: Group MonthlyIncome to spot pay disparities:< $3,000 | $3,000 - $6,000 | $6,001 - $10,000 | > $10,000
    - Tenure Band: Group YearsAtCompany to analyze when employees typically leave:0-1 Year (High Risk) | 2-5 Years | 6-10 Years | 10+ Years
## 2. Standardize Ratings into Text Labels
- Columns like EnvironmentSatisfaction, JobInvolvement, JobSatisfaction, PerformanceRating, and WorkLifeBalance are stored as numbers (1 to 4).
- Pivot Tables report these as averages by default (e.g., "3.2"), which loses clarity.
- Replace values or add a conditional column to convert numerical codes into clear descriptions:
    - 1 $\rightarrow$ 1 - Low
    - 2 $\rightarrow$ 2 - Medium
    - 3 $\rightarrow$ 3 - High
    - 4 $\rightarrow$ 4 - Very High(Including the number prefix like 1 - Low keeps them sorted logically in your Pivot Charts rather than alphabetically).
## 3. Data Types & Formatting Verification
- Ensure every remaining column has an explicitly assigned data type (look at the icon next to the column header):
    - Whole Number (123): Age, NumCompaniesWorked, PercentSalaryHike, TotalWorkingYears, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager.
    - Currency ($) or Whole Number: MonthlyIncome.
    - Text (abc): Attrition, BusinessTravel, Department, Education, Gender, JobRole, MaritalStatus, OverTime, and your new engineered bands.
## 4. Create an Attrition Flag (Numeric 0/1)
Power Query produces text Yes/No for Attrition. While great for slicers, text cannot be averaged.
- Add a custom column named Attrition Numeric:
    - if [Attrition] = "Yes" then 1 else 0
- Change its type to Whole Number.
- Why? In Excel Pivot Tables, AVERAGE(Attrition Numeric) automatically calculates your exact Attrition Rate % without needing complex DAX or calculated fields.
