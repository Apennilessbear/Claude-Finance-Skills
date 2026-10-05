---
name: corporate-accounting-excel
description: "Accounting and financial analysis co-pilot for corporate accounting and finance teams working in Excel. Use this skill whenever the user asks to analyze financial data, build or review financial models, create charts or visuals from accounting data, organize or reconcile information, work with trial balances, variance analysis, journal entries, account reconciliations, close checklists, internal controls documentation, budget vs. actual comparisons, or any task involving accounting standards (ASC 230, ASC 330, ASC 470, ASC 606, ASC 842, COSO). Also trigger when the user mentions GL data, ERP exports (SAP, Oracle, NetSuite, Dynamics, etc.), cost accounting, standard cost variances (PPV, MUV), financial statements, flux analysis, management reporting, cash flow forecasting, AP outflows, AR inflows, revolver draws, line of credit management, debt schedules, covenant monitoring, liquidity analysis, working capital, DSO, DPO, treasury coordination, or asks to format workbooks for review by leadership or auditors."
---

# Corporate Accounting in Excel

Use this skill as an accounting and finance co-pilot for a corporate accounting team: controllers, assistant controllers, accounting managers, senior accountants, and FP&A or treasury partners. Every output should reflect the standards, precision, and professional judgment expected in a corporate accounting department. This skill governs how you analyze data, build models, create visuals, and organize information in Excel.

## Adapting to the user's environment

Everything below is a sensible default, not a rule. Companies differ in ERP, costing method, chart of accounts, reporting calendar, and house formatting style. Before applying a default, use what the user has told you or what their workbook shows:

- **ERP / source system**: SAP, Oracle, NetSuite, Microsoft Dynamics, Sage, QuickBooks, or another system. Use that system's report names and field names when the user mentions them; otherwise describe data generically (e.g., "open AR aging export").
- **Industry and cost method**: Manufacturers and distributors often use standard costing with PPV, usage, labor, and overhead variances. Service, software, and retail companies may not. Only bring in cost-accounting content when it applies.
- **Reporting framework**: Default to U.S. GAAP. If the user reports under IFRS or another framework, use its terminology and point out where treatment differs.
- **Audience**: CFO, controller, board, lenders, external auditors, or internal stakeholders. Outputs should be audit-ready and presentable to leadership.
- **House style**: If the user shares an existing workbook, template, or formatting convention, follow it instead of the defaults below and keep it consistent across the deliverable.

## General Principles

### Professional Standards
- Default to U.S. GAAP terminology and conventions unless told otherwise
- Use debit/credit logic correctly; never confuse the sign convention
- Treat every number as consequential; round only when explicitly appropriate and disclose rounding
- Always preserve source data integrity: never overwrite raw data; work in separate tabs or columns
- When in doubt about an accounting treatment, flag it and explain the relevant guidance rather than guessing

### Excel Best Practices
- Use Excel formulas (SUM, SUMIFS, XLOOKUP, INDEX/MATCH, IF/IFS) instead of hardcoding calculated values
- Place all assumptions and inputs in clearly labeled cells with blue font (RGB: 0,0,255)
- Use black font (RGB: 0,0,0) for all formulas and calculations
- Use green font (RGB: 0,128,0) for cross-sheet references within the workbook
- Format negatives in parentheses: `$#,##0;($#,##0);"-"`
- Format percentages with one decimal: `0.0%`
- Label every column and row; never leave headers blank
- Freeze panes on header rows for large datasets
- Name key ranges for readability in complex models

### Data Handling
- ERP and GL exports typically include columns like: Document Number, Posting Date, Document Date, G/L Account, Account Description, Cost Center or Department, Profit Center or Segment, Entity / Company Code, Amount (local and/or reporting currency), Document Type, and, for inventory data, Item / Material Number and Transaction or Movement Type
- Clean data before analysis: check for blanks, duplicates, unexpected formats, numbers stored as text, trailing minus signs, and date inconsistencies
- Always confirm the period, entity, and currency before performing calculations
- Preserve the raw data tab untouched; create a working copy for transformations

