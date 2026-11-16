# 03 — AI Content Assistant

**Platform:** n8n  
**Input:** Google Sheets (new row trigger)  
**AI model:** GPT-4o mini  
**Output:** Google Sheets (append row)

## Objective

Build an AI-assisted article summarisation workflow that reads newly added article records from a Google Sheet, generates a concise summary, and stores the result in a separate output sheet for human review.

## Workflow

`Google Sheets Trigger` → `Message a model (GPT-4o mini)` → `Append row in sheet`

1. The input Google Sheet receives a new row containing an article title in `Name` and article content in `Text`.
2. The Google Sheets Trigger polls for newly added rows every minute.
3. The OpenAI node sends the title and article text to GPT-4o mini.
4. The prompt requests exactly two concise sentences and instructs the model to use only the supplied article without inventing facts or adding external information.
5. The output Google Sheets node appends the article title, generated summary and `Pending human review` status to the output sheet.

## Data mapping

| Source / output | Field | Purpose |
|---|---|---|
| Input sheet | `Name` | Article title |
| Input sheet | `Text` | Article body supplied to the model |
| Output sheet | `Name` | Original article title |
| Output sheet | `Summary` | Text returned by the model |
| Output sheet | `Review Status` | Set to `Pending human review` |

## Prompt design

The model instruction asks for exactly two concise sentences, a summary based only on the supplied article, and no invented facts or external information. This is an instruction, not a hard validation rule; review the generated text before use.

## Import and configuration

The committed `workflow.json` is a sanitised export.

1. Import the JSON into n8n.
2. Create or select an input Google Sheet with columns named `Name` and `Text`.
3. Create or select an output Google Sheet with columns named `Name`, `Summary` and `Review Status`.
4. In the Google Sheets Trigger, select your Google Sheets credential and input spreadsheet.
5. In the OpenAI node, select your own OpenAI credential and confirm GPT-4o mini is available.
6. In the Append row node, select your Google Sheets credential and output spreadsheet.
7. Test with a non-sensitive sample article and inspect the summary and review status.
8. Activate the workflow only after confirming the mappings and execution result.

The spreadsheet IDs are placeholders. OAuth credential references and instance-specific metadata have been removed. The imported workflow is intentionally inactive until configured and tested.

## Responsible AI and human review

- Avoid placing confidential or personal information in the input sheet unless you have an appropriate lawful basis and approved processing arrangements.
- Treat model output as a draft, not a verified account of the article.
- Check names, dates, figures, context and omissions against the source article.
- Keep the `Pending human review` status until a person has checked the summary.
- Do not automatically publish or distribute summaries without an explicit review and approval step.

## Current limitations

- The trigger polls every minute; it is not an instantaneous event trigger.
- There is no separate validation branch for missing titles or article text.
- There is no downstream sentence-count validation node.
- The workflow appends each processed record and does not deduplicate repeated article rows.

## Evidence to add

- `screenshots/workflow-canvas.png` — the three connected nodes.
- `screenshots/successful-execution.png` — successful trigger, model and append-row execution.
- `screenshots/output-sheet.png` — sample title, summary and pending-review status, using non-sensitive sample content.
