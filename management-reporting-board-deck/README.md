# Management Reporting & Board Deck Prep — a Claude Skill

A free, open skill that helps Claude turn detailed financial data into executive-ready reporting in Excel: monthly reporting packages, flash reports, KPI scorecards, variance commentary, departmental P&Ls, and board deck financials.

It's built from the reporting standards of a corporate accounting and finance team, generalized so it works for any company, whatever your industry, size, or reporting audience.

## What it covers

1. **Audience awareness**: what the CFO, CEO, board, lenders, and department heads each need, and how to layer a report for all of them
2. **Monthly reporting package**: flash report, condensed income statement, revenue detail, variance commentary, balance sheet summary with working capital days, and cash flow summary
3. **KPI scorecard**: financial, working capital, liquidity, and operational KPIs, with traffic-light status logic that handles "lower is better" metrics
4. **Variance commentary**: a clear favorable/unfavorable sign convention and the WHAT–WHY–SO WHAT framework, with dos and don'ts
5. **Departmental P&Ls**: % of budget used, run-rate projections, and a headcount vs. rate split of labor variances
6. **Formatting standards**: layout, number formats, charts, print setup, and pre-distribution tie-out checks

The skill adapts to you. Share last month's package or tell Claude your audience, units, materiality, and brand colors, and it will match your format instead of the defaults.

## When it activates

Once installed, Claude uses the skill automatically for leadership-facing financial reporting in Excel. Mentions of a monthly reporting package, flash report, executive dashboard, KPI scorecard, board deck, variance commentary, departmental P&L, or segment reporting will bring it in.

Example prompts:

- *"Build a one-page flash report from this month's trial balance and budget."*
- *"Write variance commentary for every P&L line over $10K and 10% off budget."*
- *"Create a KPI scorecard with DSO, DPO, gross margin, and EBITDA margin, with status lights."*
- *"Set up departmental P&Ls with % of budget used and run-rate for each cost center."*
- *"Format this income statement for the board: $ in thousands, one page, print-ready."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`management-reporting-board-deck.zip`** from this folder.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`SKILL.md`](SKILL.md); it's plain text.

## Folder contents

```
management-reporting-board-deck/
├── README.md
├── SKILL.md                             ← the skill's instructions
└── management-reporting-board-deck.zip  ← upload this to Claude
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip it inside a folder named `management-reporting-board-deck` and upload it again. You might:

- Replace the standard package pages with your own package's page order and line items
- Add the KPIs your leadership actually tracks, with your definitions
- Set your commentary materiality threshold
- Swap the chart palette for your company's brand colors
- Add your non-GAAP adjustment definitions so they're applied the same way every month

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request.

## Disclaimer

This skill is a reporting and presentation aid, not a substitute for professional judgment. Accounting treatment, non-GAAP definitions, and what to disclose to a board or lender are judgments for you and your advisors. Always review Claude's output before relying on it or sharing it.

## License

Released under the [MIT License](../LICENSE). You're free to use, modify, and share it.
