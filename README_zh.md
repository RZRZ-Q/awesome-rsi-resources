# Awesome RSI Resources

[English](README.md) | **简体中文**

递归自我改进（Recursive Self-Improvement, RSI）学习与研究资源导航。

A curated directory of awesome lists, learning guides, tutorials, and courses on recursive self-improvement.

本项目汇集 RSI 相关的资源集合与学习入口，帮助读者了解每项资源适合谁、值得看什么、从哪里开始，以及内容更新到什么时候。

**最近核验：2026-10-23。** 共收录 56 项资源，涵盖 Awesome 清单、综述、教材、教程、实践项目、课程、视频与复现材料。本轮新增 RSI Labs 与前置 Notebook 课程，并按与 RSI 的关系标注具体实践入口。同一项目的网站、代码和 Notebook 合并介绍。

<a id="resource-scope"></a>

## 资源范围与分类

本目录同时覆盖递归改进，以及学习它所需的机制和工具。以下标签针对**推荐的具体实践入口**及其已展示的范围，参考 [Modern Agentic Systems §3.2](https://arxiv.org/html/2607.13104v1#S3.SS2) 与 [The Last AI §§2.2–2.3](https://arxiv.org/html/2609.11873v3#S2.SS2)，是本目录的学习分类；不同论文采用的定义有所区别。

| 分类 | 入口所讲授的内容 | 本目录示例 |
| --- | --- | --- |
| **递归改进方法** | 保留对 Agent 实现或改进策略的修改，并将其用于后续改进工作。区分教学原型与研究实现；标签本身不代表已实现持续加速。 | [RSI Labs](#tutorials)：小型改进策略实验；[DGM](#practice)：继承的 Agent 代码参与后续自修改。 |
| **相关自改进机制** | 提示词优化、程序搜索、学习适应策略、经验复用或协同适应，也包括入门构件与模拟演示。条目说明改变什么、哪些部分保持固定。 | [GEPA / TextGrad](#tutorials)、[ShinkaEvolve / SEAL / Agent Lightning](#practice)、[ACE / Voyager](#memory-skills)、[协同演化](#coevolution-projects)与[自博弈](#adversarial-self-play)。 |
| **评测工具** | 衡量组件表现，或演示候选修改的验收条件。 | [LongMemEval-V2 与 RSI Atlas](#evaluation)；Atlas 是验收门控教学示例。 |

索引、综述、教材与综合课程仍作为阅读资源，可以横跨多类。记忆评测或固定优化器教程可以为 RSI 学习提供准备，其本身未必展示递归改进循环。需要基础时可先学[前置课程](#prerequisite-courses)，再比较下文的具体机制。

## 从哪里开始

| 你现在想做什么 | 推荐起点 |
| --- | --- |
| 用中文建立 RSI 概念框架 | [Prism 中文图解导读](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md) |
| 用中文和代码学习反思循环 | [Hello-Agents 第四章 §4.4](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter4/第四章%20智能体经典范式构建.md#44-reflection) → Extra10 |
| 跟着中文视频学习自我改进 | [李宏毅 2026 课程](https://speech.ee.ntu.edu.tw/~hylee/ml/2026-spring.php)，从 Self-Correction 和两讲 Self-Improving 开始 |
| 用 Python 搭建第一个 Agent 改进循环 | [The RSI Book 第 2 章](https://thersibook.com/chapters/ch02.html)与配套 Notebook |
| 看清改进从哪里开始递归 | [RSI Labs Notebook 第 4 节](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)：修改改进器的指令，并评估其后续修复选择 |
| 用中文 Notebook 学习 Agent 代码搜索 | [前置课程：WalkingLabs L07](#prerequisite-courses)，固定设计器下的教学示例 |
| 从代码理解 Agent Harness | [learn-deepseek-harness 的 L1](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop)，再按课程顺序学习 |
| 通过评估数据优化可复用提示词 | [GEPA / DSPy AIME Notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb) |
| 根据评估反馈进化一个小程序 | [ShinkaEvolve 教程 Notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) |
| 有 GPU，想用工具反馈训练 Agent | [Agent Lightning Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode) |
| 将经验变成可复用记忆或技能 | [记忆与技能学习项目](#memory-skills)：ACE 文本经验手册，或 Voyager 可执行技能 |
| 评估 Agent 经验记忆 | [LongMemEval-V2](#evaluation)：固定读者模型和问题，对比无检索与 RAG |
| 上手多智能体或 Agent—环境协同演化 | [协同演化项目](#coevolution-projects)：API 路线从 CORAL 开始，RL 路线从 JaxUED 开始 |
| 学习对抗式自博弈 | [对抗式自博弈项目](#adversarial-self-play)：OpenSpiel 基础 → SPIRAL 游戏训练，或 SPPO 偏好博弈 |
| 理解 RL 与 RSI 的关系 | [专题导读](#rl-and-rsi)：策略学习 → 自博弈 → 学习规则与系统改进 |
| 按合理顺序阅读这 12 篇近期综述 | [推荐综述阅读路线](#survey-reading-path)：入门总览 → 方法进阶；可选分支：持续自改进的可靠性与安全控制 |
| 开始系统读论文 | [natnew 的 Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths) |
| 跟着课程学自改进 Agent | [Stanford CS329A](https://cs329a.stanford.edu/)的公开课程表与阅读材料 |

可以按自己的目标选一条短路线：

- **中文学习路线**：Prism 导读 → Hello-Agents Reflection → 可选的 [WalkingLabs 前置 Notebook](#prerequisite-courses) → 李宏毅自我成长讲次 → RSI 研究札记与原始综述。
- **概念入门**：Prism 中文导读 → The RSI Book 第 1–2 章 → natnew 阅读路线。
- **Agent 工程实践**：The RSI Book 的 Python 循环 → learn-deepseek-harness 的分课实现 → selfimproving-agent 综述中的 scaffolding 与 evaluation 部分。
- **优化实践**：GEPA / DSPy → ShinkaEvolve 或 OpenEvolve → 用 DGM 进阶研究 Agent 代码演化。
- **递归改进**：RSI Labs Notebook 第 4 节 → DGM 继承 Agent 代码并继续自修改的循环，对比教学实验与研究实现；若不熟悉候选评估和归档，可先学前置 Notebook。
- **经验与记忆**：Hello Generic Agent → 用 ACE 学习文本经验手册，或用 Voyager 学习可执行技能 → 用 LongMemEval-V2 评估记忆组件；再回到综述学习纵向改进指标。
- **训练与研究**：Stanford CS329A 的 verifier / RL 阅读 → selfimproving-agent 综述中的模型改进部分 → SEAL 适应循环或 Agent Lightning 策略训练 → ICLR RSI 工作坊的相关论文。

## 目录

- [资源范围与分类](#resource-scope)
- [研究索引与 Awesome 清单](#indexes)
- [综述与研究总览](#surveys)
- [近期综述覆盖表](#survey-coverage)
- [推荐综述阅读路线](#survey-reading-path)
- [从综述到实践项目](#survey-project-map)
- [RL 与 RSI：关系、区别和阅读路线](#rl-and-rsi)
- [指南、教材与学习路径](#guides)
- [前置课程](#prerequisite-courses)
- [实践教程](#tutorials)
- [实践项目](#practice)
- [记忆与技能学习项目](#memory-skills)
- [协同演化项目](#coevolution-projects)
- [对抗式自博弈项目](#adversarial-self-play)
- [课程与工作坊](#courses)
- [中文视频课程与研究报告](#videos)
- [评测示例](#evaluation)
- [时效与核验记录](#verification)

<a id="indexes"></a>

## 研究索引与 Awesome 清单

这一类适合找相关工作、比较研究方向和制定阅读顺序。各项目采用自己的 RSI 定义与分类框架，学习时可以互相对照。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [Prism-Shadow/awesome-rsi](https://github.com/Prism-Shadow/awesome-rsi) | 用九个维度组织方法与评测，配有双语图解、论文筛选和引用图谱；适合先建立全景框架。 | 先读[中文 RSI 导读](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md)，再到[网站](https://prism-shadow.github.io/awesome-rsi/#blog/understanding-rsi)查方法与评测。 进阶读其[作者公开综述](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)：§2.3 闭环 → §3 分类 → §4 与深度学习的联系 → §5 评估。 | 中英导读、英文综述；基础 LLM / Agent 概念；纯阅读。 |
| [natnew/awesome-recursive-self-improvement](https://github.com/natnew/awesome-recursive-self-improvement) | 将领域地图与入门、系统构建、安全与边界三条路线结合，适合把零散论文串成阅读顺序。 | [Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths)，先选一条路线再进入主题目录。 | 英文；LLM / 机器学习基础；纯阅读。 |
| [lobehub/awesome-rsi](https://github.com/lobehub/awesome-rsi) | 覆盖模型、Harness、记忆、多 Agent、具身和自动 AI 研究；解释任务收益、保留收益和改进器收益等不同证据层级。 | [Fundamentals & Getting Started](https://github.com/lobehub/awesome-rsi#fundamentals--getting-started) → [Scope & Terminology](https://github.com/lobehub/awesome-rsi#scope--terminology)。 | 英文；LLM / Agent 基础；纯阅读。 |
| [Persdre/awesome-recursive-self-improvement](https://github.com/Persdre/awesome-recursive-self-improvement) | 以“修改对象 × 闭环程度”整理研究，适合辨析不同工作所说的 RSI。 | [What Counts as RSI?](https://github.com/Persdre/awesome-recursive-self-improvement#what-counts-as-rsi)，再按修改对象查论文。 | 英文；机器学习 / Agent 背景；其中层级标签是作者的整理框架。 |
| [Token-Rhythm/awesome-rsi](https://github.com/Token-Rhythm/awesome-rsi) | 双语文献表带日期、主题标签、摘要和论文 / 代码入口，适合按方向查阅。 | [中文精选读物](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#featured-rsi-readings) → [分类概览](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#category-overview)。 | 中英；纯阅读。上游最近核验标为 **2026-08-13**，9–10 月资料宜结合其他目录查阅。 |
| [jacky-leng/awesome-rsi](https://github.com/jacky-leng/awesome-rsi) | 用闭环位置、反馈、搜索、持久状态、人的角色和证据类型六个轴比较改进循环，适合做方法对照。 | [TAXONOMY.md](https://github.com/jacky-leng/awesome-rsi/blob/main/TAXONOMY.md) → [Landscape](https://github.com/jacky-leng/awesome-rsi#landscape)。 | 英文；纯阅读。上游标注核验覆盖至 **2026-10-07**。 |
| [pinkbubblebubble/awesome-rsi](https://github.com/pinkbubblebubble/awesome-rsi) | 用 RSI / Self-improvement / Enabler 标签解释资源与递归改进的关系，兼收 Harness、评测和工程报告，适合寻找近期实践方向。 | [Scope and labels](https://github.com/pinkbubblebubble/awesome-rsi#scope-and-labels) → [Start here](https://github.com/pinkbubblebubble/awesome-rsi#start-here)；实践可看 [Harness 清单](https://github.com/pinkbubblebubble/awesome-rsi#self-improvement-harnesses)。 | 英文；纯阅读。上游自报最近核验 **2026-10-21**；第三方实现各有运行条件。 |

<a id="surveys"></a>

## 综述与研究总览

本轮对照本批整理前已有的 8 个索引的 README／综述栏目、Prism 论文数据与原论文来源，补齐了 LLM 自改进、Agent 自进化、经验驱动 Harness、RSI 自主性路线、协同进化、代码 Agent 和安全等主要综述入口。已收录索引中的间接链接不等于本目录已逐篇核验；这里是有明确阅读入口的精选导航，不是全领域综述的穷尽清单。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [selfimproving-agent/Awesome-Self-Improving-Agents](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents) · [论文](https://arxiv.org/abs/2607.13104) | 综述配套资源，将模型参数改进与 prompt、记忆、工具、完整 scaffold 改进分开，并提供评测和应用领域索引。 | 读[§3 定义 → §4 分类 → §5 模型／§6 scaffold 改进 → §8 评估](https://arxiv.org/html/2607.13104)，再用 [Agent-oriented guide](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/blob/main/README_AGENT.md) 按问题定位章节。 | 英文；机器学习 / Agent 基础；纯阅读，含论文源码。 |
| [deepgrounding/recursive-self-improvement](https://github.com/deepgrounding/recursive-self-improvement) · [论文](https://arxiv.org/abs/2607.07663) | 综述配套仓库，提供冻结文献语料、分类脚本、图表和参考文献生成流程；把部署期改进、训练、自评估与自动研究放在同一分类框架中。 | 先读[综述源码](https://github.com/deepgrounding/recursive-self-improvement/blob/main/draft/main.md)的 §2 与 §5，再看 [Reproducing](https://github.com/deepgrounding/recursive-self-improvement#reproducing)和[语料文件](https://github.com/deepgrounding/recursive-self-improvement/blob/main/artifacts/corpus_v2.csv)。 | 英文；复现需 Python 3.11+、NumPy、Matplotlib，部分脚本访问 arXiv / OpenAlex。语料冻结于 **2026 年 7 月**，9 月公开发布。 |
| [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/abs/2603.25681) · [作者仓库](https://github.com/Zesearch/self-improvement-llm) | 按数据获取、筛选、模型优化、推理改进和自主评估组织模型自改进，适合把分散技术串成完整学习周期。 | 先读[论文引言和 §4](https://arxiv.org/html/2603.25681v3)，重点比较 §4.3–4.4 的自生成优化与自进化优化，再读 §6 自主评估。 | 英文；需要机器学习／LLM 训练背景。TMLR 综述；本轮核验 v3 定稿版。 |
| [A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve](https://arxiv.org/abs/2507.21046) · [CharlesQ9/Self-Evolving-Agents](https://github.com/CharlesQ9/Self-Evolving-Agents) | 比较更新什么、何时适应，以及反馈和种群如何驱动更新；尤其适合区分任务内适应与跨任务学习。 | [§2 定义 → §3–5 分类 → §7 评估](https://arxiv.org/html/2507.21046v4)，选好分支后再从配套列表找实现。 | 英文；需要 Agent／机器学习基础。TMLR 2026；本轮核验 v4，论文版本晚于配套 README 最近的内容更新。 |
| [A Comprehensive Survey of Self-Evolving AI Agents](https://arxiv.org/abs/2508.07407) · [ANative-Lab/Awesome-Self-Evolving-Agents](https://github.com/ANative-Lab/Awesome-Self-Evolving-Agents) | 用系统输入、Agent 系统、环境和优化器说明优化闭环，再区分单 Agent、多 Agent 与领域专用优化。 | 先读[§3 与图 3](https://arxiv.org/pdf/2508.07407v2#page=9)，再读 §4–5 方法和 §7 评估。 | 英文；需要 Agent／优化基础。原 EvoAgentX 仓库地址已跳转至 ANative-Lab，合并为一项资源。 |
| [Self-Improving Agents in the Era of Experience: A Survey of Self- to Meta-Evolution](https://github.com/FrontisAI/Awesome-Self-Improving-Agents) | 沿部署轨迹到可复用技能、持久记忆、环境、模型更新与元层控制组织内容，连接 Harness 工程与经验驱动改进。 | 从[作者公开 PDF](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf) 的 §2（第 5 页）开始，再读 §3–4 与 §7–8；再看姜澈的中文[青稞 Talk 146 录像](https://www.bilibili.com/video/BV13ZgA64Ept/)与[主办方提纲](https://www.qingkeai.online/blog/AI4AI-RSI)。 | 英文论文、中文讲座；需要 Agent／LLM 基础。正文和结构通过作者 PDF 核验；OpenReview 本轮返回浏览器验证页。 |
| [The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement](https://arxiv.org/abs/2609.11873) · [theseus-labs-rsi/awesome-rsi](https://github.com/theseus-labs-rsi/awesome-rsi) | 综述与路线图：比较执行、改进策略、未来经验获取、部署适应和改进机制本身的自主性，并连接应用领域与产业案例。 | [§2.2 改进闭环定义 → §3 自主性层级](https://arxiv.org/html/2609.11873v3)，再使用配套仓库的 [Start Here](https://github.com/theseus-labs-rsi/awesome-rsi#start-here)。 | 英文；需要 Agent／机器学习背景。L1–L5 是该论文的组织框架，不是全领域统一标准；产业案例属于作者报告的证据。 |
| [Co-Evolution in Agentic Systems: Toward Self-Directed Evolution Beyond Human Design](https://arxiv.org/abs/2608.10299) | 聚焦互相适应的 Agent、环境与进化机制，解释协同进化相对固定学习情境的改进闭环增加了什么。 | [§2.2–2.3 定义与三阶段地图 → §3–5](https://arxiv.org/html/2608.10299v1)，附录 A 区分协同进化与相邻概念。 | 英文；需要多 Agent／强化学习基础。综述与概念路线图；元协同进化仍作为新兴方向讨论。 |
| [Self-Evolving Coding Agents](https://arxiv.org/abs/2608.03392) | 按资产、架构和模型参数整理代码 Agent 的持久更新，并梳理代码特有反馈与评估；有助于区分改进当前任务代码与改进未来解题 Agent。 | [§2.3 操作性边界 → §3 分类 → §7–8 反馈与评估](https://arxiv.org/html/2608.03392v4)。 | 英文；需要代码 Agent／软件工程基础。本轮核验 v4；属于阅读材料，不是可运行教程。 |
| [Safety in Self-Evolving Agents: A Survey](https://arxiv.org/abs/2610.00093) · [作者仓库](https://github.com/xaddwell/awesome-self-evolving-agent-safety) | 研究经验成为可复用记忆、技能、工具、工作流或模型状态后，安全属性如何变化；SAVER 串起状态载体、适应操作、违规、暴露与响应。 | 先读[§2.3–2.4：状态转移检查与 SAVER](https://arxiv.org/html/2610.00093v1)，再读配套仓库的 [Overview 与 Corpus](https://github.com/xaddwell/awesome-self-evolving-agent-safety#overview)。 | 英文；需要 Agent／安全背景。配套语料含机器初始化标签与置信度分级，不能视为全部经人工核验的书目。 |
| [Towards AI That Improves Itself: A Survey of Recursive Self-Improvement](https://lee1003-lee.github.io/Awesome-RSI-Research/) · [作者仓库](https://github.com/Lee1003-lee/Awesome-RSI-Research) | 区分“继承已有改进”与“改进机制本身变强”，并关联验证、更新策略和记忆复用。适合学习如何设计与评估持续改进闭环。 | 先读 [§3 定义与主张检验框架](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5)，再读 §4.3（第 14 页）及 §5.2（第 21 页），了解更新与智能体系统演化。 | 英文；需智能体 / 机器学习基础。相关区分属于作者框架；文献表也包含为 RSI 提供支持的相邻方法。作者公开的综述稿件。 |

<a id="survey-coverage"></a>

### 近期综述覆盖表

**核验日期：2026-10-22。** “已覆盖”指本目录已收录的至少一个仓库明确链接该论文，或托管作者 PDF。下表 12 篇均已找到对应入口。本轮检查了 17 个已收录研究索引、综述配套及阅读札记仓库的 README，并检查了 Prism 论文数据。仓库列列出该范围内确认的匹配，简称链接指向对应仓库。本表用于交叉查询，资源总数为 **56**。

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

论文已覆盖不代表每个仓库都链接最新版：jacky-leng 当前把代码 Agent 综述固定到 v1、The Last AI 固定到 v2、LLM 技术总览固定到 v1。阅读时可使用上表的版本链接。Frontis 与 Towards AI 核验的是作者托管 PDF；OpenReview 要求浏览器验证，未能确认平台是否另有更新版本。

† 对于 `2610.00093`，arXiv 的页头与版本历史均显示 **2026-09-08**，但编号前缀指向 10 月。本表保留上游日期，差异原因未确认。

<a id="survey-reading-path"></a>

### 推荐综述阅读路线

本路线使用[覆盖表](#survey-coverage)中的 **12 篇论文及已核实版本**，适合已有基本 LLM 与 Agent 概念的读者。顺序是本目录的学习建议；各论文的定义与自主性等级属于各自作者的框架。章节号对应上述版本，PDF 页码从文件第一页起算。

**核心路线：** Prism → *Self-Improvements in Modern Agentic Systems* → *Towards AI That Improves Itself* → 选一个方法分支。先读下列推荐章节，其余论文用于补充视角，不是额外的必修前置。

#### 1. 入门总览

前两篇按顺序读，再按需选择两篇补充比较。读完应能说明：**改什么、什么会保留到下一轮、如何衡量改进**。

| 论文／路线位置 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **1. 领域总图 — [From Existing Methods to New Research Ideas: Two Perspectives on Recursive Self-Improvement](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)** | 用九个设计维度比较方法，并联系传统深度学习，为构思研究问题提供起点。 | §2.3 RSI 闭环（第 5 页）→ §3.1 分类总览（第 6 页）→ §5 评估（第 17 页）；构思研究方向时再读 §4.2。 |
| **2. 系统总图 — [Self-Improvements in Modern Agentic Systems: A Survey](https://arxiv.org/html/2607.13104v1)** | 区分模型参数更新与提示、记忆、工具、外围控制框架的更新，帮助选择要深入研究的组件。 | §3 定义 → §4 分类 → 工程方向读 §6 scaffold，训练方向读 §5 模型 → §8.1 改进的衡量。 |
| **选读：比较视角 — [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/html/2607.07663v2)** | 从改进对象与闭环由谁验证两个角度比较方法，并将评估器本身作为研究对象。 | §2.1 定义 → §2.2 两轴分类；关注评估时继续读 §§5.1–5.2 的评估器设计与验证层级，再读 §5.5 的结果改进与过程改进。 |
| **选读：系统组成 — [The Path to Recursive Self-Improving Agents: Foundation, Framework, and Future Directions](https://www.preprints.org/manuscript/202608.0051)** | 把模型、Harness、数据系统、训练器和改进机制联系起来，适合理解各组件更新之间的依赖。 | §§2.1–2.3：组件、能力等级，以及诊断—提案—评估—集成闭环 → §6 多组件共同改进。 |

#### 2. 方法进阶

先读 *Towards AI*，再选与自己项目最接近的分支。模型训练、协同演化分支适合有机器学习／强化学习基础的读者；经验与代码分支更直接衔接 Agent 工程。

| 论文／分支 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **共同基础 — [Towards AI That Improves Itself: A Survey of Recursive Self-Improvement](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5)** | 区分继承已接受的改进与改进器本身变强，并关联验证、更新决策和持久记忆。 | §3 定义与主张检验框架（第 5 页）→ §§4.2–4.3 反馈与优化；Agent 工程继续读 §5.2（第 21 页）。 |
| **模型训练 — [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/html/2603.25681v3)** | 串起数据获取与筛选、模型优化、推理改进和自主评估，形成完整的学习生命周期视角。 | §4.1 优化总览 → §§4.3–4.4 自生成优化与自演化优化 → §6 自主评估。 |
| **经验、记忆与技能 — [Self-Improving Agents in the Era of Experience: A Survey of Self- to Meta-Evolution](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf)** | 跟踪执行经验如何进入可复用技能、记忆与更高层控制，连接 Harness 工程与持续学习。 | §2 作为经验基础设施的 Harness（第 5 页）→ §§3–4 技能与记忆 → §§7–8 元演化与纵向评估。 |
| **代码 Agent — [Self-Evolving Coding Agents](https://arxiv.org/html/2608.03392v4)** | 区分修改当前任务的代码与更新供后续复用的 Agent 组件，比较资产、架构和参数三类对象。 | §2.3 操作边界 → §3 分类 → 选读 §4 资产、§5 架构或 §6 参数 → §§7–8 反馈与评估。 |
| **多智能体与环境适应 — [Co-Evolution in Agentic Systems: Toward Self-Directed Evolution Beyond Human Design](https://arxiv.org/html/2608.10299v1)** | 研究 Agent、环境和演化机制之间相互关联的变化，将视角扩展到固定环境以外。 | §§2.2–2.3 定义与阶段总图 → §3 Agent 间或 §4 Agent 与环境的协同演化 → §5 元协同演化；用附录 A 对比相邻概念。 |
| **自主性 — [The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement](https://arxiv.org/html/2609.11873v3)** | 关注系统控制了哪些改进决策、哪些仍由外部决定；其自主性等级帮助在任务得分之外比较系统。 | §§2.2–2.3 概念基础与证据范围 → §3.1 的 B0 参照边界 → §3.7 跨等级综合；再从 §§3.2–3.6 选择感兴趣的等级。 |
| **实验证据 — [Recursive Self-Improvement in AI: A Survey](https://www.preprints.org/manuscript/202609.2680)** | 按工程目标与更新对象组织方法，再区分任务收益、保留收益和改进器的贡献，适合设计对照实验时阅读。 | §3.1 定义 → §4.1 两轴总图 → §6.5 改进器修订 → §§7.4、7.6 分离改进器贡献与解释证据。 |

完成所选分支后，画出一个具体闭环：**可修改组件 → 反馈 → 接受规则 → 保留状态 → 后续任务评估**。再用[综述与项目对应表](#survey-project-map)选择实践入口。

#### 可选分支：持续自改进的可靠性与安全控制

本节为可选分支，探讨保留的经验如何影响后续行为，以及如何让持续更新保持可靠、可控。关注这些问题的读者可在入门核心与 *Towards AI* 之后进入本节。

| 论文 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **[Safety in Self-Evolving Agents: A Survey](https://arxiv.org/html/2610.00093v1)** | 跟踪经验成为可复用状态时，来源、权限和作用范围如何变化；SAVER 将状态载体、更新操作与违规、暴露、响应联系起来。 | §2.1 范围 → §§2.3–2.4 状态转移检查与 SAVER → §3.3 长期记忆或 §3.6 技能与过程。 |

随后把分析接到控制机制：*Towards AI* §4.3 与 §6.6 讨论更新策略、权限和回滚；*Recursive Self-Improvement in AI: A Survey* §8.4 讨论自修改下的评估完整性。需要系统整体视角时，再读 *The Path to Recursive Self-Improving Agents* §7.4。可以选一条记忆或一个技能，从产生追踪到后续复用，指出其权限在哪里变化、控制措施应在哪里介入。

<a id="survey-project-map"></a>

### 从综述到实践项目

本表连接已收录的教程、实践项目和评测示例；资源总数为 **56**。表中横跨[三类资源](#resource-scope)，阅读分支表示主题，不代表 RSI 能力等级。对应关系是本目录的学习建议：先围绕学习目标尝试链接中的示例，再回到对应综述章节比较机制。

以下门槛针对所链接的具体示例，依据 **2026-10-22–23** 核验的上游文档与代码整理，本轮未运行示例。仅通过 API 调用模型的入门示例在远端完成推理，需要模型访问权限和调用预算；训练项目仍需下表列出的 GPU 环境。GPU 配置是文档给出的示例，不作为已验证的最低硬件要求。

| 阅读分支／对应综述 | 项目与上手入口 | 学习目标与范围 | 所链接示例的运行门槛 |
| --- | --- | --- | --- |
| **共同基础** — [Prism §§2.3、5](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)；[Towards AI §§3–4](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5) | [The RSI Book 第 2 章](https://thersibook.com/chapters/ch02.html) → [配套 Notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb)。 | 跟踪评估、提示修订与经验跨任务复用，比较初始 Agent 和更新后的 Agent；Notebook 的经验列表保留在当前 kernel 中，未写入磁盘供跨会话使用。 | Python 3.10+、LiteLLM、Notebook 环境和模型接口。使用 API，不训练权重。 |
| **递归改进：教学原型** — [The Last AI §§2.2、3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)，本目录的学习对应 | [RSI Labs Notebook 第 4 节](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)；[配置见下文](#tutorials)。 | 跟踪反馈怎样变成新的改进器指令，经开发集验收后用于后续修复选择。3 个开发案例和 3 个留出诊断案例用于讲解可修改边界；未执行所选修复以衡量端到端收益。 | Colab / Jupyter、`google-genai==2.28.0` 与 Google API key；无需训练 GPU。状态保留在 Notebook 当前会话。 |
| **模型训练：Agent 策略** — [LLM Overview §§4、6](https://arxiv.org/html/2603.25681v3)；[Modern Agentic Systems §5](https://arxiv.org/html/2607.13104v1) | [Agent Lightning：Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode)。 | 跟踪工具调用轨迹如何变成奖励、GRPO 更新和策略 checkpoint。示例使用预设训练器更新 Agent 策略，未演示训练器自身改进。 | Python 3.12+、Linux / WSL、NVIDIA CUDA、仓库配套的 verl / vLLM 安装，以及模型／数据下载。示例配置为 **1× A100 80GB**；Local Mode 无需 Kubernetes，模型本地运行，默认启用 W&B。 |
| **模型训练：内层适应／外层学习** — [LLM Overview §§4.3–4.4](https://arxiv.org/html/2603.25681v3)；[The Path §5](https://www.preprints.org/manuscript/202608.0051) | [SEAL：general-knowledge 流程](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md)。 | 跟踪自编辑内容生成 → 临时 LoRA 适应 → 问答评估 → 编辑生成器的 ReST-EM 训练，比较内层更新和外层学习各自的作用。 | 需要微调经验；Python 3.12、Linux / CUDA、PyTorch / vLLM / PEFT、模型／数据访问，以及 SLURM 脚本和路径适配。上游示例使用 **2 张 A100/H100**；默认 TTT 评分也调用 OpenAI API。 |
| **经验、记忆与技能** — [Frontis §§2–4](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf) | [Hello Generic Agent 第 4 章](https://datawhalechina.github.io/hello-generic-agent/part1/chapter4/) → [第 12 章](https://datawhalechina.github.io/hello-generic-agent/part2/chapter12/)；安装其关联的 GenericAgent 实现。 | 将已完成任务整理成可复用 SOP／脚本，再观察后续会话如何检索。学习保留什么、何时复用；验证主要依靠提示约束，可能需要用户指导。 | 推荐 Python **3.11/3.12**、模型 API，以及所选 UI 和工具依赖；按[当前安装指南](https://github.com/lsdefine/GenericAgent/blob/main/docs/installation_zh.md)操作。教程处于 Beta。 |
| **经验：可复用上下文** — [Modern Agentic Systems §6.1.2](https://arxiv.org/html/2607.13104v1#S6.SS1.SSS2)明确讨论 ACE | [ACE Formula CLI](https://github.com/ace-agent/ace/blob/main/eval/finance/run.py) → 保存／重载 `best_playbook.txt`；[安装与启动见下文](#memory-skills)。 | 跟踪反馈如何变成保留的经验条目，并进入后续样本。在模型权重固定时，对比适应前与重载选优手册后的持出集结果。 | Python ≥3.10、uv 与模型 API。自带有标签数据，该路线无需训练 GPU；默认流程使用完整切分并反复调用 API。 |
| **经验：可执行技能** — [Modern Agentic Systems §§6.3.1–6.3.2](https://arxiv.org/html/2607.13104v1#S6.SS3.SSS2)明确讨论 Voyager | [Voyager 技能管理器](https://github.com/MineDojo/Voyager/blob/main/voyager/agents/skill.py) → README 已学习技能库示例；[安装与启动见下文](#memory-skills)。 | 跟踪 critic 验收后的代码如何落盘、跨会话重载、检索和组合。区分新增技能的 `learn()` 与复用技能的 `inference()`。 | Python ≥3.9、Node ≥16.13、Minecraft Java／Fabric／模组，以及聊天／嵌入 API。经典实现，需要处理旧依赖环境。 |
| **经验：记忆组件评测** — [Self-Evolving Agents §7.2.1](https://arxiv.org/html/2507.21046v4#S7.SS2.SSS1)与 [§7.1.4](https://arxiv.org/html/2507.21046v4#S7.SS1.SSS4)，本目录的编辑配对 | [LongMemEval-V2 基线](https://github.com/xiaowu0162/LongMemEval-V2#reproducing-baselines)：无检索 → RAG；[配置见下文](#evaluation)。 | 固定读者模型、问题、证据预算与裁判，对比答案准确率和记忆查询延迟。这里测量记忆组件，未覆盖 Agent 持续改进的完整轨迹。 | Python ≥3.11、公开数据、读者／嵌入模型端点，以及部分题型的付费裁判。限制题目数量后仍需准备数据和索引。 |
| **代码：程序演化预备练习** — [Coding Agents §§3、7–8](https://arxiv.org/html/2608.03392v4) | [ShinkaEvolve 教程](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb)；也可选 [OpenEvolve 函数最小化](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization)。 | 跟踪代码变异、评估反馈、选择和候选保存。示例演化的是任务程序，可用于理解综述中进一步要求的 Agent 组件更新边界。 | Python 3.10+；Shinka 推荐 3.11，支持本地 Python／Colab。需要模型 API 凭证和本地评估依赖；OpenEvolve 示例使用 NumPy，默认接入 Gemini 兼容接口。这两个示例无需训练 GPU。 |
| **自主性：小型工程入口** — [The Last AI §§2.2–3](https://arxiv.org/html/2609.11873v3) | [learn-deepseek-harness L1](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → 按课程顺序 → [L10](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification)。 | 观察 Agent 能提出、注册哪些工具变化。L10 生成的工具只在当前进程中保留；对照综述辨认扩展为完整改进闭环所需的评估、接受与持久化机制。 | Node.js、TypeScript 基础与 DeepSeek API。使用 API，各课为独立软件包。 |
| **代码与自主性：研究实现** — [Coding Agents §§3、7–8](https://arxiv.org/html/2608.03392v4)；[The Last AI §3](https://arxiv.org/html/2609.11873v3) | [DGM 环境搭建](https://github.com/jennyzzt/dgm#setup) → [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py)。 | 跟踪编码 Agent 自身的修改、后代评估与档案复用；继承的 Agent 实现参与下一轮自修改。对比任务程序演化，记录 Agent 可以修改什么、外部评估控制什么。 | Python、Docker、模型 API，以及 SWE-bench／Polyglot 环境和数据。环境搭建与重复评估工作较多，先追踪一轮流程，再考虑完整研究复现。 |
| **协同演化：共享经验** — [Co-Evolution §3.2.1](https://arxiv.org/html/2608.10299v1#S3.SS2.SSS1) | [CORAL 圆堆积](https://github.com/Human-Agent-Society/CORAL/tree/main/examples/circle_packing)，配置两个 Agent；[配置见下方](#coevolution-projects)。 | 跟踪带分数的尝试怎样进入共享笔记／技能，再改变另一 Agent 的方案；对照独立搜索轨迹与经验共享。 | Python 3.11–3.13、Git、uv、Docker 和模型 API；此评估器无需训练 GPU。 |
| **协同演化：独立 Agent 策略** — [Co-Evolution §3.2.1](https://arxiv.org/html/2608.10299v1#S3.SS2.SSS1) | [CoMAS 训练启动器](https://github.com/xxyQwQ/CoMAS/blob/main/scripts/train_comas.sh) → 交互／奖励／controller 代码；[配置见下方](#coevolution-projects)。 | 跟踪同伴方案与批评如何形成交互奖励、各自参数更新，以及后续多 Agent rollout。 | Python 3.10、本地权重与 CUDA 训练栈；上游推荐每 Agent 2× A100 80GB，默认四个 Agent。 |
| **协同演化：任务生成** — [Co-Evolution §4.1.2](https://arxiv.org/html/2608.10299v1#S4.SS1.SSS2) | [R-Zero 交替循环](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/main.sh)；[配置见下方](#coevolution-projects)。 | 追踪 Solver 一致性 → Challenger 奖励 → 生成任务／伪标签 → Solver 更新 → 下一轮 Challenger。这是本目录对综述任务空间分类的实践映射。 | 隔离的 Linux / CUDA 训练环境、8 GPU 脚本配置、HF／W&B，以及完整评估所需的 GPT API。 |
| **协同演化：可执行环境** — [Co-Evolution §4.3.1](https://arxiv.org/html/2608.10299v1#S4.SS3.SSS1) | [JaxUED Maze ACCEL](https://github.com/DramaCow/jaxued/blob/main/examples/maze_plr.py)，启用 `--use_accel` → PAIRED；[配置见下方](#coevolution-projects)。 | 跟踪策略表现如何影响关卡保留／变异，形成的课程又怎样更新策略；用固定评测关卡观察迁移。 | JAX / Flax 与 examples 依赖；无需 LLM API。可在 CPU 上开发，完整默认训练需要较多 RL 计算资源。 |
| **对抗式自博弈：最佳响应与历史策略** — [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1)，由本目录选择对应实现 | [OpenSpiel Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/nfsp_kuhn_pytorch.py)，先从表格型 fictitious play 开始；[安装与启动见下文](#adversarial-self-play)。 | 比较 DQN 最佳响应与蓄水池样本训练的平均策略。跟踪平均策略的可利用度，区分针对当前对手的学习与面对最佳响应的稳健性。 | Python ≥3.11、OpenSpiel、PyTorch 与 `dm-tree`；默认 CPU，无需模型 API。源码构建需要 CMake／C++ 编译器。 |
| **对抗式自博弈：共享 LLM 策略** — [Modern Agentic Systems §7.3](https://arxiv.org/html/2607.13104v1#S7.SS3)明确讨论 SPIRAL | [SPIRAL 游戏训练启动器](https://github.com/spiral-rl/spiral/blob/main/run.sh)；[安装与启动见下文](#adversarial-self-play)。 | 沿两方轨迹、按角色估计的优势、策略优化与权重更新追踪，观察新对手如何进入下一轮 rollout。 | Python 3.10 与 CUDA／OAT／vLLM；上游测试配置 8× H100。配置 W&B 和启动器默认的 OpenRouter 评估，或调整评估对手。 |
| **对抗式自博弈：偏好博弈扩展** — [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1)，本目录补充的相邻学习示例 | [SPPO 三轮启动器](https://github.com/uclaml/SPPO/blob/main/run_sppo_mistral.sh)；[安装与启动见下文](#adversarial-self-play)。 | 用固定 PairRM 评审比较当前策略的回答，检查 SPPO loss，再追踪新 checkpoint 进入下一轮。对照游戏 RL 与独立演化的多 Agent。 | Python ≥3.10 与 CUDA 训练栈；脚本使用 8 GPU。配置有权限的 Hugging Face 数据集上传或关闭调用；核心训练无需付费 LLM API。 |
| **实验证据／提示优化** — [Bounded Self-Refinement §5](https://arxiv.org/html/2607.07663v2)；[RSI in AI §7](https://www.preprints.org/manuscript/202609.2680) | [GEPA / DSPy AIME Notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb)；对照 [TextGrad Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb)。 | 检查数据划分、文本反馈和优化前后的提示表现；TextGrad 还包含验证集表现下降时的回退。两个入门示例均保持模型权重与优化器逻辑固定。 | GEPA 示例：Python 3.10–3.14、DSPy / GEPA、datasets 与 OpenAI API。TextGrad：Python 3.9+、Jupyter／Colab 与 OpenAI API，需检查旧模型 ID 的可用性。GEPA 的 MLflow 跟踪为可选。 |
| **可选：可靠性与安全控制** — [Safety §§2.3–2.4](https://arxiv.org/html/2610.00093v1)；[Towards AI §§4.3、6.6](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=14) | [RSI Atlas 接受规则示例](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py)。 | 改变传入的测试结果、质量收益和修改路径，观察接受／拒绝决策与历史记录。该练习只处理决策逻辑，不生成补丁，也不执行所传测试结果对应的测试。 | Python 3.10+ 标准库，无需模型 API 或 GPU。作为方法路线的可选延伸。 |

<a id="rl-and-rsi"></a>

## RL 与 RSI：关系、区别和阅读路线

**RL 是从奖励中学习行为的方法；RSI 关注保留下来的改进怎样参与后续改进。** 两者存在交集，但描述的是系统的不同方面。已有文献直接讨论这层关系：先读 [Modern Agentic Systems §§3.2–3.3](https://arxiv.org/html/2607.13104v1#S3.SS3)，再对照 [Towards AI §3](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5) 的定义。一些框架纳入自生成训练循环，更强的主张则要求改进器自身得到改进。下表是本目录的整理，不代表统一等级体系，也不意味着所有 RL 都采用固定架构。

| 机制 | 哪些部分变化 | 从示例中学习什么 |
| --- | --- | --- |
| 策略学习 | 在给定更新流程下改变策略参数 | [Agent Lightning](#practice)：追踪 rollout → 奖励 → checkpoint。任务奖励提高本身不能说明更新流程也变好了。 |
| 对抗式自博弈 | 策略，以及彼此形成的对手和经验 | [OpenSpiel 与 SPIRAL](#adversarial-self-play)：观察自适应学习信号。自博弈说明经验怎样产生，本身不指定使用 RL、偏好优化，或是否改写学习规则。 |
| 学习 RL 更新规则 | 用来训练其他 Agent 的参数化规则 | 下方 DiscoRL：对比“学到更好的策略”与“学会怎样更新策略”。学习到更新规则不等于发现规则的过程也会自行改写。 |
| 系统联合改进 | 可复用的 Harness 流程与模型权重 | 下方 ScienceBuddy：Harness 改进影响下一轮 RL，更新后的模型又改变后续 Harness 适应。 |
| 自修改学习机制 | 能修改自身学习行为的策略程序 | 下方 Schmidhuber 的 self-modifying policies：研究如何为影响后续修改的自修改分配信用。 |

因此，RL 可以承担 RSI 循环中的一部分更新，代码搜索或保留的技能编辑也可以提供其他更新；[DGM](#practice) 可作为没有 RL 权重训练步骤的对照。读项目时辨认**哪些变化被保留、下一轮信号由谁产生、更新流程本身是否变化**。要研究改进器的收益，可在相近任务与预算下，对照保留和不保留该变化时的后续学习效果。

**推荐顺序：** Modern Agentic Systems §3.3 → 已收录的 [Ashish Kumar 第二篇](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/)（先读 self-play template，再读 Learning to learn）→ 任选一个自博弈实践项目 → 下方三项读物。这里新增 **3 项资源**，复用的两项读物和本段整理不重复计数。研究阅读本身无需运行，项目表另列实际运行条件。

| 资源 | 与 RL、RSI 的关系 | 推荐阅读入口 | 日期／阅读门槛 |
| --- | --- | --- | --- |
| [Schmidhuber：Recursive Self-Improvement (RSI) Since 1987](https://people.idsia.ch/~juergen/recursive-self-improvement.html) | 作者回顾能修改自身学习流程的策略，让更强的“改进改进器”含义具体化；定义与历史叙述属于作者视角。 | [§2 自修改策略](https://people.idsia.ch/~juergen/recursive-self-improvement.html#secSMP) → [§7 近期工作](https://people.idsia.ch/~juergen/recursive-self-improvement.html#secLouis)，再读链接的 [1997 年章节](https://people.idsia.ch/~juergen/ssabook/ssabook.html)中的形式化概念。 | 技术笔记：**2026 年 9 月**；英文；RL 与算法基础。历史／概念阅读，不是现代环境安装教程。 |
| [DiscoRL：Discovering state-of-the-art reinforcement learning algorithms](https://www.nature.com/articles/s41586-025-09761-x) | 通过元优化学习 RL 更新规则，再用该规则训练新 Agent，连接策略改进与训练机制改进。 | [作者图解项目页](https://google-deepmind.github.io/disco_rl/)的 Method → 论文 Figure 1、Discovery method / Meta-optimization → Generalization。 | Nature 首发 **2025-10-22**，正式版 **2025-11-26**。英文；RL、神经网络与元梯度基础。作为阅读入口，本轮未审计代码／复现配置。 |
| [ScienceBuddy: Recursive-in-Recursive Self-Improvement for Interactive Scientific Agents](https://arxiv.org/abs/2609.17523) | 跨轮次结合 Harness 编辑与模型 RL；辅助编辑器与 GRPO 规则保持固定，便于辨认真正变化的组件。 | [§§2.3–2.5 与 Algorithm 1](https://arxiv.org/html/2609.17523v1#S2.SS3) → §4.2 的双轮次研究。 | arXiv **v1，2026-09-15**。英文；Agent 架构与 RL 基础。论文阅读，未独立复现产品、代码及实验结果。 |

<a id="guides"></a>

## 指南、教材与学习路径

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi) | **相关自改进机制。** 通过同一个仓储库存问答任务逐步讲解工具调用、确定性评估、prompt 改进、跨任务记忆和成本记录，适合第一个 Python 实验。 | [第 2 章：Build Your First Agent Improvement Loop](https://thersibook.com/chapters/ch02.html) + [配套 Notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb)。 | 英文；Python 3.10+、LiteLLM 与模型接口。示例主要更新 prompt 和记忆，模型权重不变。 |
| [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn) | **相关自改进机制 · 模拟演示。** 中文知识库、五阶段学习路线、架构图与进化搜索实验场，适合直观理解“生成—评估—选择—整合”。 | [页面导航与启动说明](https://github.com/Roloria/rsi-learn#页面导航)，先看[学习路线内容](https://github.com/Roloria/rsi-learn/blob/main/src/data/path.ts)，启动后进入 `/#/path` 和 `/#/lab`。 | 中文；交互站需 Node.js / Vite。实验场是**规则驱动的前端模拟**，不调用真实 LLM。 |
| [Ashish Kumar：Recursive self-improvement 三篇导读](https://ashishkumar.ai/series/recursive-self-improvement/) | 从理论基础讲到 self-play / self-training，再到自修改代码；包含 text-to-SQL 自训练循环示意与评估 Harness 讨论。 | 按顺序读 [Part 1：概念与理论](https://ashishkumar.ai/blog/recursive-self-improvement-explained/)、[Part 2：自博弈与自训练](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/)、[Part 3：自修改代码](https://ashishkumar.ai/blog/self-improving-code-alphaevolve-to-aide/)。 | 英文；适合有 LLM / 机器学习基础的读者。**2026-10-11** 发布的解释性文章，代码段用于讲解。 |
| [RSI 研究札记 · asimfish/awesome_rsi](https://github.com/asimfish/awesome_rsi) | 中文论文精读与综合分析，对照模型权重、Harness 代码和文本技能等改进方式，重点讨论评估；适合从领域概览进入单篇论文。 | 按 [Start Here](https://github.com/asimfish/awesome_rsi#1-start-here) 选择路线，先读[报告 10：汇总洞察](https://github.com/asimfish/awesome_rsi/blob/main/reports/10_synthesis_insights.md)，再读[报告 12：自进化 Agent 综述](https://github.com/asimfish/awesome_rsi/blob/main/reports/12_self_evolving_agents_survey.md)。 | 中文；LLM / Agent 基础；纯阅读。报告包含整理者的分析；配套论文中译为机器翻译，引用与技术细节应回到论文原文。 |
| [Lilian Weng：Harness Engineering for Self-Improvement](https://lilianweng.github.io/posts/2026-07-04-harness/) | 串联上下文管理、工作流搜索、自修改 Harness、进化搜索及 Harness／权重联合更新的研究长文，适合对照本目录实践项目背后的机制。 | 从 [Harness Optimization](https://lilianweng.github.io/posts/2026-07-04-harness/#harness-optimization) 开始，重点读 Self-Improving Harness 与 Evolutionary Search，再读 Future Challenges。 | 英文；Agent 与评估基础；纯阅读。属于综述性技术博客，与经过同行评审的综述论文分开标注。 |

<a id="prerequisite-courses"></a>

## 前置课程

这门可选课程帮助理解 Agent 改进所需的构件，再进入递归方法示例。已经收录的 [Hello-Agents 与 Harness 教程](#tutorials)提供更短的入门路线。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [WalkingLabs：Self-Improving Agent Notebook](https://github.com/walkinglabs/self-improving-agent-notebook) | **相关自改进机制 · 前置课程。** 17 本双语 Notebook 串联 Agent 循环、验证、RL、代码搜索、记忆与评估。参考 CS329A 大纲重建的社区材料，并非 Stanford 官方课程 Notebook。 | 基础学习从 [L01](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part1-foundation/01-course-overview.ipynb)开始；本目录重点推荐 [L07 Open-Ended Evolution](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part2-training/07-open-ended-evolution.ipynb)，跟踪代码生成 → 评分 → 归档 → 下一次提议；[英文 Notebook](https://github.com/walkinglabs/self-improving-agent-notebook/tree/main/notebooks-en)采用同样的目录结构。 | 中文／英文；Python 3.10+、仓库依赖、Jupyter / ipykernel（需另装）与 OpenAI 兼容模型 API，通过 `AGENT_LLM_*` 配置。L07 无需 GPU 训练；设计器固定，算术差错率来自教学环境设定，archive 保留在内核中。上游许可仍标为待确定。 |

<a id="tutorials"></a>

## 实践教程

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [RSI Labs · weilinear/rsi_labs](https://github.com/weilinear/rsi_labs) | **递归改进方法 · 教学原型。** 餐费示例依次区分临时修正答案、复用工具，以及修改选择后续改进的策略。第 4 节由 Gemini 改写改进器自己的指令，开发集得分提高后才采纳，并用于新案例。 | 先读[作者讲解](https://blog.weili.me/posts/recursive-self-improvement-part-1-a-simple-toy-example)，再顺序运行 [gemini_self_improvement.ipynb](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)，重点看**第 4 节：Improve how the agent chooses improvements**；也可[在 Colab 打开](https://colab.research.google.com/github/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)。 | 英文；Colab／本地 Jupyter、`google-genai==2.28.0` 与 `GOOGLE_API_KEY`；无需训练 GPU。默认 `gemini-3.8-flash`，可通过 `GEMINI_MODEL` 修改；未实测端点兼容性。状态仅在当前会话保留。元实验在 **3 个开发 + 3 个留出案例**上衡量修复选择准确率，初始策略被刻意设得较弱；未执行所选修复，也未验证多代端到端收益。该仓库后续 Notebook 保持改进器固定。 |
| [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness) | **相关自改进机制 · 前置构件。** 分课实现 Agent 循环、插件、持久 Session Log、缓存、压缩、记忆、子 Agent 和运行时自修改；每课是独立小包，适合边读边改。 | [L1：最裸的循环](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → 按[网页版课程](https://prism-shadow.github.io/learn-deepseek-harness/)顺序学习 → [L10：自我修改](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification)。 | 中英；Node.js、TypeScript 基础和 DeepSeek API。L10 展示运行时生成并注册临时工具，尚未包含自动评估、晋升与持久化的完整演化循环。 |
| [GEPA / DSPy 官方教程](https://github.com/gepa-ai/gepa) | **相关自改进机制。** 用完整数学示例串起基线评估、文本反馈、候选选择和优化后评估，适合学习模型权重固定时提示词如何逐步改进。 | 从 [GEPA for AIME Notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb) 开始，再读 [GEPA optimization](https://dspy.ai/current/getting-started/gepa-optimization/)，理解数据划分和优化后程序的保存。 | 英文；Python 3.10–3.14、DSPy / GEPA、datasets；示例需要 OpenAI API key，MLflow 跟踪可选。 |
| [TextGrad 官方 Notebook](https://github.com/zou-group/textgrad) | **相关自改进机制。** 通过类似 PyTorch 的接口讲解文本梯度，再在物体计数问题上优化共享提示词、使用验证集评估，并在验证性能下降时回退更新，适合理解反馈驱动的文本优化。 | [Primitives](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Primitives.ipynb) → [Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb)。 | 英文；Python 3.9+、Jupyter / Colab、OpenAI API key。Notebook 沿用较早的模型 ID，运行前需核对兼容模型的可用性；更新提示词文本而非模型权重。 |
| [Datawhale Hello-Agents：Reflection 与自进化](https://github.com/datawhalechina/hello-agents) | **相关自改进机制 · 前置示例。** 以中文讲解和代码串起生成、评审、修改方案的过程。素数函数示例便于逐步追踪反思循环，扩展章节再梳理四类 Agent 自进化闭环。 | 先对照阅读[第四章 §4.4 Reflection](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter4/第四章%20智能体经典范式构建.md#44-reflection)与 [Reflection.py](https://github.com/datawhalechina/hello-agents/blob/main/code/chapter4/Reflection.py)，再读 [Extra10：Agent 自进化](https://github.com/datawhalechina/hello-agents/blob/main/Extra-Chapter/Extra10-Agent自进化.md)。 | 中文；Python 3.10+、`openai`、`python-dotenv` 及 OpenAI 兼容模型接口。示例依赖模型反馈改进任务输出，不执行生成的代码，也不训练模型权重。 |
| [Datawhale Hello Generic Agent](https://github.com/datawhalechina/hello-generic-agent) | **相关自改进机制。** 讲解如何将经验沉淀为可复用 SOP 和脚本，并用四层记忆组织与检索。适合学习任务经验如何变成后续会话可发现、可复用的知识。 | [第 4 章：记忆与 Skill 系统](https://datawhalechina.github.io/hello-generic-agent/part1/chapter4/) → [第 12 章：自我进化](https://datawhalechina.github.io/hello-generic-agent/part2/chapter12/)；安装时参照实现仓库的[当前中文安装指南](https://github.com/lsdefine/GenericAgent/blob/main/docs/installation_zh.md)。 | 中文；教程仍为 **Beta**。推荐 Python 3.11/3.12、模型 API，以及所选界面／工具的依赖。更新对象是记忆和技能，可能需要用户引导；验证规则属于提示词约束，并非完整自动晋升机制。 |

第一个 Python 改进循环可从上面的 **The RSI Book 第 2 章与 Notebook** 开始。用 **RSI Labs 第 4 节**观察可修改的改进策略；GEPA 和 TextGrad 用于学习固定模型权重与优化器逻辑下的提示词优化。

<a id="practice"></a>

## 实践项目

这些项目提供程序进化、Agent 自身代码演化或模型训练的具体示例，可按改进对象、[资源分类](#resource-scope)与算力条件选择。此处 DGM 是递归改进的研究入口，其余推荐示例用于学习相关机制。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [ShinkaEvolve · SakanaAI](https://github.com/SakanaAI/ShinkaEvolve) | **相关自改进机制。** 用引导式 Notebook 串起 LLM 代码变异、程序种群、评估器和持久化搜索记录；圆堆积任务适合学习程序进化，并比较不同父代选择策略。 | [Getting Started](https://sakanaai.github.io/ShinkaEvolve/getting_started/) → [交互教程 Notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) → 阅读[圆堆积评估器](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/circle_packing/evaluate.py)。 | 英文；Python 3.10+（建议 3.11）、本地 Python 或 Colab，以及模型 API 凭据。入门示例进化的是任务程序；评估器在本地运行，不要求训练用 GPU。 |
| [OpenEvolve](https://github.com/algorithmicsuperintelligence/openevolve) | **相关自改进机制。** 受 AlphaEvolve 启发的开源程序搜索框架。函数最小化小示例展示初始搜索算法、评估反馈、配置与检查点如何组成闭环。 | 阅读 [Installation & Setup](https://github.com/algorithmicsuperintelligence/openevolve#installation--setup)，取得仓库示例后跟随 [Function Minimization](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization)，结合阅读 `initial_program.py`、`evaluator.py` 和 `config.yaml`。 | 英文；Python 3.10+、NumPy 和模型端点。示例默认经 OpenAI 兼容 API 使用 Gemini；Docker 可选。优化的是任务代码，不更新模型权重。 |
| [Darwin Gödel Machine（DGM）](https://github.com/jennyzzt/dgm) | **递归改进方法 · 研究实现。** 原论文研究实现：Agent 修改自身代码，在编程任务上评估后代，并保留归档；继承的 Agent 实现参与后续自修改。适合准备沿源码理解完整研究循环的读者。 | 阅读 [Setup / Running the DGM](https://github.com/jennyzzt/dgm#setup)，再追踪 [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py)。 | 英文；Python、Docker、模型 API，以及 SWE-bench / Polyglot 环境准备。这是需要较多环境与评估工作的研究复现入口，适合进阶学习。 |
| [SEAL · Self-Adapting Language Models](https://github.com/Continual-Intelligence/SEAL) | **相关自改进机制 · 学习生成 self-edit。** 作者原始实现学习生成 self-edit，在下游问答上评估临时 LoRA 更新，再用筛选出的编辑训练编辑生成器；适合研究内层适应与外层学习的关系。 | 从 [general-knowledge 流程](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md)依次读数据生成 → TTT server → 评估 → ReST-EM 训练，再看 [SFT 数据构建器](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/src/EM/build_SFT_dataset.py)。 | 英文；进阶 Python / 微调基础、Python 3.12、PyTorch / vLLM / PEFT。上游说明使用 2 张 A100/H100；需调整 SLURM 脚本与路径。默认 TTT 评分使用 OpenAI API（GPT-4.1）；生成／proxy 评分也可使用该 API。 |
| [Microsoft Agent Lightning v1.0](https://github.com/microsoft/agent-lightning) | **相关自改进机制。** Calc-X 将 AutoGen Agent、MCP 计算器与轨迹采集、答案奖励、GRPO 更新串起来，适合学习如何从工具调用轨迹训练并保存策略检查点。 | 先读[安装说明](https://github.com/microsoft/agent-lightning/blob/main/docs/00-installation.md)，再按 [Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode)操作；按该示例要求从 `examples/calc_x` 启动。 | 英文；Python 3.12+、Linux / WSL、CUDA、`verl` / vLLM、数据下载，默认使用 W&B。文档中的 Calc-X 配置为 **1 张 A100 80GB**。这是 v1.0 训练入口，旧 APO 教程对应旧 API。 |

<a id="memory-skills"></a>

### 记忆与技能学习项目

先用已收录的 **Hello Generic Agent** 章节建立中文基础。选择 **ACE** 学习文本经验手册，或用 **Voyager** 学习交互环境中的可执行技能。两者属于**相关自改进机制**，Modern Agentic Systems 的明确讨论见项目映射表。它们在固定模型权重之外保留经验；核验入口没有重写生成／整理或技能学习流程自身。

| 资源 | 特色与学习目标 | 推荐学习入口 | 语言与运行门槛 |
| --- | --- | --- | --- |
| [ACE：Agentic Context Engineering](https://github.com/ace-agent/ace) | **相关自改进机制。** 作者的 Generator–Reflector–Curator 实现将反馈变成可复用文本经验手册。跟踪有标签样本、有用／有害计数、增量添加、验证集选优和后续复用；默认逐样本实现将整个 playbook 放入提示。 | 先读[论文 §3](https://arxiv.org/html/2510.04618v3#S3)，再看 [finance CLI](https://github.com/ace-agent/ace/blob/main/eval/finance/run.py)。仓库根目录执行 `uv sync`，配置 `.env`／供应商模型后运行 `uv run python -m eval.finance.run --task_name formula --mode offline --save_path results --test_workers 1`。用 `--mode eval_only --initial_playbook_path ...` 重载保存的 `best_playbook.txt`。 | 英文；Python ≥3.10、uv、模型 API；该路线无需训练 GPU。默认使用 SambaNova／DeepSeek-V3.1。Formula 包含 **500/300/200** 条训练／验证／测试样本；`--test_workers 1` 限制并发，不限制样本量。如需缩小运行，在 `eval/finance/data/sample_config.json` 配置保持分离的小规模切分，并将 `--eval_steps` 设为不大于训练样本数的正整数，确保触发验证选优。当前默认操作更新计数并**新增**条目，可选 embedding 去重关闭。 |
| [Voyager](https://github.com/MineDojo/Voyager) | **相关自改进机制。** 将 Minecraft 执行经验变成持久化 JavaScript 技能库，由 LLM critic 判断成功后入库，再按描述检索代码用于后续任务。对比进入提示的技能片段与用于技能组合的完整可执行库。 | 先读[论文 §§2.2–2.3](https://arxiv.org/html/2305.16291v2#S2.SS2)，再看[技能保存／检索](https://github.com/MineDojo/Voyager/blob/main/voyager/agents/skill.py)。按 [Getting Started](https://github.com/MineDojo/Voyager#getting-started) 运行 `Voyager(...).learn()`；也可用 README 的 `skill_library_dir='./skill_library/trial1'` 示例，在新任务中复用作者发布的技能。`resume=True` 可恢复持续学习。 | 英文；Python ≥3.9、Node ≥16.13、正版 Minecraft Java **1.19**、Fabric **0.14.18**／模组、构建自定义模组所需 Java **17**，以及 OpenAI 聊天／嵌入 API。不微调模型，但需在本地运行游戏。经典实现采用较旧且部分未锁版的依赖与旧模型默认值；未实测全新安装／端点兼容性。 |

**学习练习：** 查看保存的手册或技能库，重启后加载它，再追踪它对持出样本或新任务的作用；保持模型与任务预算相近，与空状态运行作比较。[LongMemEval-V2](#evaluation) 提供独立的记忆组件对比，将这些项目接入其接口需要编写适配器。把组件准确率、保留经验带来的任务收益，以及改进流程自身的变化分开考察。

<a id="coevolution-projects"></a>

### 协同演化项目

先读 [Co-Evolution §§2.2–2.3](https://arxiv.org/html/2608.10299v1)，辨认哪些组件会变化，以及它们怎样改变彼此的学习条件。用模型 API 学习经验共享可从 **CORAL** 开始；学习环境课程可选 **JaxUED**；有多 GPU 训练条件再选 **CoMAS / R-Zero**。这些是不同机制的入口，不是必须依次完成的步骤。

综述 §3.2.1 直接讨论 CORAL 和 CoMAS；R-Zero 是本目录为 §4.1.2 选择的学习映射；JaxUED 实现了 §4.3.1 讨论的方法论文中的 ACCEL / PAIRED。这些实现仍采用人工设计的更新规则，本路线不将它们写成 §5 元协同演化的复现。

| 资源 | 哪些部分相互适应／学习目标 | 推荐运行入口 | 此入口的运行门槛 |
| --- | --- | --- | --- |
| [CORAL](https://github.com/Human-Agent-Society/CORAL) | **相关自改进机制。** **共享经验；§3.2.1。** Agent 在独立 Git worktree 中改写方案，共享带分数的尝试、笔记和技能。跟踪一个 Agent 的发现怎样改变另一个 Agent 的下一次尝试；圆堆积评估器和模型权重保持固定。 | 按[安装指南](https://coral.compounding-intelligence.ai/docs/getting-started/installation/)取得源码，阅读[圆堆积示例](https://github.com/Human-Agent-Society/CORAL/tree/main/examples/circle_packing)与[多 Agent 指南](https://coral.compounding-intelligence.ai/docs/guides/multi-agent/)。完成 `uv sync` 和网关配置后，在仓库根目录运行 `uv run coral start -c examples/circle_packing/task.yaml agents.count=2`。用 `coral log`、notes 和 skills 检查共享记录，结束时运行 `coral stop`（源码安装均加 `uv run` 前缀）。 | 英文文档和中文 README；Python **3.11–3.13**、Git、`uv`、Docker 与模型 API。此示例的 `docker-opencode` 预设使用 OpenCode 和 LiteLLM 网关，须配置 `litellm_config.yaml` 的 API-key 占位符。NumPy / SciPy 评估器不需要训练 GPU；需预留两个 Agent 的模型调用与本地评估开销。 |
| [CoMAS](https://github.com/xxyQwQ/CoMAS) | **相关自改进机制。** **独立 Agent 策略；§3.2.1。** 同伴分别求解、批评和评分，用交互奖励更新各自权重，再将新策略投入下一轮讨论。适合追踪多 Agent 交互怎样成为持久学习。 | 先读[论文 §§3.1–3.3](https://arxiv.org/html/2510.08529v2#S3)，再看[训练启动器](https://github.com/xxyQwQ/CoMAS/blob/main/scripts/train_comas.sh)。按 README 建立 Python 3.10 环境、执行 `pip install -r requirements.txt`，配置 `PRETRAIN`、GPU／batch 与 W&B，在仓库根目录运行 `bash scripts/train_comas.sh`；沿 workflow → reward → controller 追踪实现。 | 英文；RL 基础、CUDA、PyTorch / vLLM / DeepSpeed / Ray 与本地模型权重。读取仓库 `datasets/blended` 及额外评估数据。上游推荐**每 Agent 2× A100 80GB**；默认四个独立 Agent，约 **8 GPU**，不是已核实的最低需求。核心训练用本地模型，W&B 默认离线记录。 |
| [R-Zero](https://github.com/Chengsong-Huang/R-Zero) | **相关自改进机制。** **自适应任务生成；§4.1.2。** 独立 Challenger 根据当前 Solver 的答案一致性学习出题；问题与多数票伪标签再用于训练 Solver，两个 checkpoint 进入后续交替轮次。跟踪任务难度与解题策略怎样相互塑造；伪标签不等于经过独立核实的答案。 | 读 [Quickstart](https://github.com/Chengsong-Huang/R-Zero/blob/main/README.md) 与 [main.sh](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/main.sh)。安装 requirements，配置 `STORAGE_PATH`、`HUGGINGFACENAME`、`tokens.json` 和评测端点。根目录入口为 `bash scripts/main.sh Qwen/Qwen3-4B-Base qwen3-4b`；运行前读[出题者启动器](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/questioner_train_penalty.sh)和[解题者启动器](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/solver_train.sh)。 | 英文；进阶 Python / RL、Linux / CUDA、PyTorch **2.7.0** 与 vLLM **0.9.1**。脚本配置 **8 GPU**，未声明统一最低 Python／显存要求。需要模型／数据访问及 Hugging Face、W&B 配置；生成数据会上传到 HF 私有数据集，完整评估使用 GPT API。应在隔离训练环境中使用：Challenger 启动器含范围较宽的 `pkill python` 清理命令。 |
| [JaxUED](https://github.com/DramaCow/jaxued) | **相关自改进机制。** **环境课程；§4.3.1。** ACCEL 根据策略表现给迷宫关卡打分、保留与变异，再用形成的课程训练策略。对照生成关卡和策略迁移；之后读 PAIRED 的两个学习者与可训练环境生成器。 | 取得源码并执行 `pip install -e ".[examples]"`；阅读 [Maze PLR/ACCEL](https://dramacow.github.io/jaxued/maze_plr/)，在仓库根目录运行 `WANDB_MODE=disabled python examples/maze_plr.py --use_accel`，再读 [`maze_paired.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_paired.py)。使用当前 [`maze_plr.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_plr.py)，避开旧 Getting Started 页已失效的 `minigid_plr.py` 路径。 | 英文；Python / PPO / JAX 基础。包声明 Python **≥3.9**；按 [JAX 安装说明](https://docs.jax.dev/en/latest/installation.html)匹配平台与 JAX / Flax、examples 依赖。无需 LLM API，命令中关闭了 W&B。可在 CPU 上开发，但默认 ACCEL 训练约 **2.46 亿环境步**，完整运行应准备适合 RL 的计算资源；未核实最低显存与耗时。 |

<a id="adversarial-self-play"></a>

### 对抗式自博弈项目

先用 **OpenSpiel** 在 CPU 上观察最优响应和策略历史。研究语言模型游戏 RL 可选 **SPIRAL**；比较偏好博弈优化可选 **SPPO**。[Modern Agentic Systems §7.3](https://arxiv.org/html/2607.13104v1#S7.SS3) 直接讨论 SPIRAL；下列项目与 [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1) 的联系是本目录的学习延伸，不表示该综述直接点名了全部三个实现。SPPO 是相邻的偏好博弈案例，并非两个独立训练的 Agent。

| 资源／分支 | 学习目标 | 推荐运行入口 | 此入口的运行门槛 |
| --- | --- | --- | --- |
| [OpenSpiel：Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel) — 经典自博弈 | **相关自改进机制 · 自博弈前置。** 两个玩家学习 DQN 最优响应与基于 reservoir 的平均策略。观察平均策略的可利用度（面对最优响应可被利用多少），而不只看双方胜率。 | 按[安装说明](https://github.com/google-deepmind/open_spiel/blob/master/docs/install.md)配置并取得示例；先在[表格型 fictitious play](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/fictitious_play_example.py)中设置 `--game=kuhn_poker`，再于仓库根目录运行 `python3 open_spiel/python/examples/nfsp_kuhn_pytorch.py --num_train_episodes=20000 --eval_every=1000`；对照 [NFSP 源码](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/nfsp_kuhn_pytorch.py)。 | 英文；当前源码要求 **Python ≥3.11**，源码构建使用 CMake／C++ 编译器。NFSP 另需 PyTorch、`dm-tree`；默认 **CPU**，无需模型 API。上游默认 **300 万局**；命令中的 2 万局是本目录缩短的学习设置，不构成收敛证据。 |
| [SPIRAL](https://github.com/spiral-rl/spiral) — 多轮零和游戏 RL | **相关自改进机制。** 一个共享策略扮演双方，并从两方轨迹学习。观察按角色估计的优势、策略更新，以及新对手怎样改变后续经验。 | 读[论文 §§4.1–4.3](https://arxiv.org/html/2506.24119v2#S4)，按 README 安装并检查 [run.sh](https://github.com/spiral-rl/spiral/blob/main/run.sh)，在仓库根目录运行 `bash run.sh`。沿角色轨迹 → OAT 优化 → vLLM 权重同步追踪。 | 英文；Python **3.10**、CUDA、vLLM **0.8.4**、OAT **0.2.1** 与 Qwen3-4B-Base 权重。上游测试配置 **8× H100**，不是已核实的最低要求。配置 W&B 与默认 OpenRouter 评估，或修改相关设置（例如仅使用 random 对手）。训练生成游戏轨迹，数学评估还使用随仓库数据。使用这个原始本地入口；本次核验的 Tinker 启动器引用了缺失源码。 |
| [SPPO](https://github.com/uclaml/SPPO) — 偏好博弈自训练 | **相关自改进机制。** 当前策略回答由固定 PairRM 评审比较，新 checkpoint 产生下一轮回答。对照 SPPO loss 与游戏 RL；评审器和学习规则保持固定。 | 读[论文 §3.2、§§4.1–4.2](https://arxiv.org/html/2405.00675v5#S4)，按 README 安装并检查 [run_sppo_mistral.sh](https://github.com/uclaml/SPPO/blob/main/run_sppo_mistral.sh)。配置数据和上传后，在仓库根目录运行 `bash run_sppo_mistral.sh`，进入三轮流程。 | 英文；**Python ≥3.10**、vLLM、LLM-Blender / PairRM、Accelerate / DeepSpeed、Mistral 权重与 HF prompt 数据。脚本配置 **8 GPU／进程**，未给最低显存。核心训练无需付费 LLM API。数据阶段默认向 `UCLA-AGI` 上传私有 HF 数据集：应改成自己有权限的 namespace／token，或关闭这些调用；模型上传开关不会关闭数据上传。旧版／部分未锁定依赖未经过安装实测。 |

这些入口保持游戏规则或偏好评审器、训练流程固定，提供具体的自博弈学习循环；可用 [RL–RSI 导读](#rl-and-rsi)辨认“改进器自身变化”还涉及哪些机制。

<a id="courses"></a>

## 课程与工作坊

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与材料范围 |
| --- | --- | --- | --- |
| [Stanford CS329A：Self-Improving AI Agents](https://cs329a.stanford.edu/) | 系统串联 test-time compute、verifier、工具反馈、规划、RL、开放式演化和 Agent 评测，适合按周安排阅读。 | 官网 Schedule 的**第 2–7 讲**建立基础，再读**第 17 讲 Agentic Evaluations & Long-Horizon Tasks**。 | 英文；机器学习 / LLM 基础。当前公开页面为 **2025 秋季课程**，本批核验课程表与论文阅读清单。 |
| [Harvard CS 2881R：AI Safety 中的 RSI 专题](https://boazbk.github.io/mltheoryseminar/) | 从 AI 研发自动化、改进速度和安全视角理解 RSI，适合补充技术实现之外的研究问题。 | [2025-10-09 归档讲](https://boazbk.github.io/mltheoryseminar/fall2025/#lecture-oct-9)有课件、总结和录影入口；再看 [2026-09-24 RSI & AI Trajectories](https://boazbk.github.io/mltheoryseminar/#lecture-sep-24)的阅读与学生实验材料。 | 英文；机器学习、概率 / 信息论与 Python 基础。属于 AI Safety 课程中的专题；2026 该讲当前未列录影。 |
| [ICLR 2026：AI with Recursive Self-Improvement Workshop](https://recursive-workshop.github.io/) | 集中呈现自改进方法、系统与评测的研究议题，适合从议程进入具体研究工作。 | 先看官网议程与主题，再从 [Accepted Papers](https://recursive-workshop.github.io/papers.html)的 Oral / Spotlight 选论文。 | 英文；研究背景更有帮助。活动日期 **2026-04-26**；本批核验官网与论文集。 |
| [DeepLearning.AI × Oracle：Building Adaptive AI Agents](https://www.deeplearning.ai/courses/building-adaptive-ai-agents) | 讲解三层适应：从 Agent 轨迹提炼可复用技能、代码图检索和模型适应。适合学习如何跨会话保留经验；提炼出的技能需要人工批准。 | 先看 Overview of Continual Learning，再学 [Behavior Adaptation: Trajectory-to-Skill Learning](https://learn.deeplearning.ai/courses/building-adaptive-ai-agents/lesson/9i82mn/behavior-adaptation%3A-trajectory-to-skill-learning)，然后进入代码图相关课程。 | 英语；建议具备 Python 基础。课纲列有 7 个视频和 3 个代码示例；Free 计划可看视频，动手实验与评分活动属于 Pro。 |
| [Berkeley Advanced LLM Agents MOOC：自改进相关讲次](https://llmagents-learning.org/sp25) | 将自奖励、迭代偏好优化和元奖励与 LLM 推理相连接，适合学习模型如何生成训练信号并改进自身判断。 | 从 Jason Weston 的 **2025-02-03** 讲次 *Learning to reason with LLMs* 及[讲义第 40 页](https://rdi.berkeley.edu/llm-agents-mooc/slides/Jason-Weston-Reasoning-Alignment-Berkeley-Talk.pdf#page=40)开始，再读课纲中的迭代推理偏好优化论文。 | 英语；建议具备 LLM 与后训练基础。**Spring 2025** 课程已结束，仍有公开讲义与阅读材料，另列有录像入口。 |

<a id="videos"></a>

## 中文视频课程与研究报告

经验驱动的自进化到元进化中文作者讲座，可看青稞 Talk 146；它与 FrontisAI 论文合并放在[综述与研究总览](#surveys)，不重复计数。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与材料范围 |
| --- | --- | --- | --- |
| [李宏毅：机器学习 2026 — 自我成长专题](https://speech.ee.ntu.edu.tw/~hylee/ml/2026-spring.php) | 中文讲解串联答案修正、自生成训练信号、Harness 优化以及“学习如何改进”。配套讲义区分输出、提示词／代码与模型参数的变化，适合建立方法之间的联系。 | 按顺序看 [Self-Correction](https://youtu.be/m3i2mk5hs8U) → [Self-Improving 上集](https://youtu.be/s06mSAGN4gM) → [下集](https://youtu.be/cQLKVzbwN7I)；配合[上集讲义](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2026-course-data/Self-Improving.pdf)与[下集讲义第 11–18、33–46 页](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2026-course-data/self-evolving-agent.pdf#page=11)。 | 中文原讲、中文讲义夹英文术语；建议有 LLM／机器学习基础。公开课程视频链接和 PDF，部分课程作业使用 NTUCOOL。这是综合机器学习课中的专题。 |
| [2026 智源大会：AI 自进化论坛](https://www.bilibili.com/video/BV1Bijw65Ec9/) | 研究报告把智能体经验采集、可复用记忆和可验证反馈连接到自我改进；官方多分 P 录像便于按主题学习。 | 先看 [P3：张少坤《基于可扩展智能体经验的递归自学习》](https://www.bilibili.com/video/BV1Bijw65Ec9/?p=3)，再看 [P5：谷雨《The Illusion of Self-Improving Agents》](https://www.bilibili.com/video/BV1Bijw65Ec9/?p=5)，结合[主办方文字回顾](https://hub.baai.ac.cn/view/55536)串联内容。 | 中文报告，部分标题为英文；建议有 LLM／Agent 与基础强化学习知识。公开 B 站研究报告录像，不是配套实验课。 |

<a id="evaluation"></a>

## 评测示例

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI) | **评测工具 · 验收门控教学。** 图解改进循环、评估和修改准入，附小型 Python 示例，适合学习接受 / 拒绝候选修改与记录历史的代码结构。 | [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python 门控示例](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py)。 | 英文；示例使用 Python 3.10+ 标准库。接收外部传入的测试状态、收益和路径后作判断，不包含模型生成改动或自动执行评测。 |
| [LongMemEval-V2](https://github.com/xiaowu0162/LongMemEval-V2) · [论文](https://arxiv.org/abs/2605.12493) | **评测工具。** 检验保存的 Web／企业环境轨迹能否支持后续关于状态、工作流程和环境陷阱的问题。**451 道题**同时衡量答案准确率和记忆查询延迟，适合比较记忆组件；单凭分数不能认定形成了 RSI 闭环。 | 先读[论文 §3.3](https://arxiv.org/html/2605.12493v1#S3.SS3)，按说明配置数据／模型端点，再对比[无检索](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_no_retrieval.sh)与 [RAG](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_rag_query_to_slice.sh)。从仓库根目录运行 `TIER=small bash evaluation/scripts/run_no_retrieval.sh --limit 5`，再以相同 limit 运行 RAG 脚本。这会选择**每个领域前 5 题**，仍需完成数据／索引准备。 | 英文；Python ≥3.11、[公开 Apache-2.0 数据](https://huggingface.co/datasets/xiaowu0162/longmemeval-v2)（解压前约 **7.12 GB**）及模型端点。默认读者／RAG controller 为 Qwen3.5-9B；RAG 另需 Qwen3-Embedding-8B。部分题型调用付费 GPT-5.2 裁判。服务硬件取决于模型和上下文，未给最低显存。V2 评测会生成答案，没有单独导入预测文件评分的 CLI。 |

<a id="verification"></a>

## 时效与核验记录

原有 51 项资源核验于 **2026-10-22**；ACE、Voyager、LongMemEval-V2、RSI Labs 与 WalkingLabs 前置 Notebook 于 **2026-10-23** 补入，同日补读相关综述段落并标注实践入口类别，具体阅读范围记录在下表。新增候选先按项目身份与已有条目排重，再读详情；网站、Notebook 和仓库迁移前后的名称合并处理。读取了项目 README、推荐章节或课程页面，并对涉及实践能力的条目抽查相关代码。**未运行上游教程、调用模型或复现实验，也未逐篇复核清单内的论文。** 视频核验按下表分别覆盖官方课页、主办方介绍、可用讲义与视频元数据；未观看视频或核验逐字稿。

**两个新增学习仓库的覆盖核对：** 截至 2026-10-23，在已收录的 **17 个索引、103 份文本文件**中，未检出两者的仓库 URL、名称及作者别名。索引范围包括七个 Awesome 清单、九个综述配套仓库及 RSI 研究札记；文件范围包括 README、选定目录数据、研究解读与 Prism 结构化论文／方法数据，不含 PDF、历史提交、Issue 或外链网站。这表示新增了该范围之外的学习入口，不代表其方法是新研究。STOP、SICA、RRSI 与 AgentDescent 已有[所收录索引中的直接链接](https://github.com/pinkbubblebubble/awesome-rsi/blob/c91823d6ebd9969cea3b7b05e20027988ec5308b/README.md)。

下表记录有依据的内容变化、发布或上游自报核验时间；它们与本项目的核验日期不同，也不等同于整个领域的覆盖截止日期。提交日期按 Asia/Taipei 记载，上游直接标注的日期保留原值。

<details>
<summary>展开 56 项资源的内容时间与核验范围</summary>

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
| RSI 研究札记 | [2026-09-08 为汇总报告补充与外部资源的对照](https://github.com/asimfish/awesome_rsi/commit/0dfe9b2bc99663829ca20f3c3481878d795e1865)。 | README 学习路线与综述目录、报告 10／12／32、汇总报告提交差异。报告 32 明确仅基于原论文摘要；未审校翻译或逐项复核所引实验结论。 |
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

</details>

## 收录与整理原则

- 按资源形式组织主目录，主题覆盖模型训练、Agent Harness、记忆与技能、评测和自动研究。
- 将具体实践入口标为递归改进方法、相关自改进机制或评测工具，并说明前置构件与教学原型的范围；综述和综合课程可以横跨多类。
- 给出推荐理由、具体学习入口、语言、前置知识与实践条件。
- 区分纯阅读、模拟演示、真实模型调用和训练；按实际阅读或运行范围记录核验。
- 优先链接原始项目；同一项目的网站、翻译与 Notebook 合并介绍，普通镜像不重复计数。
- 以实质内容和学习价值判断时效，保留仍然有用的稳定教材与历史课程。

## 参与贡献

欢迎通过 [Issue](https://github.com/RZRZ-Q/awesome-rsi-resources/issues) 推荐资源，或提交 Pull Request。收录要求见[贡献指南（中文）](CONTRIBUTING.md)。

## 许可

本仓库原创内容采用 [MIT License](LICENSE)。链接所指向的第三方资料遵循各自的许可。
