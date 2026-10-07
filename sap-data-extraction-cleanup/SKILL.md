---
name: sap-data-extraction-cleanup
description: "Use this skill whenever the user works with SAP S/4HANA or SAP ECC data exports in Excel. Trigger when the user mentions SAP transaction codes or Fiori apps (MB51, FBL1N, FBL3N, FBL5N, F2217, S_ALR_87012277, FAGLL03, ME2M, MIR7, MIRO, VL06O), movement types, SAP field names, ACDOCA, ALV grid exports, or asks to clean up, reformat, map, or prepare ERP data for analysis. Also trigger when the user references goods issue, goods receipt, posting keys, document types, company codes, plant codes, profit centers, or cost centers from SAP, or needs to convert raw SAP output into a pivot-ready or analysis-ready format."
---

# SAP Data Extraction & Cleanup in Excel

Use this skill to clean, transform, and prepare raw SAP exports (S/4HANA or ECC) for analysis in Excel. SAP exports are notoriously messy; this skill makes sure the data is properly structured and tied out before any analysis begins.

## Adapting to the user's SAP environment

SAP is heavily configured, so the references below are standard defaults, not guarantees. Before relying on them:

- **Configuration**: Document types, posting keys, movement types, account lengths, and fiscal year variants can be customized. If a code in the user's data doesn't match the reference below, ask or check the user's configuration rather than assuming.
- **Release and interface**: S/4HANA users may export from Fiori apps instead of classic transactions, and field labels differ between the two. Recognize either.
- **User settings**: Decimal notation and date format come from each user's SAP profile (SU3 → Defaults), so two people exporting the same report can get different formats. Detect the format from the data itself.
- **House conventions**: If the user has a standard cleanup layout, field-name mapping, or table naming convention, follow it.
- **Other ERPs**: The cleanup workflow (Steps 1–6) applies to messy exports from any ERP. Only the SAP code references are SAP-specific.

## SAP Export Characteristics

### Common Data Quality Issues
- **Multi-row headers**: ALV exports often include report titles, selection parameters, and blank rows above the real column headers
- **Inline subtotals**: SAP inserts subtotal and total rows (often marked with `*` or `**`) that corrupt pivot tables and SUMIFS
- **Inconsistent signs**: Some reports show credits as negative; others show unsigned amounts with a separate debit/credit indicator column
- **Text-formatted numbers**: Amounts can export as text with leading spaces, non-breaking spaces, thousands separators, or trailing minus signs (e.g., `1.234,56-`)
- **Date formats**: Dates may arrive as DD.MM.YYYY, MM/DD/YYYY, or YYYYMMDD depending on user settings and export method
- **Truncated fields**: Long text (material descriptions, vendor names) can be cut off
- **Leading zeros**: Numeric material, GL account, vendor, and customer numbers carry leading zeros in SAP that Excel strips

### Export Tips
- From an ALV grid, exporting to a spreadsheet (XLSX) usually produces cleaner output than "unconverted" text exports
- Remove subtotals in the ALV layout before exporting when possible
- For recurring exports, save an ALV layout with the needed columns and reuse it so the structure is the same every month

### Movement Type Reference (standard settings)
Most movement types are reversed by the next number up (e.g., 101 is reversed by 102):
- **101 / 102**: Goods receipt for purchase order / reversal
- **103 / 104**: Goods receipt into GR blocked stock / reversal
- **122 / 123**: Return delivery to vendor / reversal of return
- **161 / 162**: Returns for purchase order (return PO item) / reversal
- **201 / 202**: Goods issue to cost center / reversal
- **261 / 262**: Goods issue for production or maintenance order / reversal
- **301 / 302**: Transfer posting plant to plant (one step) / reversal
- **311 / 312**: Transfer posting storage location to storage location / reversal
- **501 / 502**: Receipt without purchase order / reversal
- **551 / 552**: Withdrawal for scrapping / reversal
- **601 / 602**: Goods issue for delivery (sales) / reversal
- **651 / 652**: Returns from customer (returns delivery) / reversal
- **701 / 702**: Physical inventory difference, gain / loss (these are a pair of originals, not original and reversal)

Not every even number is a reversal (122 is reversed by 123; 702 is a loss, not a reversal of 701). To identify reversals reliably, use a lookup table of the user's reversal movement types, or the reversal/reference document fields in the export (in MSEG/MATDOC, the reversed material document is shown in the reference fields). Reversal pairs that net to zero inflate transaction counts if not filtered.

