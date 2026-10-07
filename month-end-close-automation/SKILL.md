---
name: month-end-close-automation
description: "Use this skill whenever the user is working on month-end or quarter-end financial close tasks in Excel. Trigger when the user mentions close checklist, close calendar, accruals, reconciliations, journal entries, recurring entries, intercompany eliminations, subledger tie-out, close timeline, close tasks, balance sheet reconciliation, bank reconciliation, prepaid amortization, depreciation schedules, or any reference to accelerating, organizing, or documenting the financial close process. Also trigger for flux analysis tied to close review, management review of financials, or preparation of close binders."
---

# Month-End Close Automation in Excel

Use this skill to help accounting teams manage, document, and speed up the monthly or quarterly financial close in Excel. The goal is workbooks and templates that enforce consistency, reduce errors, and make the close faster and easier to review, for the team, for management, and for auditors.

## Adapting to the user's close

Everything below is a sensible default. Close processes vary by company size, ERP, entity structure, and close-day target. Before applying a default, use what the user has told you or what their workbook shows:

- **Close calendar**: Some teams close in 3 business days, others in 10. Scale the phase timing below to the user's target rather than forcing a 10-day calendar.
- **ERP / source system**: SAP, Oracle, NetSuite, Microsoft Dynamics, Sage, QuickBooks, or another system. Use that system's report names when the user mentions them; otherwise describe reports generically (e.g., "AP aging as of period end").
- **Chart of accounts**: Account numbers and ranges in the templates below are placeholders. Replace them with the user's actual accounts.
- **Materiality**: Default flux and escalation thresholds are illustrative. Use the user's thresholds when given, and ask when the threshold drives a judgment.
- **Entity structure**: Include intercompany and consolidation steps only when the user has more than one entity.
- **House style**: If the user shares an existing close checklist, reconciliation template, or binder, follow its layout and naming rather than replacing it.

## Close Process Framework

### Standard Close Phases
Organize close work into four sequential phases. Day ranges assume a roughly 7–10 business day close; compress them for faster closes.

**Phase 1: Pre-Close (Business Days −3 to −1 before period end)**
- Send cutoff reminders to AP, AR, purchasing, receiving/warehouse, and payroll
- Review open POs, unmatched receipts, and pending invoices
- Identify large known items that won't be invoiced by period end and prepare accruals
- Confirm physical counts or cycle count adjustments are scheduled or posted
- Agree intercompany balances with counterparties (multi-entity only)

**Phase 2: Core Close (Business Days 1–4 after period end)**
- Complete subledger postings (AP, AR, fixed assets, inventory) and close the subledgers
- Post recurring journal entries (depreciation, amortization, allocations)
- Post manual accruals and adjusting entries
- Complete bank reconciliations
- Run and review the preliminary trial balance
- Perform subledger-to-GL tie-outs
- Post intercompany eliminations (if consolidating)

**Phase 3: Review & Reporting (Business Days 4–7)**
- Prepare balance sheet reconciliations for all significant accounts
- Perform flux analysis (period-over-period and budget-to-actual)
- Investigate and document variances above threshold
- Prepare draft financial statements
- Management review and sign-off

**Phase 4: Post-Close (Business Days 7–10)**
- Finalize and archive the close binder
- Update the rolling forecast with actual results
- Capture lessons learned and process improvements for next month
- Communicate results to stakeholders

### Close Calendar Template
Build a close calendar with these columns:
- Day (BD−1, BD+1, BD+2, etc.) | Date | Phase | Task | Owner | Reviewer | Dependency | Target Completion | Actual Completion | Status | Notes
- Calculate dates from the period end with `=WORKDAY(PeriodEnd, BusinessDay, Holidays)` so the calendar rolls forward each month by changing one input
- Derive status with a formula rather than typing it: `=IF(ActualCompletion<>"","Complete",IF(TODAY()>TargetCompletion,"Past Due",IF(Started="Y","In Progress","Not Started")))`
- Conditional formatting: green = Complete, yellow = In Progress, red = Past Due, gray = Not Started
- Add a Gantt-style view if space permits (conditional formatting on a business-day grid)
- Track dependencies so a late upstream task (e.g., inventory close) visibly flags the tasks that wait on it

