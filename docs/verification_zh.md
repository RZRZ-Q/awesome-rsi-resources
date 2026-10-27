# 核验与整理记录

[English](verification.md) | **简体中文**

[资源目录](../README_zh.md) · [学习指南](learning-guide_zh.md) · [实践指南](practice-guide_zh.md)

本档案保留 **2026-10-22、2026-10-23、2026-10-25、2026-10-26 和 2026-10-27** 的来源核验记录。下文的日期、版本、仓库覆盖与运行边界均以各次记录为准；迁移到独立文档不代表重新核验上游内容。

- [近期综述覆盖表](#survey-coverage)
- [核验历史与扩展排漏](#review-log)
- [逐项资源核验记录](#verification)

<a id="survey-coverage"></a>

## 近期综述覆盖表

**核验日期：2026-10-22。** “已覆盖”指本目录已收录的至少一个仓库明确链接该论文，或托管作者 PDF。下表 12 篇均已找到对应入口。2026-10-22 检查了 17 个已收录研究索引、综述配套及阅读札记仓库的 README，并检查了 Prism 论文数据。仓库列列出该范围内确认的匹配，简称链接指向对应仓库。可结合[综述阅读路线](learning-guide_zh.md#survey-reading-path)选择起点。

论文日期按行分别采用 arXiv 首次提交日期、Preprints.org 的 **Posted** 发布日期或作者标注日期。版本列记录截至本次核验能确认的最新版本；PDF 上传日期是文件历史依据，不作为论文出版日期。

| 论文 | 论文日期与口径 | 最新已核实版本／日期 | 已确认包含它的已收录仓库 |
| --- | --- | --- | --- |
| [From Existing Methods to New Research Ideas: Two Perspectives on Recursive Self-Improvement](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf) | 2026-10-09（PDF 标注） | 作者 PDF 无版本号；[2026-10-14 入库](https://github.com/Prism-Shadow/awesome-rsi/commit/b19bfb7c1ac11250d179a875f483db7089cb4458) | [Prism-Shadow](https://github.com/Prism-Shadow/awesome-rsi) |
| [Recursive Self-Improvement in AI: A Survey](https://www.preprints.org/manuscript/202609.2680) | 2026-09-30（Preprints.org 发布） | v1 · 2026-09-30 | [lobehub](https://github.com/lobehub/awesome-rsi) |
| [Self-Evolving Coding Agents](https://arxiv.org/abs/2608.03392) | 2026-08-04（arXiv v1） | [v4](https://arxiv.org/abs/2608.03392v4) · 2026-09-24 | [Token-Rhythm](https://github.com/Token-Rhythm/awesome-rsi), [jacky-leng](https://github.com/jacky-leng/awesome-rsi), [asimfish](https://github.com/asimfish/awesome_rsi) |
| [The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement](https://arxiv.org/abs/2609.11873) | 2026-09-10（arXiv v1） | [v3](https://arxiv.org/abs/2609.11873v3) · 2026-09-22 | [jacky-leng](https://github.com/jacky-leng/awesome-rsi), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi), [FrontisAI](https://github.com/FrontisAI/Awesome-Self-Improving-Agents), [theseus-labs-rsi](https://github.com/theseus-labs-rsi/awesome-rsi), [asimfish](https://github.com/asimfish/awesome_rsi) |
| [Safety in Self-Evolving Agents: A Survey](https://arxiv.org/abs/2610.00093) | 2026-09-08（arXiv v1） † | [v1](https://arxiv.org/abs/2610.00093v1) · 2026-09-08 | [lobehub](https://github.com/lobehub/awesome-rsi), [xaddwell](https://github.com/xaddwell/awesome-self-evolving-agent-safety) |
| [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/abs/2603.25681) | 2026-03-26（arXiv v1） | [v3](https://arxiv.org/abs/2603.25681v3) · 2026-09-07 | [natnew](https://github.com/natnew/awesome-recursive-self-improvement), [jacky-leng](https://github.com/jacky-leng/awesome-rsi), [Zesearch](https://github.com/Zesearch/self-improvement-llm) |
| [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/abs/2607.07663) | 2026-07-08（arXiv v1） | [v2](https://arxiv.org/abs/2607.07663v2) · 2026-09-06 | [lobehub](https://github.com/lobehub/awesome-rsi), [Persdre](https://github.com/Persdre/awesome-recursive-self-improvement), [Token-Rhythm](https://github.com/Token-Rhythm/awesome-rsi), [jacky-leng](https://github.com/jacky-leng/awesome-rsi), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi), [deepgrounding](https://github.com/deepgrounding/recursive-self-improvement), [Lee1003-lee](https://github.com/Lee1003-lee/Awesome-RSI-Research) |
| [Co-Evolution in Agentic Systems: Toward Self-Directed Evolution Beyond Human Design](https://arxiv.org/abs/2608.10299) | 2026-08-10（arXiv v1） | [v1](https://arxiv.org/abs/2608.10299v1) · 2026-08-10 | [asimfish](https://github.com/asimfish/awesome_rsi) |
| [The Path to Recursive Self-Improving Agents: Foundation, Framework, and Future Directions](https://www.preprints.org/manuscript/202608.0051) | 2026-08-03（Preprints.org 发布） | v1 · 2026-08-03 | [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi) |
| [Self-Improvements in Modern Agentic Systems: A Survey](https://arxiv.org/abs/2607.13104) | 2026-07-14（arXiv v1） | [v1](https://arxiv.org/abs/2607.13104v1) · 2026-07-14 | [lobehub](https://github.com/lobehub/awesome-rsi), [Persdre](https://github.com/Persdre/awesome-recursive-self-improvement), [Token-Rhythm](https://github.com/Token-Rhythm/awesome-rsi), [jacky-leng](https://github.com/jacky-leng/awesome-rsi), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi), [selfimproving-agent](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents), [theseus-labs-rsi](https://github.com/theseus-labs-rsi/awesome-rsi), [Lee1003-lee](https://github.com/Lee1003-lee/Awesome-RSI-Research) |
| [Self-Improving Agents in the Era of Experience: A Survey of Self- to Meta-Evolution](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf) | 2026-06-25（作者发布公告／PDF） | 作者 PDF 无版本号；[2026-06-25 上传](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/commit/16d81a652a75d095e67d50c8c92c61735cfccb7b) | [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi), [FrontisAI](https://github.com/FrontisAI/Awesome-Self-Improving-Agents) |
| [Towards AI That Improves Itself: A Survey of Recursive Self-Improvement](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf) | 出版／提交日期未确认；PDF [2026-09-07 首次入库](https://github.com/Lee1003-lee/Awesome-RSI-Research/commit/f00e049ccc0288b12c787e91ccd89f8c2d0491cf) | 作者 PDF 无版本号；[当前文件更新于 2026-09-09](https://github.com/Lee1003-lee/Awesome-RSI-Research/commit/b724036d3f9e012cd30ce22773559ea32a2b432c) | [Lee1003-lee](https://github.com/Lee1003-lee/Awesome-RSI-Research) |

论文已覆盖不代表每个仓库都链接最新版：在 2026-10-22 核验时，jacky-leng 把代码 Agent 综述固定到 v1、The Last AI 固定到 v2、LLM 技术总览固定到 v1。阅读时可使用上表的版本链接。Frontis 与 Towards AI 核验的是作者托管 PDF；OpenReview 要求浏览器验证，未能确认平台是否另有更新版本。

† 对于 `2610.00093`，arXiv 的页头与版本历史均显示 **2026-09-08**，但编号前缀指向 10 月。本表保留上游日期，差异原因未确认。

<a id="review-log"></a>

## 核验历史与扩展排漏

原有 51 项资源核验于 **2026-10-22**；ACE、Voyager、LongMemEval-V2、RSI Labs、WalkingLabs 前置 Notebook、STOP 与 SICA 于 **2026-10-23** 补入，同日补读相关综述段落并标注实践入口类别；**2026-10-25** 再补 Harness²、HyperAgents、Meta-Harness 与 Airbnb AHO，截至当日共 **62** 项。具体阅读范围记录在下表。新增候选先按项目身份与已有条目排重，再读详情；网站、Notebook 和仓库迁移前后的名称合并处理。读取了项目 README、推荐章节或课程页面，并对涉及实践能力的条目抽查相关代码。**未运行上游教程、调用模型或复现实验，也未逐篇复核清单内的论文。** 视频核验按下表分别覆盖官方课页、主办方介绍、可用讲义与视频元数据；未观看视频或核验逐字稿。

### 2026-10-23：RSI Labs 与 WalkingLabs 覆盖核对

截至 2026-10-23，在已收录的 **17 个索引、103 份文本文件**中，未检出两者的仓库 URL、名称及作者别名。索引范围包括七个 Awesome 清单、九个综述配套仓库及 RSI 研究札记；文件范围包括 README、选定目录数据、研究解读与 Prism 结构化论文／方法数据，不含 PDF、历史提交、Issue 或外链网站。这表示新增了该范围之外的学习入口，不代表其方法是新研究。同日将 STOP 与 SICA 整理为独立源码路线；它们与 RRSI、AgentDescent 已有[所收录索引中的直接链接](https://github.com/pinkbubblebubble/awesome-rsi/blob/c91823d6ebd9969cea3b7b05e20027988ec5308b/README.md)。

### 2026-10-25：扩展排漏

读取了已收录 17 个索引／综述／札记仓库截至当日的 README，加上 Prism 的方法、论文、资源三份结构数据，共 **20 份文本**。Meta-Harness 与 HyperAgents 已被其中的索引链接，例如 [Token-Rhythm](https://github.com/Token-Rhythm/awesome-rsi/blob/87681b460d6420f29f88bc3a2b848ddc6891dd1b/README.md#L260-L261)，但本目录缺少独立实践入口；Harness² 与 Airbnb AHO 的项目 URL、标题或论文 ID 在这些文件中未检出。这是限定范围核对，不含其他子文档、PDF、历史、Issue 或外部网站。新增条目采用原始实现；Meta-Harness 框架与 TB2 产物合并计数，新增中文报告入口仍归入 RSI 研究札记。

### 2026-10-26：实践入口与评测排漏

刷新已收录的 **17 个研究索引／综述配套／札记仓库、94 份文本**：17 份 README 与 77 份目录、结构数据、参考文献及研究札记；不含 PDF、历史提交、Issue 或外链网站。按项目名称、论文 ID 和仓库 URL 排重后，补入 Dream-RSI、MASS、Self-HPO、PAST-Bench、Scale RSI Bench 与 Beagle 六个直接实践入口。下方记录区分论文覆盖与实现入口覆盖；“未检出”仅适用于这次文本范围。固定来源与核验范围见[本轮六项记录](#verification-2026-10-26)。

### 2026-10-27：HarnessPro 实践入口

按名称、论文 ID 和仓库 URL 与本目录排重后，将 HarnessPro 补入现有 Harness 优化分支。它已出现在一个已收录索引中，本次补充直接学习与评测路线。[新增记录](#verification-2026-10-27)区分论文的演化方法与已发布的 Harness 产物、评测代码。

<a id="verification"></a>

## 逐项资源核验记录

**快照日期：2026-10-25。** 下表保留该快照中的全部 62 项资源记录；当前资源目录与总数统一维护在 [README](../README_zh.md)。

下表记录有依据的内容变化、发布或上游自报核验时间；它们与本项目的核验日期不同，也不等同于整个领域的覆盖截止日期。提交日期按 Asia/Taipei 记载，上游直接标注的日期保留原值。

| 资源 | 内容时间与依据 | 核验阅读范围 |
| --- | --- | --- |
| Prism Awesome RSI | [2026-10-15 新增双语文章](https://github.com/Prism-Shadow/awesome-rsi/commit/6cf55d1bbe224ca1c26c2bb5c8b66e429cce220c)；[中文导读 09-20 更新](https://github.com/Prism-Shadow/awesome-rsi/commit/775a1bdbe4dc60c55cd9d32e792d36f2ec658534)。10-19 提交仅更换二维码。综述 PDF 标注 **2026-10-09**，[10-14 加入仓库](https://github.com/Prism-Shadow/awesome-rsi/commit/b19bfb7c1ac11250d179a875f483db7089cb4458)。 | README、导读源码、网站路由与资源配置；未验证筛选网站的全部交互。已读综述 PDF 摘要、目录与 §2；未确认其同行评审状态。 |
| natnew Awesome RSI | [2026-10-18 新增六项研究](https://github.com/natnew/awesome-recursive-self-improvement/commit/b30c5fd2e36fe8a1f8381444e03377bec16135a1)。 | README、Reading Paths 与新增条目的提交差异。 |
| LobeHub Awesome RSI | [2026-10-12 更新证据分层](https://github.com/lobehub/awesome-rsi/commit/874f5c331c6d2deb70954da12ef9df4b9f255ad0)；随后排序与 CI 修改未当作资料新增。 | README 的术语、入门、目录与相关提交差异。 |
| Persdre Awesome RSI | [2026-09-02 整理并澄清分类标签](https://github.com/Persdre/awesome-recursive-self-improvement/commit/cde30351387b4abd23373884e90d508f7368b5ef)。 | README 的定义、分类与学习资源。 |
| Token-Rhythm Awesome RSI | 上游自报 Last verified **2026-08-13**；[同日补充代码入口](https://github.com/Token-Rhythm/awesome-rsi/commit/87681b460d6420f29f88bc3a2b848ddc6891dd1b)。 | 英文目录与维护说明、中文精选和分类入口。 |
| Awesome Self-Improving Agents | [2026-10-19 新增 RHD 条目](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/commit/7ffbe03841e18a21200a0384cb38f868be93bd73)。论文 v1：**2026-07-14**。 | README、README_AGENT 的分类、章节导航和评测说明，及最新条目差异。已核对原论文摘要、目录、讨论 RL 关系的 §§3.2–3.3，以及讨论 SPIRAL 的 §7.3，确认章节阅读入口。**2026-10-23** 补读讨论 ACE 的 §6.1.2 与讨论 Voyager 的 §§6.3.1–6.3.2。 |
| jacky-leng Awesome RSI | 上游核验覆盖至 **2026-10-07**；[10-08 扩充目录与六轴分类](https://github.com/jacky-leng/awesome-rsi/commit/f41e58bdf14a9a52912eefd85e10215587786c24)。 | README、TAXONOMY 与提交差异；推荐源码入口，未验证阅读网站的完整交互。 |
| pinkbubblebubble Awesome RSI | 上游自报 Last reviewed **2026-10-21**；[台北时间 10-22 新增近期资料](https://github.com/pinkbubblebubble/awesome-rsi/commit/c91823d6ebd9969cea3b7b05e20027988ec5308b)。 | 标签、Start here、Harness 和相关集合章节，以及内容提交差异。 |
| The RSI Book | [2026-07-16 新增第 3 章](https://github.com/bhavsarpratik/rsi/commit/7ce1c397323d442744be8d75ba584afca5d46afd)；8 月最新提交为页面设计更新。 | README、第 2 章、Agent 源码与配套 Notebook 的 setup / Agent 单元。 |
| Roloria/rsi-learn | [2026-09-22 加入学习站与模拟器](https://github.com/Roloria/rsi-learn/commit/64fa58065410fdc8d0c1c333f2bfc3d74019145b)。 | README、五阶段路线和模拟器引擎源码。 |
| Ashish Kumar 三篇导读 | [系列页](https://ashishkumar.ai/series/recursive-self-improvement/)与三篇正文均标注 **2026-10-11** 发布。 | 系列目录、三篇正文与篇内学习入口。 |
| learn-deepseek-harness | [2026-08-23 重组为基础 L1–L8 与进阶 L9–L10](https://github.com/Prism-Shadow/learn-deepseek-harness/commit/4c3b6492767f8af9d65a2a97776ed3bea8841aec)。 | 总 README、L1 文档 / 源码 / 依赖、L10 文档。 |
| RSI 研究札记 | [2026-09-08 为汇总报告补充与外部资源的对照](https://github.com/asimfish/awesome_rsi/commit/0dfe9b2bc99663829ca20f3c3481878d795e1865)。 | README 学习路线与综述目录、报告 10／12／32、汇总报告提交差异。报告 32 明确仅基于原论文摘要；未审校翻译或逐项复核所引实验结论。 **2026-10-25** 补读报告 13，重点为第 4 节，用作 Meta-Harness 中文衔接；作者解读与报告数值不等于独立复现。 |
| Lilian Weng Harness 研究长文 | 作者页面标注 **2026-07-04**。 | 设计模式、Harness 优化、未来挑战、基准附录与来源链接；未独立复现所引性能结果。 |
| Datawhale Hello-Agents | 第四章更新于 **2026-05-02**；Extra10 新增于 **2026-05-07**（[章节修复](https://github.com/datawhalechina/hello-agents/commit/3badb16842045cab344bcfe9e6332fb3a39b3653)、[自进化章节](https://github.com/datawhalechina/hello-agents/commit/df79520dbc5bcf62446817fdc2a3ecf67596baa2)）。 | 已读中文 Reflection 章节、配套 Python 代码、API 封装和 Extra10 四类闭环概览。示例保留内存内轨迹并依赖模型评审；未运行代码执行或持久学习实验。 |
| Datawhale Hello Generic Agent | 记忆章节更新于 **2026-04-20**，自进化章节更新于 **2026-04-22**（[记忆章节](https://github.com/datawhalechina/hello-generic-agent/commit/12f085e82f5cee337cc1c033712a7ae9f7c5eb67)、[机制章节](https://github.com/datawhalechina/hello-generic-agent/commit/33d68d2bcef6fd612270402780cc77370f5f87f7)）。 | 已读第 1/4/12 章，并对照[实现版本](https://github.com/lsdefine/GenericAgent/commit/b70079dce7d7768338a17c693f67b9d8dac541b5)核对记忆更新及索引加载代码。两个推荐章节均有实质内容，仍标为 Beta。教程依赖与现实现存在变化，安装应看实现仓库指南；未复现性能主张。 |
| GEPA / DSPy 教程 | [2025-08-14 加入 AIME 教程](https://github.com/stanfordnlp/dspy/commit/abe6487d6e2091a5a59f901a82d7e84850025d81)；[2026-08-27 补充训练 / 验证集划分说明](https://github.com/stanfordnlp/dspy/commit/2a67bcc7a53d204ae6c85eee11b73bc898819d56)。 | 两库 README、AIME Notebook 单元、GEPA optimization 指南、Python 依赖和相关提交变更；未调用模型或复现性能。 |
| TextGrad Notebook | 教程来自 2024 年；[2024-07-08 重命名为当前 Tutorial-* 路径](https://github.com/zou-group/textgrad/commit/d56d1c1cb50ffe184c46b6ef457bdcd6132c3ace)。 | README、Primitives 与 Prompt Optimization 单元、依赖文件及重命名历史；未向实际端点测试较早的模型 ID。 |
| ShinkaEvolve | [2026-04-07 更新教程示例](https://github.com/SakanaAI/ShinkaEvolve/commit/9b72c250c5c0fccff6e4d5625f4eed76c183e00e)；[07-16 在 Getting Started 中补充 Azure 配置](https://github.com/SakanaAI/ShinkaEvolve/commit/018cea578f1068cadcc617ec1369ee34b3360fe7)。 | README、Getting Started、Notebook 的环境／配置／圆堆积／结果查看单元、圆堆积运行器与评估器、包依赖及相关提交差异。 |
| OpenEvolve | [2026-10-19 修复示例评估器完整性](https://github.com/algorithmicsuperintelligence/openevolve/commit/bc366807fd05720ababd3491fbba0107bf1742e9)：函数最小化评估器从返回的坐标重新计算目标值。 | README 安装与 Quick Start；函数最小化指南、初始程序、评估器、配置及评估器修复差异。 |
| DGM | [2025-05-30（台北时间）公开核心研究循环](https://github.com/jennyzzt/dgm/commit/682eb38a3eb232f4396924cacd0a083bf1444cf8)。 | README 环境准备、依赖、外层循环及自改进／评估步骤；未独立复现链接中的实验日志与基准结果。 |
| SEAL | [2025-08-02 扩充 general-knowledge 实验并整理路径](https://github.com/Continual-Intelligence/SEAL/commit/6d9c9f9ee392c6cc618e771f399d436d190f6ca4)。 | 总 README、general-knowledge 流程、依赖、TTT server、SFT 数据构建器与训练启动脚本；未运行 GPU 实验。 |
| Agent Lightning | README 宣布于 **2026 年 8 月**发布 v1.0；[2026-08-21 整理教程路径](https://github.com/microsoft/agent-lightning/commit/5415d850af20332442fdb0662458f332c7b1e894)。 | README、安装 / Quick Start / Calc-X 文档、Python 依赖、本地启动脚本、Agent 奖励代码与 GRPO 配置。Calc-X Local Mode 符合启动脚本的工作目录要求，总 Quick Start 的写法不同；未运行训练。 |
| Stanford CS329A | 官网标为 **Autumn 2025**。 | 课程介绍、Schedule 与公开论文阅读入口。 |
| Harvard CS 2881R RSI 专题 | **2025-10-09** 归档讲与 **2026-09-24** 新一届专题。 | 官方课程页、两个讲次的阅读 / 课件 / 代码入口；未观看视频。 |
| ICLR 2026 RSI Workshop | 官网标明活动日期 **2026-04-26**。 | 官方主题、议程和 Accepted Papers 页面。 |
| Building Adaptive AI Agents | [Oracle 于 2026-08-26 宣布课程上线](https://blogs.oracle.com/developers/we-just-launched-a-new-course-on-how-to-build-adaptive-ai-agents)；课页标注更新于 **2026-08-27**。 | 官方课程介绍、课纲、学习入口、访问计划与 Oracle 介绍；未观看视频或核验 Notebook。 |
| Berkeley Advanced LLM Agents MOOC | 官方课纲标为 **Spring 2025**，Jason Weston 讲次日期为 **2025-02-03**。 | 官方课纲、阅读链接，以及讲义中自奖励、迭代优化和元奖励章节；未观看录像或核验 Lean 实验。 |
| 李宏毅 ML 2026 自我成长专题 | 官方课表分别标注 Self-Correction **2026-04-24**、Self-Improving **2026-05-08**、下集 **2026-05-22**。 | 官方课表、视频链接目标和三份 PDF 提取文本；重点读了两份自我成长讲义。未观看视频、未做课程作业；YouTube 字幕提取被登录验证拦截。 |
| 智源 2026 AI 自进化论坛 | 主办方记载论坛举行于 **2026-06-12**；官方 B 站录像上传于 **2026-06-18**。 | 主办方回顾；B 站 API 的 UP 主“智源社区”、9 个分 P、标题、时长和中文语音元数据；P3／P5 已确认，未播放或核验逐字稿。 |
| deepgrounding 综述材料 | **2026 年 7 月**冻结语料；[09-06 发布公开仓库](https://github.com/deepgrounding/recursive-self-improvement/commit/aceac9d8a8e46caa702b9651857380a4729202a7)。arXiv v2：**2026-09-06**。 | README 的复现流程与许可范围、综述分类和语料方法章节；未重新生成语料或图表。仓库稿件自述对应 v1，arXiv 则已有 v2；两者分开标注。 |
| RSI Atlas | [2026-10-22 修复冻结路径匹配](https://github.com/aniruddhaadak80/RSI/commit/f4246024469d7e7eadea7a59db64f8289e57eb2a)；Start 文档页标注 09-18。 | README、Start 页面、Python 引擎、依赖与代码差异。 |
| LLM Technical Overview / Zesearch | arXiv v3 **2026-09-07**。 | 原始摘要、目录、§4.4 与配套仓库按章节组织的阅读表。 |
| Self-Evolving Agents / CharlesQ9 | arXiv v4 **2026-01-16**。 | 原始摘要、定义、目录、评估章节导航及配套 README。**2026-10-23** 补读 §§7.1.2–7.1.4 与 §7.2.1，区分保留能力、效率与组件评测。 |
| Comprehensive Self-Evolving AI Agents / ANative-Lab | arXiv v2 **2025-08-31**。 | 摘要、PDF §3／图 3、方法与评估标题、仓库 README 及旧所有者地址跳转。 |
| Era of Experience / FrontisAI | 作者 PDF 标注 **2026-06-25**，上传于 [16d81a6](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/commit/16d81a652a75d095e67d50c8c92c61735cfccb7b)；讲座举行于 **2026-08-13**，录像上传于 **2026-08-14**。 | 作者 PDF 摘要、目录与 §2；与 Modern Agentic Systems 综述不同。已核对主办方提纲与 B 站 UP 主“青稞社区”、讲者、标题、时长（71:34）和中文语音元数据；未播放或核验逐字稿。OpenReview 返回浏览器验证页。 |
| The Last AI Built by Humans / Theseus | arXiv v3 **2026-09-22**。 | 原始摘要、目录、引言／综述定位及配套阅读路线；未独立复现产业案例主张。 |
| Co-Evolution in Agentic Systems | arXiv v1 **2026-08-10**。 | 原始摘要、目录、§2 定义与三阶段分类、附录 A，以及项目映射涉及的 §§3.1／3.2.1／4.1.2／4.3.1。 |
| Self-Evolving Coding Agents | arXiv v4 **2026-09-24**。 | 原始摘要、目录、§2.3 的持久更新边界及方法／评估章节入口。 |
| Safety in Self-Evolving Agents | arXiv 记录显示 v1 **2026-09-08**。 | 原始摘要与 §2.3–2.4、仓库 README 和语料置信度说明；arXiv HTML 仅呈现部分正文，不宣称全篇核验。 |
| Towards AI That Improves Itself / Lee1003-lee | PDF [首次加入于 **2026-09-07**](https://github.com/Lee1003-lee/Awesome-RSI-Research/commit/f00e049ccc0288b12c787e91ccd89f8c2d0491cf)；[当前 PDF 更新于 **2026-09-09**](https://github.com/Lee1003-lee/Awesome-RSI-Research/commit/b724036d3f9e012cd30ce22773559ea32a2b432c)。这些是文件历史日期，论文确切出版／提交日期仍未确认。 | 作者 PDF 摘要、引言、章节结构、§3–4 与 §5.2，仓库框架及文件历史。PDF 明确链接此仓库；更名前后地址合并为一项。[OpenReview](https://openreview.net/forum?id=I3fKQbRUGy) 及 API 要求浏览器验证，未能核实提交元数据和评审状态；未独立审计引文与所引实验结果。 |
| CORAL | **2026-10-22** 对照[源码版本 0123dfb](https://github.com/Human-Agent-Society/CORAL/tree/0123dfb939b35228cf2c1fde224cd0561e727408)核验；这是审核快照，不是发布日期。 | 作者项目页、README、安装／多 Agent 文档、Python 要求、圆堆积任务／评估器、Docker 预设／网关、CLI 覆盖参数与共享状态代码；确认双 Agent 入口及 §3.2.1 对应，未调用模型或运行 Docker。 |
| CoMAS | **2026-10-22** 对照[源码版本 0d98c97](https://github.com/xxyQwQ/CoMAS/tree/0d98c9755a9f3875888b42101e3db5278d0f9805)核验。 | 官方论文 v2、README、启动器、Agent 配置、交互奖励、按 Agent 优化及权重同步；已核文档硬件配置与 §3.2.1 对应关系，未训练。 |
| R-Zero | [**2025-09-12** 更新 main.sh](https://github.com/Chengsong-Huang/R-Zero/commit/3fa29ff74c2b8062113635b278e7bd4ce0f258a2)；**2026-10-22** 回读当前文件。 | 官方论文摘要、README、交替循环、两类启动器、一致性奖励、Solver 服务、伪标签筛选／上传、依赖与 GPT 复核；§4.1.2 是目录学习映射，未训练、上传数据或调用 API。 |
| JaxUED | **2026-10-22** 对照[源码版本 0f8f128](https://github.com/DramaCow/jaxued/tree/0f8f1284677375b889e4f13a32c9617cd009f8c4)核验。 | 作者论文、README、包依赖、Maze ACCEL／PAIRED 代码及参数文档、上游关闭 W&B 的设置；综述讨论方法论文，JaxUED 是本目录选择的实现。已避开旧 Getting Started 的失效路径，未安装或训练。 |
| OpenSpiel | **2026-10-22** 对照[源码版本 b2e0bc3](https://github.com/google-deepmind/open_spiel/tree/b2e0bc36c352b1b579a6d4403b8a60482695553c)核验。 | 安装／包依赖、fictitious play 与 PyTorch NFSP 示例、DQN／NFSP 代码、参数、默认 CPU 及可利用度评估。缩短训练局数是本目录的学习建议；未安装或训练。 |
| SPIRAL | **2026-10-22** 对照[源码版本 068b06f](https://github.com/spiral-rl/spiral/tree/068b06f6afce2e45ae3eb5d8bf677e9d69c83642)核验。 | 官方论文 v2、README、本地启动器、双方轨迹、角色条件优势、OAT 0.2.1 优化／权重同步与默认评估。Tinker 启动器引用缺失源码，推荐原始本地入口。未训练或调用 API。 |
| SPPO | **2026-10-22** 对照[源码版本 5e61c4e](https://github.com/uclaml/SPPO/tree/5e61c4e90822fe526d8bbe1a50a6e85a85c30911)核验。 | 官方论文 v5、README、三轮脚本、生成／固定 PairRM 评分、SPPO loss、训练配置与无条件数据上传调用。区分核心训练、模型上传开关和数据上传；未安装、训练或上传。 |
| Schmidhuber: RSI Since 1987 | 作者页面标注 **Technical Note IDSIA-9-26，2026 年 9 月**；链接的自修改策略章节发表于 **1997 年**。 | 作者笔记 §§2／7 与原章节摘要／基本概念。未独立审计历史优先权主张，定义和历史叙述明确归于作者观点。 |
| DiscoRL | [Nature 记录](https://www.nature.com/articles/s41586-025-09761-x)：首发 **2025-10-22**；version of record **2025-11-26**。 | 作者项目页与论文 Figure 1、Discovery method、Meta-optimization、Generalization。核对训练 Agent 与学习其更新规则的区别；未审计代码及复现配置。 |
| ScienceBuddy | [arXiv v1](https://arxiv.org/abs/2609.17523v1)，**2026-09-15**；核验时仅列出此版本。 | 原始摘要、§§2.3–2.5／Algorithm 1 与 §4.2。核对交替 Harness 改进／模型 RL，以及保持固定的辅助编辑器／GRPO 规则；未复现产品、代码或实验。 |
| ACE | **2026-10-23** 核验[源码版本 82709de](https://github.com/ace-agent/ace/tree/82709de050e1db6e6ef2f07bcb0393560b94992a)；arXiv v3 **2026-03-29**。 | 作者仓库／论文对应、Apache-2.0 许可、依赖、Formula CLI／数据、逐样本更新、计数／ADD 行为、按验证集选优保存及只评测重载。未安装、调用模型或复现性能；未运行可选去重与 AppWorld。 |
| Voyager | **2026-10-23** 核验[源码版本 55e45a8](https://github.com/MineDojo/Voyager/tree/55e45a880755d0c8c66ca7fb5fe7962ac8974f89)（**2023-07-27**）；论文 v2 **2023-10-19**。 | 作者论文／仓库、MIT 许可、安装与随库技能示例、Python／Node／游戏／模组依赖、技能管理器、critic、学习／推理流程、持久化和检索。未实测旧依赖／模型兼容性；未调用 API 或运行游戏。 |
| LongMemEval-V2 | 论文 v1 **2026-05-12**；[核验源码版本 2cc8c54](https://github.com/xiaowu0162/LongMemEval-V2/tree/2cc8c540bdb87fe6761629b585e727e1c4704520)日期为 **2026-08-10**（台北时间）。 | 于 **2026-10-23** 核对 README、公开数据卡／访问元数据与 Apache-2.0 许可、环境、基线脚本、参数、答案生成／评分流程及论文 §§3.3／5.2。未下载完整数据、调用模型、安装或运行评测。 |
| RSI Labs | 作者[讲解](https://blog.weili.me/posts/recursive-self-improvement-part-1-a-simple-toy-example)标注 **2026-10-05**；[核验源码快照 f784f51](https://github.com/weilinear/rsi_labs/tree/f784f511c3a6e61551188a34eb253ef6e91090fc)日期为 **2026-10-07**（台北时间）。 | **2026-10-23** 核对 README、讲解、餐费 Notebook 的配置、工具检查、改进器自修改、验收与留出诊断单元；区分该原型与后续固定改进器实验。未调用 API 或验证 Colab 运行环境。 |
| WalkingLabs 前置 Notebook | [核验快照 92cd3b2](https://github.com/walkinglabs/self-improving-agent-notebook/tree/92cd3b2f9850f5021e46fa9cca0438a58d353b03)日期为 **2026-10-01**；这是源码快照日期，不是课程发布日期。 | **2026-10-23** 阅读 README、依赖文件与 L07 全部单元，确认真实 API 代码生成、固定设计器、教学算术差错率及内核内 archive。requirements 文件未列 Jupyter / ipykernel。不据此宣称全课已验证；未运行 Notebook。 |
| STOP | [论文](https://arxiv.org/abs/2310.02304)：v1 **2023-10-03**，最新 v3 **2024-08-16**；核验[源码版本 0d6780c](https://github.com/microsoft/stop/tree/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4)，日期 **2023-12-22**（台北时间）。 | **2026-10-23** 核对官方 README、种子改进器、公开／实际元效用、候选接受、动态重载、配置、API 包装与执行保护；区分 scaffold 递归编辑、模型权重更新与每轮性能必升。未安装依赖、执行代码或调用 API。 |
| SICA | [论文](https://arxiv.org/abs/2504.15228)：v1 **2025-04-21**，最新 v2 **2025-05-16**；核验原版[源码版本 ed8275d](https://github.com/MaximeRobeyns/self_improving_coding_agent/tree/ed8275dca4d3c5dbf77229964351fe9b424797dc)，日期 **2025-04-24**（台北时间）。 | **2026-10-23** 核对 README／构建配置、评测循环、父代与改进器分别选择、归档模块命令与相对导入、元改进工具、评分保存、模型配置与实际 CLI 参数。未构建 Docker、调用模型或运行 benchmark；未测试旧模型的可用性。 |
| Harness² | [论文](https://arxiv.org/abs/2610.14224) v1 **2026-10-09**，为当前唯一版本；核验[源码 1cfe254](https://github.com/google-research/harness2/tree/1cfe254e8d25b15f37048c3730134686abe60335)，**2026-10-14**（台北时间）。 | **2026-10-25** 核对官方论文／代码对应、论文 §2、依赖、Setup／Experiments、Demo、调度器、经验库、上下文与递归代码。区分固定演示与模型驱动的经验库复用，确认缺少 `.env.example`；未运行演示、benchmark 或模型。 |
| HyperAgents | [论文](https://arxiv.org/abs/2603.19461) v1 **2026-03-19**，为当前唯一版本；核验[源码 59a68f6](https://github.com/facebookresearch/HyperAgents/tree/59a68f672dfb92c74aeb7e61535d776fb36e172d)，**2026-04-15**（台北时间）。 | **2026-10-25** 核对 README／许可、环境与领域数据、生成循环、父代补丁应用、元 Agent 调用、受保护领域代码恢复、Docker 配置和 CLI 参数。未安装、构建容器、调用模型或运行评测。 |
| Meta-Harness | [论文](https://arxiv.org/abs/2603.28052) v1 **2026-03-30**，为当前唯一版本；核验主框架[源码 8123cca](https://github.com/stanford-iris-lab/meta-harness/tree/8123ccabe2b19fa1123090b2e5f1bacc20963ce8)，**2026-10-02**（台北时间）。 | **2026-10-25** 核对作者论文／框架／产物仓库链接、文本分类 README、依赖、模型配置、提案器包装、内外循环、评测与最终封存。独立 TB2 产物合并计数，未审计其完整运行环境；未调用模型或复现实验。 |
| Airbnb AHO | [论文](https://arxiv.org/abs/2609.05736)：v1 **2026-09-04**，最新 v2 **2026-09-09**；[首个公开源码 0d7652b](https://github.com/airbnb/agent-harness-optimizer/tree/0d7652b42296c8df07532fa3787fc956250741e7)，**2026-08-31**（台北时间）。 | **2026-10-25** 核对论文／官方仓库对应、§§3–4、README、依赖、BFCL 数据布局、CLI、BetterHarness 提案／验收／保存、中间件范围与 scorecard 启用条件。未安装、调用模型或运行 benchmark。 |

<a id="verification-2026-10-26"></a>

### 2026-10-26：新增实践入口

以下六项按 **2026-10-26** 的上游来源核验；新增记录不改变上方 2026-10-25 历史快照。“最新版本”指本次核验时列出的版本。已读文档与所列源码，**未安装这些项目、调用模型、训练或复现实验**；完整运行条件集中在[实践指南](practice-guide_zh.md)。

| 资源 | 日期与固定来源 | 核验阅读范围 | 已收录索引中的覆盖情况 |
| --- | --- | --- | --- |
| [Dream-RSI](practice-guide_zh.md#dream-rsi) | [论文](https://arxiv.org/abs/2609.14858)：v1 **2026-09-14**，最新 [v2](https://arxiv.org/abs/2609.14858v2) **2026-10-06**；官方[源码 8ec35bd](https://github.com/google-research/dream-rsi/tree/8ec35bd2538220517ce1bfca4282db21b8c518db)。 | README、任务配置、启动脚本，以及 `orchestrate.py` 的探索／回放／策略选优。核对保留的探索策略如何进入下一轮；基础 coding agent 与评测器保持固定。dry-run 检查配置和凭证，不运行改进。 | 名称／论文命中 4 个仓库：[Prism-Shadow](https://github.com/Prism-Shadow/awesome-rsi/blob/2b2ddc085be7d62613140ac74964b2f00997b6f1/README.md#L125), [jacky-leng](https://github.com/jacky-leng/awesome-rsi/blob/f1888cd25e2dc6150e5c300046598d789b03ceda/README.md#L259), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi/blob/6785f5e3037be374504039e0a6e582026f90e5c2/README.md#L149), [theseus-labs-rsi](https://github.com/theseus-labs-rsi/awesome-rsi/blob/74ee83ec39ae5653d1ff3a151f78042a7774c9a4/README.md#L70)。所查文本未出现新的 `google-research/dream-rsi` URL；旧作者页面现已指向新实现。 |
| [MASS](practice-guide_zh.md#mass) | [论文](https://arxiv.org/abs/2610.12176)：v1 **2026-10-08**，当时唯一列出版本；[官方博文](https://sakana.ai/mass/) **2026-10-12**；[源码 fb40358](https://github.com/SakanaAI/mass/tree/fb403581bed2c974b3f99e7236224169da643079)。 | README、运行／论文代码对应文档与两轮配置：共享模型的三角色及搜索到训练的交接。`plan` 无需 GPU，也不调用模型。打包 MLR 配置覆盖旧 12 任务子集；RHI 参照与选优实现和论文 Algorithm 1 有差异。 | 命中 2 个仓库：[natnew](https://github.com/natnew/awesome-recursive-self-improvement/blob/be444d5e019290f5f1c552a6a405e9be10450f78/README.md#L160), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi/blob/6785f5e3037be374504039e0a6e582026f90e5c2/README.md#L177)。 |
| [Self-HPO](practice-guide_zh.md#self-hpo) | [论文](https://arxiv.org/abs/2610.22791)：v1 **2026-10-16**，当时唯一列出版本；[源码 3c3d0bd](https://github.com/MSR-Orchard/Self-HPO/tree/3c3d0bd93a8a5a72399c855783460b141ea27d49)。 | README、H-step 提案器、P-step 与策略导出脚本：更新后的策略参与下一轮 Harness 提案。区分 `PROPOSER=self` 与固定外部模型的 `PROPOSER=api`。文档中的 8×B200 是实验配置，不是已确认的最低门槛。 | 命中 1 个仓库：[pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi/blob/6785f5e3037be374504039e0a6e582026f90e5c2/README.md#L226)。 |
| [PAST-Bench](practice-guide_zh.md#past-bench) | [论文](https://arxiv.org/abs/2608.04003)：v1 **2026-08-04**，当时唯一列出版本；[源码 f822351](https://github.com/Gen-Verse/PAST-Bench/tree/f8223517ae7491e776b69793d9f11e9d074ab42e)。本目录新增入口，并非 10 月新论文。 | README 的 smoke test／序列比较说明与 `pyproject.toml` CLI 入口。核对新会话中保留／不保留经验的对照、`sequence_comparison.json` 及 Docker／Agent／裁判前置条件。 | 名称／论文命中 7 个仓库：[Lee1003-lee](https://github.com/Lee1003-lee/Awesome-RSI-Research/blob/c218a38901f9a6fde720e0d4cf9772b677d63876/README.md#L143), [Prism-Shadow](https://github.com/Prism-Shadow/awesome-rsi/blob/2b2ddc085be7d62613140ac74964b2f00997b6f1/README.md#L424), [Token-Rhythm](https://github.com/Token-Rhythm/awesome-rsi/blob/87681b460d6420f29f88bc3a2b848ddc6891dd1b/README.md#L465), [asimfish](https://github.com/asimfish/awesome_rsi/blob/06f599b6b8a4cb57558380b68a23ea729479d98a/reports/29_prism_awesome_rsi.md#L79), [jacky-leng](https://github.com/jacky-leng/awesome-rsi/blob/f1888cd25e2dc6150e5c300046598d789b03ceda/README.md#L398), [pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi/blob/6785f5e3037be374504039e0a6e582026f90e5c2/README.md#L416), [selfimproving-agent](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/blob/d89d1adec7ef20553ca137a9eecee8d624ecd8c4/README.md#L700)。asimfish 的匹配为报告中的名称提及，不是直接项目链接。 |
| [Scale RSI Bench](practice-guide_zh.md#scale-rsi-bench) | 未确认正式发布日期及独立论文。[GitHub 元数据](https://api.github.com/repos/scaleapi/rsi-benchmark)记录创建于 **2026-07-30 UTC**，不等同于发表日期。已读[源码 d9f7dcb](https://github.com/scaleapi/rsi-benchmark/tree/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354)。 | README 任务说明、nanoGPT 样例约束、运行器配置、GPU sandbox 要求及[官方网站](https://www.rsi-benchmark.com)。README 的四类公开样例用于选择学习入口，不作为当前任务总数；与其他同名评测保持区分。 | 94 份所查文本未检出对应项目名称／URL；不代表 17 个仓库的所有文件均未覆盖。 |
| [Beagle / DarwinX](practice-guide_zh.md#beagle) | README News：Beagle 于 **2026-09-02** 开源，**2026-10-14** 更新 DarwinX 结果；[源码 73e112f](https://github.com/SalesforceAIResearch/Beagle/tree/73e112f892aefe6226e4ee7723f23ae849eeb13f)。结果更新日不是发布日期。 | README Quick Start、演化示例、接入实验仓库／推送候选的行为、dry-run 参数及配置角色。区分 evolvee、evolver 与固定算法，归为相关机制／实验框架。dry-run 只预览计划，不代表演化成功或 evolver 自身改进。 | 未命中 Beagle 名称／URL，但 DarwinX 论文已有入口，例如 [Prism-Shadow](https://github.com/Prism-Shadow/awesome-rsi/blob/2b2ddc085be7d62613140ac74964b2f00997b6f1/README.md#L134)；缺少的是配套平台入口。 |

<a id="verification-2026-10-27"></a>

### 2026-10-27：HarnessPro

于 **2026-10-27** 核对论文与官方源码，本次新增一项记录，不刷新前面的历史快照。**未安装项目、调用模型、运行 benchmark 或演化实验。** 完整运行条件见[实践指南](practice-guide_zh.md#harnesspro)。

| 资源 | 日期与固定来源 | 核验范围 | 已收录索引中的覆盖 |
| --- | --- | --- | --- |
| [HarnessPro](practice-guide_zh.md#harnesspro) | [HarnessPro: Recursive Harness Self-Improvement with Pareto Optimization for Performance-Cost Trade-offs](https://arxiv.org/abs/2610.26770)：v1 **2026-10-19**，最新 [v2](https://arxiv.org/abs/2610.26770v2) **2026-10-20**；官方[源码 8ae622e](https://github.com/pzs19/HarnessPro/tree/8ae622eb4a4923dbb4b515be7ded614f88fd4f38)。属于方法论文，不是综述。 | 论文 §§3–4 与产物说明；README、评测指南、发布目录、TB2 策略／hook、runner 参数与数据检查。确认公开内容为九套已选 Harness 及评测代码，未发布端到端演化 runner。核对单任务参数与前置条件；GLM-5.2 演化快照未包含。 | 2026-10-26 对 17 个仓库、94 份文本的扫描中，[pinkbubblebubble](https://github.com/pinkbubblebubble/awesome-rsi/blob/6785f5e3037be374504039e0a6e582026f90e5c2/README.md#L221)已链接该工作。该限定范围不含 PDF、历史、Issue 与外链网站；本次补入未重新执行完整扫描。 |
