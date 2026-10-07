---
name: management-reporting-board-deck
description: "Use this skill whenever the user is preparing management reports, executive summaries, CFO packages, board reporting packages, or leadership-facing financial presentations in Excel. Trigger when the user mentions monthly reporting package, flash report, executive dashboard, KPI scorecard, board deck financials, management discussion, commentary, financial highlights, departmental P&L, segment reporting, earnings summary, or asks to format financial data for a non-accounting audience. Also trigger when preparing variance commentary, trend analysis for leadership, or condensing detailed financial data into executive-ready summaries."
---

# Management Reporting & Board Deck Prep in Excel

Use this skill to prepare polished, executive-ready financial reports and dashboards in Excel. These deliverables go to the CFO, CEO, board of directors, lenders, or department leaders. Clarity, brevity, and accuracy come first: the audience wants insight, not raw data, and every number must tie.

## Adapting to the user's reporting

Everything below is a sensible default. Before applying one, use what the user has told you or what their existing package shows:

- **Existing package**: If the user shares last month's package or a template, match its layout, line items, and formatting exactly. Consistency month to month matters more than any default here.
- **Business model**: Choose revenue dimensions, KPIs, and operational metrics that fit the business (manufacturing, distribution, SaaS, services, retail, nonprofit). Leave out sections that don't apply.
- **Reporting framework**: Default to U.S. GAAP captions. Use IFRS terminology if the user reports under IFRS.
- **Materiality**: Commentary thresholds below are illustrative. Use the user's.
- **Units and brand**: Follow the user's preferred units ($, $000s, $M), fiscal calendar, and brand colors when given.

## Audience Awareness

### Know Your Reader
- **CFO**: Wants precision, tie-outs, and the ability to drill into detail. Expects GAAP accuracy and will ask "why" on every variance.
- **CEO / President**: Wants the big picture: revenue trends, profitability, cash, and anything off-plan. Keep it to one page if possible.
- **Board of Directors**: Wants strategic context: performance vs. plan, key risks, and the forward outlook. Minimal accounting jargon.
- **Lenders**: Want covenant compliance, liquidity, and leverage, presented on the definitions in the credit agreement.
- **Department heads**: Want their own P&L with actionable detail: what's driving their numbers and what they control.

Adjust detail, terminology, and emphasis to the audience. When in doubt, build a layered report: summary on top, detail on supporting tabs.

---

## Monthly Financial Reporting Package

### Standard Package Contents

**Page 1: Executive Summary / Flash Report**
A single-page snapshot covering:
- Revenue: actual, budget, variance, prior year
- Gross margin: actual %, budget %, change in basis points
- Operating income / EBITDA: actual, budget, variance
- Net income
- Cash and liquidity: beginning cash, ending cash, net change, and credit facility availability if the company has one
- Two or three plain-English bullets on the key highlights or concerns
- YTD performance vs. annual plan (% of plan achieved vs. % of year elapsed)

Format as a scorecard grid with conditional formatting:
- Green for favorable to budget, red for unfavorable
- Pair color with an arrow or symbol (▲ ▼) so the report reads correctly in grayscale and for color-blind readers
- Sparklines for trend direction

**Page 2: Income Statement**
Condensed P&L format:
| | Current Month Actual | Current Month Budget | Variance $ | Variance % | YTD Actual | YTD Budget | Variance $ | Variance % | Prior Year YTD | YoY Change % |

Line items (condensed from the trial balance):
- Net Revenue
- Cost of Goods Sold
- **Gross Profit** (bold, with margin %)
- Selling Expenses
- General & Administrative Expenses
- Research & Development (if applicable)
- **Total Operating Expenses**
- **Operating Income** (bold, with margin %)
- Interest Expense
- Other Income / (Expense)
- **Income Before Tax**
- Income Tax Provision
- **Net Income** (bold, with margin %)

Include a margin % column next to each actual column: `=IF(Revenue<>0, LineItem/Revenue, "")`.

If EBITDA or "adjusted" metrics appear, show a reconciliation to net income, label them as non-GAAP, and define the adjustments the same way every month.

