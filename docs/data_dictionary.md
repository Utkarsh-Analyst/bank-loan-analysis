# 📖 Data Dictionary — Bank Loan Dataset

This document describes all fields used in the Bank Loan Analysis Power BI report.

---

## 📋 Loan Data Fields

| Field Name | Data Type | Description | Example Values |
|---|---|---|---|
| `id` | Integer | Unique identifier for each loan | 1001, 1002, ... |
| `issue_date` | Date | Date the loan was issued | 2021-01-15 |
| `loan_status` | Text | Current repayment status of the loan | Fully Paid, Charged Off, Current |
| `loan_amount` | Decimal | Total loan amount issued (in USD) | 10000, 25000 |
| `total_payment` | Decimal | Total amount received from borrower (in USD) | 12000, 8000 |
| `int_rate` | Decimal (%) | Annual interest rate on the loan | 0.1299 (12.99%) |
| `dti` | Decimal | Debt-to-Income ratio of the borrower | 18.5 |
| `grade` | Text | Credit grade assigned by the lender | A, B, C, D, E, F, G |
| `sub_grade` | Text | Sub-level within the grade | A1, B3, C5 |
| `term` | Text | Duration of the loan | 36 months, 60 months |
| `purpose` | Text | Stated purpose of the loan | debt_consolidation, home_improvement, car |
| `home_ownership` | Text | Borrower's home ownership status | RENT, OWN, MORTGAGE |
| `emp_length` | Text | Length of borrower's employment | < 1 year, 2 years, 10+ years |
| `address_state` | Text | US state of the borrower (2-letter code) | CA, TX, NY, FL |

---

## 🧮 Calculated Columns

| Column Name | Logic | Description |
|---|---|---|
| `Good v Bad Loan` | IF loan_status IN ("Fully Paid", "Current") → "Good Loan" ELSE "Bad Loan" | Classifies each loan for risk analysis |
| `Month` | MONTH(issue_date) | Extracted month number for time-based slicing |

---

## 📊 Loan Status Reference

| Status | Classification | Meaning |
|---|---|---|
| Fully Paid | ✅ Good Loan | Borrower has fully repaid the loan |
| Current | ✅ Good Loan | Loan is active and payments are on time |
| Charged Off | ❌ Bad Loan | Loan written off as a loss |
| Default | ❌ Bad Loan | Borrower has defaulted on payments |
| Late (31-120 days) | ❌ Bad Loan | Significantly overdue payments |

---

## 🏠 Home Ownership Values

| Value | Description |
|---|---|
| RENT | Borrower rents their home |
| OWN | Borrower owns their home outright |
| MORTGAGE | Borrower has a mortgage |
| OTHER | Other arrangement |

---

## 🎯 Loan Purpose Values

| Value | Description |
|---|---|
| debt_consolidation | Consolidating existing debts |
| home_improvement | Home renovation/repair |
| major_purchase | Large one-time purchase |
| car | Vehicle purchase |
| medical | Medical expenses |
| small_business | Business funding |
| vacation | Travel/vacation |
| credit_card | Credit card payoff |
| other | Other purposes |

---

## 📐 Grade Reference (Credit Risk)

| Grade | Risk Level | Typical Interest Range |
|---|---|---|
| A | Lowest Risk | ~5% – 9% |
| B | Low Risk | ~9% – 13% |
| C | Medium Risk | ~13% – 16% |
| D | Medium-High Risk | ~16% – 20% |
| E | High Risk | ~20% – 24% |
| F | Very High Risk | ~24% – 28% |
| G | Highest Risk | ~28%+ |