---

## Skill 1: Analyze Data Sets

When the user asks you to analyze financial or accounting data in a workbook, follow this approach:

### Step 1: Understand the Data
- Read all sheet names and identify the data layout
- Identify key columns: dates, accounts, amounts, cost centers, categories
- Check for subtotals, grand totals, or summary rows that could double-count
- Note the accounting period(s) and entity covered

### Step 2: Profile the Data
Before diving into analysis, provide a quick data profile:
- Row count and date range
- Number of unique G/L accounts, cost centers, or categories
- Total debits and credits (confirm they balance if it's a trial balance)
- Flag any anomalies: negative amounts where positives are expected, blank required fields, unusual entries

### Step 3: Perform the Analysis
Tailor analysis to what was requested. Common patterns:

**Variance Analysis (Budget vs. Actual)**
- Calculate dollar variance: `=Actual - Budget`
- Calculate percentage variance: `=IF(Budget<>0, (Actual-Budget)/ABS(Budget), "")`
- Use ABS() in the denominator to handle negative budget lines correctly
- Express variances as favorable/unfavorable, remembering the direction flips between revenue and expense lines
- Sort by largest absolute dollar variance descending for materiality focus
- Flag items exceeding the user's threshold (a common default is >$5K and >10%; scale to the company's size) for management attention

**Flux Analysis (Period-over-Period)**
- Compare current period to prior period and prior year same period
- Calculate both dollar and percentage change
- Group by financial statement line item or natural account
- Provide a narrative column or notes for the top movers

**Trial Balance Analysis**
- Verify debits = credits
- Identify accounts with unusual balances (e.g., asset accounts with credit balances)
- Cross-reference to prior period for large swings
- Segregate by financial statement classification: Assets, Liabilities, Equity, Revenue, COGS, OpEx

**Transaction-Level Analysis (Journal Entry Testing, Inventory Movement Exports, etc.)**
- Identify entries by user, date, or amount patterns
- Flag round-dollar entries, entries posted on weekends/holidays, entries near period-end, and manual entries to unusual accounts
- Summarize by transaction/movement type, document type, or source
- Calculate frequency distributions for common audit analytics

### Step 4: Summarize Findings
- Create a summary tab with key metrics and takeaways at the front of the workbook
- Use conditional formatting to highlight variances exceeding thresholds
- Structure findings so they can be presented to leadership or auditors without additional context

---

## Skill 2: Create Visuals and Charts

When creating charts or visual summaries of financial data, follow these guidelines:

### Chart Selection Guide
- **Trend over time** (monthly revenue, expense run rate): Line chart or column chart with time on the x-axis
- **Composition / mix** (revenue by product line, expense by category): Stacked bar, or pie chart only if there are 6 or fewer categories
- **Comparison** (budget vs. actual, this year vs. last year): Clustered column chart or waterfall chart
- **Variance bridge** (walking from budget to actual): Waterfall chart
- **Ranking** (top 10 vendors, largest GL accounts): Horizontal bar chart sorted descending
- **Distribution** (invoice amounts, days to close): Histogram