---

## Reconciliation Templates

### Balance Sheet Reconciliation: Standard Format

Every significant balance sheet account should have a reconciliation with this structure.

**Header Block**
- Account Number | Account Name | Period | Preparer | Reviewer | Date Prepared | Date Reviewed | Risk Rating (High/Medium/Low)

**Reconciliation Body**
| Line | Description | Amount |
|------|------------|--------|
| 1 | GL balance per trial balance | `=XLOOKUP(Account, TB[Account], TB[Ending Balance])` or `=SUMIFS(...)` |
| 2 | Reconciling items: timing differences | (itemized below) |
| 3 | Reconciling items: items not yet recorded in GL | (itemized below) |
| 4 | Adjusted GL balance | `=SUM(Lines 1:3)` |
| 5 | Balance per independent support (subledger, statement, schedule) | (from source) |
| 6 | **Unreconciled difference** | `=ROUND(Line 4 − Line 5, 2)` |

- Line 6 should be zero. If not, investigate and document before sign-off.
- Pull the GL balance by formula from the trial balance tab so the reconciliation updates if the TB is re-run.
- Include a prior-period column for comparison.
- Use `ROUND` on the difference so tiny floating-point residues don't show as unreconciled.

**Reconciling Item Detail**
- List each item: Description | Date Originated | Amount | Owner | Expected Resolution Date | Status | Age (days)
- Age with `=PeriodEnd − DateOriginated` and bucket as Current (0–30), 31–60, 61–90, 90+
- Flag items older than 60 days for escalation, and require a correcting entry or write-off decision for items past 90 days

### Key Account Reconciliation Specifics

**Cash / Bank Reconciliation**
Reconcile both sides to an adjusted balance:

| Bank side | Book side |
|-----------|-----------|
| Balance per bank statement | Balance per GL |
| + Deposits in transit | + Bank credits not yet recorded (interest, incoming wires) |
| − Outstanding checks | − Bank debits not yet recorded (fees, returned items) |
| ± Bank errors | ± Book errors |
| **= Adjusted bank balance** | **= Adjusted book balance** |

- The two adjusted balances must agree.
- Book-side items need a journal entry this period; bank-side items should clear next period.
- Keep a check clearing schedule: check number, payee, date issued, amount, cleared date.
- Flag checks outstanding over 90 days for follow-up, and track stale items against unclaimed property (escheatment) rules, whose dormancy periods vary by jurisdiction.
- Investigate deposits in transit that don't clear within a few business days.

**Accounts Receivable**
- GL balance should tie to the AR aging total
- Reconciling items: unapplied cash, unapplied credit memos, items posted directly to the control account, reclassifications
- Verify aging buckets foot to the total
- Review the allowance for credit losses against the aging and any specific reserves

**Accounts Payable**
- GL balance should tie to the AP aging total
- Reconciling items: unprocessed invoices, items posted directly to the control account, reclassifications
- Goods received not invoiced (GRNI): support the accrual with the open receipts report or the GR/IR clearing account detail, and review old GRNI items for receipts that will never be invoiced

**Inventory**
- GL balance should tie to the inventory valuation report from the inventory subledger
- Reconciling items: in-transit inventory, consigned inventory, cost revaluations, unposted count adjustments
- Reserve / obsolescence analysis: age the inventory, apply reserve percentages by aging bucket, and add specific reserves for known slow-moving or discontinued items

