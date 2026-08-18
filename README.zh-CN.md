\# review-loop-workflow-skill 中文说明



`review-loop-workflow` 是一个用于 Codex 的本地综述写作工作流 skill。它的目标不是让 Codex 凭感觉一次性写出综述，而是把综述拆成一个可追踪、可回退、可审稿、可评分的闭环。



\## 核心原则



每个阶段都必须先声明并调用相关 specialist skill，不能直接开始做。



每个阶段开始时，Codex 必须说明：



```text

本阶段使用 skill：...

使用原因：...

输入文件：...

预期输出：...

进入下一阶段的检查标准：...

如果相关 skill 不可用，必须说明 fallback 和风险，不能伪造文献、DOI、PDF 内容、审稿意见或评分。

Workflow 总览

```mermaid

flowchart TD

&#x20; A\[Part 0 Scope 确定主题与范围] --> B\[Part 1 Literature Search 文献检索]

&#x20; B --> C\[Human Download 人工下载全文]

&#x20; C --> D\[Part 2 Knowledge Base 全文处理与知识库]

&#x20; D --> E\[Part 3 Drafting 系统写作初稿]

&#x20; E --> F\[Figure/Table Module 图表与机制图]

&#x20; F --> G\[Part 4 Mock Review 模拟审稿]

&#x20; G --> H\[Part 5 Revision 定向修改]

&#x20; H --> I\[Final Gate 批判性评分]

&#x20; I -->|score >= 85| J\[Final Packaging 输出 Word/Markdown/图表]

&#x20; I -->|75-84| H

&#x20; I -->|evidence weak| D

&#x20; I -->|coverage weak| B

```







阶段与推荐 skill

阶段	目的	推荐 skill

Part 0 Scope	定义主题、综述类型、目标读者、纳入/排除标准	academic-writing, literature-review, markdown-mermaid-writing

Part 1 Literature Search	检索、筛选、排序、生成下载清单	literature-search, pubmed-search, paper-lookup, nature-academic-search, deep-research

Human Download	用户下载 PDF/HTML 并填写本地路径	无需 specialist skill，但必须维护 manifest

Part 2 Knowledge Base	阅读全文、提取证据、建立 claim map	pdf, pdf-processing, markitdown, nature-reader, literature-review, citation-management

Part 3 Drafting	从知识库写综述初稿	nature-writing, nature-citation, nature-polishing, academic-writing, scientific-writing

Figure/Table Module	制作图表、机制图、综合表	nature-figure, scientific-schematics, imagegen, data-visualization-expert

Part 4 Mock Review	模拟审稿人找 major concerns	nature-reviewer, peer-review, scholar-evaluation, scientific-critical-thinking

Part 5 Revision	根据审稿意见逐条修改	nature-response, nature-polishing, nature-citation

Final Gate	严格评分并决定是否输出终版	nature-reviewer, scholar-evaluation, scientific-critical-thinking, nature-citation

Final Packaging	导出 Word、Markdown、图表	docx, documents:documents, markitdown





85 分 Final Gate

最终评分采用 100 分制：

维度	权重

研究问题与范围清晰度	10

文献覆盖与检索可复现性	15

主题综合深度	15

证据强度与引用准确性	20

批判性与争议处理	10

结构与叙事逻辑	10

Nature-style 可读性	10

图表、术语和格式完整性	5

局限与未来方向	5





判定规则：

>= 90：强版本，可进入最终润色和格式整理。

85-89：可作为最终候选稿，但需要记录残余风险。

75-84：不能输出终版，回到 Part 5 修改。

< 75：回到 Part 4 重新审稿，必要时回到 Part 2 补知识库。

新项目调用示例

使用 review-loop-workflow，帮我为一个新综述创建 loop。

主题是：...

文献目录是：...

最终输出 Word + Markdown + 图表 + final scorecard。