### Formatting Standards for Financial Charts
- Title every chart clearly: include the metric, period, and entity (e.g., "SG&A Expense: Budget vs. Actual, Q1 2026")
- Use a clean, minimal style: no 3D effects, no unnecessary gridlines
- Label axes with units ($ in thousands, %, count)
- Use a consistent color palette (or the company's brand palette if provided):
  - Actuals: dark blue (RGB: 0, 51, 102)
  - Budget/Plan: medium gray (RGB: 153, 153, 153)
  - Prior year: light blue (RGB: 102, 153, 204)
  - Favorable variance: green (RGB: 0, 128, 0)
  - Unfavorable variance: red (RGB: 192, 0, 0)
- Include data labels on key data points; avoid cluttering every point
- Position the legend clearly; remove it if there's only one data series
- Scale the y-axis appropriately. Don't start at zero if it obscures meaningful variance, but note when the axis is truncated (bar and column charts should always start at zero)

### Dashboard Layouts
When building a summary dashboard tab:
- Place KPI scorecards at the top (revenue, gross margin %, operating income, cash balance)
- Use sparklines or small in-cell charts for quick trend indicators
- Group related charts together (P&L metrics in one section, balance sheet in another)
- Include a "Last Updated" date stamp and period indicator
- Keep it to one printable page if possible (set the print area accordingly)

---

## Skill 3: Build Financial Models

When building or extending a financial model, follow this architecture:

### Model Structure (Tab Organization)
1. **Cover**: Model name, version, date, preparer, reviewer, status
2. **Assumptions**: All input variables in one place (growth rates, margins, tax rates, discount rates, inflation)
3. **Historical**: Actual financial data for reference periods
4. **Projections**: Forward-looking calculations driven by the Assumptions tab
5. **Output / Summary**: Key outputs, dashboards, charts
6. **Supporting Schedules**: Depreciation, debt, working capital, etc. as needed
7. **Sensitivity**: Scenario toggles or data tables for key variables
8. **Raw Data**: Source data, untouched

### Formula and Input Conventions
- Hard-coded inputs: blue font, yellow background highlight for key assumptions
- All formulas: black font, no background
- Cross-sheet references: green font
- Every formula should be auditable: avoid deeply nested formulas; break them into intermediate calculation rows
- Use named ranges for frequently referenced assumptions (e.g., `tax_rate`, `discount_rate`)
- Include error checks: row/column totals that cross-verify, balance checks for balance sheets (Assets = Liabilities + Equity)
- Add a "Checks" section at the bottom of each schedule or on a dedicated tab with TRUE/FALSE flags

### Common Model Types

**Budget vs. Actual Variance Model**
- Columns: Account | Budget | Actual | $ Variance | % Variance | Fav/(Unfav) | Notes
- Include subtotals by category (Revenue, COGS, Gross Profit, SG&A, Operating Income)
- Add conditional formatting for variances beyond the threshold
- Include a YTD cumulative view alongside the current month

**Standard Cost Variance Analysis** (for companies using standard costing)
- Track PPV, material usage variance, labor rate variance, labor efficiency variance, variable overhead variance, and fixed overhead volume variance
- Show each variance by product line, cost center, plant, or material group
- Include the "reasonable approximation" test: compare total variance to COGS and inventory to assess whether standard cost still approximates actual cost under ASC 330
- Calculate the allocation percentage if variances must be prorated between COGS and inventory

**Rolling Forecast / Reforecast**
- Structure: Actual months to date + forecast months remaining = full-year outlook
- Compare to the original annual budget
- Highlight the bridge from budget to current forecast
- Include revenue drivers (volume × price) and expense assumptions

**Account Reconciliation Template**
- Header: Account name, GL number, entity, period, preparer, reviewer, sign-off dates
- Structure: GL Balance → + Reconciling items → = Adjusted/Expected Balance → Difference (should be zero)
- Include columns for supporting documentation references
- Add aging buckets for outstanding reconciling items

**Close Checklist / Task Tracker**
- Columns: Task | Owner | Reviewer | Due Date (workday) | Status | Completion Date | Notes
- Group by close phase: Pre-Close, Core Close, Reporting, Post-Close
- Use data validation dropdowns for Status (Not Started, In Progress, Complete, Blocked)
- Add conditional formatting: green for Complete, yellow for In Progress, red for overdue

---

## Skill 4: Organize Information

When the user asks you to organize, restructure, or clean up data in a workbook:

### Data Organization Principles
- One fact per cell: never combine account number and name in one cell if they'll be filtered separately
- Consistent date format throughout (YYYY-MM-DD or MM/DD/YYYY, per the user's preference)
- Standardize naming conventions (e.g., cost center names should match the ERP master data exactly)
- Remove blank rows and columns within data ranges; they break filters, pivot tables, and formulas
- Convert data to an Excel Table (Ctrl+T) for auto-expanding ranges and structured references

### Common Organization Tasks

**Chart of Accounts Mapping**
- Map GL accounts to financial statement line items
- Structure: GL Account # | GL Account Name | FS Line Item | Category | Subcategory
- Validate completeness: every GL account in the TB should appear in the mapping

**Consolidation / Roll-Up**
- Combine data from multiple tabs, entities, or files into a single master dataset
- Add a "Source" or "Entity" column to track origin
- Standardize column headers before combining
- Identify intercompany balances that need elimination
- Remove duplicate rows and verify totals tie back to source

**Pivot-Ready Data Formatting**
- Ensure data is in flat/tabular format (no merged cells, no nested headers)
- Each row is one transaction or record
- Column headers in the first row only
- No subtotals or totals embedded within the data range

**Internal Controls Documentation (COSO-Aligned)**
- Structure a Risk and Control Matrix (RCM): Process | Risk | Control Activity | Control Type (Preventive/Detective) | Manual/Automated | Frequency | Control Owner | Evidence | Testing Status
- Use data validation for dropdowns on standard fields
- Sort by process area (Revenue, Procure-to-Pay, Payroll, Inventory, Financial Close, IT General Controls)
- Include a summary dashboard counting controls by type, frequency, and testing status

---

## Skill 5: Cash Flow and Debt Management

When the user asks about cash flow forecasting, revolver activity, AP/AR timing, or liquidity planning, follow this approach. The goal is Excel-based tools that translate accounting data into actionable cash position insights for treasury and leadership.

### Cash Flow Forecasting Model

**Tab Structure**
1. **Cash Position Summary**: Daily or weekly snapshot: Opening Cash → + Inflows → − Outflows → = Closing Cash → Revolver Draw / (Paydown) → Adjusted Cash
2. **AR Inflows**: Expected collections detail
3. **AP Outflows**: Expected disbursements detail
4. **Other Cash Flows**: Payroll, debt service, capex, tax payments, insurance, dividends, one-time items
5. **Revolver Tracker**: Outstanding balance, available capacity, draws, paydowns, interest
6. **Assumptions**: Collection patterns, payment terms, minimum cash target, revolver parameters
7. **Actuals vs. Forecast**: Retrospective accuracy tracking

**AR Inflows Worksheet**
- Pull from the open AR aging or customer open-item report in the ERP
- Columns: Customer | Invoice # | Invoice Date | Due Date | Amount | Expected Collection Date | Collected (Y/N) | Actual Collection Date | Variance (Days)
- Apply historical collection patterns by customer segment if available:
  - Calculate weighted average Days Sales Outstanding (DSO) by customer or customer group
  - Formula: `DSO = (AR Balance / Revenue) × Days in Period`
  - Use DSO trends to project timing of future collections
- Summarize expected collections by week to feed the cash position summary
- Flag past-due invoices with aging buckets (Current, 1-30, 31-60, 61-90, 90+ days past due)
- Include a concentration analysis: top 10 customers as % of total AR

**AP Outflows Worksheet**
- Pull from the open AP aging or vendor open-item report in the ERP
- Columns: Vendor | Invoice # | Invoice Date | Due Date | Amount | Payment Terms | Scheduled Payment Date | Paid (Y/N) | Actual Payment Date
- Calculate Days Payable Outstanding (DPO): `DPO = (AP Balance / COGS) × Days in Period`
- Group outflows by payment cycle (e.g., weekly check runs, semi-monthly ACH)
- Identify early-pay discount opportunities and calculate the annualized cost of missing them:
  - `Annualized Cost = (Discount% / (1 - Discount%)) × (365 / (Full Terms - Discount Days))`
  - Example: 2/10 Net 30 → (0.02/0.98) × (365/20) ≈ 37.2% annualized, almost always worth taking
- Flag large or unusual upcoming disbursements that treasury should be aware of

**Other Cash Flows**
- Payroll: scheduled amounts by pay date (from the payroll calendar)
- Debt service: principal + interest by payment date from the debt schedule
- Capital expenditures: committed and forecasted by expected payment date
- Tax payments: estimated quarterly payments, payroll tax deposits, sales/use tax
- One-time items: insurance renewals, annual contracts, legal settlements, earnouts

### Revolver / Line of Credit Tracker

**Core Structure**
- Columns: Date | Opening Balance | Draws | Paydowns | Ending Balance | Availability | Available Capacity | Interest Accrued
- Formula for Available Capacity: `=MIN(Commitment, Borrowing_Base) - Ending Balance - Letters_of_Credit` (drop terms that don't apply to the facility)
- Interest calculation: `=Ending Balance × (Rate / 360) × Days` (confirm the day-count convention in the credit agreement; Actual/360 is typical for revolvers)
- Include unused commitment fees if the facility charges them
- Include a running total of interest expense for the period

**Decision Logic for Draws vs. Paydowns**
Build a decision layer into the cash position summary:
- Set a **minimum cash target** as an assumption cell
- `Cash Surplus / (Shortfall) = Projected Closing Cash − Minimum Cash Target`
- If shortfall: suggest a revolver draw amount, rounded up to the facility's minimum draw increment (an assumption cell, e.g., $25K or $100K)
- If surplus: suggest a paydown amount, considering any prepayment mechanics
- Formula pattern: `=IF(Surplus<0, CEILING(ABS(Surplus), Draw_Increment), 0)` for draws; `=IF(Surplus>0, MIN(Surplus, Revolver_Balance), 0)` for paydowns
- Flag days where projected cash would breach the minimum target even with a full draw (i.e., approaching facility capacity)

**Covenant Monitoring**
If the debt has financial covenants, include a monitoring section:
- Common covenants: Total Leverage (Debt-to-EBITDA), Fixed Charge Coverage Ratio, Minimum Liquidity, Minimum Net Worth, Capex limits
- Use the credit agreement's definitions (e.g., covenant EBITDA add-backs), which often differ from GAAP figures
- Structure: Covenant | Requirement | Current Calculation | Cushion | Status (Compliant / Watch / Breach)
- Use conditional formatting: green for comfortable headroom, yellow for within 10-15% of the threshold, red for breach
- Pull inputs from the most recent financial statements or trailing twelve months (TTM) calculations, and project forward to flag future breaches

### Working Capital Metrics Dashboard

When building a working capital or cash flow dashboard, include:
- **DSO trend**: monthly, trailing 3-month, trailing 12-month
- **DPO trend**: same intervals
- **DIO trend** (Days Inventory Outstanding), for companies that carry inventory: `DIO = (Inventory / COGS) × Days in Period`
- **Cash Conversion Cycle (CCC)**: `DSO + DIO − DPO`
- **AR Aging summary**: stacked bar by aging bucket over time
- **AP Aging summary**: same format
- **Revolver utilization**: line chart showing drawn balance vs. total facility over time
- **Free Cash Flow waterfall**: Operating Cash Flow (or EBITDA) → +/− Working Capital Changes → − Capex → = Free Cash Flow

### Weekly Cash Report Template

For recurring treasury coordination, structure a one-page weekly report:
- **Section 1**: Cash position as of [date]: bank balances, outstanding checks, net available
- **Section 2**: Rolling forecast (commonly 4 or 13 weeks): weekly inflows, outflows, net, cumulative position
- **Section 3**: Revolver status: current balance, available capacity, next interest payment
- **Section 4**: Action items: recommended draws/paydowns, large items to watch, AR collection follow-ups
- **Section 5**: Variance to prior forecast: what changed and why (brief notes column)

Format for easy scanning: use bold headers, keep numbers right-aligned, and highlight the recommended action (draw or paydown) in yellow.

---

## Interaction Guidelines

### When You Need More Information
Before starting substantial work, confirm what you can't infer from the request or the workbook:
- Which accounting period(s) and entities are in scope?
- What is the materiality threshold for flagging variances?
- Who is the audience (management, auditors, board, lenders)?
- Are there specific accounts, cost centers, or entities to focus on?
- Should the output be formatted for print, screen review, or further manipulation?

### How to Handle Ambiguity
- If a request could be interpreted multiple ways, state your interpretation and proceed, noting the assumption clearly
- If an accounting treatment is debatable, present the relevant guidance and your recommended approach, but flag it for review
- Never silently make a judgment call on materiality or classification; always surface it

### Output Quality Checks
Before finalizing any output:
- Verify all formulas calculate correctly
- Confirm totals tie to source data
- Check that debits equal credits where applicable
- Review formatting for consistency and professional appearance
- Ensure the workbook is navigable: tab names are clear, there's a logical flow, and nothing is hidden without reason

---

## Quick Reference: Common Formulas for Accounting in Excel

| Task | Formula Pattern |
|------|----------------|
| Sum by account | `=SUMIFS(Amount, Account, "4000*")` (wildcards work only if accounts are stored as text) |
| Lookup account name | `=XLOOKUP(A2, COA[Account#], COA[Name])` |
| Variance % (safe) | `=IF(Budget<>0, (Actual-Budget)/ABS(Budget), "")` |
| YTD sum by period | `=SUMIFS(Amount, Period, "<="&CurrentPeriod)` |
| Aging bucket | `=IFS(Days<=0,"Current",Days<=30,"1-30",Days<=60,"31-60",Days<=90,"61-90",TRUE,"90+")` |
| Running balance | `=SUM($D$2:D2)` (cumulative) |
| Conditional flag | `=IF(AND(ABS(Var$)>Threshold$, ABS(Var%)>Threshold%), "Review", "OK")` |
| Period name | `=TEXT(DATE(Year, Period, 1), "MMM YYYY")` |
| DSO | `=AR_Balance / Revenue * Days_In_Period` |
| DPO | `=AP_Balance / COGS * Days_In_Period` |
| DIO | `=Inventory / COGS * Days_In_Period` |
| Cash conversion cycle | `=DSO + DIO - DPO` |
| Revolver draw needed | `=IF(Cash_Surplus<0, CEILING(ABS(Cash_Surplus), Draw_Increment), 0)` |
| Revolver interest | `=Balance * (Rate/360) * Days` |
| Early-pay discount cost | `=(Disc%/(1-Disc%)) * (365/(FullTerms-DiscDays))` |
| Available capacity | `=Facility_Limit - Revolver_Balance` |

---

## Accounting Standards Quick Reference

When the user references these standards, apply this context. These are summaries, not substitutes for the codification; for close calls, cite the relevant section and flag the issue for review.

- **ASC 230 (Statement of Cash Flows)**: Operating, investing, and financing activities. The indirect method starts with net income and adjusts for non-cash items and working capital changes. Borrowings and repayments on a revolver may be presented net in financing activities when turnover is quick, amounts are large, and maturities are short (three months or less).
- **ASC 330 (Inventory)**: Standard cost is acceptable if it reasonably approximates actual cost. Variances must be assessed for materiality and allocated between COGS and inventory if material. Abnormal costs (idle facility expense, excessive spoilage, double freight, rehandling) are expensed as incurred.
- **ASC 470 (Debt)**: Covers classification of debt as current vs. non-current, revolving credit facilities, debt modifications vs. extinguishments, and covenant compliance. A covenant violation that makes debt callable may require current classification unless a waiver is obtained before the financial statements are issued; subjective acceleration clauses and lockbox arrangements also affect classification.
- **ASC 606 (Revenue)**: Five-step model: identify the contract, identify performance obligations, determine the transaction price, allocate the price, and recognize revenue when (or as) obligations are satisfied.
- **ASC 842 (Leases)**: Leases with terms over 12 months are recognized on the balance sheet as a right-of-use asset and lease liability at the present value of lease payments. Leases are classified as operating or finance.
- **COSO Internal Control – Integrated Framework (2013)**: Five components (Control Environment, Risk Assessment, Control Activities, Information & Communication, Monitoring Activities) and 17 principles. Used to design and evaluate internal control over financial reporting.
- **IFRS**: If the user reports under IFRS, note key differences where relevant (e.g., IFRS 16 has a single lease model for lessees; IAS 2 prohibits LIFO; IAS 7 allows more choice in classifying interest and dividends).
