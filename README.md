# 📊 **Financial Risk Analytics Dashboard – End-to-End Power BI Project**

This project presents a **three-page interactive Power BI dashboard** that analyzes **loan risk, borrower behavior, demographic trends, and default patterns**. It is built to support financial institutions, credit analysts, and risk teams in making data-driven decisions.

---

# 🧾 **Table of Contents**

1. [📌 Project Overview](#-project-overview)
2. [🎯 Objectives](#-objectives)
3. [📂 Dataset Description](#-dataset-description)
4. [🛠️ Data Preparation & Cleaning](#️-data-preparation--cleaning)
5. [📐 Data Modeling (Star Schema)](#-data-modeling-star-schema)
6. [📄 Dashboard Pages](#-dashboard-pages)

   * Page 1: Loan Default & Overview
   * Page 2: Applicant Demographics & Financial Profile
   * Page 3: Financial Risk Metrics
7. [📈 Key Insights](#-key-insights)
8. [🎨 UI/UX & Theme](#-uiux--theme)
9. [🧮 DAX Measures Used](#-dax-measures-used)
10. [📦 Project Folder Structure](#-project-folder-structure)
11. [🚀 How to Use the Dashboard](#-how-to-use-the-dashboard)
12. [💡 Future Enhancements](#-future-enhancements)
13. [📧 Contact](#-contact)

---

# 📌 **Project Overview**

The **Financial Risk Analytics Dashboard** provides a comprehensive view of:

* Borrower creditworthiness
* Loan performance patterns
* Demographic-based loan behavior
* Default risk trends over multiple years

It is designed to help financial teams **visualize, compare, and interpret risk factors** across income groups, credit score categories, employment types, and more.

The dashboard is divided into **three analytical pages**, each serving a unique purpose.

---

# 🎯 **Objectives**

✔ Identify **default trends** across years and borrower categories
✔ Compare loan amounts across demographic segments
✔ Evaluate borrower risk using **credit score**, **income**, and **employment**
✔ Understand loan purpose patterns
✔ Provide a visual storytelling report for decision-making

---

# 📂 **Dataset Description**

The dataset contains information on loan applicants with the following key attributes:

### Loan Attributes

* **LoanID**: Unique identifier for each loan
* **Loan Amount**: The amount of money borrowed
* **Loan Purpose**: Purpose of the loan (Auto, Business, Education, Home, Other)
* **Loan Date**: Date when the loan was issued
* **Interest Rate**: Annual interest rate on the loan
* **Loan Term**: Duration of the loan in months
* **DTI Ratio**: Debt-to-income ratio
* **Default**: Binary indicator (1 = Default, 0 = No Default)

### Applicant Attributes

* **Age**: Age of the applicant
* **Income**: Annual income of the applicant
* **Education**: Education level (High School, Bachelor's, Master's, PhD)
* **Employment Type**: Employment status (Full-time, Part-time, Self-employed, Unemployed)
* **Marital Status**: Marital status (Single, Married, Divorced)
* **Has Mortgage**: Whether the applicant has a mortgage (Yes/No)
* **Has Dependents**: Whether the applicant has dependents (Yes/No)
* **Credit Score**: Credit score of the applicant
* **Months Employed**: Number of months in current employment
* **Number of Credit Lines**: Number of credit lines available to the applicant

---

# 🛠️ **Data Preparation & Cleaning**

Data was extracted from **Microsoft SQL Server** and processed using **Power Query**:

✔ Removed duplicates
✔ Imputed missing values
✔ Categorized credit score into bins
✔ Created custom age groups
✔ Standardized categorical fields
✔ Converted dates into year level
✔ Built dimension tables for better model performance
✔ Connected to data source using **on-premise gateway** for secure data access

---

# 📐 **Data Modeling (Star Schema)**

A clean **Star Schema** was designed:

### **Fact Tables**

* **Fact_Loan**
* **Fact_Applicant**

### **Dimension Tables**

* Dim_AgeGroup
* Dim_Education
* Dim_EmploymentType
* Dim_MaritalStatus
* Dim_CreditScoreBins
* Dim_IncomeBracket
* Dim_LoanPurpose
* Dim_Date

Relationships are **one-to-many** with single-direction filtering.

---

# 📄 **Dashboard Pages**

Below is the complete page-wise breakdown.

---

# 🟣 **PAGE 1 — Loan Default & Overview**

This page provides a **macro view** of loan performance and default risks.

### Visuals:

* **Loan Amount by Purpose**
* **Average Income by Employment Type**
* **Default Rate by Employment Type**
* **Average Loan Amount by Age Group**
* **Default Rate (%) by Year**

### Purpose:

To understand:

* Which loan types dominate
* How employment type relates to risk
* Yearly default fluctuations
* How age influences loan amount

---

# 🟠 **PAGE 2 — Applicant Demographics & Financial Profile**

This page explores **borrower characteristics** and their loan behavior.

### Visuals:

* **Median Loan Amount by Credit Score Category**
* **Average Loan Amount (High Credit) by Age Group + Marital Status** (Donut Chart)
* **Total Loan (Adults) by Credit Score Bins**
* **Total Loan (Middle Age Adults) by Mortgage/Dependents**
* **Number of Loans by Education Type**

### Purpose:

To analyze:

* How credit score influences loan size
* How demographics correlate with borrowing behavior
* The impact of dependents/mortgage on loan amounts
* Education-wise loan distribution

---

# 🔵 **PAGE 3 — Financial Risk Metrics**

This page focuses on **high-level risk assessment** and patterns.

### Visuals:

* **YOY Default Loans Change by Year** (two variations)
* **YTD Loan Amount by Credit Score Bins & Marital Status** (Sankey)
* **Loan Flow: Income Bracket → Employment Type** (Sankey)

### Purpose:

To uncover:

* Year-over-year shifts in loan default
* Credit score & marital status influence
* Employment type based on income bracket

---

# 📈 **Key Insights**

### 🔥 Risk & Default Insights

* YOY default peaked in **2015–2016**, then slowed.
* **Unemployed** applicants show the **highest default rate**.
* **Full-time employees** have the **lowest default rate (2.4%)**.

### 🔥 Income & Employment Patterns

* High-income borrowers take **larger loans** but show **lower risk**.
* Most stable employment types (full-time) also have **better credit profiles**.

### 🔥 Demographic Insights

* Adults & middle-aged applicants take **higher loan amounts**.
* Bachelor's degree holders account for the **highest number of loans**.

### 🔥 Credit Score Trends

* Low credit score group has **lowest median loan amounts**.
* Medium & High credit bins are the primary contributors to overall loan volume.

---

# 🎨 **UI/UX & Theme**

A custom theme was created featuring:

🎨 **Lavender + Maroon palette**
🧼 Clean card layouts
📏 Consistent spacing & margin structure
🖼 Rounded corners for visuals
🔎 High contrast titles & labels
📁 Transparent icons for slicers & filters

This ensures a **modern, professional, and finance-focused visual identity**.

---

# 🧮 **DAX Measures Used**

Some essential DAX formulas include:

```DAX
Total Loan Amount = SUM(Fact_Loan[LoanAmount])

Default Rate % =
DIVIDE(
    SUM(Fact_Loan[DefaultFlag]),
    COUNT(Fact_Loan[LoanID])
)

YOY Default Change =
VAR PrevYear = CALCULATE([Default Rate %], DATEADD(Dim_Date[Date], -1, YEAR))
RETURN [Default Rate %] - PrevYear

Median Loan Amount =
MEDIAN(Fact_Loan[LoanAmount])
```

(Additional measures included for education, income groups, and age segments.)

---

# 📦 **Project Folder Structure**

```
Financial-Risk-Analytics-Dashboard/
│
├── data/
│   ├── Loan_default.csv
│   └── Store+Data.xlsx
│
├── pbix/
│   └── Loan Default.pbix
│
├── images/
│   ├── Loan default and overview page 1 (1).png
│   ├── applicant demographics and financial profile page 2.png
│   └── financial risk metrics page 3.png
│
└── README.md
```

### 🖼️ **Dashboard Preview Images**

* **Page 1 - Loan Default & Overview**: ![Page 1](https://github.com/SamyakAnand/Financial-Risk-Analytics-Dashboard-End-to-End-Power-BI-Project/blob/main/Loan%20default%20and%20overview%20page%201%20(1).png)
* **Page 2 - Applicant Demographics & Financial Profile**: ![Page 2](https://github.com/SamyakAnand/Financial-Risk-Analytics-Dashboard-End-to-End-Power-BI-Project/blob/main/applicant%20demographics%20and%20financial%20profile%20page%202.png)
* **Page 3 - Financial Risk Metrics**: ![Page 3](https://github.com/SamyakAnand/Financial-Risk-Analytics-Dashboard-End-to-End-Power-BI-Project/blob/main/financial%20risk%20metrics%20page%203.png)

---

# 🚀 **How to Use the Dashboard**

1. Download the repository
2. Open the `.pbix` file in **Power BI Desktop**
3. Use slicers on each page to explore:

   * Age groups
   * Income bracket
   * Credit score bins
   * Marital status
   * Employment type
4. Move across the 3 pages to view different perspectives of the analysis

---

# 💡 **Future Enhancements**

🔹 Add Machine Learning prediction integration (loan default model)
🔹 Create AI-generated insights panel
🔹 Add drill-through pages for applicant profiles
🔹 Add tooltips with micro-summary KPIs
🔹 Enable automatic data refresh using Power BI Gateway

---

# 📧 **Contact**

For improvements or collaborative projects:

**Samyak Anand**
📩 Email: *your-email*
🔗 LinkedIn: *your-link*
🌐 Portfolio: *your-portfolio*

---

If you want, I can also:
✅ Provide **GitHub formatting with embedded images**
✅ Generate a **PDF version** of this README
✅ Create a **LinkedIn project post**

Just tell me!"# Financial-Risk-Analytics-Dashboard-End-to-End-Power-BI-Project" 
