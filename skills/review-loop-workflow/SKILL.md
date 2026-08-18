---
name: review-loop-workflow
description: Run a disciplined literature-review loop for planning, searching, downloading handoff, PDF processing, knowledge-base construction, manuscript drafting, mock peer review, targeted revision, final scoring, and Word/figure output. Use when the user asks to create, run, resume, audit, or deploy a review workflow, especially Chinese requests such as 综述 loop、综述工作流、文献调研到写作闭环、模拟审稿、85分闸门、最终输出 Word.
version: 1.0.0
author: local-codex
---

# Review Loop Workflow

This skill orchestrates a strict, evidence-traceable workflow for literature-review projects. It is a router and governance layer, not a substitute for the specialist skills used inside each stage.

## Core Rule: No Freehand Stage Execution

For every stage, the agent must first identify and use the relevant specialist skill(s). Do not proceed from intuition alone.

At the start of each stage, state:

1. `本阶段使用 skill：...`
2. `使用原因：...`
3. `输入文件：...`
4. `预期输出：...`
5. `进入下一阶段的检查标准：...`

If an expected specialist skill is unavailable, state that clearly and either:

- ask the user whether to continue with a named fallback, or
- continue only with a documented fallback when the task is low-risk and no claims will be fabricated.

Never fabricate literature, DOI metadata, PDF-derived facts, reviewer comments, scores, or claim-evidence support.

## Stage Router

Use this table to select specialist skills.

| Stage | Purpose | Required or Preferred Skills | Main Outputs |
|---|---|---|---|
| Part 0 Scope | Define topic, review type, audience, inclusion/exclusion criteria | `academic-writing`, `literature-review`, `markdown-mermaid-writing` | `00_dashboard.md`, `01_scope_protocol.md` |
| Part 1 Literature Search | Search, screen, rank, and prepare download handoff | `literature-search`, `pubmed-search`, `paper-lookup`, `nature-academic-search`, `deep-research` | `search_plan.md`, `candidate_literature.csv`, `download_manifest.csv`, `02_search_log.md` |
| Human Download Handoff | User downloads PDFs/full texts and fills local paths | no specialist skill required, but preserve manifest contract | updated `download_manifest.csv` |
| Part 2 PDF Processing and Knowledge Base | Read downloaded papers, extract evidence, build claim map | `pdf`, `pdf-processing`, `markitdown`, `nature-reader`, `literature-review`, `citation-management` | `knowledge_base_index.csv`, paper notes, `claims_evidence_map.csv`, `05_theme_synthesis.md` |
| Part 3 Drafting | Draft manuscript from theme synthesis and evidence map | `nature-writing`, `nature-citation`, `nature-polishing`, `academic-writing`, `scientific-writing` | `section_plan.md`, `terminology_ledger.csv`, `06_manuscript_draft.md` |
| Figure/Table Module | Build review figures, tables, graphical abstract if needed | `nature-figure`, `scientific-schematics`, `imagegen`, `data-visualization-expert`, `markdown-mermaid-writing` | `figures/`, synthesis tables, figure captions |
| Part 4 Mock Review | Simulate reviewers and identify major risks | `nature-reviewer`, `peer-review`, `scholar-evaluation`, `scientific-critical-thinking` | `reviewer_reports.md`, `cross_review_synthesis.md`, `critical_issues.csv` |
| Part 5 Targeted Revision | Respond to each major concern and revise manuscript | `nature-response`, `nature-polishing`, `nature-citation`, `academic-writing`, `scientific-critical-thinking` | `revision_action_tracker.csv`, `response_to_mock_reviewers.md`, revised manuscript |
| Final Gate | Strict scoring and pass/fail decision | `nature-reviewer`, `scholar-evaluation`, `scientific-critical-thinking`, `nature-citation` | `final_scorecard.md`, final decision |
| Final Packaging | Export final manuscript and supporting files | `docx`, `documents:documents`, `markitdown` | `.docx`, final `.md`, figures, scorecard |

## Workflow Contract

Before running a project, create or reuse a project folder with this structure:

```text
review_loop_workflow/
  00_dashboard.md
  01_scope_protocol.md
  02_search_log.md
  03_screening_matrix.csv
  04_evidence_extraction.csv
  05_theme_synthesis.md
  06_manuscript_draft.md
  07_revision_loop.md
  LOOP_PIPELINE.md
  WORKFLOW_INTERFACE_CONTRACT.md
  part1_literature_search/
  part2_knowledge_base/
  part3_drafting/
  part4_mock_review/
  part5_revision/
  final_gate/
```

Use `templates/workflow_scaffold.md` when creating a new project.

## Interface Rules

### Part 1 -> Human Download

Must output:

- `candidate_literature.csv`
- `download_manifest.csv`
- `02_search_log.md`

`download_manifest.csv` must include:

| Field | Meaning |
|---|---|
| id | paper ID |
| priority | high / medium / low / core / background |
| title | title |
| doi | DOI |
| url | source URL |
| download_status | not_downloaded / downloaded / unavailable |
| local_file_path | path after user downloads full text |

### Human Download -> Part 2

Do not start Part 2 until downloaded papers have valid local paths, unless the user explicitly asks for a partial run.

### Part 2 -> Part 3

Every strong claim entering drafting must be traceable in `claims_evidence_map.csv`.

### Part 3 -> Part 4

If the manuscript contains `[Evidence needed]` or `[Citation needed]`, Part 4 must treat those as major risks.

### Part 4 -> Part 5

Every major concern must have a unique ID, such as `R1.1`.

### Part 5 -> Final Gate

Every major concern must be one of:

- `resolved`
- `downgraded_with_reason`
- `author_input_needed`

Do not enter Final Gate with unexplained open major concerns.

## Final Gate Rubric

Use a 100-point scale:

| Dimension | Weight |
|---|---:|
| Research question and scope clarity | 10 |
| Literature coverage and reproducibility | 15 |
| Depth of thematic synthesis | 15 |
| Evidence strength and citation accuracy | 20 |
| Critical thinking and controversy handling | 10 |
| Structure and narrative logic | 10 |
| Nature-style readability and cross-field expression | 10 |
| Figures, terminology, and formatting completeness | 5 |
| Limitations and future directions | 5 |

Decision:

- `>= 90`: strong version; proceed to final polishing and formatting.
- `85-89`: acceptable final candidate; record residual risks.
- `75-84`: do not output as final; return to Part 5.
- `< 75`: return to Part 4, and if evidence is weak, return to Part 2.

## Output Discipline

When completing any stage, report:

- files created or updated;
- skills used;
- unresolved risks;
- next recommended stage.

When a user asks to resume a previous project, first inspect `00_dashboard.md`, `07_revision_loop.md`, and `final_gate/final_scorecard.md` if present.

## Local Deployment Note

This skill was created for local Codex use. In a new Codex window, trigger it by saying:

> 使用 `review-loop-workflow` 帮我搭建/运行综述 loop。

Then provide the topic, literature folder, or project folder.
