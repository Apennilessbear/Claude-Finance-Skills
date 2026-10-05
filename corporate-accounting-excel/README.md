# Corporate Accounting in Excel — a Claude Skill

A free, open skill that turns Claude into an accounting and finance co-pilot for Excel work: analyzing GL and ERP data, building variance and forecast models, making leadership-ready charts, organizing and reconciling information, and managing cash, revolver, and covenant tracking.

It's built from the day-to-day standards of a corporate controllership team, generalized so it works for any company, whatever your ERP, industry, or size.

## What it covers

1. **Analyzing data sets**: data profiling, budget vs. actual and flux analysis, trial balance review, and journal entry / transaction testing
2. **Visuals and charts**: choosing the right chart, financial chart formatting standards, and one-page dashboards
3. **Financial models**: a standard tab architecture, input/formula color conventions, error checks, and templates for variance models, standard cost variances, rolling forecasts, account reconciliations, and close checklists
4. **Organizing information**: chart of accounts mapping, consolidations and roll-ups, pivot-ready formatting, and COSO-aligned risk and control matrices
5. **Cash flow and debt**: AR/AP-driven cash forecasts, revolver trackers with draw/paydown logic, covenant monitoring, working capital metrics (DSO, DPO, DIO, CCC), and a weekly cash report
6. **Quick references**: common accounting formulas in Excel and short summaries of ASC 230, 330, 470, 606, 842, and COSO

The skill adapts to you. Tell Claude your ERP (SAP, Oracle, NetSuite, Dynamics, and so on), your reporting framework, your materiality thresholds, or share an existing workbook, and it will follow your conventions instead of the defaults.

## When it activates

Once installed, Claude uses the skill automatically for accounting and finance work in Excel. Mentions of trial balances, variance or flux analysis, reconciliations, close checklists, GL or ERP exports, standard cost variances, cash forecasts, revolvers, covenants, DSO/DPO, or audit-ready formatting will bring it in.

Example prompts:

- *"Here's our trial balance export. Profile it and flag anything unusual."*
- *"Build a budget vs. actual variance model for Q3 with commentary on the top movers."*
- *"Make a waterfall chart bridging budget operating income to actual."*
- *"Set up a 13-week cash forecast from these AR and AP agings, with revolver draw logic."*
- *"Build a covenant compliance tracker for a 3.5x leverage and 1.25x FCCR covenant."*
- *"Create a month-end close checklist with owners, due dates, and status tracking."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`corporate-accounting-excel.zip`** from this folder.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`SKILL.md`](SKILL.md); it's plain text.

## Folder contents

```
corporate-accounting-excel/
├── README.md
├── SKILL.md                        ← the skill's instructions
└── corporate-accounting-excel.zip  ← upload this to Claude
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip it inside a folder named `corporate-accounting-excel` and upload it again. You might:

- Describe your ERP, chart of accounts structure, and report names so Claude recognizes your exports
- Set your default materiality thresholds and close calendar
- Swap the chart colors for your company's brand palette
- Add your credit agreement's covenant definitions
- Remove sections that don't apply (for example, standard costing if you don't use it)

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request.

## Disclaimer

This skill is an analysis and modeling aid, not a substitute for professional judgment. Accounting treatment, materiality, and covenant calculations are judgments for you and your advisors. Always review Claude's output before relying on it or sharing it.

## License

Released under the [MIT License](../LICENSE). You're free to use, modify, and share it.
