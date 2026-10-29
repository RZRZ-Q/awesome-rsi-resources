# RSI 学习指南

[English](learning-guide.md) | **简体中文**

[资源目录](../README_zh.md) · [实践指南](practice-guide_zh.md) · [核验档案](verification_zh.md)

从目标选择学习路线，再用综述章节与实践项目建立联系。资源分类与完整目录见首页，具体运行配置见实践指南。

- [按目标选择短路线](#learning-paths)
- [推荐综述阅读路线](#survey-reading-path)
  - [入门总览](#introductory-overviews)
  - [方法进阶](#methods)
  - [可选：持续自改进的可靠性与安全控制](#reliability-safety)
- [从综述到实践项目](#survey-project-map)

<a id="learning-paths"></a>

## 按目标选择短路线

可以按自己的目标选一条短路线：

- **中文学习路线**：[Prism 导读](../README_zh.md#prism) → [Hello-Agents Reflection](practice-guide_zh.md#hello-agents) → 可选的 [WalkingLabs 前置 Notebook](practice-guide_zh.md#walkinglabs) → [李宏毅自我成长讲次](../README_zh.md#hung-yi-lee) → [RSI 研究札记](../README_zh.md#rsi-research-notes)与[原始综述](../README_zh.md#surveys)。
- **概念入门**：[Prism 中文导读](../README_zh.md#prism) → [The RSI Book 第 1–2 章](practice-guide_zh.md#rsi-book) → [natnew 阅读路线](../README_zh.md#natnew)。
- **Agent 工程**：[The RSI Book 的 Python 循环](practice-guide_zh.md#rsi-book) → [learn-deepseek-harness](practice-guide_zh.md#learn-deepseek-harness) → [Harness² 流程演示](practice-guide_zh.md#harness2)，再选 [Meta-Harness](practice-guide_zh.md#meta-harness) 或 [AHO](practice-guide_zh.md#aho) → selfimproving-agent 综述中的 scaffold 与评估章节。 若要把学到的修改部署给现有 Agent，再学 [Hermit 外置 adapter](practice-guide_zh.md#hermit)。
- **Harness 收益与成本**：[Harness 专题综述](../README_zh.md#harness-rsi-survey) → [HarnessMM 本地机制演示](practice-guide_zh.md#harnessmm) → [Elicitation or Expansion 收益诊断](practice-guide_zh.md#elicitation-or-expansion)。区分减少重复推理、提高单次成功率与扩大可解任务范围，再用 [DGM／ADAS 基线对照](practice-guide_zh.md#textbook-baselines)学习工程控制与预算匹配。
- **优化实践**：[GEPA / DSPy](practice-guide_zh.md#gepa) → [GEPA-Curator 方法阅读](practice-guide_zh.md#gepa-curator)，思考哪些反馈适合指导更新 → [ShinkaEvolve](practice-guide_zh.md#shinkaevolve) 或 [OpenEvolve](practice-guide_zh.md#openevolve) → 用 [DGM](practice-guide_zh.md#dgm) 进阶研究 Agent 代码演化。
- **递归改进**：[RSI Labs Notebook 第 4 节](practice-guide_zh.md#rsi-labs) → [STOP](practice-guide_zh.md#stop-source-route) → [SICA](practice-guide_zh.md#sica-source-route) → [DGM](practice-guide_zh.md#dgm)，再用 [VERSE](practice-guide_zh.md#verse)研究优化器保留的工具、提示和技能。依次追踪改进器指令、动态加载的 Python 函数和归档 Agent 实现如何参与后续改进，再用 [Dream-RSI](practice-guide_zh.md#dream-rsi) 对比通过回放更新探索策略；若不熟悉候选评估和归档，可先学[前置 Notebook](practice-guide_zh.md#walkinglabs)。
- **多 Agent 组织**：[Co-Evolution 综述 §3](https://arxiv.org/html/2608.10299v1#S3) → [CORAL 经验共享示例](practice-guide_zh.md#coral) → [EAT 团队演化源码路线](practice-guide_zh.md#eat)。对比共享尝试记录与根据积累经验重新设计团队角色和执行阶段。
- **经验与记忆**：[Hello Generic Agent](practice-guide_zh.md#hello-generic-agent) → 用 [ACE](practice-guide_zh.md#ace) 学习文本经验手册，或用 [Voyager](practice-guide_zh.md#voyager) 学习可执行技能 → 用 [LongMemEval-V2](practice-guide_zh.md#longmemeval-v2) 评估记忆组件 → 用 [PAST-Bench](practice-guide_zh.md#past-bench) 对比任务序列中保留与不保留经验的结果。
- **训练与研究**：[Stanford CS329A](../README_zh.md#cs329a) 的 verifier / RL 阅读 → selfimproving-agent 综述中的模型改进部分 → [SEAL](practice-guide_zh.md#seal) 适应循环或 [Agent Lightning](practice-guide_zh.md#agent-lightning) 策略训练 → [ICLR RSI 工作坊](../README_zh.md#iclr-rsi)的相关论文。

<a id="survey-reading-path"></a>

## 推荐综述阅读路线

本路线使用[覆盖表](verification_zh.md#survey-coverage)中的**论文及对应日期核实的版本**，适合已有基本 LLM 与 Agent 概念的读者。顺序是本目录的学习建议；各论文的定义与自主性等级属于各自作者的框架。章节号对应上述版本，PDF 页码从文件第一页起算。

**核心路线：** Prism → *Self-Improvements in Modern Agentic Systems* → *Towards AI That Improves Itself* → 选一个方法分支。先读下列推荐章节，其余论文用于补充视角，不是额外的必修前置。

<a id="introductory-overviews"></a>

### 1. 入门总览

前两篇按顺序读，再按需选择两篇补充比较。读完应能说明：**改什么、什么会保留到下一轮、如何衡量改进**。

| 论文／路线位置 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **1. 领域总图 — [From Existing Methods to New Research Ideas: Two Perspectives on Recursive Self-Improvement](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)** | 用九个设计维度比较方法，并联系传统深度学习，为构思研究问题提供起点。 | §2.3 RSI 闭环（第 5 页）→ §3.1 分类总览（第 6 页）→ §5 评估（第 17 页）；构思研究方向时再读 §4.2。 |
| **2. 系统总图 — [Self-Improvements in Modern Agentic Systems: A Survey](https://arxiv.org/html/2607.13104v1)** | 区分模型参数更新与提示、记忆、工具、外围控制框架的更新，帮助选择要深入研究的组件。 | §3 定义 → §4 分类 → 工程方向读 §6 scaffold，训练方向读 §5 模型 → §8.1 改进的衡量。 |
| **选读：比较视角 — [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/html/2607.07663v2)** | 从改进对象与闭环由谁验证两个角度比较方法，并将评估器本身作为研究对象。 | §2.1 定义 → §2.2 两轴分类；关注评估时继续读 §§5.1–5.2 的评估器设计与验证层级，再读 §5.5 的结果改进与过程改进。 |
| **选读：系统组成 — [The Path to Recursive Self-Improving Agents: Foundation, Framework, and Future Directions](https://www.preprints.org/manuscript/202608.0051)** | 把模型、Harness、数据系统、训练器和改进机制联系起来，适合理解各组件更新之间的依赖。 | §§2.1–2.3：组件、能力等级，以及诊断—提案—评估—集成闭环 → §6 多组件共同改进。 |

<a id="methods"></a>

### 2. 方法进阶

先读 *Towards AI*，再选与自己项目最接近的分支。模型训练、协同演化分支适合有机器学习／强化学习基础的读者；经验与代码分支更直接衔接 Agent 工程。

| 论文／分支 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **共同基础 — [Towards AI That Improves Itself: A Survey of Recursive Self-Improvement](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5)** | 区分继承已接受的改进与改进器本身变强，并关联验证、更新决策和持久记忆。 | §3 定义与主张检验框架（第 5 页）→ §§4.2–4.3 反馈与优化；Agent 工程继续读 §5.2（第 21 页）。 |
| **Harness 修改与复用 — [From Harness Optimization to Recursive Self-Improvement](https://github.com/LucasXinYu/harness-rsi/blob/7f846c52fe70338ee97584c33c06f7ec99f67ed5/docs/paper/Harness_RSI_Preprint_2026-10-27.pdf)** | 将改进流程与具体接口、记忆和控制流变化对应起来，比较哪些修改能在后续任务复用。 | §2.1 工作流（第 3 页）→ §3.2 递归机制与证据（第 6 页）→ §§4.5–5 跨领域对照与评估（第 10 页）。使用 2026-10-27 作者修订版；附录 K 收录该次文献补充，领域证据仍冻结于 10-01。 |
| **模型训练 — [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/html/2603.25681v3)** | 串起数据获取与筛选、模型优化、推理改进和自主评估，形成完整的学习生命周期视角。 | §4.1 优化总览 → §§4.3–4.4 自生成优化与自演化优化 → §6 自主评估。 |
| **经验、记忆与技能 — [Self-Improving Agents in the Era of Experience: A Survey of Self- to Meta-Evolution](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf)** | 跟踪执行经验如何进入可复用技能、记忆与更高层控制，连接 Harness 工程与持续学习。 | §2 作为经验基础设施的 Harness（第 5 页）→ §§3–4 技能与记忆 → §§7–8 元演化与纵向评估。 |
| **代码 Agent — [Self-Evolving Coding Agents](https://arxiv.org/html/2608.03392v4)** | 区分修改当前任务的代码与更新供后续复用的 Agent 组件，比较资产、架构和参数三类对象。 | §2.3 操作边界 → §3 分类 → 选读 §4 资产、§5 架构或 §6 参数 → §§7–8 反馈与评估。 |
| **多智能体与环境适应 — [Co-Evolution in Agentic Systems: Toward Self-Directed Evolution Beyond Human Design](https://arxiv.org/html/2608.10299v1)** | 研究 Agent、环境和演化机制之间相互关联的变化，将视角扩展到固定环境以外。 | §§2.2–2.3 定义与阶段总图 → §3 Agent 间或 §4 Agent 与环境的协同演化 → §5 元协同演化；用附录 A 对比相邻概念。 |
| **自主性 — [The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement](https://arxiv.org/html/2609.11873v3)** | 关注系统控制了哪些改进决策、哪些仍由外部决定；其自主性等级帮助在任务得分之外比较系统。 | §§2.2–2.3 概念基础与证据范围 → §3.1 的 B0 参照边界 → §3.7 跨等级综合；再从 §§3.2–3.6 选择感兴趣的等级。 |
| **实验证据 — [Recursive Self-Improvement in AI: A Survey](https://www.preprints.org/manuscript/202609.2680)** | 按工程目标与更新对象组织方法，再区分任务收益、保留收益和改进器的贡献，适合设计对照实验时阅读。 | §3.1 定义 → §4.1 两轴总图 → §6.5 改进器修订 → §§7.4、7.6 分离改进器贡献与解释证据。 |

完成所选分支后，画出一个具体闭环：**可修改组件 → 反馈 → 接受规则 → 保留状态 → 后续任务评估**。再用[综述与项目对应表](#survey-project-map)选择实践入口。

<a id="reliability-safety"></a>

### 可选分支：持续自改进的可靠性与安全控制

本节为可选分支，探讨保留的经验如何影响后续行为，以及如何让持续更新保持可靠、可控。关注这些问题的读者可在入门核心与 *Towards AI* 之后进入本节。

| 论文 | 特色与用途 | 推荐先读章节 |
| --- | --- | --- |
| **[Safety in Self-Evolving Agents: A Survey](https://arxiv.org/html/2610.00093v1)** | 跟踪经验成为可复用状态时，来源、权限和作用范围如何变化；SAVER 将状态载体、更新操作与违规、暴露、响应联系起来。 | §2.1 范围 → §§2.3–2.4 状态转移检查与 SAVER → §3.3 长期记忆或 §3.6 技能与过程。 |

随后把分析接到控制机制：*Towards AI* §4.3 与 §6.6 讨论更新策略、权限和回滚；*Recursive Self-Improvement in AI: A Survey* §8.4 讨论自修改下的评估完整性。需要系统整体视角时，再读 *The Path to Recursive Self-Improving Agents* §7.4。可以选一条记忆或一个技能，从产生追踪到后续复用，指出其权限在哪里变化、控制措施应在哪里介入。

<a id="survey-project-map"></a>

## 从综述到实践项目

本表连接已收录的教程、实践项目和评测示例。表中横跨[三类资源](../README_zh.md#resource-scope)，阅读分支表示主题，不代表 RSI 能力等级。对应关系是本目录的学习建议；除非明确说明，不表示综述已引用该项目，部分项目晚于综述发布。先围绕学习目标尝试链接中的示例，再回到对应综述章节比较机制。

项目入口依据 **2026-10-22–29** 阅读的上游文档与代码整理，未运行示例。每行的实践说明集中记录环境、模型访问、运行门槛和具体命令；各资源的核验日期与范围见[核验档案](verification_zh.md#verification)。

| 阅读分支／对应综述 | 项目与上手入口 | 学习目标与范围 |
| --- | --- | --- |
| **共同基础** — [Prism §§2.3、5](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)；[Towards AI §§3–4](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5) | [The RSI Book 第 2 章](https://thersibook.com/chapters/ch02.html) → [配套 Notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb)。 [实践说明](practice-guide_zh.md#rsi-book)。 | 跟踪评估、提示修订与经验跨任务复用，比较初始 Agent 和更新后的 Agent；Notebook 的经验列表保留在当前 kernel 中，未写入磁盘供跨会话使用。 |
| **递归改进：教学原型** — [The Last AI §§2.2、3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)，本目录的学习对应 | [RSI Labs Notebook 第 4 节](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)；[实践说明](practice-guide_zh.md#rsi-labs)。 | 跟踪反馈怎样变成新的改进器指令，经开发集验收后用于后续修复选择。3 个开发案例和 3 个留出诊断案例用于讲解可修改边界；未执行所选修复以衡量端到端收益。 |
| **递归改进：可执行的改进器** — [The Last AI §§2.2、3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)；[Coding Agents §§3、7–8](https://arxiv.org/html/2608.03392v4)，本目录的学习配对 | [STOP 源码路线](practice-guide_zh.md#stop-source-route) → [SICA 源码路线](practice-guide_zh.md#sica-source-route)。 | 定位编辑后的代码交接给下一轮改进执行者的位置，对比直接替换函数与选择归档 Agent；区分接受候选和证明性能提升。 |
| **递归改进：优化器工具与过程** — [The Last AI §3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [VERSE：论文 §§2.1–2.3 → §3.1 → 配置／driver／meta-teacher](practice-guide_zh.md#verse)。 | 跟踪优化器对自身提示、技能、工具和笔记的修改如何进入下一轮载入的工作区；在模型权重与评测协议固定时，对比优化器自更新与执行器 Harness 修改。先读源码或分析已发布结果，再考虑运行演化。 |
| **递归改进：探索策略** — [The Last AI §3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [Dream-RSI：Quick start → `orchestrate.py`](practice-guide_zh.md#dream-rsi)。 | 跟踪在线发现树如何进入离线回放、策略选择与下一轮探索。保留的 `policy/method.py` 改变搜索方式；基础编码 Agent、任务与评估器保持固定。 |
| **反馈驱动的 Harness 优化** — [Modern Agentic Systems §6](https://arxiv.org/html/2607.13104v1#S6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4)，本目录的学习配对 | [Meta-Harness 文本分类](practice-guide_zh.md#meta-harness)或 [AHO BFCL](practice-guide_zh.md#aho)。 | 对比修改 Harness 程序与修改提示／工具中间件，识别固定提案器，并区分选择数据和最终评测。 |
| **Harness 优化：筛选有效经验** — [Modern Agentic Systems §6](https://arxiv.org/html/2607.13104v1#S6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | 学完 GEPA 后，读 [GEPA-Curator：§3 → §5.3 → 附录 B.2](practice-guide_zh.md#gepa-curator)。 | 区分提示可以修复的失败与噪声或无效反馈，再观察检索到的成功轨迹怎样指导后续编辑。§5.3 将筛选机制扩展到 Meta-Harness。这里是方法阅读入口；核验时未确认专属官方代码。 |
| **Harness 演化：统一实验入口** — [Modern Agentic Systems §6](https://arxiv.org/html/2607.13104v1#S6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [Beagle：演化示例 → evaluate／evolve 计划预览](practice-guide_zh.md#beagle)。 | 跟踪基线评估、候选编辑、选优与谱系记录。在预设算法下区分 evolver 和 evolvee；统一接口本身不代表 evolver 也在演化。 |
| **Harness 优化：外置适配层** — [Modern Agentic Systems §6](https://arxiv.org/html/2607.13104v1#S6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [Hermit：离线流程 → 首个 API 训练 → Trainer／Evolver → 部署](practice-guide_zh.md#hermit)。 | 跟踪反馈如何进入有版本记录的 adapter，并被固定宿主复用。在相同留出任务上比较无 adapter、初始与最终版本，区分结构检查、具体方法的选优和部署。离线分数变化由脚本构造；判断递归改进前需追踪具体 Evolver。 |
| **Harness 优化：效果与成本** — [Modern Agentic Systems §6](https://arxiv.org/html/2607.13104v1#S6)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [HarnessPro：论文 §§3–4 → 运行策略 → 单任务 TB2 评测](practice-guide_zh.md#harnesspro)。 | 对比 Lite／Medium／Heavy 怎样分配推理与工具调用，再将通过率、实测成本与 Pareto 选优联系起来。区分评测已发布的 Harness 与运行论文的演化流程。 |
| **Harness 成本：复用已确定的决策** — [Harness 专题综述 §§2.1、4.5–5](https://github.com/LucasXinYu/harness-rsi/blob/7f846c52fe70338ee97584c33c06f7ec99f67ed5/docs/paper/Harness_RSI_Preprint_2026-10-27.pdf)，本目录的学习配对 | [HarnessMM：控制器示例 → 集成说明](practice-guide_zh.md#harnessmm)。 | 追踪回执、动作守卫与回退条件，观察哪些慢模型回调可被替代。本地示例没有模型或真实 shell 执行；省 Token 和保持质量需完整任务测量。 |
| **Harness 收益：成功率与任务覆盖** — [Harness 专题综述 §§4.5–5](https://github.com/LucasXinYu/harness-rsi/blob/7f846c52fe70338ee97584c33c06f7ec99f67ed5/docs/paper/Harness_RSI_Preprint_2026-10-27.pdf)，本目录的学习配对 | [Elicitation or Expansion：论文分析 → 已发布候选 → HotpotQA 优化入口](practice-guide_zh.md#elicitation-or-expansion)。 | 用相同采样预算下的 pass@k 和可解任务覆盖比较单次成功率与任务范围；有限 k 不能证明能力上限，运行一次候选选优也不能替代这项分析。 |
| **实验证据：工程基线与搜索** — [RSI in AI §§7.4、7.6](https://www.preprints.org/manuscript/202609.2680)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [DGM／ADAS 基线对照：README → 方法／讨论 → 离线结果重算](practice-guide_zh.md#textbook-baselines)。 | 对比继承的自修改与工程修复、单次重设计、不修改的循环及相同预算下的采样。先重算已发布结果，再考虑新实验；区分本研究的 DGM 移植与更换模型后的评测，以及在原始条件下复现原系统。 |
| **改进经验与元 Agent 代码** — [The Last AI §3.6](https://arxiv.org/html/2609.11873v3#S3.SS6)，本目录的学习配对 | [Harness²](practice-guide_zh.md#harness2) → [HyperAgents](practice-guide_zh.md#hyperagents)。 | 对比保留经验库指导后续编辑，与继承元 Agent 代码执行后续编辑；先用 Harness² 固定演示观察状态，再追踪真实实现的复用边界。 |
| **模型训练：Agent 策略** — [LLM Overview §§4、6](https://arxiv.org/html/2603.25681v3)；[Modern Agentic Systems §5](https://arxiv.org/html/2607.13104v1) | [Agent Lightning：Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode)。 [实践说明](practice-guide_zh.md#agent-lightning)。 | 跟踪工具调用轨迹如何变成奖励、GRPO 更新和策略 checkpoint。示例使用预设训练器更新 Agent 策略，未演示训练器自身改进。 |
| **模型训练：内层适应／外层学习** — [LLM Overview §§4.3–4.4](https://arxiv.org/html/2603.25681v3)；[The Path §5](https://www.preprints.org/manuscript/202608.0051) | [SEAL：general-knowledge 流程](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md)。 [实践说明](practice-guide_zh.md#seal)。 | 跟踪自编辑内容生成 → 临时 LoRA 适应 → 问答评估 → 编辑生成器的 ReST-EM 训练，比较内层更新和外层学习各自的作用。 |
| **模型训练：共享模型承担改进角色** — [LLM Overview §§4.3–4.4](https://arxiv.org/html/2603.25681v3)；[Modern Agentic Systems §5](https://arxiv.org/html/2607.13104v1) | [MASS：计划预览 → 单任务搜索 → 两轮配置](practice-guide_zh.md#mass)。 | 跟踪搜索与选中轨迹如何进入 SFT、导出和下一轮循环，检查更新后的模型怎样再次充当工作流执行者、优化者与环内评审；区分流程预览和实际学习。 |
| **模型训练：Harness 与策略联合更新** — [LLM Overview §§4.3–4.4](https://arxiv.org/html/2603.25681v3)；[The Path §6](https://www.preprints.org/manuscript/202608.0051) | [Self-HPO：H-step 提案 → P-step RL → 策略导出](practice-guide_zh.md#self-hpo)。 | 跟踪当前策略提出的 Harness 如何经过选优、策略训练，进入下一轮 H-step；对比复用更新策略的 `PROPOSER=self` 与独立的外部 API 提案器设定。 |
| **经验、记忆与技能** — [Frontis §§2–4](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf) | [Hello Generic Agent 第 4 章](https://datawhalechina.github.io/hello-generic-agent/part1/chapter4/) → [第 12 章](https://datawhalechina.github.io/hello-generic-agent/part2/chapter12/)；安装其关联的 GenericAgent 实现。 [实践说明](practice-guide_zh.md#hello-generic-agent)。 | 将已完成任务整理成可复用 SOP／脚本，再观察后续会话如何检索。学习保留什么、何时复用；验证主要依靠提示约束，可能需要用户指导。 |
| **经验：可复用上下文** — [Modern Agentic Systems §6.1.2](https://arxiv.org/html/2607.13104v1#S6.SS1.SSS2)明确讨论 ACE | [ACE Formula CLI](https://github.com/ace-agent/ace/blob/main/eval/finance/run.py) → 保存／重载 `best_playbook.txt`；[实践说明](practice-guide_zh.md#ace)。 | 跟踪反馈如何变成保留的经验条目，并进入后续样本。在模型权重固定时，对比适应前与重载选优手册后的持出集结果。 |
| **经验：可执行技能** — [Modern Agentic Systems §§6.3.1–6.3.2](https://arxiv.org/html/2607.13104v1#S6.SS3.SSS2)明确讨论 Voyager | [Voyager 技能管理器](https://github.com/MineDojo/Voyager/blob/main/voyager/agents/skill.py) → README 已学习技能库示例；[实践说明](practice-guide_zh.md#voyager)。 | 跟踪 critic 验收后的代码如何落盘、跨会话重载、检索和组合。区分新增技能的 `learn()` 与复用技能的 `inference()`。 |
| **经验：记忆组件评测** — [Self-Evolving Agents §7.2.1](https://arxiv.org/html/2507.21046v4#S7.SS2.SSS1)与 [§7.1.4](https://arxiv.org/html/2507.21046v4#S7.SS1.SSS4)，本目录的编辑配对 | [LongMemEval-V2 基线](https://github.com/xiaowu0162/LongMemEval-V2#reproducing-baselines)：无检索 → RAG；[实践说明](practice-guide_zh.md#longmemeval-v2)。 | 固定读者模型、问题、证据预算与裁判，对比答案准确率和记忆查询延迟。这里测量记忆组件，未覆盖 Agent 持续改进的完整轨迹。 |
| **经验：跨会话评测** — [Frontis §§7–8](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf)；[Self-Evolving Agents §7.2.1](https://arxiv.org/html/2507.21046v4#S7.SS2.SSS1) | [PAST-Bench：偏好采纳任务族 → 经验保留对照](practice-guide_zh.md#past-bench)。 | 在新会话组成的任务序列中，对比保留与不保留经验；结合轨迹、保存产物与 `sequence_comparison.json`，将后续结果对应到经验的保存、检索与更新。 |
| **实验证据：AI 研发任务** — [Prism §5](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf)；[The Path §§2.1–2.3、6](https://www.preprints.org/manuscript/202608.0051) | [Scale RSI Bench：nanoGPT 数据筛选任务 → 其他样例的任务约定](practice-guide_zh.md#scale-rsi-bench)。 | 对比数据筛选、自蒸馏、稳健性与 Agent swarm 任务的可修改组件、预算和评分。任务衡量研发操作的效果，单项得分本身不代表已形成递归改进闭环。 |
| **代码：程序演化预备练习** — [Coding Agents §§3、7–8](https://arxiv.org/html/2608.03392v4) | [ShinkaEvolve 教程](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb)；也可选 [OpenEvolve 函数最小化](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization)。 [ShinkaEvolve 实践说明](practice-guide_zh.md#shinkaevolve)；[OpenEvolve 实践说明](practice-guide_zh.md#openevolve)。 | 跟踪代码变异、评估反馈、选择和候选保存。示例演化的是任务程序，可用于理解综述中进一步要求的 Agent 组件更新边界。 |
| **自主性：小型工程入口** — [The Last AI §§2.2–3](https://arxiv.org/html/2609.11873v3) | [learn-deepseek-harness L1](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → 按课程顺序 → [L10](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification)。 [实践说明](practice-guide_zh.md#learn-deepseek-harness)。 | 观察 Agent 能提出、注册哪些工具变化。L10 生成的工具只在当前进程中保留；对照综述辨认扩展为完整改进闭环所需的评估、接受与持久化机制。 |
| **代码与自主性：研究实现** — [Coding Agents §§3、7–8](https://arxiv.org/html/2608.03392v4)；[The Last AI §3](https://arxiv.org/html/2609.11873v3) | [DGM 环境搭建](https://github.com/jennyzzt/dgm#setup) → [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py)。 [实践说明](practice-guide_zh.md#dgm)。 | 跟踪编码 Agent 自身的修改、后代评估与档案复用；继承的 Agent 实现参与下一轮自修改。对比任务程序演化，记录 Agent 可以修改什么、外部评估控制什么。 |
| **协同演化：共享经验** — [Co-Evolution §3.2.1](https://arxiv.org/html/2608.10299v1#S3.SS2.SSS1) | [CORAL 圆堆积](https://github.com/Human-Agent-Society/CORAL/tree/main/examples/circle_packing)，配置两个 Agent；[实践说明](practice-guide_zh.md#coral)。 | 跟踪带分数的尝试怎样进入共享笔记／技能，再改变另一 Agent 的方案；对照独立搜索轨迹与经验共享。 |
| **协同演化：团队组织** — [Co-Evolution §3](https://arxiv.org/html/2608.10299v1#S3)；[Coding Agents §§7–8](https://arxiv.org/html/2608.03392v4) | [EAT：§3.2 → §§4.2、4.5 → Skill 与监督者／启动器源码](practice-guide_zh.md#eat)。 | 跟踪保留的结果与轨迹如何变成新的团队角色、提示、执行阶段，继而产生程序修改。比较预算控制下的改进曲线与消融；可修改的团队组织和监督者的固定更新过程是不同对象。 |
| **协同演化：独立 Agent 策略** — [Co-Evolution §3.2.1](https://arxiv.org/html/2608.10299v1#S3.SS2.SSS1) | [CoMAS 训练启动器](https://github.com/xxyQwQ/CoMAS/blob/main/scripts/train_comas.sh) → 交互／奖励／controller 代码；[实践说明](practice-guide_zh.md#comas)。 | 跟踪同伴方案与批评如何形成交互奖励、各自参数更新，以及后续多 Agent rollout。 |
| **协同演化：任务生成** — [Co-Evolution §4.1.2](https://arxiv.org/html/2608.10299v1#S4.SS1.SSS2) | [R-Zero 交替循环](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/main.sh)；[实践说明](practice-guide_zh.md#r-zero)。 | 追踪 Solver 一致性 → Challenger 奖励 → 生成任务／伪标签 → Solver 更新 → 下一轮 Challenger。这是本目录对综述任务空间分类的实践映射。 |
| **协同演化：可执行环境** — [Co-Evolution §4.3.1](https://arxiv.org/html/2608.10299v1#S4.SS3.SSS1) | [JaxUED Maze ACCEL](https://github.com/DramaCow/jaxued/blob/main/examples/maze_plr.py)，启用 `--use_accel` → PAIRED；[实践说明](practice-guide_zh.md#jaxued)。 | 跟踪策略表现如何影响关卡保留／变异，形成的课程又怎样更新策略；用固定评测关卡观察迁移。 |
| **对抗式自博弈：最佳响应与历史策略** — [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1)，由本目录选择对应实现 | [OpenSpiel Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/nfsp_kuhn_pytorch.py)，先从表格型 fictitious play 开始；[实践说明](practice-guide_zh.md#open-spiel)。 | 比较 DQN 最佳响应与蓄水池样本训练的平均策略。跟踪平均策略的可利用度，区分针对当前对手的学习与面对最佳响应的稳健性。 |
| **对抗式自博弈：共享 LLM 策略** — [Modern Agentic Systems §7.3](https://arxiv.org/html/2607.13104v1#S7.SS3)明确讨论 SPIRAL | [SPIRAL 游戏训练启动器](https://github.com/spiral-rl/spiral/blob/main/run.sh)；[实践说明](practice-guide_zh.md#spiral)。 | 沿两方轨迹、按角色估计的优势、策略优化与权重更新追踪，观察新对手如何进入下一轮 rollout。 |
| **对抗式自博弈：偏好博弈扩展** — [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1)，本目录补充的相邻学习示例 | [SPPO 三轮启动器](https://github.com/uclaml/SPPO/blob/main/run_sppo_mistral.sh)；[实践说明](practice-guide_zh.md#sppo)。 | 用固定 PairRM 评审比较当前策略的回答，检查 SPPO loss，再追踪新 checkpoint 进入下一轮。对照游戏 RL 与独立演化的多 Agent。 |
| **实验证据／提示优化** — [Bounded Self-Refinement §5](https://arxiv.org/html/2607.07663v2)；[RSI in AI §7](https://www.preprints.org/manuscript/202609.2680) | [GEPA / DSPy AIME Notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb)；对照 [TextGrad Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb)。 [GEPA 实践说明](practice-guide_zh.md#gepa)；[TextGrad 实践说明](practice-guide_zh.md#textgrad)。 | 检查数据划分、文本反馈和优化前后的提示表现；TextGrad 还包含验证集表现下降时的回退。两个入门示例均保持模型权重与优化器逻辑固定。 |
| **可选：可靠性与安全控制** — [Safety §§2.3–2.4](https://arxiv.org/html/2610.00093v1)；[Towards AI §§4.3、6.6](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=14) | [RSI Atlas 接受规则示例](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py)。 [实践说明](practice-guide_zh.md#rsi-atlas)。 | 改变传入的测试结果、质量收益和修改路径，观察接受／拒绝决策与历史记录。该练习只处理决策逻辑，不生成补丁，也不执行所传测试结果对应的测试。 |
