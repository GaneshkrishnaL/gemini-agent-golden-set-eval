# Golden Set Evaluation for Agent Engine agents

A single Colab notebook that runs a golden-set CSV against an agent deployed on
Google Cloud Agent Engine, grades every case with an LLM judge, and renders an
HTML report.

Built so that the person who owns the test cases does not have to be the person
who owns the code. They fill in a spreadsheet, upload it, and read a report.

## What it does

1. You point it at a deployed agent (`reasoningEngines/...`).
2. You upload a CSV of questions plus the answers you expect.
3. It runs each question against the live agent and captures the tool calls.
4. An LLM judge scores every case 1-5 on four metrics.
5. You get an HTML report with per-case justifications, token counts, and cost.

Metrics: `final_response_quality`, `tool_use_quality`, `hallucination`, `safety`.
A case passes only when every metric clears your threshold.

## Using it

Open the notebook in Colab or Colab Enterprise, then:

**Step 1** — set `PROJECT_ID` and `AGENT_RESOURCE_NAME`. Leave `JUDGE_LOCATION`
on `global` (see the note below).

**Step 2** — run the template cell to download `golden_set_template.csv`, fill it
in, and upload it. CSV, Google Sheets, GCS, and local paths are all supported.

**Steps 3-6** — `Runtime > Run all`. Nothing else to configure.

### Golden set format

| Column | Required | Notes |
|---|---|---|
| `case_id` | yes | Unique. Prefix `b1_`, `b2_` to group cases into buckets. |
| `question` | yes | What a user would actually type. |
| `expected` | yes | The correct answer, in plain English. |
| `must_include` | strongly | The 3-4 facts the answer must contain. Separate with `;` |
| `must_not_include` | no | Phrases that must never appear. Separate with `;` |
| `expected_tools` | no | Which tools should be called, in order. Separate with `;` |
| `active` | no | `FALSE` parks a row without deleting it. |

Write the checklist, not a polished sentence. The judge grades meaning, so
`prior authorization; 6 weeks; conservative therapy` scores far more reliably
than a paragraph.

## Two things worth knowing

**Keep `JUDGE_LOCATION` on `global`.** Gemini 3.x models return 404 on regional
endpoints such as `us-central1`. Only the older 2.5 models serve regionally, and
those are being retired. The notebook keeps the agent endpoint and the judge
endpoint separate for this reason.

**Reference-based vs reference-free.** The four metrics here judge the trace on
its own merits and do not require ground truth, so they also work on production
traffic. Your `expected` column feeds the judge extra context and drives the
`must_include` checklist. If you want strict ground-truth scoring, look at the
`FINAL_RESPONSE_MATCH` metric in the Agent Platform evaluation service.

## Saved outputs

The committed notebook keeps the outputs from a real run, so you can see what the
report looks like without running anything. All project ids, agent ids, and
session ids in those outputs are placeholders.

## Requirements

- A deployed Agent Engine agent
- `roles/aiplatform.user` on the project
- Colab, Colab Enterprise, or any Jupyter runtime with Google credentials

The notebook installs `google-cloud-aiplatform[agent_engines]` and `google-genai`
in its first cell.
