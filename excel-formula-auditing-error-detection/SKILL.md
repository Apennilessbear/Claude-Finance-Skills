---
name: excel-formula-auditing-error-detection
description: "Use this skill whenever the user asks to review, audit, validate, debug, or quality-check an Excel workbook before distribution. Trigger when the user mentions formula errors, broken references, #REF, #DIV/0, #VALUE, #N/A, #NAME, circular references, hardcoded values in formulas, inconsistent formulas, model integrity, workbook review, QC check, error checking, formula auditing, protecting cells, or asks to harden, clean up, or validate a spreadsheet before sending it to reviewers, auditors, management, clients, or other external parties. Also trigger when the user wants to document a model's logic, create a formula map, or check that a workbook follows professional modeling standards."
---

# Excel Formula Auditing & Error Detection

Use this skill to review an Excel workbook for errors, inconsistencies, and quality problems before it is shared with others or used to make decisions. Treat the review as a final quality gate: a mistake caught here saves the workbook's owner from embarrassment and keeps wrong numbers out of downstream decisions.

The checklist works for any workbook, including financial models, reconciliations, budgets, trackers, and operational reports. Some checks (balance checks, sign conventions) apply only to financial or accounting models. Skip the ones that don't fit the workbook in front of you, and say which ones you skipped and why.

## Adapting to the user's standards

Where this skill describes a convention (color coding, naming, file names, where assumptions live), treat it as a sensible default rather than a rule. If the workbook already follows a consistent convention of its own, or the user describes their organization's standard, audit against that instead. What matters is that the workbook is internally consistent and easy to review, not that it matches this document exactly.

## Audit Checklist — Run Through These In Order

### 1. Error Scan
Search every sheet for Excel error values. A finished workbook should contain none.

| Error | Meaning | Common Cause | Fix |
|-------|---------|-------------|-----|
| #REF! | Invalid cell reference | A row, column, or sheet that a formula referenced was deleted | Trace the formula, then restore the reference or rebuild the formula |
| #DIV/0! | Division by zero | Denominator is zero or blank | Test the denominator explicitly: `=IF(Denom=0, "", Num/Denom)` |
| #VALUE! | Wrong data type | Text in a cell that should be numeric, or an array size mismatch | Check the inputs; convert text-numbers with VALUE(); look for hidden spaces with TRIM() |
| #N/A | Lookup failed | VLOOKUP/XLOOKUP can't find the value | Check for trailing spaces, text vs. number mismatches, or misspelled lookup values |
| #NAME? | Unrecognized name | Misspelled function, deleted named range, or text in a formula missing its quotes | Check spelling, confirm named ranges exist, add quotes around text strings |
| #NULL! | Incorrect range operator | A space between references where a colon or comma belongs | Replace the space with the right operator (`:` for a range, `,` for a union) |
| #NUM! | Invalid numeric value | Number too large or small, or an invalid argument (e.g., SQRT of a negative) | Check the calculation's inputs and boundary conditions |

**Approach**: For large workbooks, use Go To Special (Ctrl+G → Special → Formulas → Errors) to jump straight to the error cells on each sheet. To count errors in a range: `=SUMPRODUCT(--ISERROR(A1:Z100))`. To flag them in a helper column: `=IF(ISERROR(A1), "ERROR", "OK")`.

**A caution on IFERROR**: Wrapping formulas in `IFERROR(…, 0)` or `IFERROR(…, "")` hides the symptom without fixing the cause, and it also hides any future error in that cell. Reviewers and auditors often treat blanket IFERROR as a red flag. Fix the underlying problem where possible, and use a targeted test (like `IF(Denom=0, …)`) when a specific condition is expected. If IFERROR is still the right tool, return a visible value such as "Not found" rather than a silent 0.

### 2. Hardcoded Values Hiding in Formulas
One of the most common modeling mistakes is typing a number directly into a formula instead of referencing an input cell. The value then can't be seen, changed in one place, or reviewed.

