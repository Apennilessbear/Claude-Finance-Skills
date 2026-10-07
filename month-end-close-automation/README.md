# Month-End Close Automation — a Claude Skill

A free, open skill that helps Claude build and run the month-end or quarter-end close in Excel: close calendars, balance sheet reconciliations, accrual and amortization schedules, subledger tie-outs, flux analysis, and an organized close binder.

It's built from the working standards of a corporate accounting team, generalized so it works for any company, whatever your ERP, entity structure, or close-day target.

## What it covers

1. **Close framework**: pre-close, core close, review, and post-close phases, plus a close calendar template with business-day date logic, formula-driven status, and dependency tracking
2. **Reconciliations**: a standard balance sheet reconciliation format with reconciling-item aging, and specifics for cash, AR, AP and GRNI, inventory and reserves, prepaids and accruals, and fixed assets
3. **Journal entries**: a recurring JE schedule, accrual templates (straight-line, usage-based, payroll, ASC 606 over-time revenue), and manual JE documentation standards
4. **Subledger-to-GL tie-outs**: a process and a tie-out template
5. **Flux analysis**: a period-over-period and year-over-year template with threshold flags and an investigation checklist
6. **Close binder**: a recommended workbook tab structure, naming conventions, and pre-delivery quality checks

The skill adapts to you. Tell Claude your close-day target, ERP, chart of accounts, and materiality thresholds, or share your existing checklist or reconciliation template, and it will follow your conventions instead of the defaults.

## When it activates

Once installed, Claude uses the skill automatically for close work in Excel. Mentions of close checklists or calendars, accruals, reconciliations, recurring entries, intercompany eliminations, subledger tie-outs, prepaid amortization, depreciation schedules, flux analysis, or close binders will bring it in.

Example prompts:

- *"Build a 5-day close calendar with owners, dependencies, and status that rolls forward each month."*
- *"Create a bank reconciliation template for our operating account."*
- *"Here's our prepaid schedule. Rebuild it so the remaining balances tie to the GL."*
- *"Set up a flux analysis on this trial balance, flagging changes over $25K and 10%."*
- *"Draft a subledger-to-GL tie-out for AP, AR, fixed assets, and inventory."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`month-end-close-automation.zip`** from this folder.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`SKILL.md`](SKILL.md); it's plain text.

## Folder contents

```
month-end-close-automation/
├── README.md
├── SKILL.md                        ← the skill's instructions
└── month-end-close-automation.zip  ← upload this to Claude
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip it inside a folder named `month-end-close-automation` and upload it again. You might:

- Set your close-day target and rewrite the phase timing to match
- Replace placeholder account ranges with your control accounts
- Set your default flux and escalation thresholds
- Add your ERP's report names for agings, valuation, and GR/IR
- Add your own workbook naming and sign-off conventions

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request.

## Disclaimer

This skill is a close-management and documentation aid, not a substitute for professional judgment. Accounting treatment, estimates, and materiality are judgments for you and your advisors. Always review Claude's output before relying on it or sharing it.

## License

Released under the [MIT License](../LICENSE). You're free to use, modify, and share it.
