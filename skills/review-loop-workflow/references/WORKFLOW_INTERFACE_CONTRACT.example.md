# Loop Workflow Interface Contract

这个文件定义每个 Part 之间如何交接，避免后续跑 loop 时材料散掉。

## Part 1 -> 人工下载

必须输出：

- `candidate_literature.csv`
- `download_manifest.csv`
- `02_search_log.md`

`download_manifest.csv` 必须至少包含：

| 字段 | 含义 |
| --- | --- |
| id | 文献编号 |
| priority | high / medium / low / core / background |
| title | 文献题名 |
| doi | DOI |
| url | 原文链接 |
| download_status | not_downloaded / downloaded / unavailable |
| local_file_path | 下载后的本地路径 |

## 人工下载 -> Part 2

进入 Part 2 前，`download_status=downloaded` 的文献必须有本地路径。Part 2 不负责猜测 PDF 在哪里。

## Part 2 -> Part 3

必须输出：

- `knowledge_base_index.csv`
- `04_evidence_extraction.csv`
- `claims_evidence_map.csv`
- `05_theme_synthesis.md`

任何进入初版写作的强结论都必须能在 `claims_evidence_map.csv` 中找到来源。

## Part 3 -> Part 4

必须输出：

- `06_manuscript_draft.md`
- `part3_drafting/terminology_ledger.csv`
- `part3_drafting/claim_evidence_map.csv`

如果正文中有 `[Evidence needed]` 或 `[Citation needed]`，Part 4 必须把它们视为 major risk。

## Part 4 -> Part 5

必须输出：

- `part4_mock_review/reviewer_reports.md`
- `part4_mock_review/cross_review_synthesis.md`
- `part4_mock_review/critical_issues.csv`

每条 major concern 必须有唯一 ID，例如 `R1.1`。

## Part 5 -> Final Gate

必须输出：

- `part5_revision/revision_action_tracker.csv`
- `part5_revision/response_to_mock_reviewers.md`
- 更新后的 `06_manuscript_draft.md`

所有 major concern 必须是：

- resolved
- downgraded_with_reason
- author_input_needed

不能保留无说明的 open 状态进入 Final Gate。

## Final Gate

评分文件：

- `final_gate/final_scorecard.md`

判定：

- `score >= 85`：输出最终版本。
- `score < 85`：根据最低分维度回退到 Part 1-5。