**Page 3: Revenue Detail**
Break revenue into the dimensions that matter to the business:
- Product line or service category
- Customer segment or geography
- Channel (if applicable)

Show actual vs. budget and prior year for each. Add a bridge (waterfall) when there are major volume, price, or mix shifts.

**Page 4: Variance Commentary**
For every P&L line with a material variance (e.g., over $5K and over 10%, or the user's threshold):

| Account Group | Budget | Actual | Variance | Fav/(Unfav) | Explanation |
|--------------|--------|--------|----------|-------------|-------------|

The explanation column is the most important part of management reporting. Write explanations that are:
- Specific: "IT consulting $15K over budget due to Phase 2 of the ERP migration," not "Professional fees higher than expected"
- Classified: say whether it's timing (will reverse), a run-rate change (ongoing), or a one-time item
- Forward-looking: if it affects the forecast, say so

**Page 5: Balance Sheet Summary**
Condensed balance sheet with:
- Current month vs. prior month vs. prior year end
- Key ratios: current ratio, quick ratio, debt-to-equity (and net leverage if the company has debt)
- Working capital components highlighted (AR, inventory, AP) with days metrics. State the method and keep it consistent:
  - DSO = AR / Revenue for the period × Days in period
  - DIO = Inventory / COGS for the period × Days in period
  - DPO = AP / COGS (or purchases) for the period × Days in period
  - Cash conversion cycle = DSO + DIO − DPO

**Page 6: Cash Flow Summary**
Indirect method or a simplified direct method:
- Operating cash flow (net income + non-cash items + working capital changes)
- Investing cash flow (capex, asset sales)
- Financing cash flow (debt draws and repayments, distributions or dividends)
- Net change in cash, with beginning and ending cash
- Credit facility draws and repayments shown gross, not netted

**Supporting tabs** (available for drill-down, not presented unless asked):
- Departmental P&Ls
- Headcount and labor cost detail
- Capital expenditures vs. budget
- Intercompany activity summary (multi-entity only)

---

## KPI Scorecard

### Structure
Build the scorecard as a dedicated tab or standalone report:

| KPI | Definition | Better When (Higher/Lower) | Current Month | Prior Month | Trend | YTD | Target | Status |

**Financial KPIs**
- Revenue growth (MoM and YoY)
- Gross margin %
- Operating margin %
- EBITDA and EBITDA margin
- SG&A as % of revenue
- Free cash flow

**Working Capital KPIs**
- DSO, DIO, DPO
- Cash conversion cycle
- Working capital as % of revenue

**Liquidity KPIs**
- Cash on hand
- Credit facility availability (drawn vs. total commitment, net of borrowing base limits if any)
- Current ratio
- Quick ratio

**Operational KPIs** (customize to the business)
- Revenue per employee
- Cost per unit or per FTE
- Backlog
- Customer count or retention
- On-time delivery %

### Status Indicators
Use a traffic-light system that respects each KPI's direction, because for some metrics (DSO, SG&A %, cost per unit) lower is better:
- Green: at or better than target
- Yellow: worse than target, but within the tolerance (default 10%)
- Red: worse than target by more than the tolerance

Formula, with `Dir` = "Higher" or "Lower" and `Tol` = 10%:
```
=IF(Dir="Higher",
    IF(Actual>=Target,"Green",IF(Actual>=Target-ABS(Target)*Tol,"Yellow","Red")),
    IF(Actual<=Target,"Green",IF(Actual<=Target+ABS(Target)*Tol,"Yellow","Red")))
```
Using `ABS(Target)` keeps the logic correct for negative targets. For targets at or near zero, use an absolute tolerance instead of a percentage. Apply conditional formatting to the Status column.

---

## Variance Commentary Best Practices

### Sign Convention
Present every variance so the reader can tell instantly whether it's good or bad:
- Revenue and income lines: Variance = Actual − Budget (positive is favorable)
- Expense lines: Variance = Budget − Actual (positive is favorable)
- Or keep Actual − Budget throughout and add a Fav/(Unfav) column. Either way, state the convention on the report and color by favorability, not by sign.

### The WHAT–WHY–SO WHAT Framework
For every significant variance:
1. **WHAT**: State the variance plainly ("SG&A was $42K over budget")
2. **WHY**: Explain the driver ("driven by unplanned legal fees on the vendor dispute")
3. **SO WHAT**: Explain the implication ("one-time; no run-rate impact. Counsel expects a $10K recovery in Q2")

### Commentary Dos and Don'ts
**Do**:
- Quantify everything: "labor was $30K over," not "labor was higher"
- Distinguish timing, run-rate, and one-time items
- Note offsets ("rent $8K under budget, partially offsetting the $12K utilities overage")
- Reference specific business events, contracts, or decisions
- Flag items that need a management decision

**Don't**:
- State the obvious ("revenue was $50K below budget because sales were lower"; why were sales lower?)
- Use accounting jargon the audience won't know
- Bury bad news; lead with the most significant items
- Leave material variances unexplained
- Write a novel; one or two sentences per line is ideal

---

## Departmental P&L Reporting

### Structure
Each department head gets a P&L for their cost center or department:

| Account | Account Name | Current Month Actual | Current Month Budget | Variance | YTD Actual | YTD Budget | Variance | Annual Budget | Remaining Budget | % Used | Run-Rate |

- **% Used**: `=YTD Actual / Annual Budget`; compare it to the % of the year elapsed
- **Run-rate**: `=(YTD Actual / Months Elapsed) × 12`, projected annual spend at the current pace. For seasonal spend, compare YTD actual to YTD budget instead, since a straight-line run-rate will mislead.
- **Run-rate vs. annual budget**: flags whether the department is trending over or under for the year

Group expenses by natural account category:
- Salaries & Wages
- Benefits & Payroll Taxes
- Contract Labor / Consulting
- Travel & Entertainment
- Software & Subscriptions
- Supplies & Materials
- Facilities / Occupancy
- Other

### Headcount Tie-Out
Include a headcount section at the bottom:
- Budgeted vs. actual headcount (use average headcount for the period, not ending)
- Open positions
- Average cost per FTE: `=Total Labor Cost / Average Headcount`
- Split the labor variance into its two drivers (the two pieces sum to the total variance):
  - Headcount (volume) variance: `=(Actual HC − Budget HC) × Budget Avg Cost`
  - Rate variance: `=(Actual Avg Cost − Budget Avg Cost) × Actual HC`

---

## Formatting Standards for Management Reports

### Layout Principles
- Lead with the summary, support with the detail
- One key message per page or tab
- Leave white space; don't cram
- Numbers right-aligned, text left-aligned, column headers centered
- Bold subtotals and key metrics (Gross Profit, Operating Income, Net Income)
- Light gray shading on alternating sections (not every row)
- Thin top border on subtotals, double bottom border on grand totals

### Number Formatting
- Amounts in thousands or millions for executive reports, with the unit stated ("$ in thousands")
- Zero decimals for dollars in thousands; one decimal for percentages
- Negatives in parentheses
- Show zeros as a dash: `#,##0;(#,##0);"–"`
- Make sure rounded figures still foot, or add a footnote that totals may not sum due to rounding

### Chart Standards
- At most two or three charts per page
- Every chart title states the metric, period, and unit
- Default palette (swap for the user's brand colors): actuals dark blue, budget gray, prior year light blue, favorable green, unfavorable red
- No 3D, no unnecessary gridlines, no decoration
- Waterfall charts work well for bridges (budget to actual, prior year to current year)

### Print Optimization
- Set report tabs to print one page wide (adjust row heights and column widths; don't drop fonts below 9 pt)
- Headers and footers: company name (left), report title (center), period and page number (right)
- Margins of 0.5" to 0.75"
- Preview before distributing: check for orphaned rows, cut-off columns, and readability

---

## Output Quality Checks
Before handing back a reporting deliverable, confirm:
- Revenue, net income, and total assets tie to the trial balance or final financial statements
- Every subtotal foots and every page agrees with every other page (the flash report matches the income statement)
- Variance signs and favorable/unfavorable coloring are correct for both revenue and expense lines
- Every material variance has commentary
- Units are stated and consistent, and non-GAAP measures are labeled and reconciled
