# Quickstart: Review Loop Workflow

## New Project

User prompt:

```text
使用 review-loop-workflow，帮我为这个主题创建综述 loop：
主题：...
文献目录：...
最终输出：Word + Markdown + 图表 + final scorecard
```

Agent behavior:

1. Invoke `review-loop-workflow`.
2. State the current stage and the specialist skills required.
3. Create the workflow folder and scaffold files.
4. Do not run literature search, PDF processing, writing, review, or revision without declaring the relevant specialist skills.

## Resume Existing Project

User prompt:

```text
使用 review-loop-workflow，继续这个项目：
项目目录：...
请先判断现在应该从哪个 Part 继续。
```

Agent behavior:

1. Inspect `00_dashboard.md`.
2. Inspect `07_revision_loop.md`.
3. Inspect `final_gate/final_scorecard.md` if it exists.
4. Report current stage and recommended next action.

## Mandatory Stage Header

At each stage, begin with:

```text
本阶段使用 skill：...
使用原因：...
输入文件：...
预期输出：...
进入下一阶段的检查标准：...
```

## Common Fallbacks

If a specialist skill is unavailable:

- Search/lookup tasks: use official databases or web only with source links and dates.
- PDF tasks: use local PDF/text extraction tools and mark extracted fields as `needs_author_check`.
- Writing tasks: draft only from the evidence map; use placeholders for unsupported claims.
- Review tasks: label the review as a fallback reviewer simulation, not a Nature-style review.
- Citation tasks: do not invent DOI or bibliographic metadata.

## Trigger Phrases

- 综述 loop
- 文献调研到写作闭环
- 帮我跑综述工作流
- 模拟审稿并修改到 85 分
- review-loop-workflow
- 综述最终输出 Word