**Prepaids and Accrued Liabilities**
- Roll-forward format: Beginning Balance + Additions − Amortization/Usage = Ending Balance
- Schedule columns: Vendor | Description | Total Amount | Term (months) | Start Date | End Date | Monthly Amortization | Months Elapsed | Remaining Balance
- Formulas:
  - `Monthly Amortization = Total / Term`
  - `Months Elapsed = IF(PeriodEnd<StartDate, 0, MIN(Term, DATEDIF(StartDate, PeriodEnd, "m") + 1))` (adjust the +1 to your convention for the first month; the IF avoids the #NUM! error DATEDIF returns for items that haven't started)
  - `Remaining = Total − Months Elapsed × Monthly Amortization`
- Capping months elapsed at the term keeps fully amortized items at zero instead of going negative.
- The schedule's remaining-balance total should tie to the GL balance.

**Fixed Assets**
- Roll-forward cost and accumulated depreciation separately, then net:
  - Cost: Beginning + Additions − Disposals ± Transfers = Ending
  - Accumulated depreciation: Beginning + Depreciation − Disposals ± Transfers = Ending
  - Net book value = Ending cost − Ending accumulated depreciation
- Cross-reference additions to capital expenditure approvals and construction-in-progress transfers
- Verify depreciation expense ties to the depreciation register
- Check for assets past their useful life that are still depreciating, and for fully depreciated assets still in service (useful-life review)

---

## Journal Entry Templates

### Recurring Journal Entry Schedule
Maintain a master list of all recurring entries:
- JE # | Description | Frequency (Monthly/Quarterly/Annual) | Debit Account | Credit Account | Amount or Formula | Auto-Reverse (Y/N) | Auto/Manual | Owner | Last Posted Period

For entries with fixed or formula-driven amounts, reference an assumptions tab so amounts update in one place when contracts or allocation drivers change.

### Accrual Calculation Templates

**Straight-Line Accruals (insurance, rent, service contracts billed in arrears)**
- Monthly accrual = Annual cost / 12
- Track: Vendor | Description | Annual Amount | Monthly Accrual | Months Remaining | Accrued YTD | Paid YTD | Variance
- If the accrual auto-reverses, post the reversal on the first day of the next period and book the actual invoice when it arrives.

**Usage-Based Accruals (utilities, professional fees)**
- Estimate with a trailing 3-month average or the prior-year same month adjusted for known changes: `=AVERAGE(Prior3Months)` or `=PriorYearSameMonth * (1 + Escalator)`
- Track accuracy: compare each accrual to the actual invoice and calculate the variance %
- If variances consistently exceed about 10%, refine the estimation method

**Payroll Accruals**
- Salaried: `(Annual Salary / Workdays in Year) × Unpaid Workdays in Period`
- Hourly: `Hours Worked but Unpaid × Hourly Rate`
- Add employer payroll taxes and, if benefits aren't accrued separately, a benefits load: `Base Accrual × (1 + LoadRate)`. Don't apply the load where benefits are already accrued elsewhere, or you'll double count.
- Track by department or cost center for proper allocation
- Consider bonus, commission, and paid-time-off accruals separately

**Revenue Accruals (ASC 606, performance obligations satisfied over time)**
- Cumulative revenue to date = Transaction Price × % Complete
- Revenue this period = Cumulative revenue to date − Revenue recognized in prior periods (a change in estimate is picked up as a cumulative catch-up)
- Variable consideration: estimate with the expected value or most likely amount method, and constrain it to the amount not likely to reverse significantly
- Document the basis for each accrual with a reference to the contract

### Manual Journal Entry Documentation
Every manual JE should include:
- Purpose / business reason
- Calculation (show the math, or link to the supporting schedule)
- Supporting documentation reference
- Preparer and approver, with dates (the approver should not be the preparer)
- Reversal indicator (auto-reverse Y/N, and the reversal period)

---

## Subledger-to-GL Tie-Out

### Process
For each subledger (AP, AR, fixed assets, inventory):
1. Pull the subledger detail report as of period end
2. Sum it to get the subledger total
3. Pull the GL balance for the control account(s)
4. Compare; the difference should be zero
5. If not, investigate: posting timing, unposted batches, manual entries made directly to control accounts

### Tie-Out Template
| Subledger | GL Account(s) | GL Balance | Subledger Total | Difference | Status | Notes |
|-----------|--------------|------------|----------------|------------|--------|-------|
| AP | (your AP control accounts) | `=SUMIFS(...)` | from report | `=GL − Sub` | `=IF(ROUND(Diff,2)=0,"Tied","Investigate")` | |
| AR | (your AR control accounts) | `=SUMIFS(...)` | from report | `=GL − Sub` | `=IF(ROUND(Diff,2)=0,"Tied","Investigate")` | |
| Fixed Assets | (cost and accumulated depreciation) | `=SUMIFS(...)` | from register | `=GL − Sub` | `=IF(ROUND(Diff,2)=0,"Tied","Investigate")` | |
| Inventory | (your inventory accounts) | `=SUMIFS(...)` | from valuation | `=GL − Sub` | `=IF(ROUND(Diff,2)=0,"Tied","Investigate")` | |

To sum an account range, use numeric bounds: `=SUMIFS(TB[Balance], TB[Account], ">="&LowAcct, TB[Account], "<="&HighAcct)`. This requires accounts stored as numbers; if they're stored as text, add a numeric helper column first.

---

## Flux Analysis for Close Review

### Period-over-Period Flux Template
| Account | Account Name | Current Period | Prior Period | $ Change | % Change | Prior Year Same Period | $ Change (YoY) | % Change (YoY) | Flag | Commentary |
|---------|-------------|---------------|-------------|----------|----------|----------------------|----------------|-----------------|------|------------|

- % change: `=IF(Prior=0, IF(Current=0, 0, "New"), Change/ABS(Prior))`. Dividing by the absolute prior value keeps the sign meaningful when the prior balance is negative.
- Flag: `=IF(AND(ABS(Change)>DollarThreshold, OR(Prior=0, ABS(Change/Prior)>PctThreshold)), "Explain", "")`. Default thresholds of $5,000 and 10% are illustrative; use the user's materiality.
- Sort by absolute dollar change, descending, for prioritized review.
- Require commentary for every flagged line.
- Group by financial statement section: Revenue, COGS, Gross Profit, Operating Expenses, Other Income/Expense, Tax, and the balance sheet captions.

### Flux Investigation Checklist
When investigating a flagged variance, ask:
1. Is it timing? (e.g., an invoice received early or late)
2. Is it a known business event? (new contract, headcount change, one-time item)
3. Is it a classification error? (wrong account or cost center)
4. Is it an accrual issue? (missed accrual, accrual not reversed, double-counted reversal)
5. Is it a data issue? (duplicate posting, wrong amount, wrong period)

Document the root cause and whether a correcting entry is needed.

---

## Close Binder / Workbook Organization

### Recommended Tab Structure for a Monthly Close Workbook
1. **Cover**: period, entity, preparer, status summary
2. **Close Calendar**: task list with status tracking
3. **Trial Balance**: full TB with mapping to financial statement lines
4. **Flux Analysis**: P&L and balance sheet flux with commentary
5. **Reconciliations**: one tab per significant account (or grouped)
6. **Journal Entries**: log of all manual entries posted
7. **Subledger Tie-Outs**: all tie-out results
8. **Supporting Schedules**: depreciation, amortization, accrual detail
9. **Open Items**: reconciling items carried forward and issues to resolve
10. **Sign-Off**: preparer and reviewer sign-off with dates

### Naming Convention (default; follow the user's if they have one)
- Workbook: `[Entity]_Close_[YYYY-MM].xlsx` (e.g., `ACME_Close_2026-03.xlsx`)
- Journal entries: `JE_[Seq#]_[Brief Description]` (e.g., `JE_001_Depreciation`)
- Reconciliations: `Recon_[Account#]_[AccountName]`

---

## Output Quality Checks
Before handing back a close deliverable, confirm:
- Every reconciliation's GL balance is formula-linked to the trial balance and the unreconciled difference is zero or explained
- Debits equal credits on every journal entry and in the trial balance
- Roll-forwards foot and cross-foot, and ending balances tie to the GL
- Flux thresholds and account ranges match what the user specified, and any placeholders are clearly marked
- No hardcoded numbers sit where a formula should be; inputs are labeled and kept on an assumptions tab
