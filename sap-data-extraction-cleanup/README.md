# SAP Data Extraction & Cleanup — a Claude Skill

A free, open skill that helps Claude turn raw SAP S/4HANA or ECC exports into clean, analysis-ready Excel tables: stripping report headers and inline subtotals, fixing text-formatted amounts and dates, restoring leading zeros, converting debit/credit indicators to signed amounts, and tying everything back to the raw export.

It's built from hands-on experience cleaning SAP data for month-end and audit work, generalized so it works for any company running SAP, whatever its configuration or user settings.

## What it covers

1. **Common SAP export problems**: multi-row headers, inline subtotals, sign conventions, text-formatted numbers, date formats, truncated text, and lost leading zeros, plus export tips that prevent them
2. **Reference tables**: standard movement types (with a note on which aren't simple reversal pairs), document types, and posting keys
3. **Common exports**: key fields, uses, and pitfalls for MB51, FBL1N, FBL3N / FAGLL03, FBL5N, and F2217 / S_ALR_87012277
4. **Field-name mapping**: classic table fields and their universal journal (ACDOCA) equivalents, mapped to plain-English headers
5. **A six-step cleanup workflow**: remove garbage rows, rename headers, fix data types with locale-safe formulas, remove subtotals, validate and enrich, and save as a named Excel Table (or a refreshable Power Query)
6. **Output standards**: raw data preserved, transformations documented, and row counts and control totals tied out

The skill adapts to you. SAP is heavily configured, so tell Claude about any custom document types, movement types, or naming conventions and it will use them instead of the standard defaults. The cleanup workflow also works for messy exports from other ERPs.

## When it activates

Once installed, Claude uses the skill automatically for SAP data in Excel. Mentions of SAP transaction codes or Fiori apps, movement types, document types, posting keys, ALV exports, ACDOCA, company codes, plants, profit centers, or cost centers will bring it in.

Example prompts:

- *"Here's an FBL3N export. Clean it up and convert it to signed amounts."*
- *"This MB51 file has European number formats and trailing minus signs. Fix the amounts."*
- *"Strip the headers and subtotals from this ALV export and make it pivot-ready."*
- *"Flag reversal pairs in this material document list so I can exclude them."*
- *"Build a Power Query that cleans this FBL1N export every month."*

## Installation

Custom skills are available on Claude's **Pro, Max, Team, and Enterprise** plans.

1. Download **`sap-data-extraction-cleanup.zip`** from this folder.
2. In Claude, go to **Settings → Capabilities** and make sure **Code execution and file creation** is turned on.
3. In the **Skills** section, choose **Upload skill** and select the ZIP file.
4. Confirm the skill appears in your Skills list and is toggled on.

Uploaded skills are private to your account. Team and Enterprise admins can provision skills for their whole organization.

For current details, see Anthropic's help article: [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

> **Tip:** As with anything you install, read a skill before you use it. The full instructions are in [`SKILL.md`](SKILL.md); it's plain text.

## Folder contents

```
sap-data-extraction-cleanup/
├── README.md
├── SKILL.md                         ← the skill's instructions
└── sap-data-extraction-cleanup.zip  ← upload this to Claude
```

## Customizing it

The whole skill is one Markdown file. To tailor it, edit `SKILL.md`, then re-zip it inside a folder named `sap-data-extraction-cleanup` and upload it again. You might:

- Add your company's custom document types, movement types, or posting keys
- Add the Z-reports or saved ALV layouts your team exports most often
- Set your G/L account and material number lengths
- Add your table naming convention and the field names your team prefers

## Contributing

Suggestions and improvements are welcome. Open an issue or submit a pull request.

## Disclaimer

This skill is a data preparation aid, not a substitute for professional judgment. SAP configurations vary, so confirm codes and field meanings against your own system, and always tie cleaned data back to the source before relying on it. SAP, S/4HANA, and Fiori are trademarks of SAP SE; this project is not affiliated with or endorsed by SAP.

## License

Released under the [MIT License](../LICENSE). You're free to use, modify, and share it.
