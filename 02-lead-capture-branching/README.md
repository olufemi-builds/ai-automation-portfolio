# 02 — Lead Capture with Branching Logic

**Platform:** n8n  
**Input:** Google Sheets (Google Form responses)  
**Condition:** Budget (₦) greater than or equal to ₦500,000  
**True branch:** Gmail notification  
**False branch:** Google Sheets nurture log

## Objective

Capture lead details from a form response and use a budget threshold to route each lead to the appropriate action.

## Workflow

`Google Sheets Trigger` → `If`

- **True (budget ≥ ₦500,000):** Send an email notification containing the lead's name, email address and budget.
- **False (budget < ₦500,000):** Append the lead's name, email address and budget to the **Lead Capture - Nurture** Google Sheet.

The workflow polls the form-response sheet every minute for newly added rows.

## Condition

The IF node evaluates:

```text
{{ $json["Budget (₦)"] }} >= 500000
```

The comparison uses a strict numeric condition. The incoming budget value must be a number (or a numeric value accepted by n8n's number validation). If the form or spreadsheet supplies formatted text such as `₦500,000`, normalise or convert it to a numeric value before the IF node, then test both sides of the threshold.

## Field mapping

| Source field | Gmail notification | Nurture sheet |
|---|---|---|
| `Name` | Name in email body | `Name` |
| `Email Address` | Email in email body | `Email` |
| `Budget (₦)` | Budget in email body | `Budget (₦)` |

The source column is named `Email Address`; the nurture destination column is named `Email`.

The form also generates a submission timestamp. The current workflow does not map that timestamp into the nurture sheet or include it in the email notification.

## Assignment notes

**Condition chosen:** The workflow checks whether `Budget (₦)` is greater than or equal to ₦500,000. Leads meeting this threshold trigger an email alert. Leads below the threshold are added to the Nurture sheet.

**Field mapping:** The source sheet provides `Name`, `Email Address` and `Budget (₦)`. These fields are mapped to the Gmail alert and the Nurture sheet. The email column is named `Email Address` in the source sheet and `Email` in the Nurture sheet.

**Data check:** The form collects `Name`, `Email Address` and `Budget (₦)`. Name and email identify and allow contact with the lead, while budget determines which branch the lead follows. A timestamp is also generated automatically to track submissions.

## Import and configuration

The committed `workflow.json` is a sanitised export. Before using it:

1. Import the JSON into your n8n instance.
2. Connect your Google Sheets credential to the trigger and the nurture-sheet append node.
3. Select your own form-response spreadsheet and the correct response worksheet.
4. Select your own nurture spreadsheet and worksheet.
5. Connect your Gmail credential and replace the notification email placeholder with the intended recipient.
6. Confirm that the budget column is numeric. If it contains currency symbols or separators as text, add a conversion step before the IF node.
7. Test one lead below ₦500,000 and confirm it is appended to the nurture sheet.
8. Test one lead at or above ₦500,000 and confirm the notification is sent.
9. Activate the workflow only after both branches have been verified.

Spreadsheet IDs, credential references, the original notification address, webhook ID and instance-specific metadata have been removed or replaced with placeholders. The workflow is intentionally inactive in this public export.

## Privacy and responsible handling

- Keep real lead names, email addresses and form submissions out of public repository files and screenshots.
- Send lead details only to an authorised notification recipient.
- Collect only information required for lead qualification and follow-up.
- Apply appropriate access controls to both the response and nurture spreadsheets.

## Testing and evidence

Capture and add the following using synthetic lead records:

- `screenshots/workflow-canvas.png` — trigger, IF node and both branches.
- `screenshots/true-branch-notification.png` — successful qualified-lead email with personal details masked.
- `screenshots/false-branch-sheet-log.png` — lead successfully appended to the nurture sheet.
- `screenshots/branch-test-cases.png` — test values showing one budget below and one at or above ₦500,000.

## Implementation note

The workflow's branch logic is based on the configured ₦500,000 threshold. The IF node routes qualifying leads to Gmail and non-qualifying leads to the nurture spreadsheet; it does not send an email to leads on the false branch.
