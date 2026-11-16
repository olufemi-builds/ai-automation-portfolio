# 01 — Customer Registration Form Automation

**Platform:** n8n  
**Trigger:** n8n Form Trigger  
**Action:** Insert Row in an n8n Data Table

## Objective

Capture customer registration details through an n8n form and automatically store the submitted values in an n8n Data Table.

## Workflow

`On form submission` → `Insert row`

1. The form collects **Customer Name** and **Email Address**.
2. The Form Trigger starts the workflow when a registration is submitted.
3. The Insert Row node writes the submitted values to the **Customer Registrations** data table.

## Field mapping

| Form field | Data Table column | Expression |
|---|---|---|
| Customer Name | `Customer_Name` | `={{ $json["Customer Name"] }}` |
| Email Address | `Email_Address` | `={{ $json["Email Address"] }}` |

## Import and configuration

The committed `workflow.json` is a sanitised export. Before running it in your n8n instance:

1. Import the JSON workflow.
2. Open the **Insert row** node and select your own **Customer Registrations** data table (or create a table with the two columns above).
3. Save the node configuration and verify the form trigger's test/production URL settings in your instance.
4. Submit a test registration using synthetic data.
5. Confirm that the submitted name and email appear in the corresponding data-table columns.

The original export's instance metadata, pinned test submission and personal email address were excluded. The data-table identifier was replaced with a placeholder, so the node must be configured for your own n8n instance after import.

## Evidence to add

- `screenshots/workflow-canvas.png` — workflow canvas.
- `screenshots/successful-execution.png` — successful execution using synthetic test data.
- Optionally, a screenshot of the resulting data-table row with all personal information masked.

## Privacy and security

Customer names and email addresses are personal data. Use synthetic or anonymised records in public demonstrations. Do not commit real registration submissions, credentials, webhook URLs or private instance identifiers.
