# 实践指南

[English](practice-guide.md) | **简体中文**

[返回资源目录](../README_zh.md) · [学习指南](learning-guide_zh.md) · [核验档案](verification_zh.md)

这里集中记录具体示例的学习目标、源码入口和运行条件。先按主题选择项目；综述章节与项目的对应关系见[学习指南](learning-guide_zh.md#survey-project-map)。条目的[三类标签](../README_zh.md#resource-scope)描述所推荐入口的范围，主题分组不表示 RSI 能力等级。

以下说明来自 **2026-10-22–29** 对上游文档与部分源码的核验，**未运行教程、调用模型或复现实验**；逐项日期与范围见[核验档案](verification_zh.md#verification)。API 示例需要相应模型权限与调用预算，训练配置是上游示例而非本目录实测的最低硬件要求。

## 目录

- [入门教材、Notebook 与 Agent 构件](#foundations)
- [提示词优化](#prompt-optimization)
- [程序搜索](#program-search)
- [Agent 与改进器代码](#agent-code)
- [Harness 优化](#harness-optimization)
- [模型训练](#model-training)
- [记忆与技能](#memory-skills)
- [协同演化](#coevolution-projects)
- [对抗式自博弈](#adversarial-self-play)
- [评测](#evaluation)

<a id="foundations"></a>

## 入门教材、Notebook 与 Agent 构件

<a id="rsi-book"></a>

### [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi)

**相关自改进机制。** 通过同一个仓储库存问答任务逐步讲解工具调用、确定性评估、prompt 改进、跨任务记忆和成本记录，适合第一个 Python 实验。

**推荐入口。** [第 2 章：Build Your First Agent Improvement Loop](https://thersibook.com/chapters/ch02.html) + [配套 Notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb)。

**语言与运行条件。** 英文；Python 3.10+、LiteLLM、Notebook 环境与模型接口。示例主要更新 prompt 和记忆，模型权重不变。经验列表仅保留在当前 kernel 中，未写入磁盘供跨会话使用。

<a id="rsi-learn"></a>

### [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn)

**相关自改进机制 · 模拟演示。** 中文知识库、五阶段学习路线、架构图与进化搜索实验场，适合直观理解“生成—评估—选择—整合”。

**推荐入口。** [页面导航与启动说明](https://github.com/Roloria/rsi-learn#页面导航)，先看[学习路线内容](https://github.com/Roloria/rsi-learn/blob/main/src/data/path.ts)，启动后进入 `/#/path` 和 `/#/lab`。

**语言与运行条件。** 中文；交互站需 Node.js / Vite。实验场是**规则驱动的前端模拟**，不调用真实 LLM。

<a id="walkinglabs"></a>

### [WalkingLabs：Self-Improving Agent Notebook](https://github.com/walkinglabs/self-improving-agent-notebook)

**相关自改进机制 · 前置课程。** 17 本双语 Notebook 串联 Agent 循环、验证、RL、代码搜索、记忆与评估。参考 CS329A 大纲重建的社区材料，并非 Stanford 官方课程 Notebook。

**推荐入口。** 基础学习从 [L01](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part1-foundation/01-course-overview.ipynb)开始；本目录重点推荐 [L07 Open-Ended Evolution](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part2-training/07-open-ended-evolution.ipynb)，跟踪代码生成 → 评分 → 归档 → 下一次提议；[英文 Notebook](https://github.com/walkinglabs/self-improving-agent-notebook/tree/main/notebooks-en)采用同样的目录结构。

**语言与运行条件。** 中文／英文；Python 3.10+、仓库依赖、Jupyter / ipykernel（需另装）与 OpenAI 兼容模型 API，通过 `AGENT_LLM_*` 配置。L07 无需 GPU 训练；设计器固定，算术差错率来自教学环境设定，archive 保留在内核中。上游许可仍标为待确定。

<a id="rsi-labs"></a>

### [RSI Labs · weilinear/rsi_labs](https://github.com/weilinear/rsi_labs)

**递归改进方法 · 教学原型。** 餐费示例依次区分临时修正答案、复用工具，以及修改选择后续改进的策略。第 4 节由 Gemini 改写改进器自己的指令，开发集得分提高后才采纳，并用于新案例。

**推荐入口。** 先读[作者讲解](https://blog.weili.me/posts/recursive-self-improvement-part-1-a-simple-toy-example)，再顺序运行 [gemini_self_improvement.ipynb](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)，重点看**第 4 节：Improve how the agent chooses improvements**；也可[在 Colab 打开](https://colab.research.google.com/github/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb)。

**语言与运行条件。** 英文；Colab／本地 Jupyter、`google-genai==2.28.0` 与 `GOOGLE_API_KEY`；无需训练 GPU。默认 `gemini-3.8-flash`，可通过 `GEMINI_MODEL` 修改；未实测端点兼容性。状态仅在当前会话保留。元实验在 **3 个开发 + 3 个留出案例**上衡量修复选择准确率，初始策略被刻意设得较弱；未执行所选修复，也未验证多代端到端收益。该仓库后续 Notebook 保持改进器固定。

<a id="hello-agents"></a>

### [Datawhale Hello-Agents：Reflection 与自进化](https://github.com/datawhalechina/hello-agents)

**相关自改进机制 · 前置示例。** 以中文讲解和代码串起生成、评审、修改方案的过程。素数函数示例便于逐步追踪反思循环，扩展章节再梳理四类 Agent 自进化闭环。

**推荐入口。** 先对照阅读[第四章 §4.4 Reflection](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter4/第四章%20智能体经典范式构建.md#44-reflection)与 [Reflection.py](https://github.com/datawhalechina/hello-agents/blob/main/code/chapter4/Reflection.py)，再读 [Extra10：Agent 自进化](https://github.com/datawhalechina/hello-agents/blob/main/Extra-Chapter/Extra10-Agent自进化.md)。

**语言与运行条件。** 中文；Python 3.10+、`openai`、`python-dotenv` 及 OpenAI 兼容模型接口。示例依赖模型反馈改进任务输出，不执行生成的代码，也不训练模型权重。

<a id="learn-deepseek-harness"></a>

### [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness)

**相关自改进机制 · 前置构件。** 分课实现 Agent 循环、插件、持久 Session Log、缓存、压缩、记忆、子 Agent 和运行时自修改；每课是独立小包，适合边读边改。

**推荐入口。** [L1：最裸的循环](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → 按[网页版课程](https://prism-shadow.github.io/learn-deepseek-harness/)顺序学习 → [L10：自我修改](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification)。

**语言与运行条件。** 中英；Node.js、TypeScript 基础和 DeepSeek API。L10 展示运行时生成并注册临时工具，尚未包含自动评估、晋升与持久化的完整演化循环。

<a id="hello-generic-agent"></a>

### [Datawhale Hello Generic Agent](https://github.com/datawhalechina/hello-generic-agent)

**相关自改进机制。** 讲解如何将经验沉淀为可复用 SOP 和脚本，并用四层记忆组织与检索。适合学习任务经验如何变成后续会话可发现、可复用的知识。

**推荐入口。** [第 4 章：记忆与 Skill 系统](https://datawhalechina.github.io/hello-generic-agent/part1/chapter4/) → [第 12 章：自我进化](https://datawhalechina.github.io/hello-generic-agent/part2/chapter12/)；安装时参照实现仓库的[当前中文安装指南](https://github.com/lsdefine/GenericAgent/blob/main/docs/installation_zh.md)。

**语言与运行条件。** 中文；教程仍为 **Beta**。推荐 Python 3.11/3.12、模型 API，以及所选界面／工具的依赖。更新对象是记忆和技能，可能需要用户引导；验证规则属于提示词约束，并非完整自动晋升机制。

<a id="prompt-optimization"></a>

## 提示词优化

<a id="gepa"></a>

### [GEPA / DSPy 官方教程](https://github.com/gepa-ai/gepa)

**相关自改进机制。** 用完整数学示例串起基线评估、文本反馈、候选选择和优化后评估，适合学习模型权重固定时提示词如何逐步改进。

**推荐入口。** 从 [GEPA for AIME Notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb) 开始，再读 [GEPA optimization](https://dspy.ai/current/getting-started/gepa-optimization/)，理解数据划分和优化后程序的保存。

**语言与运行条件。** 英文；Python 3.10–3.14、DSPy / GEPA、datasets；示例需要 OpenAI API key，MLflow 跟踪可选。

<a id="textgrad"></a>

### [TextGrad 官方 Notebook](https://github.com/zou-group/textgrad)

**相关自改进机制。** 通过类似 PyTorch 的接口讲解文本梯度，再在物体计数问题上优化共享提示词、使用验证集评估，并在验证性能下降时回退更新，适合理解反馈驱动的文本优化。

**推荐入口。** [Primitives](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Primitives.ipynb) → [Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb)。

**语言与运行条件。** 英文；Python 3.9+、Jupyter / Colab、OpenAI API key。Notebook 沿用较早的模型 ID，运行前需核对兼容模型的可用性；更新提示词文本而非模型权重。

<a id="program-search"></a>

## 程序搜索

<a id="shinkaevolve"></a>

### [ShinkaEvolve · SakanaAI](https://github.com/SakanaAI/ShinkaEvolve)

**相关自改进机制。** 用引导式 Notebook 串起 LLM 代码变异、程序种群、评估器和持久化搜索记录；圆堆积任务适合学习程序进化，并比较不同父代选择策略。

**推荐入口。** [Getting Started](https://sakanaai.github.io/ShinkaEvolve/getting_started/) → [交互教程 Notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) → 阅读[圆堆积评估器](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/circle_packing/evaluate.py)。

**语言与运行条件。** 英文；Python 3.10+（建议 3.11）、本地 Python 或 Colab，以及模型 API 凭据。入门示例进化的是任务程序；评估器在本地运行，不要求训练用 GPU。

<a id="openevolve"></a>

### [OpenEvolve](https://github.com/algorithmicsuperintelligence/openevolve)

**相关自改进机制。** 受 AlphaEvolve 启发的开源程序搜索框架。函数最小化小示例展示初始搜索算法、评估反馈、配置与检查点如何组成闭环。

**推荐入口。** 阅读 [Installation & Setup](https://github.com/algorithmicsuperintelligence/openevolve#installation--setup)，取得仓库示例后跟随 [Function Minimization](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization)，结合阅读 `initial_program.py`、`evaluator.py` 和 `config.yaml`。

**语言与运行条件。** 英文；Python 3.10+、NumPy 和模型端点。示例默认经 OpenAI 兼容 API 使用 Gemini；Docker 可选。该 API 示例无需训练 GPU。优化的是任务代码，不更新模型权重。

<a id="agent-code"></a>

## Agent 与改进器代码

建议按 [RSI Labs](#rsi-labs) → [STOP](#stop) → [SICA](#sica) → [DGM](#dgm) 阅读，再用 [HyperAgents](#hyperagents) 比较元 Agent 的继承。STOP 与 SICA 的源码链接固定到 2026-10-23 核验的提交；阅读无需模型凭证。

<a id="dgm"></a>

### [Darwin Gödel Machine（DGM）](https://github.com/jennyzzt/dgm)

**递归改进方法 · 研究实现。** 原论文研究实现：Agent 修改自身代码，在编程任务上评估后代，并保留归档；继承的 Agent 实现参与后续自修改。适合准备沿源码理解完整研究循环的读者。

**推荐入口。** 阅读 [Setup / Running the DGM](https://github.com/jennyzzt/dgm#setup)，再追踪 [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py)。

**语言与运行条件。** 英文；Python、Docker、模型 API，以及 SWE-bench / Polyglot 环境和数据。这是需要较多环境与评估工作的研究复现入口，适合进阶学习。

<a id="stop"></a>

### [STOP · Self-Taught Optimizer](https://github.com/microsoft/stop) · [论文](https://arxiv.org/abs/2310.02304)

**递归改进方法 · 研究实现。** Python 改进器编辑自身实现，选中的代码成为后续自改进的执行者。学习区分改进任务解答与改进生成解答的函数；语言模型、评分函数和外层循环保持固定。

**推荐入口。** [种子改进器](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_seed_algorithm.py#L3) → 元效用 → 候选选择 → 动态加载；按 [STOP 路线](#stop-source-route)阅读。

<a id="stop-source-route"></a>

#### STOP：修改后的函数如何成为下一轮改进器

1. **识别改进器接口。** 读 [`improve_algorithm`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_seed_algorithm.py#L3-L23)：输入程序、效用函数和语言模型，生成并评分候选。种子实现从生成的候选中选择，不会自动把未修改的输入加入比较。
2. **向下一层追踪评测。** 先读公开的[元效用接口](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/utility.py#L5)，再读 [`get_improver` 与实际元效用](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_utility.py#L28-L112)。候选被加载成改进器，通过修改下游任务程序接受评测。默认是对**同一个带噪奇偶校验任务／种子重复五次**，并非五个不同任务；选择使用验证效用。
3. **定位递归交接。** 在 [`run_improver.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/run_improver.py#L122-L179) 中，当前改进器编辑 `algorithm_to_improve`，而目标本身就是改进器代码。接受后，代码写入 `results/<run_id>/improved_algorithm_<iteration>.py`，并替换待改目标。默认 `iterative=True` 时，它还替换 `improver_str`；[`temp_override`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/helpers.py#L154-L192) 加载新的 `improve_algorithm`，用于下一次编辑。若设为 `iterative=False`，目标继续变化，执行者仍是种子实现。
4. **核对接受意味着什么。** 外层门槛排除异常或零效用，**不要求分数超过父代**。默认六轮会保存并加载最后一个候选，但不会再用它执行第七次自编辑。通过这条路线辨认可执行实现的继承，不把它等同于每轮性能必然提高或整个系统都能递归改变。

#### 运行入口与条件

英文；Python、模型 API 与隔离执行环境，不进行本地权重训练。旧 SDK／模型配置和缺失的依赖清单需要适配。

 从 [`config.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/config.py#L1) 与 [`language_model.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/language_model.py#L10) 开始；根目录入口为 `python run_improver.py`，按源码要求在 `api_key.py` 提供 `openai_key` 字典。源码使用旧 `openai.ChatCompletion.create` 接口，默认模型为 `gpt-4-0314`，运行前需适配 SDK 与可访问模型。仓库没有依赖清单，导入至少涉及 `openai`、`pebble`、`multiprocess`、`numpy`、`jsonlines`、`tqdm`。嵌套候选评测会放大 API 工作量，语言模型的调用上限不是整个实验的总预算。生成的 Python 会被执行；现有[可靠性保护](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/helpers.py#L80)不构成安全沙箱，应使用隔离环境。

<a id="sica"></a>

### [SICA · Self-Improving Coding Agent](https://github.com/MaximeRobeyns/self_improving_coding_agent) · [论文](https://arxiv.org/abs/2504.15228)

**递归改进方法 · 研究实现。** 选中的归档 Agent 用自身代码与工具修改后继，学习 benchmark 反馈与归档选择如何决定后续改进器。待改父代与执行改进的 Agent 可以不同；外部评测／选择框架保持固定，不训练模型权重。

**推荐入口。** [Runner 主循环](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L1022-L1049) → 父代／改进器选择 → 归档模块执行 → 改进工具 → 下一轮评测；按 [SICA 路线](#sica-source-route)阅读。

<a id="sica-source-route"></a>

#### SICA：选中的后代如何成为后续编辑者

1. **画出外层循环。** 从 [`runner.main`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L1022-L1049) 开始：评测 `agent_i` → 记录分数与轨迹 → 生成 `agent_{i+1}` → 下一轮评测后继。生成后继不等于它已成为最佳 Agent。
2. **区分父代与改进器。** [`select_base_agent`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L87-L145) 选择分数达到最佳代下置信界门槛的较近期父代，将[该代代码复制到后继工作目录](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L769-L785)；另由 [`get_best_agent_iteration`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/utils/archive_analysis.py#L291-L308) 选择 benchmark 平均分最高者执行改进。两次选择可以指向不同版本。
3. **追踪继承的实现进入执行。** [Docker 挂载与命令](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L823-L869) 将归档设为只读、后继工作目录设为可写，然后运行 `python -m archive.agent_{best_iter}.agent_code improve`。沿[相对 `Agent` 导入](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/__main__.py#L17)和[相对实现导入](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/agent.py#L17-L26)往下读，确认实际执行改进任务的是被选中版本的代码。
4. **阅读改进流程。** 按 [`improve_agent`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/__main__.py#L113-L214) → [`MetaImprovementReasoningStructure`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/tools/reasoning_structures/meta_improvement.py#L18-L85) → [工具注册](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/agents/implementations/main_orchestrator.py#L77-L95) 阅读，观察归档反馈怎样进入提案、编码、要求执行的测试和变更日志。这些工具与指令本身属于可继承的 Agent 代码。
5. **用 benchmark 证据闭合循环。** 读[候选执行](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L469-L475)和[分数保存](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L531-L552)。后代经过评测并被选中后，其实现才可能成为后续改进器。编辑进程成功本身不代表任务性能提升；晋升由外部 runner 与评分／选择规则控制。

#### 运行入口与条件

英文；Python、Docker／buildx、benchmark 下载及实际模型配置对应的 API。需准备 Docker 环境并反复执行 benchmark 的进阶工程路线；API 路线未要求本地训练 GPU。

 参照固定版本的 [Quickstart](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/README.md#quickstart) 与 [Makefile](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/Makefile)。在仓库根目录的 Python 环境中执行 `pip install -r base_agent/requirements.txt`、`pip install swebench`。配置 [Agent 模型](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/config.py#L12-L19)与 runner 的[总结模型调用](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L326-L338)：默认涉及 Sonnet 3.7、o3-mini 和 Gemini 2.0 Flash，任意一个供应商的 key 并不足够。将两处配置对齐到可访问模型，并在宿主 shell 导出对应供应商的环境变量，**之后**再用 `make image` 构建 Docker 镜像（Apple Silicon 使用 `make image-mac`）。上游构建会把 API 凭证写入镜像环境；更换凭证后需重新构建，并保留为私有镜像。

启动前先读 `python runner.py --help`；完成配置后可用 `python runner.py --workers 1 --iterations 2` 限定并发和轮次。[参数解析器](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L48-L65) 用 `--experiment-id`／`-id` 指定已有实验，README 示例中的 `--id` 不适用。默认 [benchmark 注册表](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/benchmarks/__init__.py#L31-L53) 启用 GSM8K；[任务队列](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L648-L699) 仍为**每个 benchmark 选择 18 题**，不会随 worker 数减少。两轮会评测 agent 0、1，最后生成的 agent 2 留待后续评测。worker／轮次限制不等于总费用上限，元改进流程没有配置整个运行的 API 总预算；应按需要数据、Docker 资源和付费模型调用的研究运行准备。

<a id="hyperagents"></a>

### [HyperAgents · Meta 与合作团队](https://github.com/facebookresearch/HyperAgents) · [论文](https://arxiv.org/abs/2603.19461)

**递归改进方法 · 可修改的元 Agent。** 任务 Agent 与负责修改它的元 Agent 都可编辑；先应用所选父代的补丁，再由继承的元 Agent 生成下一候选。学习改进流程自身的修改怎样跨代传递，外部领域评测保持固定。

**推荐入口。** 读[论文框架与 DGM-H 实现](https://arxiv.org/html/2603.19461v1) → [Setup](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/README.md#setup) → [`generate_loop.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/generate_loop.py) → [`run_meta_agent.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/run_meta_agent.py) → [`meta_agent.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/meta_agent.py)。追踪继承的补丁进入执行，再看新候选的评分。

**语言与运行条件。** 英文；Python **3.12**、Docker、构建依赖、模型 API 与领域数据。`bash ./setup_initial.sh` 准备默认论文评审路线；之后可用 `python generate_loop.py --domains paper_review --max_generation 1 --eval_workers 1` 限定代数／并发，仍需完成相应评测。上游 Docker 构建辅助脚本含内网代理设置，需按环境调整。公开研究代码采用 **CC BY-NC-SA 4.0**。

<a id="dream-rsi"></a>

### [Dream-RSI · Google Research](https://github.com/google-research/dream-rsi) · [论文](https://arxiv.org/abs/2609.14858)

**递归改进方法 · 探索策略代码。** 在线探索形成发现树，离线回放比较改写后的搜索预算分配策略。选中的策略保存为 `policy/method.py`，用于下一轮在线探索。学习搜索策略的变化如何影响后续改进尝试；编码 Agent、任务与评估器固定，选优也可能保留原策略。

**推荐入口。** 读 [Quick start](https://github.com/google-research/dream-rsi/blob/8ec35bd2538220517ce1bfca4282db21b8c518db/README.md#quick-start)，再沿 [`orchestrate.py`](https://github.com/google-research/dream-rsi/blob/8ec35bd2538220517ce1bfca4282db21b8c518db/dream_rsi/orchestrate.py#L439-L479) 跟踪 explore → learn → promote。完成配置后，先检查圆堆积任务配置，再尝试上游的短运行：

```bash
DRY_RUN=1 bash scripts/run_dream_rsi.sh circle_packing_26
WORKSPACE=workspace/smoke ROUNDS=2 BRANCHES=3 REFINE=1 MAX_WORKERS=3 \
  bash scripts/run_dream_rsi.sh circle_packing_26
```

**语言与运行条件。** 英文；Python ≥3.10、以 editable 模式安装任务依赖、Gemini CLI/API 访问，以及下载的 Math/Lasso 任务文件。Dry run 仍检查任务文件、依赖、Agent 与 API key；第二条命令会真实调用模型。Lasso 另需 `g++`／Eigen，KernelBench 另需 GPU 评估服务。已发布工程不包含论文中的 Harness 优化实验与 Current History Only 消融。

<a id="verse"></a>

### [VERSE · Verified Self-Evolving Optimizer](https://github.com/wzekai/VERSE) · [论文](https://arxiv.org/abs/2610.02616)

**递归改进方法 · 优化器 Harness 继承。** VERSE 根据执行反馈，同时改进执行器 Harness 和优化器自身的提示、技能、工具、hooks 与笔记。追踪更新后的优化器如何参与下一轮；模型权重、评测划分和选择规则保持固定。

**推荐入口。** 读[论文 §§2.1–2.3 → §3.1](https://arxiv.org/html/2610.02616v1) → [`verse_mh.yaml`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/configs/self_teacher/verse_mh.yaml) → [`driver.py`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/evolution/driver.py) → [`meta_teacher.py`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/evolution/meta_teacher.py)。重点跟踪 `end_round()`：meta-episode 用当前工具修改持久化的 `teacher_ws/`，通过结构检查的编辑被提交，下一轮 `begin_round()` 重新加载优化器的工具与指令。可执行 hooks 的健康检查与改进质量评测是两个不同环节。

低门槛第一步是在克隆的仓库中运行 `python results/make_table.py`，从[已发布结果](https://github.com/wzekai/VERSE/tree/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/results)重算论文表格；只使用 Python 标准库，无需模型调用。完成[安装、数据准备与模型服务](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/README.md)后，实际演化入口为：

```bash
CONFIG=self_teacher/verse_mh TAG=-r1 bash scripts/run_swe.sh
```

**语言与运行条件。** 英文；完整运行需要 Python ≥3.12、Docker、另行准备的任务数据与模型服务。参考 vLLM 部署为**优化器 4 GPU、执行器 1 GPU**，不是经本目录验证的最低配置。启动脚本默认六轮演化、24 个并发任务，并进行三次重复测试评估，需据此准备预算。结合 `rounds.jsonl`、优化器工作区和 `test110.json`，将继承的变化与持出结果对应起来。重算已发布数字与重新执行这些实验应分开理解。

<a id="harness-optimization"></a>

## Harness 优化

<a id="harness2"></a>

### [Harness² · Google Cloud AI Research／Northwestern](https://github.com/google-research/harness2) · [论文](https://arxiv.org/abs/2610.14224)

**递归改进方法 · 改进器经验库。** 对当前任务执行“提案—试跑—组合”，再将采纳的 Harness 与有证据支持的经验保留下来，供后续改进会话使用。学习任务内适应与跨任务改进经验如何连接；模型权重、阶段指令与决策规则固定。

**推荐入口。** 读[论文 §2 与 Figure 3](https://arxiv.org/html/2610.14224v1#S2) → [Install](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/README.md#install) → 运行 Demo：

```bash
harness2-demo --output runs/demo --k 2
```

查看 `demo.json`、`INDEX.md`、`EXPERIENCE.md`，沿[经验库上下文与采纳流程](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/schedule.py#L499-L563)追到后续任务。

**语言与运行条件。** 英文；Python **3.12/3.13**、uv。Demo 使用固定编辑器与真实 Python 执行，无需模型凭证或 Docker。真实模型运行需 Linux、Node.js 20+、模型访问与 benchmark 依赖，按 [Setup](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/docs/SETUP.md) 配置。核验提交未附文档提到的 `.env.example`，需手工设置所列变量。

**Harness²：跟踪被保留的状态。** 每个新任务从共同基础执行 Harness 开始；之前采纳的 Harness 与经验提供给改进器选择复用。对照[经验库持久化](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/library.py#L106-L151)与[传给改进器的上下文](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/context.py#L161-L164)。Demo 的[固定提案器](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/demo.py#L120-L163)展示流程连接，不会从经验库学习其编辑。真实运行的默认路线使用 Google Cloud／Vertex AI 凭证；LAB 另需 Pandoc／Poppler，WorkBuddy-Bench 另需 Docker。

<a id="hermit"></a>

### [Hermit · CMU InfiniAI Lab](https://github.com/Infini-AI-Lab/hermit)

**相关自改进机制 · 外置 adapter 训练。** Hermit 固定模型和原有 Harness，演化独立 adapter 中的指令、技能、记忆或工具代码。Trainer 记录反馈、检查文件结构并保存 adapter 版本，Evolver 提供更新方法。是否形成递归改进取决于所选方法，不能由框架名称直接判断。

**推荐入口。** 读[离线教程](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/get-started/quickstart.md) → [Trainer](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/framework/trainer.md) → [Evolver](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/framework/evolver.md)。准备 **Python 3.12+** 与 Git，在虚拟环境中安装以下固定版本源码：

```bash
git clone https://github.com/Infini-AI-Lab/hermit.git
cd hermit
git checkout 2056e435d4be138358872208c3b233890cecf74c
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -e .
hermit check --config docs/_examples/first_training/run.yaml
hermit eval --config docs/_examples/first_training/run.yaml --adapter none
hermit train --config docs/_examples/first_training/run.yaml
hermit eval --config docs/_examples/first_training/run.yaml --adapter final
```

查看生成的 `ADAPTER.md` 与评测汇总。脚本化 learner 从预设反馈写入大写输出规则，构造的分数增长用于演示训练契约，不代表真实模型改进。这个可信本地例子关闭了 learner sandbox，无需凭证、GPU 或外部数据。

**语言与运行条件。** 英文。[首个真实模型教程](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/get-started/first-model.md)使用九个内置情感任务（训练、验证、测试各三个）、chat-completions API，以及 `python -m pip install -e . --group gepa`；依赖组要求 **pip ≥25.1**。应配套使用固定源码版本的依赖与例子，其布局和 Python 要求不同于最初的 PyPI 0.1.0 发布。[OfficeQA](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/recipes/officeqa.md)另需数据集权限与模型配置；沙箱中的 learner 程序需 Linux／bubblewrap，其 Codex 执行路线还需 Docker／npm。

规格检查通过不等于分数提升，应在相同测试划分比较 no-adapter、root 与 final。Evolver 决定 `final`，它并不统一代表最高分检查点。[部署与转换](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/tutorials/deploy-an-adapter.md)生成宿主工作区或受支持的插件文件，不会启动 Codex／Claude Code，也不会执行训练。

<a id="meta-harness"></a>

### [Meta-Harness · Stanford IRIS 与合作团队](https://github.com/stanford-iris-lab/meta-harness) · [论文](https://arxiv.org/abs/2603.28052)

**相关自改进机制 · 外部 Harness 搜索。** 编码 Agent 提案器读取历史候选源码、分数与原始轨迹，再修改任务专用 Harness。学习反馈怎样支持记忆、检索与编排变化；提案器与搜索驱动本身不参与演化。框架与其 [Terminal-Bench 产物仓库](https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact)合为一项。

**推荐入口。** 从[文本分类示例](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/reference_examples/text_classification/README.md)开始：

```bash
cd reference_examples/text_classification
uv sync
uv run python meta_harness.py --iterations 1
```

按 [`meta_harness.py`](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/reference_examples/text_classification/meta_harness.py) → `benchmark.py` → `inner_loop.py` 阅读；中文预习可选 [RSI 研究札记报告 13 第 4 节](https://github.com/asimfish/awesome_rsi/blob/63f83e581ff3161932b62ab5fbe845fdf03cf84b/reports/13_meta_harness.md)。

**语言与运行条件。** 英文代码／文档；Python **≥3.11**、uv、已认证的 Claude Code CLI 提案器与任务模型访问。示例默认用 OpenRouter；包装器会从提案器环境移除 `ANTHROPIC_API_KEY`。数据已附带，一轮仍包含多个候选／数据集的评测。API 路线无需训练 GPU；迁移到新领域前读 [ONBOARDING](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/ONBOARDING.md)。

<a id="aho"></a>

### [Agent Harness Optimizer（AHO）· Airbnb](https://github.com/airbnb/agent-harness-optimizer) · [论文](https://arxiv.org/abs/2609.05736)

**相关自改进机制 · 提示与中间件优化。** BetterHarness、PRISM、GEPA、MIPROv2 在固定模型周围搜索修改。学习区分指令失败与工具边界失败，再连接评测、验收和已保存的差异；优化器自身保持固定。

**推荐入口。** 读[论文 §3](https://arxiv.org/html/2609.05736v2#S3)与 [§4.3](https://arxiv.org/html/2609.05736v2#S4.SS3) → [Quick Start](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/README.md#quick-start) → [BFCL 数据配置](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/data/bfcl/README.md)。沿 [BetterHarness 循环](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/agent_harness_optimizer/optimizers/better_harness/loop.py)追到 `decision.json`、`report.json`、`final_diff.md`，再对照 PRISM。

**语言与运行条件。** 英文；Python **≥3.12**、源码安装（`pip install -e .`）、内外模型 API，以及单独下载的 BFCL v4 题目与答案文件。根目录 CLI 为 `python -m agent_harness_optimizer.cli`，需补齐 Quick Start 的 benchmark／optimizer／model／output 必填参数。学习时限制样本与轮次；API 路线无需训练 GPU。

**AHO：区分选择与最终评测。** `train`／`holdout` 分别承担修复／验证作用，反复使用的验收数据不属于未触碰的最终测试。在核验的 BetterHarness 路径中，`--split-seed` 还会启用**完整 600 题 BFCL scorecard**，即使 train／holdout 样本较少也一样。应有意识地设置 `--train-cases`、`--holdout-cases`、`--max-iterations`。[实际默认验收规则](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/agent_harness_optimizer/framework/acceptance.py#L58-L82)要求通过验收题数严格增加，README 中较旧的错误率／成本回退伪代码不描述该默认行为。每题时间／token 限制也不等于整个运行的费用上限。

<a id="beagle"></a>

### [Beagle / DarwinX · Salesforce AI Research](https://github.com/SalesforceAIResearch/Beagle)

**相关自改进机制 · Harness 演化框架。** DarwinX 先评估基线，再由 evolver 修改 evolvee Harness、检查候选，并记录保留版本与谱系。学习区分可修改的 Harness、提案 Agent 与固定选优算法。文档中的入口演化的是 Harness，尚不能据此认定 evolver 自身也在演化。

**推荐入口。** 按 [Quick Start](https://github.com/SalesforceAIResearch/Beagle/blob/73e112f892aefe6226e4ee7723f23ae849eeb13f/README.md#quick-start) → [演化示例](https://github.com/SalesforceAIResearch/Beagle/blob/73e112f892aefe6226e4ee7723f23ae849eeb13f/examples/evolution/README.md) 阅读。准备 benchmark 缓存、Harness checkout 并生成配置后，预览两任务实验：

```bash
.venv/bin/beagle evolve \
  --config tests/smoke/terminal_bench_2_1/opencode-1.18.16_darwinx_evolution_smoke2.yaml \
  --dry-run
```

查看 YAML 中的 `evolvee`、`evolver`、`algorithm`，再追踪真实运行产物中的 `state.db`、候选证据与提案／评估日志。Dry run 解析运行计划，不调用模型或启动容器，也不验证凭证与本地 checkout。

**语言与运行条件。** 英文；Python ≥3.12、uv、Docker、benchmark 数据、已接入的 Harness 仓库与模型访问。当前公开的 evolver 集成使用已安装并认证的 Cursor Agent。Onboarding 会在你的 GitHub 账户下建立实验仓库；真实演化会消耗模型额度，并将保留候选推送到这些副本，需使用自己有权限的实验仓库。小规模示例用于检查流程，不代表 benchmark 性能。

<a id="harnesspro"></a>

### [HarnessPro](https://github.com/pzs19/HarnessPro) · [论文](https://arxiv.org/abs/2610.26770)

**相关自改进机制 · 效果与成本权衡。** 论文通过轨迹诊断、Harness 编辑、生成测试与 Pareto 选优，保留 Lite／Medium／Heavy 三条谱系供后续轮次使用，提案与选择框架保持固定。公开包提供 Terminal-Bench 2、SWE-bench Pro、ProgramBench 的九套已选 Harness 及评测脚本；实践入口是阅读和对比这些产物，不是重跑完整演化流程。

**推荐入口。** 读[论文 §§3–4](https://arxiv.org/html/2610.26770v2#S3)，理解优化目标与选择循环 → [评测说明](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/docs/evaluation.md) → 对比 [TB2 三种模式](https://github.com/pzs19/HarnessPro/tree/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/harnesses/terminal-bench-2)下的 `runtime/policy.json` → [Medium hook](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/harnesses/terminal-bench-2/medium/runtime/hook.py) → [TB2 runner](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/scripts/run_tb2_harness_eval.py)。跟踪 profile 选择、推理强度、工具预算和输出压缩。例如，三种模式的 `standard` profile 分别设定 38／44／60 次工具上限，hook 会拒绝超过配置上限的调用。

按上游说明准备环境后，在其仓库根目录运行。将 `TB2_TASKS` 设为已准备的数据集目录，`CODEX_CONFIG` 设为 Codex Responses 供应商 TOML，`CODEX_BIN` 设为 Codex 可执行文件：

```bash
uv sync --frozen
uv run python scripts/prepare_runtime.py
uv run python scripts/run_tb2_harness_eval.py \
  --dataset "$TB2_TASKS" --heldout-ids splits/terminal-bench-2-test.txt \
  --run-dir runs/tb2-medium-one-task --harness-label medium \
  --harness-dir harnesses/terminal-bench-2/medium \
  --codex-config "$CODEX_CONFIG" --codex-binary "$CODEX_BIN" \
  --model gpt-5.5 --concurrency 1 --max-tasks 1
```

Runner 会先核对完整 held-out 清单与数据集验证划分，再选取一个任务；只准备一个任意任务的目录不够。先用该命令检查流程，再在相同任务集、相同模型下对比模式；每次使用新的 `--run-dir`，并同步修改 `--harness-label`／`--harness-dir`。同时记录通过率与成本；单任务运行不能建立 Pareto 前沿。

**语言与运行条件。** 英文；Linux、Python 3.12/3.13、uv、Docker + Compose、Codex CLI（上游使用 0.147.0）、具备相应模型权限与凭据的 Responses 兼容端点，以及另行获取的 TB2 数据和任务／评分镜像。该命令会真实调用模型，入口属于 API 评测而非参数训练。附带的 RTK 工具面向 Linux x86-64，其他架构需通过 `--rtk-binary` 提供兼容版本。代码为 MIT，附带评测器保留各自许可。公开包未包含论文中 GLM-5.2 演化后的 Harness 快照。

<a id="harnessmm"></a>

### [HarnessMM](https://github.com/YuhuaJiang2002/HarnessMM) · [论文](https://arxiv.org/abs/2610.32813)

**相关自改进机制 · 决策复用与 Token 核算。** Executable Decision Graph 保存 Agent 已确定的动作及其具体参数。工具回执使满足条件的动作可执行，并替代已注册的推理回调；需要新决策时交回原 Agent。独立的配套优化流程依据训练反馈修改提示词、上下文设置和适配规则，经验证集选优后冻结，再进入测试；Agent 权重与更新流程保持固定。

**推荐入口。** 读[论文 §4](https://arxiv.org/html/2610.32813v1#S4) → [本地示例](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/examples/guarded_reuse.mjs) → [`ExecutableSubdag.stream`／`observeTool`](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/integrations/deepseek_harness/sar_v2.mjs#L206) → [集成指南](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/docs/INTEGRATION.md)。克隆上游仓库后，在其根目录运行：

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -e '.[dev,analysis]'
node examples/guarded_reuse.mjs
python examples/partition.py
```

第一个示例使用三个预定义动作、合成回执和内存中的 dispatcher，断言检查三份替代记录，以及图耗尽后返回慢回调的行为；不调用模型，也不执行实际 shell 命令。划分示例仅将十个合成任务按 20% 训练、20% 验证、60% 测试分组。这两例用于学习机制和数据划分，不展示自主演化或实测 Token 节省。

继续读 [`CodexChiselController` 的接口约定](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/phiagent/harness/codex_chisel.py#L1)，追踪 `train` → `select_validation` → `freeze` → `evaluate_test`；准备新的实验配置后，才能接入真实执行器与优化器回调。对比完整任务的质量和输入加输出 Token，计入重试与回退；评估改进总成本时，另外核算开发与选优开销。

**语言与运行条件。** 英文；Python **3.10–3.14**、Node.js **22+**。两项本地示例不需模型凭证或 GPU。完整实验需要选定的上游 Harness、benchmark 数据与原生评分器、模型访问或服务，以及任务对应的执行环境；代码评测需要隔离的验证环境。[复现指南](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/docs/REPRODUCIBILITY.md)说明了部署占位符、源码与配置冻结要求。参考配置描述历史协议，不能直接作为启动任务。代码为 Apache-2.0，外部组件保留各自条款。

<a id="elicitation-or-expansion"></a>

### [Elicitation or Expansion?](https://github.com/furiosa-ai/elicitation-or-expansion) · [论文](https://arxiv.org/abs/2610.27889)

**相关自改进机制 · Harness 搜索与收益诊断。** 研究在 solver 权重固定时，比较基础 Harness 与经验证选择的 Meta-Harness 候选。学习区分“成功更频繁”和“已观察到的可解任务更多”：对照 pass@k 曲线、任务难度，以及更大模型／更多推理计算的参照。有限尝试下的覆盖率描述的是被测条件，不能当作模型固有能力上限。公开代码运行 Harness 优化；论文的重复采样分析属于另一项实验步骤。

**推荐学习入口。** 先读[论文 §§3.1–3.2 与 §§5.1–5.3](https://arxiv.org/html/2610.27889v1#S3) → 对照 [HotpotQA 配置](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/configs/hotpotqa-8b.yaml)与 [harnesses/hotpotqa](https://github.com/furiosa-ai/elicitation-or-expansion/tree/aa5de8564688c63640b22e42374a7df6cc41ed2d/harnesses/hotpotqa) 中的已发布候选 → 追踪[搜索循环与最终评测](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/core/meta_harness.py)。该配置将每题限制为四次 solver 调用、两次检索、每次最多七个段落；单独的 relaxed 配置采用不同限制。

完成上游[环境准备](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/README.md#hotpotqa-and-appworld)与[数据准备](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/data/hotpotqa/DATA.md)后，从 `agentic/` 运行：

```bash
scripts/run_one.sh configs/hotpotqa-8b.yaml
```

启动器在后台运行。查看 `runs/hotpotqa-8b-seed0/run.log`，待优化结束后再运行 `scripts/finalize.sh hotpotqa-8b-seed0`。检查该 run 下的 `results/selection.json`、`results/test_table.txt` 与 `results/finalized.json`；最后一个文件记录 `complete` 或 `incomplete`。候选先在独立 selection 集上选优，再于留出测试集计分。这些结果本身不等于复现论文的 pass@k 曲线；进行后续比较时，保持任务与评分规则一致，区分尝试次数和单次资源上限，并同时记录执行成本与覆盖率。

**语言与运行门槛。** 英文；Linux 启动脚本使用 `setsid`，agentic 包要求 Python 3.12、uv 与 Docker。需有配置中 proposer 模型的 Claude Code OAuth 访问、与容器匹配的 CLI 版本（本机 CLI 或 `PREFLIGHT_CLAUDE_VERSION`），以及兼容 OpenAI 的 solver 服务。HotpotQA 示例使用 Qwen3-8B 和 BM25 检索服务，两者均须能从 Docker 访问。HotpotQA 问题与 Wikipedia 摘要需单独获取；上游估计构建索引需约 10 GB 内存。GPU 条件取决于 solver 的部署方式；真实运行会调用模型。代码为 MIT，依赖和数据保留各自条款。公开包不含 AppWorld 候选快照，但保留其优化框架。

<a id="gepa-curator"></a>

### [GEPA-Curator: Curated Learning for Self Improving Agents](https://arxiv.org/abs/2610.37651)

**相关自改进机制 · 反馈筛选。** Curator 选择能提供有效信号的任务，并检索可信的成功轨迹用于提示优化。学习区分提示本身的不足、环境故障与评测噪声；筛选流程本身保持固定。

**推荐入口。** 读[§3 → §5.3 → Appendix B.2](https://arxiv.org/html/2610.37651v1)：任务筛选和成功轨迹检索 → 扩展到 Meta-Harness → Curator 提示。结合 [GEPA](#gepa) 与 [Meta-Harness](#meta-harness) 阅读。

**语言与运行条件。** 英文；阅读需要 Agent 与提示优化基础，无需 API 或 GPU。[核验时](verification_zh.md#verification-2026-10-29)尚未确认专属官方实现；本项作为论文阅读入口，暂无经过核验的复现命令。

<a id="model-training"></a>

## 模型训练

<a id="seal"></a>

### [SEAL · Self-Adapting Language Models](https://github.com/Continual-Intelligence/SEAL)

**相关自改进机制 · 学习生成 self-edit。** 作者原始实现学习生成 self-edit，在下游问答上评估临时 LoRA 更新，再用筛选出的编辑训练编辑生成器；适合研究内层适应与外层学习的关系。

**推荐入口。** 从 [general-knowledge 流程](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md)依次读数据生成 → TTT server → 评估 → ReST-EM 训练，再看 [SFT 数据构建器](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/src/EM/build_SFT_dataset.py)。

**语言与运行条件。** 英文；进阶 Python / 微调基础、Python 3.12、Linux / CUDA、PyTorch / vLLM / PEFT，以及模型／数据访问。上游说明使用 2 张 A100/H100；需调整 SLURM 脚本与路径。默认 TTT 评分使用 OpenAI API（GPT-4.1）；生成／proxy 评分也可使用该 API。

<a id="agent-lightning"></a>

### [Microsoft Agent Lightning v1.0](https://github.com/microsoft/agent-lightning)

**相关自改进机制。** Calc-X 将 AutoGen Agent、MCP 计算器与轨迹采集、答案奖励、GRPO 更新串起来，适合学习如何从工具调用轨迹训练并保存策略检查点。

**推荐入口。** 先读[安装说明](https://github.com/microsoft/agent-lightning/blob/main/docs/00-installation.md)，再按 [Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode)操作；按该示例要求从 `examples/calc_x` 启动。

**语言与运行条件。** 英文；Python 3.12+、Linux / WSL、NVIDIA CUDA、仓库配套的 `verl` / vLLM 安装、模型／数据下载，默认使用 W&B。Local Mode 无需 Kubernetes，模型本地运行。文档中的 Calc-X 配置为 **1 张 A100 80GB**。这是 v1.0 训练入口，旧 APO 教程对应旧 API。

<a id="mass"></a>

### [MASS · Sakana AI](https://github.com/SakanaAI/mass) · [论文](https://arxiv.org/abs/2610.12176)

**递归改进方法 · 共享模型更新。** 当前模型同时担任工作流执行者、优化者与环内评审。搜索与轨迹筛选产生监督数据，SFT 和导出产生下一轮三个角色共同使用的模型。沿 `L0` → `L1` → `L2` 学习更新后的模型如何继续参与改进。

**推荐入口。** 在克隆的仓库中先预览流水线，无需 GPU 或模型服务：

```bash
python3 -m mass plan --config configs/paper.json
```

再按 [Try one task](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/docs/running.md#try-one-task) 创建只更新一次的本地配置，然后执行 `search --tasks 51`。结合[论文与代码对照](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/docs/paper_to_code.md)与 [`configs/cycle2.json`](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/configs/cycle2.json)，将 search → collect → rank → select → render → train → export 连接到下一轮。`plan` 只打印配置和训练命令。

**语言与运行条件。** 英文；真实实验需 Linux、Python 3.12、Node.js 22、uv、vLLM、模型权重与 GPU 资源。论文第一轮 SFT 示例使用 **6×H100，约 19 小时**，不含搜索与轨迹采集。合成任务会在宿主环境执行生成的命令，应使用隔离的研究环境。打包的 MLR 配置覆盖较早的 **12 任务子集**，未包含完整 107 任务配置及若干 benchmark adapter；仓库还说明了当前 RHI 参照／champion 逻辑与论文 Algorithm 1 的差异。

<a id="self-hpo"></a>

### [Self-HPO · MSR Orchard](https://github.com/MSR-Orchard/Self-HPO) · [论文](https://arxiv.org/abs/2610.22791)

**递归改进方法 · Harness 与策略交替更新。** H-step 由当前策略分析失败、提议 Harness 修改；P-step 在选定 Harness 下用 RL 训练该策略，导出的新策略再参与下一轮 H-step 提案。跟踪 Harness 与模型这两个继承对象，以及之前未解出的任务如何形成新的搜索集。

**推荐入口。** 读 [Running Self-HPO](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/README.md#running-self-hpo) → [`scripts/h_step/proposer.sh`](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/scripts/h_step/proposer.sh) → [`scripts/p_step/run_p_step.sh`](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/scripts/p_step/run_p_step.sh)，再沿 `export_policy.sh` 回到加载 `work/p_step_<round>/policy` 的模型服务。准备训练前可先比较已发布的 `harnesses/seed` 与 `harnesses/self-hpo`。默认 `PROPOSER=self` 使用当前策略；`PROPOSER=api` 对应固定外部提案器的另一种 HPO 设定。

**语言与运行条件。** 英文；Python 3.12、uv、SGLang、Docker/slime、benchmark 数据、模型权重，以及已配置的 Orchard Agentic sandbox 地址与 key。上游训练和评测使用 **8×B200**，适合作为源码阅读与研究复现路线，不是轻量本地教程。完整一轮需要配置 H-step 模型服务、候选评估与 P-step RL。

<a id="memory-skills"></a>

## 记忆与技能

<a id="ace"></a>

### [ACE：Agentic Context Engineering](https://github.com/ace-agent/ace)

**相关自改进机制。** 作者的 Generator–Reflector–Curator 实现将反馈变成可复用文本经验手册。跟踪有标签样本、有用／有害计数、增量添加、验证集选优和后续复用；默认逐样本实现将整个 playbook 放入提示。

**推荐入口。** 先读[论文 §3](https://arxiv.org/html/2510.04618v3#S3)，再看 [finance CLI](https://github.com/ace-agent/ace/blob/main/eval/finance/run.py)。仓库根目录执行 `uv sync`，配置 `.env`／供应商模型后运行 `uv run python -m eval.finance.run --task_name formula --mode offline --save_path results --test_workers 1`。用 `--mode eval_only --initial_playbook_path ...` 重载保存的 `best_playbook.txt`。

**语言与运行条件。** 英文；Python ≥3.10、uv、模型 API；该路线无需训练 GPU。默认使用 SambaNova／DeepSeek-V3.1。Formula 默认处理完整的 **500/300/200** 条训练／验证／测试切分，并反复调用 API；`--test_workers 1` 限制并发，不限制样本量。如需缩小运行，在 `eval/finance/data/sample_config.json` 配置保持分离的小规模切分，并将 `--eval_steps` 设为不大于训练样本数的正整数，确保触发验证选优。当前默认操作更新计数并**新增**条目，可选 embedding 去重关闭。

<a id="voyager"></a>

### [Voyager](https://github.com/MineDojo/Voyager)

**相关自改进机制。** 将 Minecraft 执行经验变成持久化 JavaScript 技能库，由 LLM critic 判断成功后入库，再按描述检索代码用于后续任务。对比进入提示的技能片段与用于技能组合的完整可执行库。

**推荐入口。** 先读[论文 §§2.2–2.3](https://arxiv.org/html/2305.16291v2#S2.SS2)，再看[技能保存／检索](https://github.com/MineDojo/Voyager/blob/main/voyager/agents/skill.py)。按 [Getting Started](https://github.com/MineDojo/Voyager#getting-started) 运行 `Voyager(...).learn()`；也可用 README 的 `skill_library_dir='./skill_library/trial1'` 示例，在新任务中复用作者发布的技能。`resume=True` 可恢复持续学习。

**语言与运行条件。** 英文；Python ≥3.9、Node ≥16.13、正版 Minecraft Java **1.19**、Fabric **0.14.18**／模组、构建自定义模组所需 Java **17**，以及 OpenAI 聊天／嵌入 API。不微调模型，但需在本地运行游戏。经典实现采用较旧且部分未锁版的依赖与旧模型默认值；未实测全新安装／端点兼容性。

**学习练习：** 查看保存的手册或技能库，重启后加载它，再追踪它对持出样本或新任务的作用；保持模型与任务预算相近，与空状态运行作比较。[LongMemEval-V2](#longmemeval-v2) 提供独立的记忆组件对比，将这些项目接入其接口需要编写适配器。把组件准确率、保留经验带来的任务收益，以及改进流程自身的变化分开考察。

<a id="coevolution-projects"></a>

## 协同演化

先读 [Co-Evolution §§2.2–2.3](https://arxiv.org/html/2608.10299v1)，辨认哪些组件会变化，以及它们怎样改变彼此的学习条件。用模型 API 学习经验共享可从 **CORAL** 开始；学习环境课程可选 **JaxUED**；有多 GPU 训练条件再选 **CoMAS / R-Zero**。这些是不同机制的入口，不是必须依次完成的步骤。

综述 §3.2.1 直接讨论 CORAL 和 CoMAS；R-Zero 是本目录为 §4.1.2 选择的学习映射；JaxUED 实现了 §4.3.1 讨论的方法论文中的 ACCEL / PAIRED。这些实现仍采用人工设计的更新规则，本路线不将它们写成 §5 元协同演化的复现。

<a id="coral"></a>

### [CORAL](https://github.com/Human-Agent-Society/CORAL)

**相关自改进机制。** **共享经验；§3.2.1。** Agent 在独立 Git worktree 中改写方案，共享带分数的尝试、笔记和技能。跟踪一个 Agent 的发现怎样改变另一个 Agent 的下一次尝试；圆堆积评估器和模型权重保持固定。

**推荐入口。** 按[安装指南](https://coral.compounding-intelligence.ai/docs/getting-started/installation/)取得源码，阅读[圆堆积示例](https://github.com/Human-Agent-Society/CORAL/tree/main/examples/circle_packing)与[多 Agent 指南](https://coral.compounding-intelligence.ai/docs/guides/multi-agent/)。完成 `uv sync` 和网关配置后，在仓库根目录运行 `uv run coral start -c examples/circle_packing/task.yaml agents.count=2`。用 `coral log`、notes 和 skills 检查共享记录，结束时运行 `coral stop`（源码安装均加 `uv run` 前缀）。

**语言与运行条件。** 英文文档和中文 README；Python **3.11–3.13**、Git、`uv`、Docker 与模型 API。此示例的 `docker-opencode` 预设使用 OpenCode 和 LiteLLM 网关，须配置 `litellm_config.yaml` 的 API-key 占位符。NumPy / SciPy 评估器不需要训练 GPU；需预留两个 Agent 的模型调用与本地评估开销。

<a id="eat"></a>

### [Evolving Agent Teams（EAT）](https://github.com/caoshiyi/EAT) · [论文](https://arxiv.org/abs/2610.36848)

**相关自改进机制 · 从经验重组团队。** 监督者诊断进展停滞的原因，修改编码团队的角色、提示和执行阶段；团队产物、学习笔记与演化历史进入下一次重组，团队则在固定评测器下修改任务程序。学习持久化经验如何改变团队组织，不据此假定监督者的更新算法会改写自身。

**推荐入口。** 读[论文 §3.2 → §§4.2、4.5](https://arxiv.org/html/2610.36848v1) → [`SKILL.md` 的任务配置](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/SKILL.md) → [`SUPERVISOR.md`](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/agent_team/SUPERVISOR.md) → [`launch_stateless.sh`](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/agent_team/launch_stateless.sh)，跟踪团队配置 → 执行 → 正式评测 → 反思。[Claude Code 入口](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/README.md#get-started)为：

```text
/plugin install eat --marketplace caoshiyi/EAT
```

准备任务 Git 仓库中的 `eat/task.md` 和 `eat/eval.sh`，记录初始分数，并设置迭代上限、团队人数和美元预算。脚本的 `--persistent` 模式保留监督者会话。结合 `eat/log/TEAM_CONFIG.md`、每轮评测和 `eat/log/BUDGET.md`，将团队变化与分数、成本联系起来。

**语言与运行条件。** 英文；文档运行环境为 Linux、Claude Code 模型访问、Git、tmux 与 Python ≥3.11。EAT Gym 另需 uv、Hugging Face CLI，以及具体任务的依赖／硬件。插件命令只是安装入口，不是免模型演示；实际运行会调用模型。应使用独立任务环境：启动器关闭编码 Agent 的权限提示；上游可选的 [clean-room 配置](https://github.com/caoshiyi/EAT/tree/737e1665eeeffd3fce35d319174f88ea4613d7aa/cleanroom)另需 Linux bubblewrap 与网络白名单。

<a id="comas"></a>

### [CoMAS](https://github.com/xxyQwQ/CoMAS)

**相关自改进机制。** **独立 Agent 策略；§3.2.1。** 同伴分别求解、批评和评分，用交互奖励更新各自权重，再将新策略投入下一轮讨论。适合追踪多 Agent 交互怎样成为持久学习。

**推荐入口。** 先读[论文 §§3.1–3.3](https://arxiv.org/html/2510.08529v2#S3)，再看[训练启动器](https://github.com/xxyQwQ/CoMAS/blob/main/scripts/train_comas.sh)。按 README 建立 Python 3.10 环境、执行 `pip install -r requirements.txt`，配置 `PRETRAIN`、GPU／batch 与 W&B，在仓库根目录运行 `bash scripts/train_comas.sh`；沿 workflow → reward → controller 追踪实现。

**语言与运行条件。** 英文；RL 基础、CUDA、PyTorch / vLLM / DeepSpeed / Ray 与本地模型权重。读取仓库 `datasets/blended` 及额外评估数据。上游推荐**每 Agent 2× A100 80GB**；默认四个独立 Agent，约 **8 GPU**，不是已核实的最低需求。核心训练用本地模型，W&B 默认离线记录。

<a id="r-zero"></a>

### [R-Zero](https://github.com/Chengsong-Huang/R-Zero)

**相关自改进机制。** **自适应任务生成；§4.1.2。** 独立 Challenger 根据当前 Solver 的答案一致性学习出题；问题与多数票伪标签再用于训练 Solver，两个 checkpoint 进入后续交替轮次。跟踪任务难度与解题策略怎样相互塑造；伪标签不等于经过独立核实的答案。

**推荐入口。** 读 [Quickstart](https://github.com/Chengsong-Huang/R-Zero/blob/main/README.md) 与 [main.sh](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/main.sh)。安装 requirements，配置 `STORAGE_PATH`、`HUGGINGFACENAME`、`tokens.json` 和评测端点。根目录入口为 `bash scripts/main.sh Qwen/Qwen3-4B-Base qwen3-4b`；运行前读[出题者启动器](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/questioner_train_penalty.sh)和[解题者启动器](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/solver_train.sh)。

**语言与运行条件。** 英文；进阶 Python / RL、Linux / CUDA、PyTorch **2.7.0** 与 vLLM **0.9.1**。脚本配置 **8 GPU**，未声明统一最低 Python／显存要求。需要模型／数据访问及 Hugging Face、W&B 配置；生成数据会上传到 HF 私有数据集，完整评估使用 GPT API。应在隔离训练环境中使用：Challenger 启动器含范围较宽的 `pkill python` 清理命令。

<a id="rsi-anything"></a>

### [RSI-Anything · Gen-Verse](https://github.com/Gen-Verse/RSI-Anything) · [论文](https://arxiv.org/abs/2610.13912)

**相关自改进机制 · 策略与世界模型协同改进。** 策略提出动作，世界模型预测后果，观测反馈支持持久更新。GUI 实现在固定训练与选优规则下更新两者；跟踪保留的 checkpoint 怎样参与后续交互，不据此假定更新算法会改写自身。

**推荐入口。** 读[论文 §§2.3–2.5 → 表 4](https://arxiv.org/html/2610.13912v1) → [GUI 指南](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/README.md) → [`rsi.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/rsi.py) → [`policy_train.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/policy_train.py)／[`gui_world.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/gui_world.py)。跟踪成功动作的 SFT 与回放、浏览器状态转移及专家延续带来的世界模型更新，再看开发集如何决定是否保留新策略／模型组合。两轮候选版本均在交叉评测策略与世界模型前冻结。报告中的 selected controller 使用 `alpha=0`（策略排序），须与纯世界模型排序模式区分。

先从固定源码版本运行以下 CPU 浏览器检查，分别安装公共 CLI 和浏览器运行环境：

```bash
git clone https://github.com/Gen-Verse/RSI-Anything.git
cd RSI-Anything
git checkout 8ba44cd73ec6f57b151ec06e2f71a0726adfb687
python3.10 -m venv .venv
.venv/bin/python -m pip install -e .
python3.10 -m venv .venv-gui
.venv-gui/bin/python -m pip install -e 'tasks/gui[browser]'
.venv-gui/bin/python -m playwright install chromium
.venv/bin/rsi run --config configs/gui/smoke.json
.venv/bin/rsi report --run runs/gui-smoke
```

该检查用规则控制器在 Chromium 中操作复选框，无需模型凭证或 GPU；验证的是环境与报告流程，不是学习效果或 RSI 性能。Linux 若缺少浏览器系统库，需按 GUI 指南安装 Playwright 依赖。

**语言与运行条件。** 英文指南与中文 README。完整 GUI 训练使用 Linux、Python 3.10、CUDA，基础模型下载约 **22 GB**，还需为轨迹与 checkpoint 预留空间。默认将**三张 GPU**分配给不同角色；A800 80 GB 是记录中的环境，不是已核实的最低要求。模型获取、资源配置与完整工作流见 GUI 指南。另一条[代码修复路线](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/docs/reproduction.en.md)保持 coder 固定，其中评测入口不会更新参数。

<a id="jaxued"></a>

### [JaxUED](https://github.com/DramaCow/jaxued)

**相关自改进机制。** **环境课程；§4.3.1。** ACCEL 根据策略表现给迷宫关卡打分、保留与变异，再用形成的课程训练策略。对照生成关卡和策略迁移；之后读 PAIRED 的两个学习者与可训练环境生成器。

**推荐入口。** 取得源码并执行 `pip install -e ".[examples]"`；阅读 [Maze PLR/ACCEL](https://dramacow.github.io/jaxued/maze_plr/)，在仓库根目录运行 `WANDB_MODE=disabled python examples/maze_plr.py --use_accel`，再读 [`maze_paired.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_paired.py)。使用当前 [`maze_plr.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_plr.py)，避开旧 Getting Started 页已失效的 `minigid_plr.py` 路径。

**语言与运行条件。** 英文；Python / PPO / JAX 基础。包声明 Python **≥3.9**；按 [JAX 安装说明](https://docs.jax.dev/en/latest/installation.html)匹配平台与 JAX / Flax、examples 依赖。无需 LLM API，命令中关闭了 W&B。可在 CPU 上开发，但默认 ACCEL 训练约 **2.46 亿环境步**，完整运行应准备适合 RL 的计算资源；未核实最低显存与耗时。

<a id="adversarial-self-play"></a>

## 对抗式自博弈

先用 **OpenSpiel** 在 CPU 上观察最优响应和策略历史。研究语言模型游戏 RL 可选 **SPIRAL**；比较偏好博弈优化可选 **SPPO**。[Modern Agentic Systems §7.3](https://arxiv.org/html/2607.13104v1#S7.SS3) 直接讨论 SPIRAL；下列项目与 [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1) 的联系是本目录的学习延伸，不表示该综述直接点名了全部三个实现。SPPO 是相邻的偏好博弈案例，并非两个独立训练的 Agent。

<a id="open-spiel"></a>

### [OpenSpiel：Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel) — 经典自博弈

**相关自改进机制 · 自博弈前置。** 两个玩家学习 DQN 最优响应与基于 reservoir 的平均策略。观察平均策略的可利用度（面对最优响应可被利用多少），而不只看双方胜率。

**推荐入口。** 按[安装说明](https://github.com/google-deepmind/open_spiel/blob/master/docs/install.md)配置并取得示例；先在[表格型 fictitious play](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/fictitious_play_example.py)中设置 `--game=kuhn_poker`，再于仓库根目录运行 `python3 open_spiel/python/examples/nfsp_kuhn_pytorch.py --num_train_episodes=20000 --eval_every=1000`；对照 [NFSP 源码](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/nfsp_kuhn_pytorch.py)。

**语言与运行条件。** 英文；当前源码要求 **Python ≥3.11**，源码构建使用 CMake／C++ 编译器。NFSP 另需 PyTorch、`dm-tree`；默认 **CPU**，无需模型 API。上游默认 **300 万局**；命令中的 2 万局是本目录缩短的学习设置，不构成收敛证据。

<a id="spiral"></a>

### [SPIRAL](https://github.com/spiral-rl/spiral) — 多轮零和游戏 RL

**相关自改进机制。** 一个共享策略扮演双方，并从两方轨迹学习。观察按角色估计的优势、策略更新，以及新对手怎样改变后续经验。

**推荐入口。** 读[论文 §§4.1–4.3](https://arxiv.org/html/2506.24119v2#S4)，按 README 安装并检查 [run.sh](https://github.com/spiral-rl/spiral/blob/main/run.sh)，在仓库根目录运行 `bash run.sh`。沿角色轨迹 → OAT 优化 → vLLM 权重同步追踪。

**语言与运行条件。** 英文；Python **3.10**、CUDA、vLLM **0.8.4**、OAT **0.2.1** 与 Qwen3-4B-Base 权重。上游测试配置 **8× H100**，不是已核实的最低要求。配置 W&B 与默认 OpenRouter 评估，或修改相关设置（例如仅使用 random 对手）。训练生成游戏轨迹，数学评估还使用随仓库数据。使用这个原始本地入口；本次核验的 Tinker 启动器引用了缺失源码。

<a id="sppo"></a>

### [SPPO](https://github.com/uclaml/SPPO) — 偏好博弈自训练

**相关自改进机制。** 当前策略回答由固定 PairRM 评审比较，新 checkpoint 产生下一轮回答。对照 SPPO loss 与游戏 RL；评审器和学习规则保持固定。

**推荐入口。** 读[论文 §3.2、§§4.1–4.2](https://arxiv.org/html/2405.00675v5#S4)，按 README 安装并检查 [run_sppo_mistral.sh](https://github.com/uclaml/SPPO/blob/main/run_sppo_mistral.sh)。配置数据和上传后，在仓库根目录运行 `bash run_sppo_mistral.sh`，进入三轮流程。

**语言与运行条件。** 英文；**Python ≥3.10**、CUDA、vLLM、LLM-Blender / PairRM、Accelerate / DeepSpeed、Mistral 权重与 HF prompt 数据。脚本配置 **8 GPU／进程**，未给最低显存。核心训练无需付费 LLM API。数据阶段默认向 `UCLA-AGI` 上传私有 HF 数据集：应改成自己有权限的 namespace／token，或关闭这些调用；模型上传开关不会关闭数据上传。旧版／部分未锁定依赖未经过安装实测。

这些入口保持游戏规则或偏好评审器、训练流程固定，提供具体的自博弈学习循环；可用 [RL–RSI 导读](../README_zh.md#rl-and-rsi)辨认“改进器自身变化”还涉及哪些机制。

<a id="evaluation"></a>

## 评测

<a id="rsi-atlas"></a>

### [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI)

**评测工具 · 验收门控教学。** 图解改进循环、评估和修改准入，附小型 Python 示例，适合学习接受 / 拒绝候选修改与记录历史的代码结构。

**推荐入口。** [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python 门控示例](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py)。

**语言与运行条件。** 英文；示例使用 Python 3.10+ 标准库。接收外部传入的测试状态、收益和路径后作判断，不包含模型生成改动或自动执行评测。

<a id="textbook-baselines"></a>

### [Do Self-Improving Coding Agents Beat Textbook Baselines?](https://github.com/tejasvi/self-improving-agents-textbook-baselines) · [论文](https://aixiv.online/abs/2610.02812)

**评测工具 · 对照研究与结果重分析。** 将 DGM 移植实现与常规工程改进、单次重设计、空改动循环及计算量匹配的采样比较，并重新评测已发布的 DGM、ADAS Agent。学习区分搜索与选优的作用、基线质量、测试集迁移和资源预算。结论针对所测模型、任务与实现；更换模型后的评测不等于对原实验的完全复现。

**推荐入口。** 读固定版本的 [README](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/README.md) → [方法](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/paper/sec_methods_v2.tex) → [讨论](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/paper/sec_discussion_v2.tex) → [`replay.sh`](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/replay.sh)。在克隆的仓库中运行：

```bash
bash replay.sh
```

这会用已发布结果重新生成汇总、表格和图，不调用模型。解释总体分数前，先对比逐任务结果和 Agent 补丁。论文为 **aiXiv v2**；仓库标签 **v4** 指代码／数据归档，不是论文版本。aiXiv 与 arXiv 是不同平台。

**语言与运行条件。** 英文；离线重分析需要 Python 3、NumPy、SciPy 与 Matplotlib，无需 GPU 或模型 API。不同 Matplotlib 版本生成的图片字节可能不同。完整实验另需模型访问、外部 LiveCodeBench 数据、bubblewrap、上游要求的项目布局与 Agent 依赖；SWE-bench 部分需 Docker 和 swebench 2.1.0。归档没有提供完整 Agent 对话轨迹，三份依赖未公开日志的汇总以既有结果形式输入 replay。因此重分析核对的是发布结果，不会重新产生全部实验观测。

<a id="longmemeval-v2"></a>

### [LongMemEval-V2](https://github.com/xiaowu0162/LongMemEval-V2) · [论文](https://arxiv.org/abs/2605.12493)

**评测工具。** 检验保存的 Web／企业环境轨迹能否支持后续关于状态、工作流程和环境陷阱的问题。**451 道题**同时衡量答案准确率和记忆查询延迟，适合比较记忆组件；单凭分数不能认定形成了 RSI 闭环。

**推荐入口。** 先读[论文 §3.3](https://arxiv.org/html/2605.12493v1#S3.SS3)，按说明配置数据／模型端点，再对比[无检索](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_no_retrieval.sh)与 [RAG](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_rag_query_to_slice.sh)。从仓库根目录运行 `TIER=small bash evaluation/scripts/run_no_retrieval.sh --limit 5`，再以相同 limit 运行 RAG 脚本。这会选择**每个领域前 5 题**，仍需完成数据／索引准备。

**语言与运行条件。** 英文；Python ≥3.11、[公开 Apache-2.0 数据](https://huggingface.co/datasets/xiaowu0162/longmemeval-v2)（解压前约 **7.12 GB**）及模型端点。默认读者／RAG controller 为 Qwen3.5-9B；RAG 另需 Qwen3-Embedding-8B。部分题型调用付费 GPT-5.2 裁判。服务硬件取决于模型和上下文，未给最低显存。V2 评测会生成答案，没有单独导入预测文件评分的 CLI。

<a id="past-bench"></a>

### [PAST-Bench · Gen-Verse](https://github.com/Gen-Verse/PAST-Bench) · [论文](https://arxiv.org/abs/2608.04003)

**评测工具 · 跨会话改进。** 有序任务族在新会话中对照持久化开／关，结合轨迹和产物观察早期经验如何影响后续行为。学习区分偏好保留、流程复用、主动查找历史上下文与过期知识更新，为记忆组件评测补上纵向比较。

**推荐入口。** 按 [README 安装与 Smoke Test](https://github.com/Gen-Verse/PAST-Bench/blob/f8223517ae7491e776b69793d9f11e9d074ab42e/README.md)操作。安装 Hermes/Hermes+、构建 sandbox 镜像并配置 Agent／裁判 profile 后，运行一个偏好采纳任务族：

```bash
HERMES_PLUS_MECHANISMS=all past-bench evolve \
  --family memory_ability/SM01_preference_adoption \
  --agent hermes-plus --agent-profile minimax \
  --runtime local --sandbox --sandbox-tools \
  --compare-no-persistence --judge-model MiniMax-M2.7 \
  --trace-dir traces/smoke/hermes_plus_minimax_sm01
```

将 `sequence_comparison.json` 与逐任务结果、轨迹一起阅读；持久化对照有助于判断收益是否来自保留的经验，而不只看单题分数。

**语言与运行条件。** 英文；Python ≥3.11、uv、Docker、所选 Agent 集成，以及 Agent／裁判模型 API 访问。示例使用 `MINIMAX_API_KEY`，其他 profile 需相应配置。虽然上游称为 smoke test，它仍会真实调用模型。PAST-Bench 评估改进行为，不能仅凭名称认定被测 Agent 已递归改进其改进器。

<a id="scale-rsi-bench"></a>

### [Scale RSI Bench · scaleapi/rsi-benchmark](https://github.com/scaleapi/rsi-benchmark) · [官网](https://www.rsi-benchmark.com)

**评测工具 · AI 研发任务。** README 的四类公开样例覆盖自蒸馏、越狱鲁棒性、Agent swarm 优化与 nanoGPT 数据筛选。先学习研究任务如何规定可编辑产物、算力限制与验证方式；这些是任务样例，不能据此认定 Agent 已完成递归自改进循环。

**推荐入口。** 先读 [`samples/nano-gpt-data-curation/README.md`](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/samples/nano-gpt-data-curation/README.md)：为固定的 30M 参数模型筛选 12M token 子集，再通过训练与留出集困惑度验证。接着读该任务的 `instruction.md` 与 `task.toml`，最后按 [Running the Benchmark](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/README.md#running-the-benchmark) 使用 `harbor run`，填入该任务路径、Agent／模型参数与 Modal runtime。

**语言与运行条件。** 英文；Python ≥3.12、`pip install -e ".[runner]"`、Harbor、模型 API 访问与已配置的 Modal GPU sandbox。核验 README 中的任务需要 GPU，具体硬件与超时由各任务规定。只读任务合同无需算力服务。使用上面链接的 Scale 仓库／官网；`recursive-self-improvement-bench.com` 与 RSIBench-Data 是不同资源，任务数量也不同。
