# Eval Set Evaluation for Agent Engine agents -refernce based metrics

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GaneshkrishnaL/gemini-agent-golden-set-eval/blob/main/01_golden_set_eval_report.ipynb)
[![View on nbviewer](https://img.shields.io/badge/view-nbviewer-orange)](https://nbviewer.org/github/GaneshkrishnaL/gemini-agent-golden-set-eval/blob/main/01_golden_set_eval_report.ipynb)
[![Sample report](https://img.shields.io/badge/sample-HTML%20report-blue)](https://ganeshkrishnal.github.io/gemini-agent-golden-set-eval/eval_report.html)

notebook that runs a golden-set CSV against an agent deployed on
Google Cloud Agent Engine, grades every case with an LLM judge, and renders an
HTML report.

## Viewing this notebook

Two things do not render on GitHub. Neither is a fault in the notebook.

| On GitHub you see | Why | Look here instead |
|---|---|---|
| Forms shown as commented code | Colab forms are a Colab-only feature; no other viewer renders them | [Open in Colab](https://colab.research.google.com/github/GaneshkrishnaL/gemini-agent-golden-set-eval/blob/main/01_golden_set_eval_report.ipynb) |
| Report shown as `<IPython.core.display.HTML object>` | GitHub strips `text/html` output from notebooks for security | [nbviewer](https://nbviewer.org/github/GaneshkrishnaL/gemini-agent-golden-set-eval/blob/main/01_golden_set_eval_report.ipynb) or the [rendered sample report](https://ganeshkrishnal.github.io/gemini-agent-golden-set-eval/eval_report.html) |

`docs/eval_report.html` is the report from a real run, committed so the output is
viewable without running anything. All project, agent and session identifiers in
this repo are placeholders.
