# 01 — Build Your First Workflow

**Platform:** n8n

## Objective

Build a simple automation that connects one trigger to one action, maps at least one field from the trigger into the action, and verifies the result with a test execution.

## Workflow design

1. A configured trigger starts the workflow.
2. The workflow passes a selected trigger field to the next node.
3. An action node processes or delivers the mapped value.
4. A test execution is reviewed to confirm the workflow behaves as expected.

## Implementation evidence

Add the sanitised n8n workflow export and screenshots to this folder:

- `workflow.json` — exported workflow with credentials and sensitive values removed.
- `screenshots/workflow-canvas.png` — workflow canvas.
- `screenshots/successful-execution.png` — successful test execution.

## What to document

- The repetitive task the workflow addresses.
- Why the trigger and action were selected.
- Which trigger field is mapped into the action.
- A testing issue encountered and how it was resolved.

## Security

Do not commit credentials, API keys, tokens, private email addresses or personal data.
