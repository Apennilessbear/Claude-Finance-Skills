# Excel Formula Auditing & Error Detection — a Claude Skill

A free, open skill that turns Claude into a methodical reviewer for Excel workbooks. It catches the problems that cause embarrassment and bad decisions before a workbook reaches auditors, management, clients, or anyone else.

It's built from the pre-distribution review a finance team runs on its own workbooks, generalized so it works for anyone.

## What it checks

The skill walks Claude through a 10-step audit:

1. **Error scan**: #REF!, #DIV/0!, #VALUE!, #N/A, #NAME?, #NULL!, #NUM!, with causes and fixes for each
2. **Hardcoded values hiding in formulas**: assumptions like `=B5*1.05` that belong in labeled input cells
3. **Inconsistent formulas**: the one cell in a row that breaks the pattern
4. **Circular references**: including whether iterative calculation is quietly switched on
5. **Named ranges**: broken, stale, duplicate, or mis-scoped names
6. **Data validation**: input cells with no guardrails
7. **Structural integrity**: balance checks, cross-foots, period roll-forwards, sign conventions, and record counts
8. **Formatting consistency**: number formats, color coding, alignment, and print setup
9. **Protection**: lock the formulas, leave the inputs open
10. **Documentation**: a model map, version history, and an assumptions summary

It finishes with quick-fix formula patterns and a pre-distribution checklist.

The skill adapts to your standards. If your organization uses its own color-coding or naming conventions, tell Claude, and it will audit against those instead of the defaults.

## When it activates

Once installed, Claude uses the skill automatically when you ask it to review, audit, QC, debug, or clean up a spreadsheet, or when you mention things like formula errors, #REF!, circular references, hardcoded values, or getting a workbook ready for reviewers.

Example prompts:

- *"Can you QC this budget model before I send it to leadership?"*
- *"I'm getting #REF! errors all over my forecast after deleting a tab. Help me find and fix them."*
- *"Review this reconciliation workbook for anything an auditor would flag."*
- *"Build me a pre-distribution checklist for this financial model."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`excel-formula-auditing-error-detection.zip`** from this repository.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`excel-formula-auditing-error-detection/SKILL.md`](excel-formula-auditing-error-detection/SKILL.md); it's plain text.

## Repository contents

```
├── README.md
├── excel-formula-auditing-error-detection.zip   ← upload this to Claude
└── excel-formula-auditing-error-detection/
    └── SKILL.md                                 ← the skill's instructions
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip the folder and upload it again. You might:

- Add your organization's color-coding, naming, or file-naming standards
- Add checks specific to your ERP's data exports
- Remove sections that don't apply to your work

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request. If you've found an audit check that saved you from a bad number, I'd love to add it.

## Disclaimer

This skill is a review aid, not a substitute for professional judgment. Always review Claude's findings and any changes it suggests before relying on a workbook.

## License

Released under the [MIT License](LICENSE). You're free to use, modify, and share it.