### Document Types (standard settings)
- **SA**: G/L account document
- **AB**: Accounting document (used for clearing, reversals, and reclasses)
- **KR**: Vendor invoice
- **KG**: Vendor credit memo
- **KZ**: Vendor payment
- **DR**: Customer invoice
- **DG**: Customer credit memo
- **DZ**: Customer payment
- **RV**: Billing document transfer from SD
- **RE**: Invoice receipt (MIRO)
- **WE**: Goods receipt
- **WA**: Goods issue
- **AA**: Asset posting

### Posting Keys (standard settings)
- **40 / 50**: Debit / credit to G/L account
- **01 / 11**: Customer invoice (debit) / customer credit memo (credit)
- **15**: Incoming payment (customer credit)
- **21 / 31**: Vendor credit memo (debit) / vendor invoice (credit)
- **25**: Outgoing payment (vendor debit)
- **70 / 75**: Debit / credit to asset

## Common Exports and Their Structures

### MB51: Material Document List
Key fields: Material | Plant | Storage Location | Movement Type | Posting Date | Document Date | Quantity | Unit | Amount in LC | Vendor / Customer | Purchase Order | Cost Center | Order
- Use for: inventory movement analysis, goods issue/receipt reconciliation, movement type trending
- Watch for: quantity vs. amount sign mismatches, reversed documents, and amounts that may reflect standard price rather than actual cost

### FBL1N: Vendor Line Items
Key fields: Vendor | Company Code | Document Number | Document Type | Document Date | Posting Date | Amount in LC | Clearing Document | Clearing Date | Payment Terms | Net Due Date
- Use for: AP aging, vendor spend analysis, payment timing
- Watch for: open vs. cleared items (filter on clearing document), special G/L indicators (down payments, retentions)

### FBL3N / FAGLL03: G/L Line Items
Key fields: G/L Account | Company Code | Document Number | Document Type | Posting Date | Amount in LC | Debit/Credit Indicator | Cost Center | Profit Center | Assignment | Text
- Use for: account detail, journal entry testing, flux analysis support
- Watch for: the debit/credit indicator; convert to signed amounts early. In S/4HANA, line item reports read from the universal journal (ACDOCA).

### FBL5N: Customer Line Items
Key fields: Customer | Company Code | Document Number | Posting Date | Amount in LC | Clearing Document | Net Due Date | Days in Arrears | Dunning Level
- Use for: AR aging, collections analysis, DSO calculation
- Watch for: credit memos, unapplied payments, disputed items

### F2217 / S_ALR_87012277: G/L Account Balances / Trial Balance
Key fields: G/L Account | Account Name | Opening Balance | Period Debits | Period Credits | Closing Balance (may include cumulative and period columns)
- Use for: trial balance review, period-over-period flux, financial statement mapping
- Watch for: when the period range doesn't start at period 1, some layouts roll earlier periods' activity into the opening balance column. If balances look off, rerun from period 1 of the fiscal year, or use S_ALR_87012277 or a Report Painter report for multi-period detail. Also check whether special periods (13–16) are included.

## Cleanup Workflow

### Step 1: Remove Header and Footer Garbage
- Scan the first 10–20 rows for report titles, selection parameters, timestamps, and blank rows
- Identify the true header row (the row with field names)
- Delete everything above it
- Delete trailing total rows, record counts, and report footers
- Record the raw row count and the raw amount total before changing anything else

### Step 2: Standardize Column Headers
Rename technical field names to plain English. Classic table fields and their universal journal (ACDOCA) equivalents:

| Classic Field | ACDOCA Field | Clean Header |
|---------------|--------------|-------------|
| MATNR | MATNR | Material Number |
| WERKS | WERKS | Plant |
| LGORT | — | Storage Location |
| BWART | BWART | Movement Type |
| BUDAT | BUDAT | Posting Date |
| BLDAT | BLDAT | Document Date |
| MENGE | MSL | Quantity |
| DMBTR | HSL | Amount (Company Code Currency) |
| WRBTR | WSL | Amount (Transaction Currency) |
| WAERS | RWCUR / RHCUR | Currency |
| LIFNR | LIFNR | Vendor Number |
| KUNNR | KUNNR | Customer Number |
| KOSTL | RCNTR | Cost Center |
| PRCTR | PRCTR | Profit Center |
| BELNR | BELNR | Document Number |
| GJAHR | GJAHR | Fiscal Year |
| MONAT | POPER | Fiscal Period |
| BUKRS | RBUKRS | Company Code |
| HKONT | RACCT | G/L Account |
| SHKZG | DRCRK | Debit/Credit Indicator |

