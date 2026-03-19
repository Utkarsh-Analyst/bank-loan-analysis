# 🏦 Bank Loan Analysis Dashboard — Power BI

A comprehensive **Bank Loan Performance & Risk Analysis** dashboard built in Power BI, designed to help financial analysts and loan officers monitor lending activity, track portfolio health, and distinguish between good and bad loan distributions.

---

## 📊 Dashboard Overview

The report is structured across **3 interactive pages**:

| Page | Description |
|------|-------------|
| **Summary** | High-level KPIs — total applications, funded amounts, repayments, interest rates, DTI |
| **Overview** | Visual trends — area charts, geographic maps, treemaps, bar charts, donut charts |
| **Details** | Granular loan-level table with full filtering capability |

---

## 🖼️ Screenshots

> *(Add screenshots of your dashboard pages here)*

| Summary Page | Overview Page | Details Page |
|---|---|---|
| ![Summary](screenshots/summary.png) | ![Overview](screenshots/overview.png) | ![Details](screenshots/details.png) |

---

## 📌 Key Metrics Tracked

### 💰 Loan Volume
- **Total Loan Applications** — with MTD & MoM comparisons
- **Total Funded Amount** — MTD & MoM
- **Total Amount Received** — MTD & MoM

### 📈 Risk Indicators
- **Average Interest Rate** — MTD & MoM
- **Average DTI (Debt-to-Income Ratio)** — MTD & MoM

### ✅ Loan Quality Split
| Category | Metrics |
|----------|---------|
| **Good Loans** | Good Loan %, Applications, Funded Amount, Total Received |
| **Bad Loans** | Bad Loan %, Applications, Funded Amount, Total Received |

---

## 🗂️ Data Fields Used

| Field | Description |
|-------|-------------|
| `id` | Unique loan identifier |
| `issue_date` | Date loan was issued |
| `loan_status` | Current status of the loan |
| `grade` / `sub_grade` | Credit grade assigned to the loan |
| `term` | Loan term (36 or 60 months) |
| `purpose` | Purpose of the loan |
| `home_ownership` | Borrower's home ownership status |
| `emp_length` | Employment length of the borrower |
| `address_state` | Borrower's state (used for map visual) |
| `Good v Bad Loan` | Calculated classification column |

---

## 📐 DAX Measures

<details>
<summary>Click to expand all measures</summary>

```dax
-- Volume Metrics
Total Loan Applications = COUNT(loan_data[id])
Total Funded Amount = SUM(loan_data[loan_amount])
Total Amount Received = SUM(loan_data[total_payment])

-- Month-to-Date
MTD Loan Applications = TOTALMTD(COUNT(loan_data[id]), loan_data[issue_date])
MTD Funded Amount = TOTALMTD(SUM(loan_data[loan_amount]), loan_data[issue_date])
MTD Total Amount Received = TOTALMTD(SUM(loan_data[total_payment]), loan_data[issue_date])

-- Month-over-Month (%)
MoM Loan Applications = ([MTD Loan Applications] - [PMTD Loan Applications]) / [PMTD Loan Applications]
MoM Total Funded Amount = ([MTD Funded Amount] - [PMTD Funded Amount]) / [PMTD Funded Amount]
MoM Total Amount Received = ([MTD Total Amount Received] - [PMTD Total Amount Received]) / [PMTD Total Amount Received]

-- Risk Metrics
Avg Interest Rate = AVERAGE(loan_data[int_rate])
Avg DTI = AVERAGE(loan_data[dti])

-- Good Loan Metrics
Good Loan % = (COUNTROWS(FILTER(loan_data, loan_data[Good v Bad Loan] = "Good Loan")) / COUNT(loan_data[id]))
Good Loan Applications = COUNTROWS(FILTER(loan_data, loan_data[Good v Bad Loan] = "Good Loan"))
Good Loan Funded Amount = SUMX(FILTER(loan_data, loan_data[Good v Bad Loan] = "Good Loan"), loan_data[loan_amount])
Good Loan Total Received = SUMX(FILTER(loan_data, loan_data[Good v Bad Loan] = "Good Loan"), loan_data[total_payment])

-- Bad Loan Metrics
Bad Loan % = (COUNTROWS(FILTER(loan_data, loan_data[Good v Bad Loan] = "Bad Loan")) / COUNT(loan_data[id]))
Bad Loan Applications = COUNTROWS(FILTER(loan_data, loan_data[Good v Bad Loan] = "Bad Loan"))
Bad Loan Funded Amount = SUMX(FILTER(loan_data, loan_data[Good v Bad Loan] = "Bad Loan"), loan_data[loan_amount])
Bad Loan Total Received = SUMX(FILTER(loan_data, loan_data[Good v Bad Loan] = "Bad Loan"), loan_data[total_payment])
```

</details>

---

## 🔍 Visuals Used

| Visual | Used On |
|--------|---------|
| Card Visuals | Summary, Overview, Details |
| Donut Chart | Summary, Overview |
| Area Chart | Overview |
| Shape Map (USA States) | Overview |
| Treemap | Overview |
| Bar Chart | Overview |
| Table | Summary, Details |
| Slicers | All Pages |

### Slicers / Filters Available
- 📅 **Month / Issue Date**
- 🏠 **Home Ownership**
- 🎯 **Loan Purpose**
- 📊 **Grade**
- 📋 **Loan Status**
- ⏳ **Term**
- 💼 **Employee Length**

---

## 🚀 How to Use

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/bank-loan-analysis.git
   ```

2. **Open the report**
   - Open `bank_loan.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/)

3. **Connect your data** *(if using your own dataset)*
   - Go to **Home → Transform Data → Data Source Settings**
   - Point to your loan data CSV/database

4. **Publish** *(optional)*
   - Go to **Home → Publish** to share on Power BI Service

---

## 📁 Repository Structure

```
bank-loan-analysis/
│
├── bank_loan.pbix          # Main Power BI report file
├── README.md               # Project documentation
│
├── screenshots/            # Dashboard screenshots
│   ├── summary.png
│   ├── overview.png
│   └── details.png
│
├── data/                   # Sample or reference data
│   └── sample_data.csv     # (Add your dataset here)
│
└── docs/                   # Additional documentation
    └── data_dictionary.md  # Field descriptions
```

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Microsoft](https://img.shields.io/badge/Microsoft-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

- **Power BI Desktop** — Report authoring
- **DAX** — All custom measures and KPIs
- **Power Query (M)** — Data transformation
- **USA Topographic Map** — Built-in shape map

---

## 👤 Author

**Utkarsh**
- GitHub: [Utkarsh-Analyst](https://github.com/your_username)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
