# 04 — Invoice Tracking and AI-Assisted Reporting

**Platform:** Zapier  
**Services:** QuickBooks Online, Google Sheets, GPT for Sheets

## Overview

This project connects a paid-invoice event in QuickBooks Online to a Google Sheets invoice tracker, then uses GPT for Sheets to generate an AI-assisted summary from spreadsheet data.

The documented implementation is limited to the workflow and spreadsheet configuration shown in the project evidence. It does not include a verified weekly email or Slack reporting workflow.

## Implemented workflow

1. **Trigger — QuickBooks Online: New Invoice Paid**  
   Zapier listens for a newly paid invoice in QuickBooks Online.

2. **Action — Google Sheets: Update Spreadsheet Row**  
   The Zap updates a row in the `Zaps Automation` spreadsheet, on `Sheet2`. The demonstrated field mapping sends QuickBooks' `Document Number` to the spreadsheet's `Invoice ID` column.

3. **AI-assisted summary — GPT for Sheets**  
   The spreadsheet uses a GPT formula to create a natural-language summary from invoice fields.

   ```excel
   =GPT("Summarize this month's invoices: " & TEXTJOIN(", ", TRUE, B2:F2))
   ```

   The displayed example summarises the customer, amount, payment status, invoice date and due date.

## Demonstrated example

The spreadsheet screenshot shows one example record:

| Field | Displayed value |
|---|---|
| Invoice ID | 1003 |
| Customer | Toyo |
| Amount | 100 |
| Status | paid |
| Invoice date | 2025-05-03 |
| Due date | 2025-06-02 |

This is an example shown in the evidence, not a claim about live production volume or business results.

## Technical considerations and limitations

- The demonstrated Google Sheets action displays row `2`. Confirm that the actual Zap identifies the correct row dynamically (for example, by searching for the Invoice ID) before using it for multiple invoices. A fixed row reference could update the same row repeatedly.
- The shown GPT formula references only `B2:F2`. Although its prompt says “this month's invoices,” this formula alone does not aggregate all invoices for a month. A range-based formula with date filtering, or a separate aggregation step, would be needed for a true monthly summary.
- The evidence does not show a separate scheduled weekly report or email/Slack delivery step. Those capabilities are therefore not included in this project's implementation claims.
- The evidence does not establish a configured invoice-amount filter such as a less-than-$200 condition.

## Evidence to add

Add screenshots to this folder when available. Useful evidence includes:

- QuickBooks Online trigger showing **New Invoice Paid**.
- Google Sheets action showing the spreadsheet, worksheet and field mapping.
- GPT for Sheets formula and generated summary.

## Security and privacy

Do not publish QuickBooks credentials, Zapier connection details, API keys, customer information, real invoice records or confidential business data. Use synthetic or anonymised spreadsheet examples in public screenshots.

## Project scope

This is a focused demonstration of event-triggered invoice tracking and AI-assisted spreadsheet summarisation. It should not be described as a complete accounts-receivable platform or as an automated weekly reporting system.
