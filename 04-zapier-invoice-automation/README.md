# 04 — Invoice Tracking and Reporting Automation

**Platform:** Zapier  
**Services:** QuickBooks Online, Google Sheets, GPT for Sheets

## Overview

This project automates parts of an invoice-tracking and reporting process by connecting invoice data with a Google Sheets tracker and AI-assisted summaries.

## Capabilities described for this implementation

- Track invoice information from QuickBooks Online in Google Sheets.
- Apply workflow filtering to selected invoice records.
- Generate AI-assisted summaries from spreadsheet data.
- Reflect paid-invoice updates in the tracking workflow.
- Prepare recurring performance reports for delivery by email or Slack, depending on the configured workflow.

## Workflow documentation

Document each Zap separately, including:

1. Trigger application and event.
2. Data fields retrieved from the source.
3. Filters and conditional rules.
4. Google Sheets actions and field mappings.
5. AI summary prompt and output handling.
6. Reporting schedule and delivery destination.

Only describe steps that are present in the actual Zap configuration. Confirm whether examples such as a less-than-$200 filter are part of the published implementation before documenting them as configured rules.

## Implementation evidence

Add sanitised screenshots under `screenshots/`, for example:

- Zap workflow overview.
- Invoice tracker with synthetic or anonymised data.
- AI summary output.
- Scheduled report configuration or test output.

If exporting workflow configuration is supported, add a sanitised export and explain any setup requirements.

## Security and privacy

Do not publish QuickBooks credentials, Zapier connection details, API keys, customer names, real invoice numbers, email addresses or confidential financial records. Use synthetic or anonymised examples in public evidence.

## Notes

This project is an invoice and reporting automation use case. Keep the description factual and avoid publishing performance claims unless they have been measured and verified.
