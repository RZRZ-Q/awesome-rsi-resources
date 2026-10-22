# Awesome RSI Resources

递归自我改进（Recursive Self-Improvement, RSI）学习与研究资源导航。

A curated directory of awesome lists, learning guides, tutorials, and courses on recursive self-improvement.

本项目汇集 RSI 相关的资源集合与学习入口，帮助读者了解每项资源适合谁、值得看什么、从哪里开始，以及内容更新到什么时候。

**最近核验：2026-10-22。** 首批收录 17 项资源，涵盖 Awesome 清单、教材、教程、课程、工作坊与复现材料。同一项目的网站、代码和 Notebook 合并介绍。

## 从哪里开始

| 你现在想做什么 | 推荐起点 |
| --- | --- |
| 用中文建立 RSI 概念框架 | [Prism 中文图解导读](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md) |
| 用 Python 搭建第一个 Agent 改进循环 | [The RSI Book 第 2 章](https://thersibook.com/chapters/ch02.html)与配套 Notebook |
| 从代码理解 Agent Harness | [learn-deepseek-harness 的 L1](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop)，再按课程顺序学习 |
| 开始系统读论文 | [natnew 的 Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths) |
| 跟着课程学自改进 Agent | [Stanford CS329A](https://cs329a.stanford.edu/)的公开课程表与阅读材料 |

可以按自己的目标选一条短路线：

- **概念入门**：Prism 中文导读 → The RSI Book 第 1–2 章 → natnew 阅读路线。
- **Agent 工程实践**：The RSI Book 的 Python 循环 → learn-deepseek-harness 的分课实现 → Self-Improving Agents 综述中的 scaffolding 与 evaluation 部分。
- **训练与研究**：Stanford CS329A 的 verifier / RL 阅读 → Self-Improving Agents 综述中的模型改进部分 → ICLR RSI 工作坊的相关论文。

## 目录

- [研究索引与 Awesome 清单](#indexes)
- [指南、教材与学习路径](#guides)
- [实践教程](#tutorials)
- [课程与工作坊](#courses)
- [评测与综述复现](#evaluation)
- [时效与核验记录](#verification)

<a id="indexes"></a>

## 研究索引与 Awesome 清单

这一类适合找相关工作、比较研究方向和制定阅读顺序。各项目采用自己的 RSI 定义与分类框架，学习时可以互相对照。

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [Prism-Shadow/awesome-rsi](https://github.com/Prism-Shadow/awesome-rsi) | 用九个维度组织方法与评测，配有双语图解、论文筛选和引用图谱；适合先建立全景框架。 | 先读[中文 RSI 导读](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md)，再到[网站](https://prism-shadow.github.io/awesome-rsi/#blog/understanding-rsi)查方法与评测。 | 中英；基础 LLM / Agent 概念；纯阅读。 |
| [natnew/awesome-recursive-self-improvement](https://github.com/natnew/awesome-recursive-self-improvement) | 将领域地图与入门、系统构建、安全与边界三条路线结合，适合把零散论文串成阅读顺序。 | [Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths)，先选一条路线再进入主题目录。 | 英文；LLM / 机器学习基础；纯阅读。 |
| [lobehub/awesome-rsi](https://github.com/lobehub/awesome-rsi) | 覆盖模型、Harness、记忆、多 Agent、具身和自动 AI 研究；解释任务收益、保留收益和改进器收益等不同证据层级。 | [Fundamentals & Getting Started](https://github.com/lobehub/awesome-rsi#fundamentals--getting-started) → [Scope & Terminology](https://github.com/lobehub/awesome-rsi#scope--terminology)。 | 英文；LLM / Agent 基础；纯阅读。 |
| [Persdre/awesome-recursive-self-improvement](https://github.com/Persdre/awesome-recursive-self-improvement) | 以“修改对象 × 闭环程度”整理研究，适合辨析不同工作所说的 RSI。 | [What Counts as RSI?](https://github.com/Persdre/awesome-recursive-self-improvement#what-counts-as-rsi)，再按修改对象查论文。 | 英文；机器学习 / Agent 背景；其中层级标签是作者的整理框架。 |
| [Token-Rhythm/awesome-rsi](https://github.com/Token-Rhythm/awesome-rsi) | 双语文献表带日期、主题标签、摘要和论文 / 代码入口，适合按方向查阅。 | [中文精选读物](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#featured-rsi-readings) → [分类概览](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#category-overview)。 | 中英；纯阅读。上游最近核验标为 **2026-08-13**，9–10 月资料宜结合其他目录查阅。 |
| [selfimproving-agent/Awesome-Self-Improving-Agents](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents) | 综述配套资源，将模型参数改进与 prompt、记忆、工具、完整 scaffold 改进分开，并提供评测和应用领域索引。 | [Agent-oriented guide](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/blob/main/README_AGENT.md)中的 Quick Start 与 Reading Map，可按问题定位综述章节。 | 英文；机器学习 / Agent 基础；纯阅读，含论文源码。 |
| [jacky-leng/awesome-rsi](https://github.com/jacky-leng/awesome-rsi) | 用闭环位置、反馈、搜索、持久状态、人的角色和证据类型六个轴比较改进循环，适合做方法对照。 | [TAXONOMY.md](https://github.com/jacky-leng/awesome-rsi/blob/main/TAXONOMY.md) → [Landscape](https://github.com/jacky-leng/awesome-rsi#landscape)。 | 英文；纯阅读。上游标注核验覆盖至 **2026-10-07**。 |
| [pinkbubblebubble/awesome-rsi](https://github.com/pinkbubblebubble/awesome-rsi) | 用 RSI / Self-improvement / Enabler 标签解释资源与递归改进的关系，兼收 Harness、评测和工程报告，适合寻找近期实践方向。 | [Scope and labels](https://github.com/pinkbubblebubble/awesome-rsi#scope-and-labels) → [Start here](https://github.com/pinkbubblebubble/awesome-rsi#start-here)；实践可看 [Harness 清单](https://github.com/pinkbubblebubble/awesome-rsi#self-improvement-harnesses)。 | 英文；纯阅读。上游自报最近核验 **2026-10-21**；第三方实现各有运行条件。 |

<a id="guides"></a>

## 指南、教材与学习路径

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi) | 通过同一个仓储库存问答任务逐步讲解工具调用、确定性评估、prompt 改进、跨任务记忆和成本记录，适合第一个 Python 实验。 | [第 2 章：Build Your First Agent Improvement Loop](https://thersibook.com/chapters/ch02.html) + [配套 Notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb)。 | 英文；Python 3.10+、LiteLLM 与模型接口。示例主要更新 prompt 和记忆，模型权重不变。 |
| [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn) | 中文知识库、五阶段学习路线、架构图与进化搜索实验场，适合直观理解“生成—评估—选择—整合”。 | [页面导航与启动说明](https://github.com/Roloria/rsi-learn#页面导航)，先看[学习路线内容](https://github.com/Roloria/rsi-learn/blob/main/src/data/path.ts)，启动后进入 `/#/path` 和 `/#/lab`。 | 中文；交互站需 Node.js / Vite。实验场是**规则驱动的前端模拟**，不调用真实 LLM。 |
| [Ashish Kumar：Recursive self-improvement 三篇导读](https://ashishkumar.ai/series/recursive-self-improvement/) | 从理论基础讲到 self-play / self-training，再到自修改代码；包含 text-to-SQL 自训练循环示意与评估 Harness 讨论。 | 按顺序读 [Part 1：概念与理论](https://ashishkumar.ai/blog/recursive-self-improvement-explained/)、[Part 2：自博弈与自训练](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/)、[Part 3：自修改代码](https://ashishkumar.ai/blog/self-improving-code-alphaevolve-to-aide/)。 | 英文；适合有 LLM / 机器学习基础的读者。**2026-10-11** 发布的解释性文章，代码段用于讲解。 |

<a id="tutorials"></a>

## 实践教程

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness) | 分课实现 Agent 循环、插件、持久 Session Log、缓存、压缩、记忆、子 Agent 和运行时自修改；每课是独立小包，适合边读边改。 | [L1：最裸的循环](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → 按[网页版课程](https://prism-shadow.github.io/learn-deepseek-harness/)顺序学习 → [L10：自我修改](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification)。 | 中英；Node.js、TypeScript 基础和 DeepSeek API。L10 展示运行时生成并注册临时工具，尚未包含自动评估、晋升与持久化的完整演化循环。 |

Python 路线可直接使用上面的 **The RSI Book 第 2 章与 Notebook**；两个项目分别适合学习改进循环和 Harness 工程结构。

<a id="courses"></a>

## 课程与工作坊

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与材料范围 |
| --- | --- | --- | --- |
| [Stanford CS329A：Self-Improving AI Agents](https://cs329a.stanford.edu/) | 系统串联 test-time compute、verifier、工具反馈、规划、RL、开放式演化和 Agent 评测，适合按周安排阅读。 | 官网 Schedule 的**第 2–7 讲**建立基础，再读**第 17 讲 Agentic Evaluations & Long-Horizon Tasks**。 | 英文；机器学习 / LLM 基础。当前公开页面为 **2025 秋季课程**，本批核验课程表与论文阅读清单。 |
| [Harvard CS 2881R：AI Safety 中的 RSI 专题](https://boazbk.github.io/mltheoryseminar/) | 从 AI 研发自动化、改进速度和安全视角理解 RSI，适合补充技术实现之外的研究问题。 | [2025-10-09 归档讲](https://boazbk.github.io/mltheoryseminar/fall2025/#lecture-oct-9)有课件、总结和录影入口；再看 [2026-09-24 RSI & AI Trajectories](https://boazbk.github.io/mltheoryseminar/#lecture-sep-24)的阅读与学生实验材料。 | 英文；机器学习、概率 / 信息论与 Python 基础。属于 AI Safety 课程中的专题；2026 该讲当前未列录影。 |
| [ICLR 2026：AI with Recursive Self-Improvement Workshop](https://recursive-workshop.github.io/) | 集中呈现自改进方法、系统与评测的研究议题，适合从议程进入具体研究工作。 | 先看官网议程与主题，再从 [Accepted Papers](https://recursive-workshop.github.io/papers.html)的 Oral / Spotlight 选论文。 | 英文；研究背景更有帮助。活动日期 **2026-04-26**；本批核验官网与论文集。 |

<a id="evaluation"></a>

## 评测与综述复现

| 资源 | 特色与适合读者 | 推荐学习入口 | 语言与实践条件 |
| --- | --- | --- | --- |
| [deepgrounding/recursive-self-improvement](https://github.com/deepgrounding/recursive-self-improvement) | 综述配套仓库，提供冻结文献语料、分类脚本、图表和参考文献生成流程；把部署期改进、训练、自评估与自动研究放在同一分类框架中。 | 先读[综述源码](https://github.com/deepgrounding/recursive-self-improvement/blob/main/draft/main.md)的 §2 与 §5，再看 [Reproducing](https://github.com/deepgrounding/recursive-self-improvement#reproducing)和[语料文件](https://github.com/deepgrounding/recursive-self-improvement/blob/main/artifacts/corpus_v2.csv)。 | 英文；复现需 Python 3.11+、NumPy、Matplotlib，部分脚本访问 arXiv / OpenAlex。语料冻结于 **2026 年 7 月**，9 月公开发布。 |
| [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI) | 图解改进循环、评估和修改准入，附小型 Python 示例，适合学习接受 / 拒绝候选修改与记录历史的代码结构。 | [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python 门控示例](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py)。 | 英文；示例使用 Python 3.10+ 标准库。接收外部传入的测试状态、收益和路径后作判断，不包含模型生成改动或自动执行评测。 |

<a id="verification"></a>

## 时效与核验记录

本批核验日期为 **2026-10-22**：读取了项目 README、推荐章节或课程页面，并对涉及实践能力的条目抽查相关代码。**未运行上游教程、调用模型或复现实验，也未逐篇复核清单内的论文。** 视频只核对课程页提供的入口。

下表记录有依据的内容变化、发布或上游自报核验时间；它们与本项目的核验日期不同，也不等同于整个领域的覆盖截止日期。提交日期按 Asia/Taipei 记载，上游直接标注的日期保留原值。

<details>
<summary>展开 17 项资源的内容时间与核验范围</summary>

| 资源 | 内容时间与依据 | 本批阅读范围 |
| --- | --- | --- |
| Prism Awesome RSI | [2026-10-15 新增双语文章](https://github.com/Prism-Shadow/awesome-rsi/commit/6cf55d1bbe224ca1c26c2bb5c8b66e429cce220c)；[中文导读 09-20 更新](https://github.com/Prism-Shadow/awesome-rsi/commit/775a1bdbe4dc60c55cd9d32e792d36f2ec658534)。10-19 提交仅更换二维码。 | README、导读源码、网站路由与资源配置；未验证筛选网站的全部交互。 |
| natnew Awesome RSI | [2026-10-18 新增六项研究](https://github.com/natnew/awesome-recursive-self-improvement/commit/b30c5fd2e36fe8a1f8381444e03377bec16135a1)。 | README、Reading Paths 与新增条目的提交差异。 |
| LobeHub Awesome RSI | [2026-10-12 更新证据分层](https://github.com/lobehub/awesome-rsi/commit/874f5c331c6d2deb70954da12ef9df4b9f255ad0)；随后排序与 CI 修改未当作资料新增。 | README 的术语、入门、目录与相关提交差异。 |
| Persdre Awesome RSI | [2026-09-02 整理并澄清分类标签](https://github.com/Persdre/awesome-recursive-self-improvement/commit/cde30351387b4abd23373884e90d508f7368b5ef)。 | README 的定义、分类与学习资源。 |
| Token-Rhythm Awesome RSI | 上游自报 Last verified **2026-08-13**；[同日补充代码入口](https://github.com/Token-Rhythm/awesome-rsi/commit/87681b460d6420f29f88bc3a2b848ddc6891dd1b)。 | 英文目录与维护说明、中文精选和分类入口。 |
| Awesome Self-Improving Agents | [2026-10-19 新增 RHD 条目](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/commit/7ffbe03841e18a21200a0384cb38f868be93bd73)。 | README、README_AGENT 的分类、章节导航和评测说明，及最新条目差异。 |
| jacky-leng Awesome RSI | 上游核验覆盖至 **2026-10-07**；[10-08 扩充目录与六轴分类](https://github.com/jacky-leng/awesome-rsi/commit/f41e58bdf14a9a52912eefd85e10215587786c24)。 | README、TAXONOMY 与提交差异；推荐源码入口，未验证阅读网站的完整交互。 |
| pinkbubblebubble Awesome RSI | 上游自报 Last reviewed **2026-10-21**；[台北时间 10-22 新增近期资料](https://github.com/pinkbubblebubble/awesome-rsi/commit/c91823d6ebd9969cea3b7b05e20027988ec5308b)。 | 标签、Start here、Harness 和相关集合章节，以及内容提交差异。 |
| The RSI Book | [2026-07-16 新增第 3 章](https://github.com/bhavsarpratik/rsi/commit/7ce1c397323d442744be8d75ba584afca5d46afd)；8 月最新提交为页面设计更新。 | README、第 2 章、Agent 源码与配套 Notebook 的 setup / Agent 单元。 |
| Roloria/rsi-learn | [2026-09-22 加入学习站与模拟器](https://github.com/Roloria/rsi-learn/commit/64fa58065410fdc8d0c1c333f2bfc3d74019145b)。 | README、五阶段路线和模拟器引擎源码。 |
| Ashish Kumar 三篇导读 | [系列页](https://ashishkumar.ai/series/recursive-self-improvement/)与三篇正文均标注 **2026-10-11** 发布。 | 系列目录、三篇正文与篇内学习入口。 |
| learn-deepseek-harness | [2026-08-23 重组为基础 L1–L8 与进阶 L9–L10](https://github.com/Prism-Shadow/learn-deepseek-harness/commit/4c3b6492767f8af9d65a2a97776ed3bea8841aec)。 | 总 README、L1 文档 / 源码 / 依赖、L10 文档。 |
| Stanford CS329A | 官网标为 **Autumn 2025**。 | 课程介绍、Schedule 与公开论文阅读入口。 |
| Harvard CS 2881R RSI 专题 | **2025-10-09** 归档讲与 **2026-09-24** 新一届专题。 | 官方课程页、两个讲次的阅读 / 课件 / 代码入口；未观看视频。 |
| ICLR 2026 RSI Workshop | 官网标明活动日期 **2026-04-26**。 | 官方主题、议程和 Accepted Papers 页面。 |
| deepgrounding 综述材料 | **2026 年 7 月**冻结语料；[09-06 发布公开仓库](https://github.com/deepgrounding/recursive-self-improvement/commit/aceac9d8a8e46caa702b9651857380a4729202a7)。 | README 的复现流程与许可范围、综述分类和语料方法章节；未重新生成语料或图表。 |
| RSI Atlas | [2026-10-22 修复冻结路径匹配](https://github.com/aniruddhaadak80/RSI/commit/f4246024469d7e7eadea7a59db64f8289e57eb2a)；Start 文档页标注 09-18。 | README、Start 页面、Python 引擎、依赖与代码差异。 |

</details>

## 收录与整理原则

- 按资源形式组织主目录，主题覆盖模型训练、Agent Harness、记忆与技能、评测和自动研究。
- 同时收录理解 RSI 所需的自改进 Agent 等相邻主题，在条目中说明具体用途。
- 给出推荐理由、具体学习入口、语言、前置知识与实践条件。
- 区分纯阅读、模拟演示、真实模型调用和训练；按实际阅读或运行范围记录核验。
- 优先链接原始项目；同一项目的网站、翻译与 Notebook 合并介绍，普通镜像不重复计数。
- 以实质内容和学习价值判断时效，保留仍然有用的稳定教材与历史课程。

## 参与贡献

欢迎通过 [Issue](https://github.com/RZRZ-Q/awesome-rsi-resources/issues) 推荐资源，或提交 Pull Request。收录要求见 [贡献指南](CONTRIBUTING.md)。

## 许可

本仓库原创内容采用 [MIT License](LICENSE)。链接所指向的第三方资料遵循各自的许可。
