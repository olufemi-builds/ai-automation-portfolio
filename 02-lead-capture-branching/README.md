# 02 — Lead Capture with Branching Logic

**Platform:** n8n  
**Supporting services:** Google Forms and Google Sheets

## Objective

Capture submitted lead information and route each record according to a defined condition.

## Workflow design

1. Receive a form submission or new lead record.
2. Evaluate a condition using an IF node.
3. Route records that meet the condition to a notification action.
4. Route records that do not meet the condition to a nurture/logging destination.
5. Test both branches with separate sample records.

## Validation

The project should include evidence that:

- The condition evaluates correctly.
- The true branch sends the intended notification.
- The false branch records the lead in the intended sheet.
- Field mappings preserve the required lead details.

## Implementation evidence

Add the sanitised workflow export and screenshots:

- `workflow.json`
- `screenshots/workflow-canvas.png`
- `screenshots/true-branch-notification.png`
- `screenshots/false-branch-sheet-log.png`

## Data minimisation

Only collect and transfer fields needed for the workflow. Use synthetic or anonymised lead records in public screenshots and examples.

## Configuration

Document the condition and the destination fields used in your actual implementation. Do not publish credentials or private lead data.
