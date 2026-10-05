# Audit Support & SOX Documentation — a Claude Skill

A free, open skill that helps Claude prepare audit-ready documentation: PBC trackers, roll-forwards and lead sheets, risk and control matrices, walkthrough narratives, control testing workpapers, and deficiency remediation trackers.

It's built from the documentation standards a finance team works to during real audits, generalized so it works for any company, whether you're under SOX 404, applying COSO voluntarily, or supporting an internal audit.

## What it covers

1. **Workpaper standards**: headers, purpose, source, conclusion, cross-references, and a default tickmark legend
2. **System reports (IPE)**: documenting report parameters and how completeness and accuracy were checked
3. **PBC request management**: a tracker with status dropdowns and conditional formatting, plus common request items by area
4. **Roll-forwards and lead sheets**: templates that tie to the trial balance by formula
5. **Risk and Control Matrix**: column structure, field definitions, how to write a testable control description, and segregation-of-duties review
6. **Narratives and walkthroughs**: a four-section template, with flowchart conventions
7. **Control testing**: population definition, sample sizes by control frequency, attribute testing, and conclusions
8. **Deficiency evaluation**: PCAOB-aligned definitions of control deficiency, significant deficiency, and material weakness, and the factors to weigh
9. **Remediation tracking**: a tracker that includes retest dates
10. **Auditor deliverable formatting**: what to include, and what to leave out

The skill adapts to your standards. If your audit firm or company uses its own templates, tickmarks, or sample-size tables, tell Claude or share an example, and it will follow those instead of the defaults.

## When it activates

Once installed, Claude uses the skill automatically when you're preparing for or supporting an audit, or documenting and testing internal controls. Mentions of PBC lists, lead sheets, roll-forwards, RCMs, walkthroughs, control testing, SOX 404, ITGCs, segregation of duties, or deficiencies will bring it in.

Example prompts:

- *"Build me a PBC tracker for our year-end audit from this request list."*
- *"Draft a risk and control matrix for our procure-to-pay process."*
- *"Here's our fixed asset subledger export. Make an audit-ready roll-forward that ties to the TB."*
- *"Write a walkthrough narrative for the month-end close process."*
- *"Set up a testing workpaper for our monthly bank reconciliation control."*
- *"Two of our 25 samples failed. Help me think through whether this is a significant deficiency."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`audit-support-sox-documentation.zip`** from this folder.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`SKILL.md`](SKILL.md); it's plain text.

## Folder contents

```
audit-support-sox-documentation/
├── README.md
├── SKILL.md                               ← the skill's instructions
└── audit-support-sox-documentation.zip    ← upload this to Claude
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip it inside a folder named `audit-support-sox-documentation` and upload it again. You might:

- Replace the default tickmarks and sample sizes with your firm's methodology
- Add your ERP's report names to the PBC list and source documentation
- Add process areas or controls specific to your industry
- Remove sections that don't apply to you

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request.

## Disclaimer

This skill is a documentation aid, not a substitute for professional judgment or your auditor's guidance. Deficiency severity in particular is a judgment for management and the auditor. Always review Claude's output before relying on it or sharing it.

## License

Released under the [MIT License](../LICENSE). You're free to use, modify, and share it.
