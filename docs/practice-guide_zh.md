# 实践指南

[English](practice-guide.md) | **简体中文**

[返回资源目录](../README_zh.md) · [学习指南](learning-guide_zh.md) · [核验档案](verification_zh.md)

这里集中记录具体示例的学习目标、源码入口和运行条件。先按主题选择项目；综述章节与项目的对应关系见[学习指南](learning-guide_zh.md#survey-project-map)。条目的[三类标签](../README_zh.md#resource-scope)描述所推荐入口的范围，主题分组不表示 RSI 能力等级。

以下说明来自 **2026-10-22–25** 对上游文档与部分源码的核验，**未运行教程、调用模型或复现实验**；逐项范围见[核验档案](verification_zh.md#verification)。API 示例需要相应模型权限与调用预算，训练配置是上游示例而非本目录实测的最低硬件要求。

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

<a id="longmemeval-v2"></a>

### [LongMemEval-V2](https://github.com/xiaowu0162/LongMemEval-V2) · [论文](https://arxiv.org/abs/2605.12493)

**评测工具。** 检验保存的 Web／企业环境轨迹能否支持后续关于状态、工作流程和环境陷阱的问题。**451 道题**同时衡量答案准确率和记忆查询延迟，适合比较记忆组件；单凭分数不能认定形成了 RSI 闭环。

**推荐入口。** 先读[论文 §3.3](https://arxiv.org/html/2605.12493v1#S3.SS3)，按说明配置数据／模型端点，再对比[无检索](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_no_retrieval.sh)与 [RAG](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_rag_query_to_slice.sh)。从仓库根目录运行 `TIER=small bash evaluation/scripts/run_no_retrieval.sh --limit 5`，再以相同 limit 运行 RAG 脚本。这会选择**每个领域前 5 题**，仍需完成数据／索引准备。

**语言与运行条件。** 英文；Python ≥3.11、[公开 Apache-2.0 数据](https://huggingface.co/datasets/xiaowu0162/longmemeval-v2)（解压前约 **7.12 GB**）及模型端点。默认读者／RAG controller 为 Qwen3.5-9B；RAG 另需 Qwen3-Embedding-8B。部分题型调用付费 GPT-5.2 裁判。服务硬件取决于模型和上下文，未给最低显存。V2 评测会生成答案，没有单独导入预测文件评分的 CLI。
