# Review Loop Workflow Scaffold

Use this scaffold when creating a new literature-review project.

## 00_dashboard.md

```markdown
# Review Loop Dashboard

## Project

- Topic:
- Review type: narrative / systematic / mini-review / perspective / methods review
- Target journal or audience:
- Language:
- Final output: Markdown / Word / figures / tables / scorecard

## Current Stage

- Stage:
- Status:
- Last updated:
- Next action:

## Stage Checklist

| Stage | Status | Main Output | Notes |
|---|---|---|---|
| Part 0 Scope | pending | 01_scope_protocol.md | |
| Part 1 Literature Search | pending | download_manifest.csv | |
| Human Download | pending | local_file_path filled | |
| Part 2 Knowledge Base | pending | claims_evidence_map.csv | |
| Part 3 Drafting | pending | 06_manuscript_draft.md | |
| Part 4 Mock Review | pending | critical_issues.csv | |
| Part 5 Revision | pending | response_to_mock_reviewers.md | |
| Final Gate | pending | final_scorecard.md | |
```

## 01_scope_protocol.md

```markdown
# Scope Protocol

## Review Question


## Scope

- Population/topic:
- Mechanism/domain:
- Time range:
- Databases:
- Included study types:
- Excluded study types:

## Inclusion Criteria

1.
2.
3.

## Exclusion Criteria

1.
2.
3.

## Boundary Topics

Topics that may be discussed only as context:

- 
```

## download_manifest.csv

```csv
id,priority,title,doi,url,download_status,local_file_path,notes
```

## claims_evidence_map.csv

```csv
claim_id,claim,source_id,evidence_type,evidence_strength,section_target,citation_status,notes
```

## critical_issues.csv

```csv
issue_id,reviewer,severity,issue,affected_section,required_action,status,notes
```

## revision_action_tracker.csv

```csv
issue_id,action_type,manuscript_location,revision_summary,citation_or_evidence_added,status,notes
```

## final_scorecard.md

```markdown
# Final Gate Scorecard

## Decision

- Score:
- Pass threshold: 85
- Decision: pass / revise / return_to_review / return_to_knowledge_base

## Rubric

| Dimension | Weight | Score | Rationale |
|---|---:|---:|---|
| Research question and scope clarity | 10 | | |
| Literature coverage and reproducibility | 15 | | |
| Depth of thematic synthesis | 15 | | |
| Evidence strength and citation accuracy | 20 | | |
| Critical thinking and controversy handling | 10 | | |
| Structure and narrative logic | 10 | | |
| Nature-style readability and cross-field expression | 10 | | |
| Figures, terminology, and formatting completeness | 5 | | |
| Limitations and future directions | 5 | | |

## Required Revisions If Score < 85

1.
2.
3.
```
