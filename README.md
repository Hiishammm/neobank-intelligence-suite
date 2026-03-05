# neobank-intelligence-suite[README.md](https://github.com/user-attachments/files/25756263/README.md)
# 🏦 NeoBank Intelligence Suite
### Enterprise-Grade Power BI Dashboard · Financial & Risk Analytics · FY 2020–2025

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL Server](https://img.shields.io/badge/SQL%20Server-2019-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-45%20Measures-0078D4?style=for-the-badge)
![Deneb](https://img.shields.io/badge/Deneb-Vega--Lite-FF6B6B?style=for-the-badge)

---

## 📊 Dashboard Preview

| Page | Description |
|------|-------------|
| 🏦 Executive Overview | P&L Waterfall · KPIs · Funnel · Channels · AI Recommendations |
| 🛡 Loan Portfolio & Risk | NPL Heatmap · DPD Aging · Provision Analysis · Risk Summary |
| 💹 P&L Deep Dive | Revenue Trend · Margin Analysis · Full Income Statement |
| 🎯 Marketing & Customer | CAC by Channel · Segments · Conversion Donut · Funnel |
| 🔮 Forecasting & Trends | Revenue Forecast · NPL Prediction · Rolling Averages |

---

## 🚀 Key Metrics (FY 2025)

```
Total Revenue      →  3.55B EGP       Net Profit       →  1.70B EGP
Gross Margin       →  85.3%           EBITDA Margin    →  63.1%
NPL Ratio          →  1.49%           Provision Cover  →  490%
Total Portfolio    →  3.82B EGP       Loans at Risk    →  262M EGP
Avg CAC            →  144 EGP         Marketing ROI    →  3.0x
Conversion Rate    →  16.33%          Active Customers →  5K
```

---

## 🛠 Tech Stack

| Component | Technology |
|-----------|-----------|
| **BI Tool** | Power BI Desktop |
| **Database** | SQL Server 2019 — NeoBankDW |
| **Data Model** | Star Schema (6 tables) |
| **Measures** | 45+ DAX measures |
| **Custom Visuals** | Deneb (Vega-Lite), HTML Content |
| **Canvas Size** | 1600 × 1260 px |
| **Theme** | Custom Dark (#06080F background) |

---

## 🗄 Data Model

```
DimDate ──────────────────────────────────────┐
DimCustomer ──────────────────────────────┐   │
DimProduct ───────────────────────────┐   │   │
                                      ↓   ↓   ↓
                               FactLoans
                               FactTransactions
                               FactMarketing
```

### Tables

| Table | Rows | Description |
|-------|------|-------------|
| `DimDate` | 2,191 | Calendar FY 2020–2025 |
| `DimCustomer` | 5,000 | Customer master with Segment/RFM |
| `DimProduct` | 10 | Loan products & interest rates |
| `FactLoans` | 15,000 | Loan book with DPD & provisions |
| `FactTransactions` | 500K+ | Daily transaction ledger |
| `FactMarketing` | 2,600 | Campaign leads & conversions |

---

## 📐 DAX Measures (45+)

### P&L Measures
```dax
Total Revenue = SUMX(FactTransactions, FactTransactions[Amount])
Gross Profit = [Total Revenue] - [Total COGS]
EBITDA = [Gross Profit] - [Total OpEx]
Net Profit = [EBITDA] - [Total Provisions]
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)
Net Profit Margin % = DIVIDE([Net Profit], [Total Revenue], 0)
Cost to Income Ratio = DIVIDE([Total OpEx], [Total Revenue], 0)
```

### NPL & Risk Measures
```dax
NPL Amount = CALCULATE([Total Outstanding], FactLoans[LoanStatus] IN {"Doubtful","Loss"})
NPL Ratio = DIVIDE([NPL Amount], [Total Outstanding], 0)
Provision Coverage Ratio = DIVIDE([Total Provisions Balance], [NPL Amount], 0)
Cost of Risk = DIVIDE([Total Provisions Balance], [Total Outstanding], 0)
Loans at Risk = CALCULATE([Total Outstanding], FactLoans[LoanStatus] IN {"Substandard","Doubtful","Loss"})
```

### Marketing Measures
```dax
Conversion Rate = DIVIDE([Total Converted], [Total Leads], 0)
Avg CAC = DIVIDE([Total Marketing Spend], [Total Converted], 0)
Marketing ROI = DIVIDE([Total Revenue from Marketing], [Total Marketing Spend], 0)
Customer LTV = DIVIDE([Total Revenue], [Active Customers], 0)
```

### Time Intelligence
```dax
Revenue YTD = CALCULATE([Total Revenue], DATESYTD(DimDate[FullDate]))
Revenue YoY % = DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY], 0)
Revenue Rolling 12M = CALCULATE([Total Revenue], DATESINPERIOD(DimDate[FullDate], LASTDATE(DimDate[FullDate]), -12, MONTH))
NPL Forecast = [NPL Ratio] * 1.5
Profit Forecast = [Net Profit] * 1.05
```

---

## 🎨 Custom Visuals (Deneb / Vega-Lite)

### 1. P&L Waterfall Chart (Page 1)
- 7-bar waterfall: Revenue → COGS → Gross Profit → OpEx → EBITDA → Provisions → Net Profit
- Color-coded: Cyan (start) · Red (negative) · Green (positive)
- Rounded corners + value labels

### 2. NPL Ratio Heatmap (Page 2)
- Year × Month matrix
- Color scale: Dark → Purple → Pink (low → high NPL)
- Interactive tooltip with exact NPL %

### 3. DPD Aging Bars (Page 2)
- Horizontal bars by Loan Status
- Color-coded: Green (Current) → Red (Loss)

### 4. Provision vs Outstanding (Page 2)
- Grouped bars: Provision (colored) vs Outstanding (dark background)
- Filtered to risk buckets only (excl. Current)

### 5. Revenue vs Net Profit (Page 3)
- Combo: Bar (Revenue) + Line (Net Profit)
- By Fiscal Year with dashed forecast line

### 6. Margin Analysis (Page 3)
- 3-line chart: Gross · EBITDA · Net margins
- By year with interactive legend

### 7. CAC by Channel (Page 4)
- Horizontal bars sorted by CAC value
- Color-coded by channel type

### 8. Customer Segments (Page 4)
- Vertical bars with value labels
- 5 segments: Corporate · Micro Business · Premium Retail · Retail · SME

### 9. Conversions Donut (Page 4)
- Donut chart with channel labels + values
- Inner radius for clean look

### 10. Revenue Forecast Trend (Page 5)
- Bar + dashed line combo
- Actual vs Rolling 12M

### 11. NPL Actual vs Forecast (Page 5)
- Dual line: Actual (purple) · Forecast (red dashed)
- By fiscal year

---

## 📱 Pages Overview

### Page 1 — Executive Overview
```
Header (gradient, live badge)
5 KPI Cards: Revenue · Net Profit · NPL · CAC · Conversion
P&L Waterfall (Deneb)
Risk Panel (HTML) with DPD distribution
Acquisition Funnel · Channel Performance · AI Recommendations
```

### Page 2 — Loan Portfolio & Risk
```
Header (purple theme)
4 KPI Cards: NPL Amount · Coverage · Loans at Risk · Cost of Risk
NPL Heatmap · DPD Aging · Provision vs Outstanding
Risk Summary Panel (8 metrics + AI assessment)
```

### Page 3 — P&L Deep Dive
```
Header (green theme)
4 KPI Cards: Revenue YTD · EBITDA · Gross Profit · Cost to Income
Revenue vs Net Profit Bar+Line · Margin Analysis 3-line
Full P&L Statement Summary (8 metrics + insights)
```

### Page 4 — Marketing & Customer
```
Header (yellow theme)
4 KPI Cards: Leads · CAC · LTV · Active Customers
CAC by Channel · Customer Segments · Conversions Donut
Marketing Performance Summary (7 metrics + opportunities)
```

### Page 5 — Forecasting & Trends
```
Header (blue theme)
4 KPI Cards: Revenue Forecast · NPL Forecast · Profit · Growth
Revenue Trend · NPL Actual vs Forecast
Forecast Summary Panel (6 metrics + insights)
```

---

## 🎯 Business Insights Generated

1. **NPL at 1.49%** — below 2% threshold, portfolio is healthy ✅
2. **Provision Coverage 490%** — overcollateralized, potential release of ~85M EGP 💡
3. **Email CAC lowest** at ~50 EGP vs Branch at ~295 EGP — budget shift opportunity 📊
4. **LTV/CAC ratio 4,930x** — exceptional customer economics 🚀
5. **NPL forecast trending up to 2.23%** — monitor SME book ⚠️
6. **Gross Margin 85.3%** — strong pricing power in loan products 💰

---

## 🚀 How to Run

### Prerequisites
```
- Power BI Desktop (latest)
- SQL Server 2019+
- Custom Visuals: Deneb, HTML Content by Daniel Marsh-Patrick
```

### Setup
```sql
-- 1. Restore/Create NeoBankDW database
-- 2. Run SQL scripts in order:
--    01_DimDate.sql
--    02_DimCustomer.sql
--    03_DimProduct.sql
--    04_FactLoans.sql
--    05_FactTransactions.sql
--    06_FactMarketing.sql

-- 3. Open NeoBank_Intelligence_Suite_v1.pbix
-- 4. Update connection string to your SQL Server instance
-- 5. Refresh data
```

---

## 👨‍💻 Author

**Hisham Mahmoud**
Data Analyst · Power BI Developer · Financial Analytics

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Hisham%20Mahmoud-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hiisham-mahmooud)
[![Email](https://img.shields.io/badge/Email-hiishammahmooud%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:hiishammahmooud@gmail.com)
[![Phone](https://img.shields.io/badge/Phone-%2B201050542047-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/201050542047)

> *This dashboard demonstrates enterprise-level financial analytics capabilities for a NeoBank, covering the full spectrum from P&L reporting to credit risk management and marketing analytics.*

---

⭐ **Star this repo if you found it useful!**