**What to look for**:
- Formulas containing literal numbers other than structural constants such as 0, 1, -1, 100, 12, and 365
- Examples of bad practice:
  - `=B5*1.05` (the growth rate belongs in its own cell)
  - `=Revenue*0.21` (the tax rate should be a labeled assumption)
  - `=SUMIFS(Range,Criteria,"East")` (a filter value may be fine, but if it's a key assumption that could change, reference a cell instead)

**How to check**: Review formulas for embedded constants. Toggle formula view (Ctrl+`) to scan a sheet quickly, and use `=ISFORMULA(A1)` to find cells that should be formulas but have been overwritten with typed values.

**Fix**: Move assumptions to a dedicated, clearly labeled inputs area or tab, and replace each hardcoded value with a reference to its input cell. A common convention formats input cells with blue font (sometimes with a light yellow fill) so they stand out.

### 3. Inconsistent Formulas Across Rows or Columns
When a formula is meant to repeat across a range (e.g., monthly columns in a projection), every cell should follow the same pattern.

**What to look for**:
- A row of formulas where one cell differs from its neighbors
- A column of SUMIFS where one row references a different range
- Absolute and relative references mixed within the same pattern (e.g., `$A$1` in some cells and `A1` in others), which breaks the formula when it is copied

**How to check**:
- Toggle formula view (Ctrl+`) and scan visually for the outlier
- Go To Special → Row Differences or Column Differences highlights cells that break the pattern of the selection
- Excel's built-in error checking flags "Inconsistent formula" with a green triangle; make sure that rule is enabled under File → Options → Formulas
- Note that comparing FORMULATEXT() of adjacent cells does not work: correctly copied relative formulas have different text (`=B1*2` vs. `=C1*2`) even though they follow the same pattern

**Fix**: Correct the outlier to match the intended pattern. If the difference is intentional (e.g., a different calculation for the first period), add a cell comment explaining why.

### 4. Circular Reference Check
Circular references can silently corrupt a model's results or cause Excel to iterate unpredictably.

**How to check**:
- Look at the Excel status bar, which shows "Circular References" and a cell address if one exists
- Go to Formulas → Error Checking → Circular References to see each instance
- Check File → Options → Formulas. If "Enable iterative calculation" is on, ask whether that is intentional. In most models it should be off, because it also hides accidental circular references. Intentional circularity is uncommon and should be clearly documented (a classic example is a debt schedule where interest expense affects cash, which affects the debt balance).

**Fix**: Trace the dependency loop and break it. Usually one reference should point to a prior-period value instead of the current period, or an intermediate calculation step is needed.

### 5. Named Range Audit
Named ranges improve readability but can become stale or broken over time.

**How to check**:
- Open Name Manager (Ctrl+F3)
- Look for names that refer to #REF! (deleted source), names pointing to sheets that no longer exist, duplicate or confusingly similar names, and scope problems (workbook vs. sheet level)
- Confirm each name still points to the intended cells, since inserted rows or columns may have shifted the data

**Fix**: Delete broken names, update stale references, and rename ambiguous names to follow one consistent convention (for example, prefixes such as `input_tax_rate`, `calc_gross_profit`, `output_net_income`).

### 6. Data Validation Check
Input cells should have guardrails against bad entries.

**What to look for**:
- Key assumption cells (rates, quantities, percentages) that accept any value
- Dropdowns whose validation list is outdated or points to a deleted range
- Date cells that accept text
- Cells where a negative value makes no sense but isn't prevented

**Recommendations**:
- Add data validation to the major input cells: whole-number ranges, decimal ranges, list dropdowns, date ranges
- Include input messages (e.g., "Enter the annual growth rate as a decimal, e.g., 0.05 for 5%")
- Include error alerts for invalid entries
- Rely on validation rather than on each user's care to keep inputs sensible

### 7. Structural Integrity Checks
These checks apply mainly to financial models, reconciliations, and anything with totals. Use the ones that fit.

**Balance checks**: In any model with a balance sheet, include `=Assets - (Liabilities + Equity)`, which must equal zero. Place it prominently and use conditional formatting (green at zero, red otherwise).

**Cross-foot checks**: Where a total is calculated both across and down (e.g., monthly values summed across should equal the annual total, which should also equal the sum of the line items), add `=Row_Total - Column_Total`, which must equal zero.

**Period continuity**: Each period's beginning balance must equal the prior period's ending balance. Check with `=Current_Beginning - Prior_Ending`, which must be zero for every period.

**Sign convention consistency**: Signs should follow one convention throughout. If revenue is positive in one place, it should be positive everywhere, unless a sheet deliberately uses debit/credit signs; in that case, label it clearly and flag any place where the two conventions meet.

**Row count verification**: After any data manipulation, confirm the record count still matches the source. `=COUNTA(A:A)-1` (subtracting the header) should equal the expected count.

### 8. Formatting Consistency Review

**Number formats**: All currency cells should share one format, as should all percentages and all dates. Mixed formats within a column (some cells showing $1,000, others 1000.00) undermine credibility.

**Color coding**: Check that the workbook applies its color convention consistently. A widely used default is:
- Blue: inputs and hardcoded values
- Black: formulas
- Green: links to other sheets or files

Spot-check 10–15 formula cells to confirm their color matches their contents. A blue cell holding a formula, or a black cell holding a typed number, often means someone overwrote something.

**Alignment**: Numbers right-aligned, text left-aligned, headers consistent. Check that merged cells don't interfere with sorting or filtering.

**Print readiness**: On every tab meant for distribution, confirm the print area is set, headers repeat, page breaks fall in logical places, and nothing is cut off.

### 9. Protection and Access Controls

**What to protect**:
- Formula cells, to prevent accidental overwrites
- Structural elements such as headers, labels, and section formatting
- Finished workpapers or reconciliations being handed to reviewers

**What to leave unlocked**:
- Input and assumption cells
- Commentary and notes fields
- Status dropdowns on trackers

**How to implement**:
- Select the input cells → Format Cells → Protection → uncheck "Locked"
- Then Review → Protect Sheet → set a password → allow "Select unlocked cells"
- Sheet protection prevents accidental changes; it is not real security, so don't rely on it to protect confidential data

### 10. Documentation and Map

For complex models, add a **Model Map** tab that documents:

| Tab Name | Purpose | Key Inputs (from) | Key Outputs (to) | Owner |
|----------|---------|-------------------|-------------------|-------|

Also include:
- Version history: Date | Version | Change Description | Changed By
- Assumption summary: each key assumption with its current value, source, and last-updated date
- Known limitations: simplifications, manual overrides, or areas where the model doesn't capture the full picture

---

## Quick-Fix Formula Patterns

| Problem | Solution Formula |
|---------|-----------------|
| Avoid #DIV/0! | `=IF(B1=0, "", A1/B1)` (preferred over a blanket IFERROR) |
| Catch lookup failures visibly | `=XLOOKUP(val, range, return, "Not found")` |
| Force text to number | `=VALUE(TRIM(CLEAN(A1)))` |
| Remove non-printing characters and extra spaces | `=TRIM(CLEAN(A1))` |
| Check formula vs. typed value | `=ISFORMULA(A1)` returns TRUE if A1 contains a formula |
| Conditional error highlighting | `=ISERROR(A1)` as a conditional formatting rule with red fill |
| Verify a cross-sheet link | `=IF(Sheet1!A1=Sheet2!A1, "Match", "BREAK")` |
| Count errors in a range | `=SUMPRODUCT(--ISERROR(A1:Z100))` |

---

## Pre-Distribution Checklist

Before a workbook goes to reviewers, auditors, management, clients, or other outside parties, verify:

- [ ] Zero formula errors across all sheets (#REF!, #DIV/0!, etc.)
- [ ] No hardcoded assumptions hiding in formulas
- [ ] Formulas are consistent across repeated ranges
- [ ] No unintentional circular references, and iterative calculation is off unless documented
- [ ] Named ranges are current and valid
- [ ] Balance checks and cross-foots all return zero (where applicable)
- [ ] Number formatting is consistent throughout
- [ ] Color coding follows the workbook's convention
- [ ] Print areas are set and previewed
- [ ] Formula cells are protected and input cells are unlocked
- [ ] Tab names are clear and in logical order
- [ ] No hidden sheets, rows, or columns containing sensitive or draft data (unless intentional and documented)
- [ ] No unexpected links to external files (Data → Edit Links)
- [ ] Version and date stamp are current
- [ ] The file name follows the applicable naming convention
- [ ] The file has been saved, closed, and reopened to confirm nothing breaks on reload
