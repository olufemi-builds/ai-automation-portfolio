# Prompt Practice and Reflection

This document records the three prompt iterations used while developing the AI Content Assistant, the observed outputs, and the reflection on factual reliability and human review.

## 1. Prompt 1 — Vague

**Prompt**

> Summarize this text.

**Actual AI output**

> Of course! Please provide the text you'd like me to summarize.

**Observation**

The instruction did not identify or provide the source text, so the model asked for the missing input instead of producing a summary.

## 2. Prompt 2 — Better

**Prompt**

```text
Summarize the following article in two sentences. Include its main topic and key points.

{{ $json.Text }}
```

**Actual AI output**

> The article discusses how artificial intelligence is transforming business operations by automating tasks, analyzing data, enhancing customer service, and aiding decision-making. It also emphasizes the importance of addressing data privacy, accuracy, and the necessity of human oversight during AI implementation.

**Observation**

This version specified the source article text, requested a two-sentence summary and identified the content to prioritise. It did not explicitly tell the model to avoid adding information beyond the source.

## 3. Prompt 3 — Final

**Prompt**

```text
Summarize the following article in exactly two concise sentences.

Article title: {{ $json.Name }}

Article text: {{ $json.Text }}

Use only information from the supplied article. Do not invent facts or add external information.
```

**Actual AI output**

> Artificial intelligence is transforming business operations by automating tasks, analyzing information, enhancing customer service, and aiding decision-making. Organizations must prioritize data privacy, accuracy, and human oversight when implementing AI systems.

**Observation**

The final prompt supplies both the article title and body, specifies exactly two concise sentences, and constrains the model to the supplied source. These instructions reduce ambiguity and discourage unsupported additions, but they do not guarantee factual accuracy.

## 4. What changed between the prompts?

The prompts became progressively more specific:

- **Prompt 1** was vague and did not identify or include the text to summarise.
- **Prompt 2** specified the article text, the two-sentence length and the need to include the main topic and key points.
- **Prompt 3** added dynamic title and text fields, requested exactly two concise sentences, and explicitly prohibited invented facts or external information.

## 5. Where could the assistant hallucinate?

The model could introduce information that is absent from the original article, misrepresent the author's meaning, omit important qualifications, or make unsupported claims while summarising.

Restricting the prompt to the supplied article helps reduce this risk, but does not eliminate it. The generated summary must still be checked against the source.

## 6. Where does a human review the output?

The workflow appends the generated summary to the **AI Content Assistant - Output** Google Sheet with the status **Pending human review**.

A human reviewer compares the summary with the original article, checks factual accuracy and context, and approves it before it is shared outside the team. The workflow does not automatically send or publish the generated summary.

## 7. Workflow summary

The workflow uses a Google Sheets Trigger to detect new rows, an OpenAI model to generate a two-sentence summary, and a Google Sheets Append Row action to save the result for human review.

**Workflow:** Google Sheets Trigger → OpenAI Message a Model → Google Sheets Append Row

**Safety measure:** AI-generated summaries are not automatically sent to external recipients.

## Reflection

The exercise demonstrates how prompt specificity affects the usefulness of model responses. It also shows why prompt constraints should be combined with a human review step: instructions can guide a model, but they cannot independently verify that a summary faithfully represents its source.
