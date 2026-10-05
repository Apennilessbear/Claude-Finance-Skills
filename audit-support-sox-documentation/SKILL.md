---
name: audit-support-sox-documentation
description: "Use this skill whenever the user is preparing for, supporting, or responding to an external audit or internal audit engagement, or documenting internal controls for SOX or COSO compliance. Trigger when the user mentions PBC list, audit schedules, audit requests, roll-forward schedules, lead sheets, supporting workpapers, walkthroughs, narratives, flowcharts, Risk and Control Matrix (RCM), control testing, control deficiencies, remediation plans, SOX 404, management testing, key controls, IT general controls (ITGCs), segregation of duties, or any request to organize documentation for auditor review. Also trigger when building reconciliation packages, preparing debt compliance certificates, or structuring evidence for control effectiveness."
---

# Audit Support & SOX Documentation

Use this skill to help a company's finance or accounting team prepare audit-ready workpapers, manage PBC (Prepared by Client) request lists, document internal controls, test them, and track deficiencies to remediation. The goal is documentation an experienced external or internal auditor can pick up and follow without asking for an explanation: clear purpose, traceable sources, and numbers that tie.

Most deliverables here are Excel workbooks, but the same standards apply to narratives and memos written in Word or another document tool.

## Adapting to the user's standards

Everything below is a sensible default, not a rule. Audit firms, internal audit departments, and companies each have their own templates, tickmark sets, sample-size tables, and terminology. If the user describes their firm's or company's standard, or shares an existing workpaper or RCM, follow that instead and keep it consistent across the deliverable.

A few things to establish early when they matter to the task:

- **Framework**: SOX 404 applies to U.S. public companies (404(a) management assessment; 404(b) auditor attestation for accelerated filers). Private companies, lenders, and internal audit teams often apply COSO 2013 without SOX. Use the vocabulary that fits.
- **Systems**: Ask which ERP and reporting tools the company uses, and refer to their actual report names when documenting sources.
- **Auditor methodology**: When the work supports an external audit, the auditor's sample sizes and documentation requirements win over the defaults here.

---

## Workpaper Standards

### Every workpaper or schedule should include
- **Header**: Company name, account/topic, period end date, preparer initials and date, reviewer initials and date
- **Purpose**: One sentence on what the workpaper demonstrates
- **Source**: Where the data came from — system, report or query name, run date/time, and parameters used (company code, date range, filters)
- **Conclusion**: A brief statement that the balance is fairly stated, or a description of the issues found
- **Cross-references**: Tickmarks or cell comments linking to supporting detail, with a legend whenever symbols are used
- **Table of contents**: On the first tab when the workpaper spans multiple tabs

### Reports produced by the system (IPE)
Auditors test the completeness and accuracy of any system report a control or schedule relies on (Information Produced by the Entity). When a workpaper uses a system report, document:
- Report name and whether it is standard or custom-built
- Parameters used, with a screenshot of the selection screen where practical
- How completeness and accuracy were checked (e.g., report total agreed to the trial balance; record count agreed to the source table)

### Default tickmark legend
Firms vary, so substitute the user's symbols if they have them.

| Symbol | Meaning |
|--------|---------|
| √ | Agreed to source document |
| F | Footed (column totals verified) |
| CF | Cross-footed (row totals verified) |
| TB | Agreed to trial balance |
| PY | Agreed to prior year workpaper |
| GL | Agreed to general ledger detail |
| R | Recalculated without exception |
| N/A | Not applicable — explanation provided |
| PBC | Prepared by client |
| AJE | Audit adjusting entry posted |

Include the legend on every workpaper that uses tickmarks.

---

## PBC (Prepared by Client) Request Management

### PBC request tracker
Columns:
- Request # | Category | Description | Auditor Contact | Date Requested | Due Date | Priority (High/Med/Low) | Assigned To | Status | Date Submitted | File Name / Location | Auditor Follow-Up Notes

**Status values** (data validation dropdown):
- Not Started | In Progress | Under Review | Submitted | Resubmitted | Complete | N/A

**Conditional formatting**:
- Red: past due and not submitted
- Yellow: due within 3 business days (`=AND(Status<>"Submitted", Status<>"Complete", NETWORKDAYS(TODAY(), DueDate) <= 3)`)
- Green: submitted or complete
- Gray: N/A

Order the rules so red evaluates before yellow (past-due items also satisfy the yellow formula).

Add a summary block at the top (count by status, count past due) so the tracker can double as a status update for the audit team.

### Common PBC categories and items
Tailor this list to the actual request list the auditor sends; it is a starting point for anticipating requests.

**General / Entity-Level**
- Organization chart
- Board and committee minutes and resolutions
- Significant contracts entered into or amended during the period
- Litigation summary and legal representation letters
- Insurance policy summary

**Revenue & Receivables**
- Revenue by product/service line by month
- AR aging as of period end
- Top customers by revenue with prior year comparison
- Credit memo summary with reasons
- Allowance for credit losses calculation and roll-forward
- Sample invoices and proof of delivery or performance for revenue testing

