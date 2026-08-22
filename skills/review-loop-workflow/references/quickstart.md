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
5. If a required specialist skill is missing, use or recommend `skill-installer` before considering fallback.

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

## Literature Quantity Gate

For a full review manuscript, use 50 papers as the default minimum evidence-pool target.

If the user provides fewer than 50 papers, pause before PDF processing and ask whether they want a more comprehensive literature search first.

If a nested literature-search specialist skill returns fewer than 50 retained candidate papers after first-pass screening, run a broader second-pass search before closing Part 1. Lower relevance only one controlled level at a time, document the broadening rules, and label broadened papers with `relevance_tier`, `search_pass=broadening`, and `inclusion_reason`.

If fewer than 50 papers remain after broadening, continue only with a documented saturation or scope exception.

## Common Fallbacks

If a specialist skill is unavailable:

- First try to use or recommend `skill-installer` when a trusted source is available.
- Record the missing skill name, stage, installation source, install result, and user decision if confirmation is required.
- Use fallback only if installation is unavailable, fails, or the user explicitly declines installation.
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