Note that ACDOCA amounts (HSL, WSL) are already signed, so don't apply a debit/credit conversion on top of them.

### Step 3: Fix Data Types
- **Leading zeros**: Store material, G/L account, vendor, and customer numbers as text. SAP only pads numeric values, so alphanumeric IDs need no padding. If numeric IDs lost their zeros, restore them with `=TEXT(A2, REPT("0", 10))` (adjust the length: G/L accounts, vendors, and customers are 10 characters internally; materials are 18, or 40 with extended material numbers in S/4HANA). Only pad columns that are entirely numeric.
- **Amounts stored as text**: Use `NUMBERVALUE`, which lets you specify the separators instead of relying on Excel's locale.
  - European format (`1.234,56-`):
    ```
    =LET(t, TRIM(SUBSTITUTE(A2, CHAR(160), "")),
         neg, RIGHT(t,1)="-",
         n, NUMBERVALUE(IF(neg, LEFT(t, LEN(t)-1), t), ",", "."),
         IF(neg, -n, n))
    ```
  - US format with a trailing minus (`1,234.56-`): the same formula with `NUMBERVALUE(..., ".", ",")`
  - Check a few values afterward; if a column mixes formats, the user's SAP decimal setting changed between exports.
- **Dates**: Convert to real Excel dates.
  - YYYYMMDD text: `=DATE(LEFT(A2,4), MID(A2,5,2), RIGHT(A2,2))`
  - DD.MM.YYYY text: `=DATE(RIGHT(A2,4), MID(A2,4,2), LEFT(A2,2))`
  - Watch for dates Excel already auto-converted with day and month swapped (e.g., 03.04.2026 read as March 4 instead of April 3). Importing the column as text, or through Power Query with the correct locale, prevents this.
- **Debit/credit conversion**: If the export has unsigned amounts and an indicator (S = debit / Soll, H = credit / Haben), create a signed column: `=IF(DC="S", ABS(Amount), -ABS(Amount))`. First confirm the amounts aren't already signed.

### Step 4: Remove Subtotals and Blank Rows
- Delete rows where key identifiers (document number, material, G/L account) are blank but amount columns have values; these are subtotals
- Delete rows with `*` or `**` markers in the first column
- Delete fully blank rows
- Compare row counts before and after to confirm only non-data rows were removed

### Step 5: Validate and Enrich
- Spot-check three to five rows against SAP to confirm amounts, signs, and dates converted correctly
- Tie the control total: the clean amount total should equal the raw detail total (excluding the subtotal rows you removed)
- Add helper columns as needed:
  - **Period**: `=TEXT(PostingDate, "yyyy-mm")` for calendar months. If the fiscal year doesn't follow the calendar, use the fiscal year and period fields from SAP instead of deriving them from the date.
  - **Absolute amount**: `=ABS(Amount)` for ranking and sorting
  - **Reversal flag**: `=IF(ISNUMBER(MATCH(MovementType, ReversalTypes, 0)), "Reversal", "Original")`, where `ReversalTypes` is a named list of the user's reversal movement types
  - **Offset flag**: use COUNTIFS to find offsetting pairs (same material or account, same amount with opposite sign)

### Step 6: Convert to a Table and Save
- Convert the clean range to an Excel Table (Ctrl+T)
- Name it descriptively (e.g., `tbl_MB51_2026_01`, `tbl_FBL1N_Open`)
- Keep the raw export untouched on a tab labeled "RAW – Do Not Modify"
- Put the clean version on a new tab named "Clean" or after the source report
- For a monthly refresh, recommend building the cleanup as a Power Query so next month's export is cleaned with one refresh instead of repeated manual steps

## Output Standards
- Always preserve the raw data tab untouched
- Document every transformation applied (a short note at the top of the clean tab or on a Notes tab)
- Confirm final row counts and control totals tie back to the raw export, and show the tie-out
- Format the clean data for immediate use in pivots, SUMIFS, and XLOOKUP