**Expenses & Payables**
- AP aging as of period end
- Top vendors by spend
- Subsequent disbursements listing and invoices received after period end (supports the auditor's search for unrecorded liabilities)
- Expense accrual support and calculations
- Sample vendor invoices with three-way match documentation (PO, receipt, invoice)

**Inventory** (if applicable)
- Inventory valuation report as of period end
- Inventory reserve / obsolescence analysis and roll-forward
- Physical count results and reconciliation to the book balance
- Cost variance analysis (e.g., purchase price and usage variances) with disposition
- Slow-moving and excess inventory report

**Fixed Assets**
- Fixed asset roll-forward: Beginning + Additions − Disposals − Depreciation = Ending
- Capital expenditure listing with approval documentation
- Disposal/retirement listing with gain/loss calculations
- Depreciation detail by asset class and method

**Leases** (if applicable)
- Lease listing with right-of-use asset and liability roll-forwards
- New, modified, and terminated leases during the period

**Debt & Equity**
- Debt schedule covering all outstanding instruments
- Loan agreements and amendments
- Covenant compliance calculations as of period end
- Interest expense recalculation support
- Equity roll-forward: Beginning + Net Income ± OCI − Dividends ± Other = Ending

**Payroll & Benefits**
- Payroll summary by department and month
- Headcount reconciliation
- Benefits, bonus, and incentive accrual support
- Workers' compensation and insurance accruals

**Tax**
- Tax provision calculation and support
- Deferred tax roll-forward
- Estimated tax payments schedule
- State apportionment factors
- Return-to-provision reconciliation

---

## Audit Schedules and Roll-Forwards

### Roll-forward template
Works for most balance sheet accounts:

| | Current Period | Prior Period |
|---|---|---|
| Beginning Balance | = Prior period ending | |
| Add: Increases / Additions | (detail) | |
| Less: Decreases / Reductions | (detail) | |
| Adjustments / Reclassifications | (detail) | |
| **Ending Balance** | =SUM(...) | |
| Per Trial Balance | =SUMIFS (or XLOOKUP) to the TB tab | |
| **Difference** | = Ending − Per TB | |

The Difference line must be zero. If it isn't, investigate before submitting. Pull the TB balance by formula rather than typing it, so the tie-out updates if the TB is refreshed.

### Lead sheet format
A lead sheet summarizes a financial statement line item across periods:
- Columns: Account # | Account Name | Prior Year Balance | Current Year Balance | $ Change | % Change | W/P Ref
- Subtotal by account group
- The grand total ties to the trial balance and the financial statement line
- Flag fluctuations above the user's or auditor's threshold (e.g., both a $ and % threshold) and leave room for an explanation column

---

## Internal Controls Documentation (COSO / SOX)

### Risk and Control Matrix (RCM)

**Columns**:
| Process Area | Sub-Process | Risk ID | Risk Description | Risk Rating (H/M/L) | Control ID | Control Description | Control Type | Control Nature | Frequency | Control Owner | Key Control (Y/N) | Assertion(s) | Evidence / Documentation | Testing Status | Test Result | Deficiency (if any) |

**Field definitions**:
- **Control Type**: Preventive (stops errors before they occur) or Detective (identifies errors after they occur)
- **Control Nature**: Manual, Automated (system-enforced), or IT-Dependent Manual (a manual control that relies on system-generated data — flag the IPE)
- **Frequency**: Per transaction / multiple times a day, Daily, Weekly, Monthly, Quarterly, Annually
- **Assertion(s)**: Existence/Occurrence, Completeness, Accuracy/Valuation, Rights & Obligations, Cutoff, Classification, Presentation & Disclosure
- **Key Control**: A control relied on to prevent or detect, on a timely basis, a misstatement that could be material
- **Control Owner**: A role or title, not an individual's name, so the RCM survives turnover

**Write control descriptions that are testable.** A good description answers who performs it, what they do, how often, using what information, at what precision (threshold for investigation), and what evidence is retained. "Management reviews the bank reconciliation" is not testable; "Each month, the Controller reviews the completed bank reconciliation for each account within 10 business days of month end, investigates reconciling items over $5,000 older than 30 days, and signs off in the reconciliation tool" is.

**Process areas to consider** (keep what applies):
1. Revenue and Accounts Receivable
2. Procurement and Accounts Payable
3. Inventory and Cost of Sales
4. Payroll and Human Resources
5. Fixed Assets and Leases
6. Treasury and Cash Management
7. Financial Close and Reporting (including journal entries and management review)
8. Tax
9. Entity-Level Controls
10. IT General Controls (access, change management, operations, program development)

**Segregation of duties**: When reviewing an RCM or process, flag cases where one role can initiate, approve, record, and reconcile the same transaction, or has system access that allows it. Note compensating controls where full segregation isn't practical.

### Control narrative / walkthrough

For each significant process:

**Section 1 — Process Overview**
- Objective of the process
- Key personnel involved (by role)
- Systems used (ERP modules, spreadsheets, third-party tools)
- Key inputs and outputs

**Section 2 — Detailed Process Steps**
- Numbered steps covering the end-to-end flow
- For each step: who performs it, what they do, which system or tool they use, what evidence is created
- Mark where controls sit in the flow, referencing Control IDs from the RCM

**Section 3 — Key Controls Summary**
- For each control: Control ID | Description | Risk it addresses | How effectiveness is evidenced

**Section 4 — IT Dependencies**
- System reports relied upon (and how their completeness and accuracy are established)
- Automated controls (three-way match, tolerance checks, approval workflows)
- Interfaces between systems
- Access controls relevant to the process

When the user asks for a flowchart, use consistent symbols (start/end, process step, decision, document, system), swimlanes by role, and control IDs placed at the steps where they operate.

### Control testing workpaper

**Header**: Control ID | Control Description | Control Owner | Testing Period | Tester | Test Date

**Testing approach**: State whether this is a test of design (walkthrough of a single instance) or operating effectiveness (a sample across the period).

**Population and sample**:
- Define the population and how its completeness was confirmed (e.g., all manual journal entries over $10,000 posted in Q1, agreed to a system-generated listing)
- Document the sample size and the rationale. Common minimums by frequency — always defer to the auditor's or internal audit's own methodology:

| Control Frequency | Typical Sample Size |
|---|---|
| Annual | 1 |
| Quarterly | 2 |
| Monthly | 2–5 |
| Weekly | 5–15 |
| Daily | 20–40 |
| Multiple times per day / per transaction | 25–60 |
| Automated (with effective ITGCs) | 1 instance per configuration |

  Use the higher end of the range for higher-risk controls or when relying on the control heavily.
- Document the selection method (random, systematic, or haphazard). If selections are judgmental, say why.

**Test procedures**:
- Describe exactly what was examined (e.g., "Inspected the reviewer's sign-off and date on the bank reconciliation; agreed the book balance to the GL")
- For each sample item: Sample # | Date | Description | Attribute A (e.g., performed timely) | Attribute B (e.g., evidence of review) | Attribute C (e.g., reconciling items investigated) | Result (Pass/Fail) | Notes

**Conclusion**:
- # Tested | # Passed | # Failed | Exception Rate
- Overall assessment: Operating effectively / Not operating effectively
- For any exception, describe its nature and cause, consider whether the sample should be expanded under the methodology being followed, and carry it to the deficiency evaluation below

---

## Deficiency Evaluation and Remediation

### Deficiency classification
These follow the PCAOB AS 2201 definitions; AICPA standards for non-public audits use the same three terms with substantially the same meaning.

- **Control Deficiency**: The design or operation of a control does not allow management or employees, in the normal course of their assigned functions, to prevent or detect misstatements on a timely basis. A design deficiency means a needed control is missing or wouldn't meet its objective even if it operated as designed; an operating deficiency means a well-designed control didn't operate as designed or the person performing it lacked the authority or competence to do it effectively.
- **Significant Deficiency**: A deficiency, or combination of deficiencies, less severe than a material weakness yet important enough to merit attention by those responsible for oversight of financial reporting.
- **Material Weakness**: A deficiency, or combination of deficiencies, such that there is a reasonable possibility that a material misstatement of the annual or interim financial statements will not be prevented or detected on a timely basis.

When helping evaluate severity, walk through: the likelihood that the deficiency could result in a misstatement, the potential magnitude, the accounts and assertions affected, whether compensating controls exist and were tested, and whether deficiencies aggregate within the same account or process. Severity is ultimately a judgment for management and the auditor — lay out the factors rather than declaring a classification on your own.

### Remediation tracker
| Deficiency ID | Description | Classification | Process Area | Control ID(s) | Root Cause | Remediation Plan | Owner | Target Date | Status | Evidence of Remediation | Validated By | Validation Date |

A remediated control needs to operate for a long enough period, and be retested, before it can be considered effective. Note the planned retest date alongside the remediation target.

---

## Formatting Auditor Deliverables

### General rules
- One consistent, professional font throughout (e.g., Arial 10 pt or Calibri 11 pt)
- Right-align numbers, left-align text
- Consistent number format, e.g. `$#,##0;($#,##0);"-"` for currency
- Freeze the header row and label columns
- Lock formula cells; leave input cells unlocked
- Repeat header rows on every printed page
- Set the print area to exclude working columns not meant for the auditor
- Name and order tabs to match the PBC request list or audit section references

### What not to include in auditor deliverables
- Internal commentary about audit strategy or disagreements with the auditor
- Draft or unreviewed calculations
- Personal notes or TODO items
- Data unrelated to the request
- Hidden sheets, rows, or columns with data the auditor shouldn't receive — remove it entirely rather than hiding it

Before handing over a deliverable, check that every total ties, every tickmark is in the legend, the header is complete, and the preparer/reviewer sign-offs are filled in.
