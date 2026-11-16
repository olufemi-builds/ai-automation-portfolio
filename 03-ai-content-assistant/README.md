# 03 — Build an AI Content Assistant

**Platform:** n8n  
**AI service:** OpenAI

## Objective

Build an AI-assisted workflow that accepts text, processes it using a model, and passes the generated result to a downstream step.

The assistant may be configured for a text-processing task such as summarisation, reply drafting or classification. This documentation should be updated to name the exact task implemented in the published workflow.

## Workflow design

1. Receive source text through the configured trigger.
2. Pass the text and task instructions to the AI node using mapped workflow data.
3. Send the model output to the configured downstream action.
4. Review output quality and test edge cases.

## Prompt development

Document three prompt iterations:

- **Version 1:** initial instruction and its limitations.
- **Version 2:** improved instruction with clearer context, constraints and output format.
- **Final version:** the prompt used in the tested workflow.

Store the comparison in [prompts/prompt-comparison.md](./prompts/prompt-comparison.md).

## Human review and reliability

AI output can be incomplete, inaccurate or unsupported by the input. Define a human review point before generated content is sent externally or used for consequential decisions.

## Implementation evidence

Add the sanitised workflow export and screenshots:

- `workflow.json`
- `screenshots/workflow-canvas.png`
- `screenshots/test-execution.png`

Never include API keys, credentials, private source text or personal information in committed files.
