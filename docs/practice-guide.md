# Practice Guide

**English** | [简体中文](practice-guide_zh.md)

[Back to the resource directory](../README.md) · [Learning guide](learning-guide.md) · [Verification records](verification.md)

This guide collects learning goals, source entry points, and running requirements for specific examples. Choose a project by topic; use the [learning guide](learning-guide.md#survey-project-map) to connect it to survey chapters. The [three resource labels](../README.md#resource-scope) describe the recommended entry point; topic groups are not RSI capability levels.

These notes come from upstream documentation and selected source reviews on **2026-10-22–29**. **No tutorials, model calls, or experiments were run.** See the [verification records](verification.md#verification) for each resource's review date and scope. API examples require model access and a call budget; training configurations are upstream examples, not minimum hardware requirements tested by this directory.

## Contents

- [Introductory Books, Notebooks, and Agent Building Blocks](#foundations)
- [Prompt Optimization](#prompt-optimization)
- [Program Search](#program-search)
- [Agent and Improver Code](#agent-code)
- [Harness Optimization](#harness-optimization)
- [Model Training](#model-training)
- [Memory and Skills](#memory-skills)
- [Co-Evolution](#coevolution-projects)
- [Adversarial Self-Play](#adversarial-self-play)
- [Evaluation](#evaluation)

<a id="foundations"></a>

## Introductory Books, Notebooks, and Agent Building Blocks

<a id="rsi-book"></a>

### [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi)

**Related self-improvement mechanism · introductory loop.** Uses one warehouse-inventory question-answering task to introduce tool use, deterministic evaluation, prompt improvement, memory across tasks, and cost tracking. A good first Python experiment.

**Recommended entry.** [Chapter 2: Build Your First Agent Improvement Loop](https://thersibook.com/chapters/ch02.html) + [companion notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb).

**Language and running requirements.** English; Python 3.10+, LiteLLM, a notebook environment, and access to a model endpoint. The example mainly updates prompts and memory while keeping model weights fixed. Its lesson list stays in the current kernel and is not saved across sessions.

<a id="rsi-learn"></a>

### [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn)

**Related self-improvement mechanism · prerequisite simulation.** A Chinese knowledge base, five-stage learning path, architecture diagrams, and evolutionary-search playground for building intuition about “generate–evaluate–select–integrate.”

**Recommended entry.** See the [navigation and setup instructions](https://github.com/Roloria/rsi-learn#页面导航), read the [learning-path content](https://github.com/Roloria/rsi-learn/blob/main/src/data/path.ts), then visit `/#/path` and `/#/lab` after starting the site locally.

**Language and running requirements.** Chinese; the interactive site requires Node.js / Vite. The playground is a **rule-based frontend simulation** and does not call a real LLM.

<a id="walkinglabs"></a>

### [WalkingLabs: Self-Improving Agent Notebooks](https://github.com/walkinglabs/self-improving-agent-notebook)

**Related self-improvement mechanism · prerequisite course.** Seventeen bilingual notebooks connect agent loops, verification, RL, code search, memory, and evaluation. A community reconstruction inspired by the Stanford CS329A syllabus, not official Stanford notebooks. L07 makes candidate agent-code generation, evaluation, archive selection, and regeneration easy to follow. The designer stays fixed; the multiplication environment assigns artificial error rates, and the archive remains in the current kernel.

**Recommended entry.** Start with [L01: Course Overview](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part1-foundation/01-course-overview.ipynb), then [L07: Open-Ended Evolution](https://github.com/walkinglabs/self-improving-agent-notebook/blob/main/notebooks/part2-training/07-open-ended-evolution.ipynb). [English notebooks](https://github.com/walkinglabs/self-improving-agent-notebook/tree/main/notebooks-en) follow the same course structure. Use L07 before ShinkaEvolve / DGM to learn how candidates and feedback enter an archive.

**Language and running requirements.** Chinese and English; Python 3.10+, repository dependencies, and a model endpoint configured through `AGENT_LLM_*`. Install Jupyter / ipykernel separately; the requirements file does not include them. L07 calls a model API but requires no GPU training. The upstream license is undetermined; no installation or lesson was run in this review.

<a id="rsi-labs"></a>

### [rsi_labs · weilinear](https://github.com/weilinear/rsi_labs)

**Recursive improvement method · teaching prototype.** A meal-cost example separates revising an answer, adding tools, and changing the instructions used to choose improvements. In §4, the improver proposes replacement instructions, accepts them when repair-selection accuracy improves on three labeled development cases, then uses them on three new cases. The initial policy is deliberately weak. This demonstrates one change to the improver; it does not execute the selected repairs for an end-to-end comparison or demonstrate gains across multiple recursive generations. State remains in the notebook session.

**Recommended entry.** Read the [author's walkthrough](https://blog.weili.me/posts/recursive-self-improvement-part-1-a-simple-toy-example), then [gemini_self_improvement.ipynb](https://github.com/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb), especially **§4: Improve how the agent chooses improvements**; [open in Colab](https://colab.research.google.com/github/weilinear/rsi_labs/blob/main/gemini_self_improvement.ipynb). Trace the accepted instructions into held-out repair selection. Later comparison notebooks in this repository use a fixed improver; this recommendation is for the named notebook.

**Language and running requirements.** English; Colab or local Jupyter, `google-genai==2.28.0`, and `GOOGLE_API_KEY`. Defaults to `gemini-3.8-flash`; override through `GEMINI_MODEL`. No training GPU. API access and a call budget are required; installation, endpoint compatibility, and notebook results were not runtime-tested here.

<a id="hello-agents"></a>

### [Datawhale Hello-Agents: Reflection and self-evolution](https://github.com/datawhalechina/hello-agents)

**Related self-improvement mechanism · reflection prerequisite.** A Chinese, code-led introduction to generating, critiquing, and revising a solution. The prime-number example makes the reflection loop easy to trace; an extra chapter maps four types of agent self-evolution.

**Recommended entry.** Read [Chapter 4, §4.4 Reflection](https://github.com/datawhalechina/hello-agents/blob/main/docs/chapter4/第四章%20智能体经典范式构建.md#44-reflection) alongside [Reflection.py](https://github.com/datawhalechina/hello-agents/blob/main/code/chapter4/Reflection.py), then read [Extra10: Agent Self-Evolution](https://github.com/datawhalechina/hello-agents/blob/main/Extra-Chapter/Extra10-Agent自进化.md).

**Language and running requirements.** Chinese; Python 3.10+, `openai`, `python-dotenv`, and an OpenAI-compatible model endpoint. The example improves task output through model feedback; it does not execute the generated code or train model weights.

<a id="learn-deepseek-harness"></a>

### [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness)

**Related self-improvement mechanism · engineering prerequisite.** Implements agent loops, plugins, persistent session logs, caching, compaction, memory, subagents, and runtime self-modification lesson by lesson. Each lesson is a standalone package for reading and modifying the code.

**Recommended entry.** [L1: The minimal agent loop](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → follow the [web course](https://prism-shadow.github.io/learn-deepseek-harness/) in order → [L10: Self-modification](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification).

**Language and running requirements.** Chinese and English; Node.js, TypeScript fundamentals, and the DeepSeek API. L10 demonstrates generating and registering temporary tools at runtime; it does not yet include a complete evolution loop with automated evaluation, promotion, and persistence.

<a id="hello-generic-agent"></a>

### [Datawhale Hello Generic Agent](https://github.com/datawhalechina/hello-generic-agent)

**Related self-improvement mechanism.** A Chinese tutorial on retaining experience as reusable SOPs and scripts, with a four-layer memory design. Useful for learning how task experience becomes discoverable knowledge for later sessions.

**Recommended entry.** [Chapter 4: Memory and Skills](https://datawhalechina.github.io/hello-generic-agent/part1/chapter4/) → [Chapter 12: Self-evolution](https://datawhalechina.github.io/hello-generic-agent/part2/chapter12/); for setup, use the implementation's [current Chinese installation guide](https://github.com/lsdefine/GenericAgent/blob/main/docs/installation_zh.md).

**Language and running requirements.** Chinese; tutorial remains in **Beta**. Python 3.11/3.12 recommended, model API access, and dependencies for the chosen UI/tools. Updates memory and skills; user guidance may be needed, and validation rules are prompt guidance rather than a fully automated promotion gate.

<a id="prompt-optimization"></a>

## Prompt Optimization

<a id="gepa"></a>

### [GEPA / DSPy official tutorials](https://github.com/gepa-ai/gepa)

**Related self-improvement mechanism.** Teaches reflective prompt evolution through a complete math example: baseline evaluation, textual feedback, candidate selection, and evaluation after optimization. Useful for learning how prompts improve while model weights stay fixed.

**Recommended entry.** Start with the [GEPA for AIME notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb), then read [GEPA optimization](https://dspy.ai/current/getting-started/gepa-optimization/) for split design and saving the optimized program.

**Language and running requirements.** English; Python 3.10–3.14, DSPy / GEPA, datasets, and an OpenAI API key for the example. MLflow tracing is optional.

<a id="textgrad"></a>

### [TextGrad official notebooks](https://github.com/zou-group/textgrad)

**Related self-improvement mechanism.** Introduces textual gradients with a PyTorch-style API, then optimizes a shared prompt on object-counting questions, evaluates it on validation data, and reverts updates that reduce validation performance. Useful for understanding feedback-driven text optimization.

**Recommended entry.** [Primitives](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Primitives.ipynb) → [Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb).

**Language and running requirements.** English; Python 3.9+, Jupyter / Colab, and an OpenAI API key. The notebooks use older model IDs; check compatible model availability before running. Updates prompt text rather than model weights.

<a id="program-search"></a>

## Program Search

<a id="shinkaevolve"></a>

### [ShinkaEvolve · SakanaAI](https://github.com/SakanaAI/ShinkaEvolve)

**Related self-improvement mechanism.** A guided notebook connects LLM code mutations, program populations, evaluators, and saved search histories. Circle packing provides a concrete task for learning program evolution and comparing parent-selection strategies.

**Recommended entry.** [Getting Started](https://sakanaai.github.io/ShinkaEvolve/getting_started/) → [interactive tutorial notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) → inspect the [circle-packing evaluator](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/circle_packing/evaluate.py).

**Language and running requirements.** English; Python 3.10+ (3.11 recommended), local Python or Colab, and model API credentials. The introductory example evolves a task program; its evaluator runs locally without a required training GPU.

<a id="openevolve"></a>

### [OpenEvolve](https://github.com/algorithmicsuperintelligence/openevolve)

**Related self-improvement mechanism.** An open-source AlphaEvolve-inspired program-search framework. The small function-minimization example shows how an initial search algorithm, evaluator feedback, configuration, and checkpoints fit together.

**Recommended entry.** Read [Installation & Setup](https://github.com/algorithmicsuperintelligence/openevolve#installation--setup), obtain the repository examples, then follow [Function Minimization](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization), reading `initial_program.py`, `evaluator.py`, and `config.yaml` together.

**Language and running requirements.** English; Python 3.10+, NumPy, and a model endpoint. The example defaults to Gemini through an OpenAI-compatible API; Docker is optional. This API example needs no training GPU. It optimizes task code rather than model weights.

<a id="agent-code"></a>

## Agent and Improver Code

Read [RSI Labs](#rsi-labs) → [STOP](#stop) → [SICA](#sica) → [DGM](#dgm), then compare meta-agent inheritance with [HyperAgents](#hyperagents). STOP and SICA source links are pinned to the commits reviewed on 2026-10-23; reading requires no model credentials.

<a id="dgm"></a>

### [Darwin Gödel Machine (DGM)](https://github.com/jennyzzt/dgm)

**Recursive improvement method · research implementation.** The original research implementation for studying agents that modify their own code, evaluate descendants on coding tasks, and retain an archive for further evolution. Best suited to readers ready to trace a complete research loop.

**Recommended entry.** Read [Setup / Running the DGM](https://github.com/jennyzzt/dgm#setup), then trace [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py).

**Language and running requirements.** English; Python, Docker, model API access, and SWE-bench / Polyglot environments and data. This is a research reproduction path with substantial environment and evaluation work, rather than a small introductory notebook.

<a id="stop"></a>

### [STOP · Self-Taught Optimizer](https://github.com/microsoft/stop) · [paper](https://arxiv.org/abs/2310.02304)

**Recursive improvement method · research implementation.** A Python improver edits its own implementation; the selected code becomes the executor for later self-improvement. Learn to distinguish improving a task solution from improving the function that generates solutions. The language model, scoring function, and outer loop remain fixed.

**Recommended entry.** [Seed improver](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_seed_algorithm.py#L3) → meta-utility → candidate selection → dynamic loading; follow the [STOP route](#stop-source-route).

<a id="stop-source-route"></a>

#### STOP: when the edited function becomes the next improver

1. **Identify the improver's contract.** Read [`improve_algorithm`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_seed_algorithm.py#L3-L23): it takes a program, a utility function, and a language model, then generates and scores candidates. The seed chooses among generated candidates; the unchanged input is not automatically included.
2. **Follow evaluation one level down.** Read the public [meta-utility interface](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/utility.py#L5), then [`get_improver` and the actual meta-utility](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/tasks/meta_optimization/secret_utility.py#L28-L112). A candidate is loaded as an improver and evaluated by having it improve a downstream task program. The default repeats the **same noisy-parity task / seed five times**, rather than testing five distinct tasks; selection uses validation utility.
3. **Find the recursive handoff.** In [`run_improver.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/run_improver.py#L122-L179), the current improver edits `algorithm_to_improve`, which is itself improver code. After acceptance, the code is saved to `results/<run_id>/improved_algorithm_<iteration>.py` and replaces the target. With the default `iterative=True`, it also replaces `improver_str`; [`temp_override`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/helpers.py#L154-L192) loads the new `improve_algorithm` used for the next edit. With `iterative=False`, the target changes but the executor stays at the seed implementation.
4. **Check what acceptance establishes.** The outer gate rejects exceptions or zero utility; it does **not** require beating the parent's score. The default six rounds save and load the final candidate, but do not execute a seventh self-edit with it. Use this route to locate executable inheritance, without assuming every round improves performance or the entire system recursively changes.

#### Running Entry and Requirements

English; Python, model API access, and an isolated execution environment. No local weight training. Legacy SDK / model configuration and missing dependency manifest require setup work.

 Start with [`config.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/config.py#L1) and [`language_model.py`](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/language_model.py#L10). The root entry is `python run_improver.py`; provide the `openai_key` dictionary in `api_key.py` as the source expects. The code uses the legacy `openai.ChatCompletion.create` interface and defaults to `gpt-4-0314`; adapt the SDK / accessible model before attempting a run. There is no dependency manifest; imports include `openai`, `pebble`, `multiprocess`, `numpy`, `jsonlines`, and `tqdm`. Nested candidate evaluation multiplies API work, so the language-model call limit is not a whole-experiment budget. Generated Python is executed: the supplied [reliability guard](https://github.com/microsoft/stop/blob/0d6780c54306b2486dd36e9c4ae9b49aceb27ea4/helpers.py#L80) is not a security sandbox; use an isolated environment.

<a id="sica"></a>

### [SICA · Self-Improving Coding Agent](https://github.com/MaximeRobeyns/self_improving_coding_agent) · [paper](https://arxiv.org/abs/2504.15228)

**Recursive improvement method · research implementation.** A selected archived agent uses its own code and tools to modify a successor. Learn how benchmark feedback and archive selection determine which implementation later acts as the improver. The editable parent and executing improver can differ; the external evaluation / selection framework remains fixed and model weights are not trained.

**Recommended entry.** [Runner loop](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L1022-L1049) → parent / improver selection → archived-module execution → improvement tools → next evaluation; follow the [SICA route](#sica-source-route).

<a id="sica-source-route"></a>

#### SICA: when a selected descendant becomes a later editor

1. **Draw the outer loop.** Start at [`runner.main`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L1022-L1049): evaluate `agent_i` → record scores and traces → generate `agent_{i+1}` → evaluate that successor in the next iteration. Creating a successor does not make it the best agent.
2. **Separate the parent from the improver.** [`select_base_agent`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L87-L145) chooses a recent parent meeting the best iteration's lower-confidence score threshold; [its code is copied into the successor workdir](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L769-L785). Separately, [`get_best_agent_iteration`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/utils/archive_analysis.py#L291-L308) chooses the highest mean benchmark score as the executing improver. These two selections need not identify the same version.
3. **Trace the inherited implementation into execution.** The [Docker mounts and command](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L823-L869) expose the archive read-only and the successor workdir read-write, then run `python -m archive.agent_{best_iter}.agent_code improve`. Follow the [relative `Agent` import](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/__main__.py#L17) and [relative implementation imports](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/agent.py#L17-L26): the selected version's code actually performs the improvement job.
4. **Read the improvement workflow.** Follow [`improve_agent`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/__main__.py#L113-L214) → [`MetaImprovementReasoningStructure`](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/tools/reasoning_structures/meta_improvement.py#L18-L85) → [tool registration](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/agents/implementations/main_orchestrator.py#L77-L95). Inspect how archive feedback informs proposals, coding, requested tests, and the change log. These tools and instructions are part of the inherited agent code.
5. **Close the loop with benchmark evidence.** Read [candidate execution](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L469-L475) and [score persistence](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L531-L552). Once evaluated and selected, a descendant's implementation can become a later improver. A successful editing process is not itself a task-performance gain; the external runner and scoring / selection rules govern promotion.

#### Running Entry and Requirements

English; Python, Docker / buildx, benchmark downloads, and API access matching the model configuration. Advanced engineering route with Docker and repeated benchmark evaluation; no local training GPU specified for the API route.

 Follow the pinned [Quickstart](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/README.md#quickstart) and [Makefile](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/Makefile). In the repository root, prepare a Python environment with `pip install -r base_agent/requirements.txt` and `pip install swebench`. Configure [agent models](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/config.py#L12-L19) and the runner's [summary-model calls](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L326-L338): defaults involve Sonnet 3.7, o3-mini, and Gemini 2.0 Flash, so one arbitrary provider key is insufficient. Align both locations with accessible models and export the corresponding provider environment variables in the host shell **before** building the Docker image with `make image` (`make image-mac` on Apple Silicon). The supplied build embeds API credentials in the image environment; rebuild after credential changes and keep those images private.

Read `python runner.py --help` before launching. A bounded starting configuration is `python runner.py --workers 1 --iterations 2`, after the above setup. The [parser](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L48-L65) uses `--experiment-id` / `-id` for an existing experiment, rather than the README's `--id`. The default [benchmark registry](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/base_agent/src/benchmarks/__init__.py#L31-L53) activates GSM8K; the [queue](https://github.com/MaximeRobeyns/self_improving_coding_agent/blob/ed8275dca4d3c5dbf77229964351fe9b424797dc/runner.py#L648-L699) selects **18 questions per benchmark**, regardless of worker count. Two iterations evaluate agents 0 and 1 and leave the generated agent 2 for a subsequent evaluation. Worker / iteration limits are not a total spending cap: meta-improvement has no configured whole-run API budget. Treat this as a research run requiring data, Docker resources, and paid model calls, rather than an offline exercise.

<a id="hyperagents"></a>

### [HyperAgents · Meta and collaborators](https://github.com/facebookresearch/HyperAgents) · [paper](https://arxiv.org/abs/2603.19461)

**Recursive improvement method · editable meta-agent.** A task agent and its modifying meta-agent are both editable. The selected parent's patches are applied before its meta-agent generates another candidate. Learn how changes to the improvement procedure propagate across generations, while external domain evaluation remains fixed.

**Recommended entry.** Read [the paper's framework and DGM-H implementation](https://arxiv.org/html/2603.19461v1) → [Setup](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/README.md#setup) → [`generate_loop.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/generate_loop.py) → [`run_meta_agent.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/run_meta_agent.py) → [`meta_agent.py`](https://github.com/facebookresearch/HyperAgents/blob/59a68f672dfb92c74aeb7e61535d776fb36e172d/meta_agent.py). Follow the inherited patch into execution, then inspect the next candidate's scores.

**Language and running requirements.** English; Python **3.12**, Docker, build dependencies, model APIs, and domain data. `bash ./setup_initial.sh` prepares the default paper-review route; then `python generate_loop.py --domains paper_review --max_generation 1 --eval_workers 1` bounds generations / concurrency, not all evaluation work. Adapt the Docker build helper's internal proxy settings. Public research code under **CC BY-NC-SA 4.0**.

<a id="dream-rsi"></a>

### [Dream-RSI · Google Research](https://github.com/google-research/dream-rsi) · [paper](https://arxiv.org/abs/2609.14858)

**Recursive improvement method · exploration-policy code.** Online exploration builds a discovery tree; offline replay compares rewritten policies that allocate the search budget. The selected policy is saved as `policy/method.py` and directs the next online round. Learn how changing the search policy changes later improvement attempts while the coding agent, task, and evaluator stay fixed. Selection may retain the incumbent policy.

**Recommended entry.** Read [Quick start](https://github.com/google-research/dream-rsi/blob/8ec35bd2538220517ce1bfca4282db21b8c518db/README.md#quick-start), then trace explore → learn → promote in [`orchestrate.py`](https://github.com/google-research/dream-rsi/blob/8ec35bd2538220517ce1bfca4282db21b8c518db/dream_rsi/orchestrate.py#L439-L479). After setup, check the circle-packing configuration before trying the upstream short run:

```bash
DRY_RUN=1 bash scripts/run_dream_rsi.sh circle_packing_26
WORKSPACE=workspace/smoke ROUNDS=2 BRANCHES=3 REFINE=1 MAX_WORKERS=3 \
  bash scripts/run_dream_rsi.sh circle_packing_26
```

**Language and running requirements.** English; Python ≥3.10, editable task-dependency installation, Gemini CLI/API access, and downloaded Math/Lasso task files. The dry run still checks task files, dependencies, the agent, and API keys; the second command makes real model calls. Lasso additionally needs `g++` / Eigen; KernelBench needs a GPU evaluation server. The published package omits the paper's harness-optimization experiment and Current History Only ablation.

<a id="verse"></a>

### [VERSE · Verified Self-Evolving Optimizer](https://github.com/wzekai/VERSE) · [paper](https://arxiv.org/abs/2610.02616)

**Recursive improvement method · optimizer-harness inheritance.** VERSE uses execution feedback to improve both an executor harness and the optimizer's own prompts, skills, tools, hooks and notes. Trace how the updated optimizer participates in the next round while model weights, evaluation splits and selection rules remain fixed.

**Recommended entry.** Read [paper §§2.1–2.3 → §3.1](https://arxiv.org/html/2610.02616v1) → [`verse_mh.yaml`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/configs/self_teacher/verse_mh.yaml) → [`driver.py`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/evolution/driver.py) → [`meta_teacher.py`](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/verse/evolution/meta_teacher.py). Follow `end_round()`: the meta-episode uses current tools to edit persistent `teacher_ws/`; edits that pass structural checks are committed, and the next `begin_round()` reloads the optimizer's equipment. Health checks govern executable hooks; they are distinct from measuring improvement quality.

For a CPU-only first step, run `python results/make_table.py` from the cloned repository to recompute the published table from [released outcomes](https://github.com/wzekai/VERSE/tree/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/results). This uses Python's standard library and makes no model calls. After [installation, data preparation and model serving](https://github.com/wzekai/VERSE/blob/d8ff0adab0cf82e13d7878f84ff84f823cb2f6c9/README.md), the actual evolution entry is:

```bash
CONFIG=self_teacher/verse_mh TAG=-r1 bash scripts/run_swe.sh
```

**Language and running requirements.** English; full runs require Python ≥3.12, Docker, separately prepared task data and model serving. The reference vLLM setup uses **4 GPUs for the optimizer and 1 for the executor**, not a verified minimum. The launcher defaults to six evolution rounds and 24 concurrent tasks, followed by three-repeat test evaluations; budget accordingly. Inspect `rounds.jsonl`, optimizer workspaces and `test110.json` to connect inherited changes with held-out outcomes. Recomputing released numbers is separate from rerunning these experiments.

<a id="harness-optimization"></a>

## Harness Optimization

<a id="harness2"></a>

### [Harness² · Google Cloud AI Research / Northwestern](https://github.com/google-research/harness2) · [paper](https://arxiv.org/abs/2610.14224)

**Recursive improvement method · improver experience library.** Propose, probe, and compose changes for the current task, then retain adopted harnesses and supported lessons for later improvement sessions. Learn how task-level adaptation connects to cross-task improvement experience. Model weights, stage instructions, and the decision rule stay fixed.

**Recommended entry.** Read [§2 and Figure 3](https://arxiv.org/html/2610.14224v1#S2) → [Install](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/README.md#install) → run the demo:

```bash
harness2-demo --output runs/demo --k 2
```

Inspect `demo.json`, `INDEX.md`, and `EXPERIENCE.md`; trace [library context and adoption](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/schedule.py#L499-L563) into subsequent tasks.

**Language and running requirements.** English; Python **3.12/3.13**, uv. The demo uses scripted editors and real Python execution, with no model credentials or Docker. Model-backed runs require Linux, Node.js 20+, model access, and benchmark dependencies; use the [Setup guide](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/docs/SETUP.md). The reviewed commit lacks the referenced `.env.example`, so set the documented variables manually.

**Harness²: follow the retained state.** Each new task starts from a common base execution harness; earlier adopted harnesses and lessons are available to the improver for selective reuse. Compare [library persistence](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/library.py#L106-L151) with [the context supplied to the improver](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/core/context.py#L161-L164). The demo's [scripted proposer](https://github.com/google-research/harness2/blob/1cfe254e8d25b15f37048c3730134686abe60335/harness2/demo.py#L120-L163) demonstrates the plumbing but does not learn its edits from that library. For real runs, the default route uses Google Cloud / Vertex AI credentials; LAB additionally needs Pandoc / Poppler, and WorkBuddy-Bench needs Docker.

<a id="hermit"></a>

### [Hermit · CMU InfiniAI Lab](https://github.com/Infini-AI-Lab/hermit)

**Related self-improvement mechanism · external adapter training.** Hermit keeps the model and original harness fixed while evolving a separate adapter containing instructions, skills, memory or tool code. The Trainer records feedback, checks file structure and versions adapters; an Evolver supplies the update method. Recursive behavior depends on the selected method, rather than the framework name.

**Recommended entry.** Follow the [offline walkthrough](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/get-started/quickstart.md) → [Trainer](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/framework/trainer.md) → [Evolver](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/framework/evolver.md). With Python **3.12+** and Git, install this pinned source revision in a virtual environment:

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

Inspect the generated `ADAPTER.md` and evaluation summaries. The scripted learner writes an uppercase-output rule from predefined feedback; the constructed score gain demonstrates the training contract, not real-model improvement. This trusted local example disables the learner sandbox and needs no credentials, GPU or external data.

**Language and running requirements.** English. The [first real-model tutorial](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/get-started/first-model.md) uses nine included sentiment tasks (three each for training, validation and testing), a chat-completions API and `python -m pip install -e . --group gepa`; dependency groups require **pip ≥25.1**. Keep the pinned checkout's dependencies and examples together; its layout and Python requirement differ from the initial PyPI 0.1.0 release. [OfficeQA](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/recipes/officeqa.md) adds dataset access and model configuration; sandboxed learner programs need Linux / bubblewrap, and its Codex acting route adds Docker / npm.

Specification validity does not establish a score gain; compare no-adapter, root and final on the same test split. The Evolver selects `final`, which is not universally the highest-scoring checkpoint. [Deployment and conversion](https://github.com/Infini-AI-Lab/hermit/blob/2056e435d4be138358872208c3b233890cecf74c/docs/tutorials/deploy-an-adapter.md) generate host workspaces or supported plugin files; they do not start Codex / Claude Code or run training.

<a id="meta-harness"></a>

### [Meta-Harness · Stanford IRIS and collaborators](https://github.com/stanford-iris-lab/meta-harness) · [paper](https://arxiv.org/abs/2603.28052)

**Related self-improvement mechanism · external harness search.** A coding-agent proposer reads earlier candidates' source, scores, and raw traces, then edits task-specific harness code. Learn how feedback supports changes to memory, retrieval, and orchestration; the proposer and search driver are not evolved. The framework and its [Terminal-Bench artifact](https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact) are grouped here.

**Recommended entry.** Start with the [text-classification example](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/reference_examples/text_classification/README.md):

```bash
cd reference_examples/text_classification
uv sync
uv run python meta_harness.py --iterations 1
```
 Read [`meta_harness.py`](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/reference_examples/text_classification/meta_harness.py) → `benchmark.py` → `inner_loop.py`; optional Chinese preparation: [RSI Research Notes, Report 13 §4](https://github.com/asimfish/awesome_rsi/blob/63f83e581ff3161932b62ab5fbe845fdf03cf84b/reports/13_meta_harness.md).

**Language and running requirements.** English code / docs; Python **≥3.11**, uv, an authenticated Claude Code CLI proposer, and task-model access. The example defaults to OpenRouter; its wrapper removes `ANTHROPIC_API_KEY` from the proposer environment. Data are bundled; one iteration still evaluates multiple candidates / datasets. API route needs no training GPU. Read [ONBOARDING](https://github.com/stanford-iris-lab/meta-harness/blob/8123ccabe2b19fa1123090b2e5f1bacc20963ce8/ONBOARDING.md) before adapting to another domain.

<a id="aho"></a>

### [Agent Harness Optimizer (AHO) · Airbnb](https://github.com/airbnb/agent-harness-optimizer) · [paper](https://arxiv.org/abs/2609.05736)

**Related self-improvement mechanism · prompt and middleware optimization.** BetterHarness, PRISM, GEPA, and MIPROv2 search changes around a fixed model. Learn to distinguish instruction failures from tool-boundary failures, then connect evaluation, acceptance, and saved diffs. The optimizer itself remains fixed.

**Recommended entry.** Read [paper §3](https://arxiv.org/html/2609.05736v2#S3) and [§4.3](https://arxiv.org/html/2609.05736v2#S4.SS3) → [Quick Start](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/README.md#quick-start) → [BFCL data setup](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/data/bfcl/README.md). Follow the [BetterHarness loop](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/agent_harness_optimizer/optimizers/better_harness/loop.py) into `decision.json`, `report.json`, and `final_diff.md`; then compare PRISM.

**Language and running requirements.** English; Python **≥3.12**, source install (`pip install -e .`), inner / outer model APIs, and separately downloaded BFCL v4 cases plus answer files. Root CLI: `python -m agent_harness_optimizer.cli`, with the required benchmark / optimizer / model / output arguments from Quick Start. Limit cases and iterations for learning; no training GPU for the API route.

**AHO: separate selection from final evaluation.** Its `train` / `holdout` splits act as repair / validation data; repeatedly consulting the gate is not untouched final testing. In the audited BetterHarness path, `--split-seed` also enables a **full 600-case BFCL scorecard**, even with small train / holdout counts. Use `--train-cases`, `--holdout-cases`, and `--max-iterations` deliberately. The [actual default acceptance rule](https://github.com/airbnb/agent-harness-optimizer/blob/0d7652b42296c8df07532fa3787fc956250741e7/agent_harness_optimizer/framework/acceptance.py#L58-L82) requires strictly more passed gate cases; the README's older error-rate / cost fallback pseudocode does not describe this default. Per-case time / token limits are not a whole-run spending cap.

<a id="beagle"></a>

### [Beagle / DarwinX · Salesforce AI Research](https://github.com/SalesforceAIResearch/Beagle)

**Related self-improvement mechanism · harness-evolution framework.** DarwinX evaluates a baseline, asks an evolver to edit an evolvee harness, checks candidates, and records surviving versions and their genealogy. Study the distinction between the editable harness, the proposing agent, and the fixed selection algorithm. The documented entry evolves the harness; it does not establish that the evolver itself evolves.

**Recommended entry.** Follow [Quick Start](https://github.com/SalesforceAIResearch/Beagle/blob/73e112f892aefe6226e4ee7723f23ae849eeb13f/README.md#quick-start) → [evolution example](https://github.com/SalesforceAIResearch/Beagle/blob/73e112f892aefe6226e4ee7723f23ae849eeb13f/examples/evolution/README.md). After preparing the benchmark cache, harness checkout, and generated configuration, preview the two-task experiment:

```bash
.venv/bin/beagle evolve \
  --config tests/smoke/terminal_bench_2_1/opencode-1.18.16_darwinx_evolution_smoke2.yaml \
  --dry-run
```

Inspect `evolvee`, `evolver`, and `algorithm` in the YAML, then trace real-run artifacts to `state.db`, candidate evidence, and proposal/evaluation logs. The dry run resolves the plan without model calls or containers; it does not validate credentials or the local checkout.

**Language and running requirements.** English; Python ≥3.12, uv, Docker, benchmark data, an onboarded harness repository, and model access. The current public evolver integration uses an installed, authenticated Cursor Agent. Onboarding creates experiment repositories under your GitHub account; real evolution uses model credits and pushes kept candidates to those copies. Use an experiment repository you control. The small example checks the pipeline, not benchmark performance.

<a id="harnesspro"></a>

### [HarnessPro](https://github.com/pzs19/HarnessPro) · [paper](https://arxiv.org/abs/2610.26770)

**Related self-improvement mechanism · performance–cost trade-offs.** The paper uses trajectory diagnosis, harness edits, generated tests, and Pareto selection to retain Lite / Medium / Heavy lineages for subsequent rounds. The proposal and selection framework stays fixed. The public package provides nine selected harnesses for Terminal-Bench 2, SWE-bench Pro, and ProgramBench, plus evaluation runners; the practical entry is to inspect and compare these artifacts, not to rerun the full evolution procedure.

**Recommended entry.** Read [paper §§3–4](https://arxiv.org/html/2610.26770v2#S3) for the objective and selection loop → [evaluation guide](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/docs/evaluation.md) → compare `runtime/policy.json` under [the three TB2 modes](https://github.com/pzs19/HarnessPro/tree/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/harnesses/terminal-bench-2) → [Medium hook](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/harnesses/terminal-bench-2/medium/runtime/hook.py) → [TB2 runner](https://github.com/pzs19/HarnessPro/blob/8ae622eb4a4923dbb4b515be7ded614f88fd4f38/scripts/run_tb2_harness_eval.py). Trace profile selection, reasoning effort, tool budgets, and output compaction. For example, the modes' `standard` profiles set tool ceilings of 38 / 44 / 60; the hook rejects calls beyond the configured ceiling.

After following the upstream setup, run from its repository root. Set `TB2_TASKS` to the prepared dataset directory, `CODEX_CONFIG` to the Codex Responses-provider TOML, and `CODEX_BIN` to the Codex executable:

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

The runner validates the full held-out manifest against the dataset's validation split before selecting one task; a directory containing one arbitrary task is insufficient. Start with this pipeline check, then compare modes on the same task set and model, using a fresh `--run-dir` and matching `--harness-label` / `--harness-dir` each time. Record both pass rate and cost; a one-task run does not establish a Pareto frontier.

**Language and running requirements.** English; Linux, Python 3.12/3.13, uv, Docker + Compose, Codex CLI (upstream used 0.147.0), a Responses-compatible endpoint with model access and credentials, and separately obtained TB2 data and task / grader images. The command makes real model calls; this entry uses API-backed evaluation rather than parameter training. The bundled RTK helper targets Linux x86-64; other architectures need a compatible `--rtk-binary`. Code is MIT; bundled evaluators retain their own licenses. The release omits the paper's GLM-5.2 evolved harness snapshots.

<a id="harnessmm"></a>

### [HarnessMM](https://github.com/YuhuaJiang2002/HarnessMM) · [paper](https://arxiv.org/abs/2610.32813)

**Related self-improvement mechanism · decision reuse and token accounting.** An Executable Decision Graph stores literal actions already resolved by the actor. Observed tool receipts activate eligible actions, which replace registered reasoning callbacks; new decisions return to the actor. Separate companion optimization revises prompts, context settings and adapter rules from training feedback, selects on validation, and freezes the configuration before testing. Actor weights and the update procedure stay fixed.

**Recommended entry.** Read [paper §4](https://arxiv.org/html/2610.32813v1#S4) → [local example](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/examples/guarded_reuse.mjs) → [`ExecutableSubdag.stream` / `observeTool`](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/integrations/deepseek_harness/sar_v2.mjs#L206) → [integration guide](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/docs/INTEGRATION.md). After cloning the upstream repository, run from its root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -e '.[dev,analysis]'
node examples/guarded_reuse.mjs
python examples/partition.py
```

The first example uses three predefined actions, synthetic receipts and an in-memory dispatcher. Its assertions check three substitution certificates and a return to the slow callback after graph exhaustion; no model or shell command is executed. The partition example only divides ten synthetic tasks into 20% training, 20% validation and 60% test. These teach the mechanism and data split, not autonomous evolution or measured token savings.

For the improvement lifecycle, read the [`CodexChiselController` contract](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/phiagent/harness/codex_chisel.py#L1): `train` → `select_validation` → `freeze` → `evaluate_test`. Connect real executor/optimizer callbacks only after preparing a new experiment configuration. Compare complete-task quality and input-plus-output tokens, including retries and fallback; account for development and selection costs separately when evaluating all-in improvement.

**Language and running requirements.** English; Python **3.10–3.14**, Node.js **22+**. Both local examples require no model credentials or GPU. Full experiments need the selected upstream harness, benchmark data/native scorer, model access or serving, and benchmark-specific execution environments; coding evaluation needs an isolated verifier. The [reproduction guide](https://github.com/YuhuaJiang2002/HarnessMM/blob/9c2ed7b38aec25b137106c7d1276ed589efb0661/docs/REPRODUCIBILITY.md) explains deployment placeholders and source/configuration freezes. Reference configurations are historical protocols, not ready-to-launch jobs. Code is Apache-2.0; external components retain their own terms.

<a id="elicitation-or-expansion"></a>

### [Elicitation or Expansion?](https://github.com/furiosa-ai/elicitation-or-expansion) · [paper](https://arxiv.org/abs/2610.27889)

**Related self-improvement mechanism · harness search and gain diagnosis.** The study compares a base harness with validation-selected Meta-Harness candidates while keeping solver weights fixed. Learn to distinguish more frequent success from broader observed task coverage: inspect pass@k curves, task difficulty, and stronger-model / higher-compute references. Finite-attempt coverage describes the tested setting, not an intrinsic capability ceiling. The public code runs harness optimization; repeated-sampling analysis from the paper is a separate experimental step.

**Recommended entry.** Read [paper §§3.1–3.2 and §§5.1–5.3](https://arxiv.org/html/2610.27889v1#S3) → compare the [HotpotQA configuration](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/configs/hotpotqa-8b.yaml) with its released candidates in [harnesses/hotpotqa](https://github.com/furiosa-ai/elicitation-or-expansion/tree/aa5de8564688c63640b22e42374a7df6cc41ed2d/harnesses/hotpotqa) → trace [the search loop and finalization](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/core/meta_harness.py). This configuration limits each task to four solver calls, two retrievals, and at most seven passages per retrieval; the separate relaxed configuration uses different limits.

After completing the upstream [setup](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/README.md#hotpotqa-and-appworld) and [data instructions](https://github.com/furiosa-ai/elicitation-or-expansion/blob/aa5de8564688c63640b22e42374a7df6cc41ed2d/agentic/data/hotpotqa/DATA.md), run from `agentic/`:

```bash
scripts/run_one.sh configs/hotpotqa-8b.yaml
```

The launcher runs in the background. Follow `runs/hotpotqa-8b-seed0/run.log` until optimization finishes, then run `scripts/finalize.sh hotpotqa-8b-seed0`. Inspect `results/selection.json`, `results/test_table.txt`, and `results/finalized.json` under that run; the last file records `complete` or `incomplete`. Candidates are selected on a separate selection split, then scored on held-out tests. These results do not by themselves reproduce the paper's pass@k curves. For those comparisons, preserve the task set and scorer, distinguish attempt count from per-attempt resource limits, and track execution cost alongside coverage.

**Language and running requirements.** English; Linux launch scripts use `setsid`, and the agentic package requires Python 3.12, uv and Docker. Provide Claude Code OAuth access to the configured proposer model, a matching CLI version in the proposer image (host CLI or `PREFLIGHT_CLAUDE_VERSION`), and an OpenAI-compatible solver service. The HotpotQA example serves Qwen3-8B and a BM25 retriever; both must be reachable from Docker. Obtain HotpotQA questions and Wikipedia abstracts separately; upstream estimates about 10 GB RAM to build the index. GPU requirements depend on how the solver is hosted. Runs make real model calls. MIT code; dependencies and datasets retain their own terms. AppWorld candidate snapshots are excluded from the release, although its optimization framework is included.

<a id="gepa-curator"></a>

### [GEPA-Curator: Curated Learning for Self Improving Agents](https://arxiv.org/abs/2610.37651)

**Related self-improvement mechanism · feedback selection.** A Curator selects informative tasks and retrieves trustworthy successful trajectories for prompt optimization. Learn to distinguish prompt weaknesses from environment failures or noisy evaluation; the curation procedure remains fixed.

**Recommended entry.** Read [§3 → §5.3 → Appendix B.2](https://arxiv.org/html/2610.37651v1): task selection and success retrieval → extension to Meta-Harness → Curator prompts. Pair this reading with [GEPA](#gepa) and [Meta-Harness](#meta-harness).

**Language and running requirements.** English; reading needs agent and prompt-optimization fundamentals, without an API or GPU. No dedicated official implementation was confirmed at the [review date](verification.md#verification-2026-10-29); this is a paper-reading entry, with no verified reproduction command.

<a id="model-training"></a>

## Model Training

<a id="seal"></a>

### [SEAL · Self-Adapting Language Models](https://github.com/Continual-Intelligence/SEAL)

**Related self-improvement mechanism · learned self-edit generation.** The authors' implementation learns to generate self-edits, tests temporary LoRA updates on downstream questions, then uses selected edits to train the edit generator. Useful for studying the inner adaptation / outer learning loop.

**Recommended entry.** Start with the [general-knowledge pipeline](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md): data generation → TTT server → evaluation → ReST-EM training; then inspect the [SFT-data builder](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/src/EM/build_SFT_dataset.py).

**Language and running requirements.** English; advanced Python / fine-tuning background, Python 3.12, Linux / CUDA, PyTorch / vLLM / PEFT, and model / data access. Upstream documents 2 A100/H100 GPUs; adapt SLURM scripts and paths. Default TTT grading uses the OpenAI API (GPT-4.1); generation / proxy scoring can use it too.

<a id="agent-lightning"></a>

### [Microsoft Agent Lightning v1.0](https://github.com/microsoft/agent-lightning)

**Related self-improvement mechanism.** Calc-X connects an AutoGen agent and MCP calculator to rollout collection, answer-based rewards, and GRPO updates. A concrete entry into learning from tool-using trajectories and saving policy checkpoints.

**Recommended entry.** Follow [Installation](https://github.com/microsoft/agent-lightning/blob/main/docs/00-installation.md), then [Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode); launch from `examples/calc_x` as that example specifies.

**Language and running requirements.** English; Python 3.12+, Linux / WSL, NVIDIA CUDA, the repository's matching `verl` / vLLM setup, model / dataset downloads, and W&B by default. Local Mode runs the model locally without Kubernetes. The documented Calc-X setup uses **1 A100 80GB**. This is the v1.0 training path; older APO tutorials target the legacy API.

<a id="mass"></a>

### [MASS · Sakana AI](https://github.com/SakanaAI/mass) · [paper](https://arxiv.org/abs/2610.12176)

**Recursive improvement method · shared-model updates.** The current model acts as workflow executor, optimizer, and in-loop evaluator. Search and trajectory selection produce supervision; SFT and export produce the model used in all three roles in the next cycle. Learn to follow that handoff from `L0` to `L1` to `L2`.

**Recommended entry.** From the cloned repository, preview the pipeline without a GPU or model server:

```bash
python3 -m mass plan --config configs/paper.json
```

Then follow [Try one task](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/docs/running.md#try-one-task), which makes a one-update local configuration before `search --tasks 51`. Read the [paper-to-code map](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/docs/paper_to_code.md) and [`configs/cycle2.json`](https://github.com/SakanaAI/mass/blob/fb403581bed2c974b3f99e7236224169da643079/configs/cycle2.json) to connect search → collect → rank → select → render → train → export to the next cycle. `plan` only prints the configuration and training command.

**Language and running requirements.** English; actual experiments require Linux, Python 3.12, Node.js 22, uv, vLLM, model weights, and GPU resources. The first-cycle paper SFT example used **6×H100 for about 19 hours**, excluding search and trajectory collection. Synthetic tasks execute generated commands on the host, so use an isolated research environment. The packaged MLR configuration covers an earlier **12-task subset**; the full 107-task configuration and several benchmark adapters are absent. The repository also documents differences between its RHI reference/champion logic and paper Algorithm 1.

<a id="self-hpo"></a>

### [Self-HPO · MSR Orchard](https://github.com/MSR-Orchard/Self-HPO) · [paper](https://arxiv.org/abs/2610.22791)

**Recursive improvement method · harness–policy alternation.** In the H-step, the current policy analyzes failures and proposes harness revisions. The P-step trains that policy with RL under the selected harness; the exported policy proposes revisions in the next H-step. Trace both inherited objects—the harness and the model—and how previously unsolved tasks form the next search set.

**Recommended entry.** Read [Running Self-HPO](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/README.md#running-self-hpo) → [`scripts/h_step/proposer.sh`](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/scripts/h_step/proposer.sh) → [`scripts/p_step/run_p_step.sh`](https://github.com/MSR-Orchard/Self-HPO/blob/3c3d0bd93a8a5a72399c855783460b141ea27d49/scripts/p_step/run_p_step.sh), then follow `export_policy.sh` back to serving `work/p_step_<round>/policy`. Compare the published `harnesses/seed` and `harnesses/self-hpo` before preparing a training run. Default `PROPOSER=self` uses the current policy; `PROPOSER=api` selects the separate fixed-external-proposer HPO setting.

**Language and running requirements.** English; Python 3.12, uv, SGLang, Docker/slime, benchmark data, model weights, and the configured Orchard Agentic sandbox endpoint/key. Upstream training and evaluation use **8×B200**; this is a source-reading and research-reproduction route, not a small local tutorial. H-step model serving, candidate evaluation, and P-step RL must all be configured before a complete cycle can run.

<a id="memory-skills"></a>

## Memory and Skills

<a id="ace"></a>

### [ACE: Agentic Context Engineering](https://github.com/ace-agent/ace)

**Related self-improvement mechanism.** The authors' Generator–Reflector–Curator implementation turns feedback into a reusable text playbook. Trace labeled examples, helpful / harmful counters, incremental additions, validation-based selection, and later reuse. The default sequential implementation inserts the whole playbook into the prompt.

**Recommended entry.** Read [paper §3](https://arxiv.org/html/2510.04618v3#S3), then the [finance CLI](https://github.com/ace-agent/ace/blob/main/eval/finance/run.py). From the repo root, run `uv sync`, configure `.env` / provider models, then `uv run python -m eval.finance.run --task_name formula --mode offline --save_path results --test_workers 1`. Reload the saved `best_playbook.txt` with `--mode eval_only --initial_playbook_path ...`.

**Language and running requirements.** English; Python ≥3.10, uv, model API; no training GPU for this route. Defaults use SambaNova / DeepSeek-V3.1. By default, Formula processes its full **500/300/200** train / validation / test splits with repeated API calls; `--test_workers 1` limits concurrency, not sample count. To reduce a run, configure smaller separate splits in `eval/finance/data/sample_config.json` and set `--eval_steps` to a positive value no greater than the training-sample count, so validation can select a playbook. Current default operations update counters and **add** entries; optional embedding deduplication is off.

<a id="voyager"></a>

### [Voyager](https://github.com/MineDojo/Voyager)

**Related self-improvement mechanism.** Turns Minecraft execution experience into a persistent JavaScript skill library. An LLM critic approves additions; description-based retrieval supplies useful code for later tasks. Compare the retrieved prompt snippets with the full executable library used for skill composition.

**Recommended entry.** Read [paper §§2.2–2.3](https://arxiv.org/html/2305.16291v2#S2.SS2), then [skill storage / retrieval](https://github.com/MineDojo/Voyager/blob/main/voyager/agents/skill.py). Follow [Getting Started](https://github.com/MineDojo/Voyager#getting-started) for `Voyager(...).learn()`, or the README's `skill_library_dir='./skill_library/trial1'` example to reuse released skills on a new task. `resume=True` reloads an ongoing learning run.

**Language and running requirements.** English; Python ≥3.9, Node ≥16.13, licensed Minecraft Java **1.19**, Fabric **0.14.18** / mods, Java **17** for the custom mod, and OpenAI chat / embedding APIs. No model fine-tuning; the game must run locally. This classic implementation has legacy, partly unpinned dependencies and old model defaults; fresh installation / endpoint compatibility was not tested.

**Learning exercise:** inspect the saved playbook or skill library, restart with that state, and trace its effect on a held-out example or new task. Compare with an empty-state run while keeping models and task budgets comparable. [LongMemEval-V2](#longmemeval-v2) offers a separate memory-component comparison; connecting these projects to its interface requires an adapter. Treat component accuracy, retained task gains, and changes to the improvement procedure as distinct questions.

<a id="coevolution-projects"></a>

## Co-Evolution

Read [Co-Evolution §§2.2–2.3](https://arxiv.org/html/2608.10299v1) first: identify which components change and how each changes the other's learning conditions. Start with **CORAL** for shared experience through a model API, **JaxUED** for environment curricula, or **CoMAS / R-Zero** for multi-GPU training. These are different mechanisms, not successive required steps.

The survey explicitly discusses CORAL and CoMAS in §3.2.1. R-Zero is our learning pairing for §4.1.2; JaxUED implements ACCEL / PAIRED, whose method papers are discussed in §4.3.1. These implementations retain human-designed update rules; this route does not claim to reproduce §5's meta co-evolution.

<a id="coral"></a>

### [CORAL](https://github.com/Human-Agent-Society/CORAL)

**Related self-improvement mechanism.** **Shared experience; §3.2.1.** Agents revise solutions in separate Git worktrees and reuse shared scored attempts, notes, and skills. Trace how one agent's discovery changes another's next attempt; the circle-packing evaluator and model weights remain fixed.

**Recommended entry.** Follow [installation](https://coral.compounding-intelligence.ai/docs/getting-started/installation/), clone the source, and inspect [circle packing](https://github.com/Human-Agent-Society/CORAL/tree/main/examples/circle_packing) plus the [multi-agent guide](https://coral.compounding-intelligence.ai/docs/guides/multi-agent/). After `uv sync` and gateway configuration, run `uv run coral start -c examples/circle_packing/task.yaml agents.count=2` from the repository root. Inspect `coral log`, notes, and skills; finish with `coral stop` (prefix with `uv run` for the source install).

**Language and running requirements.** English docs and a Chinese README; Python **3.11–3.13**, Git, `uv`, Docker, and model API access. This example's `docker-opencode` preset uses OpenCode and a LiteLLM gateway; configure the API-key placeholder in `litellm_config.yaml`. Its NumPy / SciPy grader needs no training GPU. Budget for two agents' model calls and local evaluations.

<a id="eat"></a>

### [Evolving Agent Teams (EAT)](https://github.com/caoshiyi/EAT) · [paper](https://arxiv.org/abs/2610.36848)

**Related self-improvement mechanism · team redesign from experience.** A supervisor diagnoses stalled progress and changes the coding team's roles, prompts and execution phases. Team artifacts, learning notes and evolution history inform the next redesign; the team edits the task program under a fixed evaluator. Learn how persistent experience changes team organization, without assuming that the supervisor's update algorithm rewrites itself.

**Recommended entry.** Read [paper §3.2 → §§4.2 and 4.5](https://arxiv.org/html/2610.36848v1) → [task setup in `SKILL.md`](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/SKILL.md) → [`SUPERVISOR.md`](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/agent_team/SUPERVISOR.md) → [`launch_stateless.sh`](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/agent_team/launch_stateless.sh). Follow team configuration → execution → official evaluation → reflection. The [Claude Code entry](https://github.com/caoshiyi/EAT/blob/737e1665eeeffd3fce35d319174f88ea4613d7aa/README.md#get-started) is:

```text
/plugin install eat --marketplace caoshiyi/EAT
```

Prepare a task Git repository with `eat/task.md` and `eat/eval.sh`; record the starting score and specify the iteration limit, team size and dollar budget. The script's `--persistent` mode retains the supervisor conversation. Read `eat/log/TEAM_CONFIG.md`, iteration evaluations and `eat/log/BUDGET.md` together to relate team changes to score and cost.

**Language and running requirements.** English; documented runtime is Linux, Claude Code model access, Git, tmux and Python ≥3.11. EAT Gym additionally uses uv, the Hugging Face CLI and task-specific dependencies / hardware. The plugin is an installation entry, not a model-free demo; runs make real model calls. Use a dedicated task environment: the launcher runs coding agents with permission prompts disabled; upstream's optional [clean-room setup](https://github.com/caoshiyi/EAT/tree/737e1665eeeffd3fce35d319174f88ea4613d7aa/cleanroom) adds Linux bubblewrap and a network allowlist.

<a id="comas"></a>

### [CoMAS](https://github.com/xxyQwQ/CoMAS)

**Related self-improvement mechanism.** **Independent agent policies; §3.2.1.** Peers solve, critique, and score, then use interaction rewards to update their own weights. Follow the new policies into the next discussion; this connects multi-agent interaction to persistent learning.

**Recommended entry.** Read [paper §§3.1–3.3](https://arxiv.org/html/2510.08529v2#S3), then the [training launcher](https://github.com/xxyQwQ/CoMAS/blob/main/scripts/train_comas.sh). Follow the README's Python 3.10 setup and `pip install -r requirements.txt`, configure `PRETRAIN`, GPU / batch and W&B settings, then run `bash scripts/train_comas.sh` from the repository root. Trace workflow → reward → controller.

**Language and running requirements.** English; RL background, CUDA, PyTorch / vLLM / DeepSpeed / Ray, and local model weights. Uses the repository's `datasets/blended` and extra evaluation data. Upstream recommends **2× A100 80GB per agent**; the default has four independent agents, about **8 GPUs**, not a verified minimum. Core training uses local models; W&B defaults to offline logging.

<a id="r-zero"></a>

### [R-Zero](https://github.com/Chengsong-Huang/R-Zero)

**Related self-improvement mechanism.** **Adaptive task generation; §4.1.2.** An independent Challenger learns from the current Solver's answer consistency. Its questions and majority-vote pseudo-labels train the Solver; both checkpoints carry into later alternating rounds. Trace how task difficulty and solving policy shape each other; pseudo-labels are not independently verified answers.

**Recommended entry.** Read [Quickstart](https://github.com/Chengsong-Huang/R-Zero/blob/main/README.md) and [main.sh](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/main.sh). Install requirements, configure `STORAGE_PATH`, `HUGGINGFACENAME`, `tokens.json`, and evaluation endpoints. The root entry is `bash scripts/main.sh Qwen/Qwen3-4B-Base qwen3-4b`; inspect the [Challenger launcher](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/questioner_train_penalty.sh) and [Solver launcher](https://github.com/Chengsong-Huang/R-Zero/blob/main/scripts/solver_train.sh) first.

**Language and running requirements.** English; advanced Python / RL, Linux / CUDA, PyTorch **2.7.0** and vLLM **0.9.1**. Scripts configure **8 GPUs**; no unified minimum Python / VRAM is stated. Requires model / data access, Hugging Face and W&B configuration; generated data is uploaded to a private HF dataset, and full evaluation uses a GPT API. Use an isolated training environment: the Challenger launcher contains broad `pkill python` cleanup.

<a id="jaxued"></a>

### [JaxUED](https://github.com/DramaCow/jaxued)

**Related self-improvement mechanism.** **Environment curricula; §4.3.1.** ACCEL scores, retains, and mutates maze levels using policy performance, then trains on the resulting curriculum. Compare generated levels and policy transfer; later inspect PAIRED's two learners and learned environment generator.

**Recommended entry.** Clone the source and install `pip install -e ".[examples]"`; read [Maze PLR/ACCEL](https://dramacow.github.io/jaxued/maze_plr/), then run `WANDB_MODE=disabled python examples/maze_plr.py --use_accel` from the repository root. Continue to [`maze_paired.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_paired.py). Use the current [`maze_plr.py`](https://github.com/DramaCow/jaxued/blob/main/examples/maze_plr.py), not the stale `minigid_plr.py` path on the older Getting Started page.

**Language and running requirements.** English; Python / PPO / JAX background. Package declares Python **≥3.9**; match JAX / Flax and the example dependencies to your platform using [JAX installation guidance](https://docs.jax.dev/en/latest/installation.html). No LLM API; the command disables W&B. CPU development is possible, but default ACCEL training is about **246 million environment steps**; full runs need suitable RL compute. No minimum VRAM or runtime was established.

<a id="adversarial-self-play"></a>

## Adversarial Self-Play

Start with **OpenSpiel** to observe best responses and strategy history on a CPU. Choose **SPIRAL** for language-model game RL, or **SPPO** to study preference-game optimization. SPIRAL is explicitly discussed in [Modern Agentic Systems §7.3](https://arxiv.org/html/2607.13104v1#S7.SS3); the connections below to [Co-Evolution §3.1](https://arxiv.org/html/2608.10299v1#S3.SS1) are our learning extensions, not claims that this survey names all three implementations. SPPO is an adjacent preference-game example rather than two separately trained agents.

<a id="open-spiel"></a>

### [OpenSpiel: Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel) — classical self-play

**Related self-improvement mechanism · self-play prerequisite.** Two players learn DQN best responses and reservoir-based average policies. Track average-policy exploitability (how much a best response can exploit it), rather than only their head-to-head win rate.

**Recommended entry.** Follow [installation](https://github.com/google-deepmind/open_spiel/blob/master/docs/install.md) and obtain the examples. Start with [tabular fictitious play](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/fictitious_play_example.py) using `--game=kuhn_poker`, then run `python3 open_spiel/python/examples/nfsp_kuhn_pytorch.py --num_train_episodes=20000 --eval_every=1000` from the repository root; [NFSP source](https://github.com/google-deepmind/open_spiel/blob/master/open_spiel/python/examples/nfsp_kuhn_pytorch.py).

**Language and running requirements.** English; current source requires **Python ≥3.11**; source builds use CMake / a C++ compiler. NFSP additionally needs PyTorch and `dm-tree`; default **CPU**, no model API. Upstream defaults to **3M episodes**; the 20,000-episode command is our shorter learning setting, not convergence evidence.

<a id="spiral"></a>

### [SPIRAL](https://github.com/spiral-rl/spiral) — multi-turn zero-sum game RL

**Related self-improvement mechanism.** One shared policy plays both roles and learns from both trajectories. Study role-conditioned advantages, policy updates, and how the updated opponent changes subsequent experience.

**Recommended entry.** Read [paper §§4.1–4.3](https://arxiv.org/html/2506.24119v2#S4), follow the README setup, inspect [run.sh](https://github.com/spiral-rl/spiral/blob/main/run.sh), then run `bash run.sh` from the repository root. Trace role trajectories → OAT optimization → vLLM weight synchronization.

**Language and running requirements.** English; Python **3.10**, CUDA, vLLM **0.8.4**, OAT **0.2.1**, and Qwen3-4B-Base weights. Upstream tested **8× H100**; not a verified minimum. Configure W&B and the default OpenRouter evaluation, or change those settings (for example, random-only opponents). Training produces game trajectories; math evaluation also uses bundled data. Use this original local entry; the reviewed Tinker launcher references missing source files.

<a id="sppo"></a>

### [SPPO](https://github.com/uclaml/SPPO) — preference-game self-play

**Related self-improvement mechanism.** Current-policy answers compete under a fixed PairRM judge. A new checkpoint supplies the next round's answers. Compare SPPO's loss with game RL; the judge and learning rule stay fixed.

**Recommended entry.** Read [paper §3.2 and §§4.1–4.2](https://arxiv.org/html/2405.00675v5#S4), follow the README setup, and inspect [run_sppo_mistral.sh](https://github.com/uclaml/SPPO/blob/main/run_sppo_mistral.sh). After configuring data and uploads, run `bash run_sppo_mistral.sh` from the repository root for the three-round pipeline.

**Language and running requirements.** English; **Python ≥3.10**, CUDA, vLLM, LLM-Blender / PairRM, Accelerate / DeepSpeed, Mistral weights and HF prompt data. Scripts configure **8 GPUs / processes**; minimum VRAM is unspecified. Core training needs no paid LLM API. Data generation uploads private HF datasets to `UCLA-AGI` by default: choose your own authorized namespace / token or disable those calls; the model-upload flag does not disable data uploads. Old / partly unpinned dependencies were not installation-tested.

These entries retain fixed game rules or preference judges and fixed training procedures. They offer concrete self-play learning loops; use the [RL–RSI guide](../README.md#rl-and-rsi) to identify the additional mechanisms involved when the improver itself changes.

<a id="evaluation"></a>

## Evaluation

<a id="rsi-atlas"></a>

### [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI)

**Evaluation tool · admission-gate exercise.** Illustrates improvement loops, evaluation, and change admission, with a small Python example for learning how to accept / reject candidate changes and record their history.

**Recommended entry.** [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python admission-gate example](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py).

**Language and running requirements.** English; the example uses the Python 3.10+ standard library. It makes decisions from externally supplied test status, gains, and file paths; it does not generate changes with a model or run evaluations automatically.

<a id="textbook-baselines"></a>

### [Do Self-Improving Coding Agents Beat Textbook Baselines?](https://github.com/tejasvi/self-improving-agents-textbook-baselines) · [paper](https://aixiv.online/abs/2610.02812)

**Evaluation tool · comparative study and result reanalysis.** Compares a DGM port with standard engineering changes, one-shot redesign, placebo loops and compute-matched sampling; also re-evaluates released DGM and ADAS agents. Learn to separate search and selection effects from baseline quality, test-set transfer and resource budgets. Conclusions concern the tested models, tasks and implementations; changing the model is not an exact replication of the original experiment.

**Recommended entry.** Read the pinned [README](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/README.md) → [methods](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/paper/sec_methods_v2.tex) → [discussion](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/paper/sec_discussion_v2.tex) → [`replay.sh`](https://github.com/tejasvi/self-improving-agents-textbook-baselines/blob/ee6419a25590578197e9acf1565cbb8bfda4661f/replay.sh). From the cloned repository:

```bash
bash replay.sh
```

This regenerates summaries, tables and figures from shipped results without model calls. Compare the per-task outcomes and agent patches before interpreting aggregate scores. The paper is **aiXiv v2**; repository tag **v4** identifies the code/data archive, not the paper version. aiXiv is a separate platform from arXiv.

**Language and running requirements.** English; offline reanalysis needs Python 3, NumPy, SciPy and Matplotlib, with no GPU or model API. Figure bytes can differ across Matplotlib versions. Full experiments additionally require model access, external LiveCodeBench data, bubblewrap, the upstream project layout and agent dependencies; SWE-bench runs need Docker and swebench 2.1.0. Full agent transcripts are absent, and three summaries derived from omitted logs are supplied as replay inputs. Reanalysis therefore checks the released results without recreating every experimental observation.

<a id="longmemeval-v2"></a>

### [LongMemEval-V2](https://github.com/xiaowu0162/LongMemEval-V2) · [paper](https://arxiv.org/abs/2605.12493)

**Evaluation tool.** Tests whether stored web / enterprise trajectories support later questions about states, workflows, and environment pitfalls. Its **451 questions** pair answer accuracy with memory-query latency. Useful for comparing memory components; a score alone does not establish an RSI loop.

**Recommended entry.** Read [paper §3.3](https://arxiv.org/html/2605.12493v1#S3.SS3), follow data / endpoint setup, then compare [no retrieval](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_no_retrieval.sh) with [RAG](https://github.com/xiaowu0162/LongMemEval-V2/blob/main/evaluation/scripts/run_rag_query_to_slice.sh). From the repo root, start with `TIER=small bash evaluation/scripts/run_no_retrieval.sh --limit 5`, then use the RAG wrapper with the same limit. This selects **5 questions per domain**, while retaining data / index setup.

**Language and running requirements.** English; Python ≥3.11, [public Apache-2.0 data](https://huggingface.co/datasets/xiaowu0162/longmemeval-v2) (about **7.12 GB** before extraction), and model endpoints. Defaults: Qwen3.5-9B reader / RAG controller; RAG also needs Qwen3-Embedding-8B. Some categories call a paid GPT-5.2 judge. Serving hardware depends on the models and context; no minimum VRAM is documented. V2 generates answers as part of evaluation; it has no standalone imported-prediction scoring CLI.

<a id="past-bench"></a>

### [PAST-Bench · Gen-Verse](https://github.com/Gen-Verse/PAST-Bench) · [paper](https://arxiv.org/abs/2608.04003)

**Evaluation tool · cross-session improvement.** Ordered task families compare persistence on/off in fresh sessions, with traces and artifacts showing how earlier experience affects later behavior. Learn to distinguish retaining preferences, reusing procedures, gathering prior context, and updating stale knowledge. This complements component-level memory evaluation with a longitudinal comparison.

**Recommended entry.** Follow the [README setup and Smoke Test](https://github.com/Gen-Verse/PAST-Bench/blob/f8223517ae7491e776b69793d9f11e9d074ab42e/README.md). After installing Hermes/Hermes+, building the sandbox image, and configuring the agent/judge profile, run the single preference-adoption family:

```bash
HERMES_PLUS_MECHANISMS=all past-bench evolve \
  --family memory_ability/SM01_preference_adoption \
  --agent hermes-plus --agent-profile minimax \
  --runtime local --sandbox --sandbox-tools \
  --compare-no-persistence --judge-model MiniMax-M2.7 \
  --trace-dir traces/smoke/hermes_plus_minimax_sm01
```

Read `sequence_comparison.json` alongside per-episode results and traces; the persistence comparison helps attribute a gain to retained experience instead of an isolated task score.

**Language and running requirements.** English; Python ≥3.11, uv, Docker, the chosen agent integration, and agent/judge model API access. The example uses `MINIMAX_API_KEY`; other profiles require corresponding configuration. It performs real model calls even though upstream calls it a smoke test. PAST-Bench measures improvement behavior; its name alone does not establish that an evaluated agent recursively improves its improver.

<a id="scale-rsi-bench"></a>

### [Scale RSI Bench · scaleapi/rsi-benchmark](https://github.com/scaleapi/rsi-benchmark) · [website](https://www.rsi-benchmark.com)

**Evaluation tool · AI R&D tasks.** The README's four public sample types cover self-distillation, jailbreak robustness, agent-swarm optimization, and nanoGPT data curation. Start by learning how a research task specifies editable artifacts, compute limits, and verification. These are task examples, not evidence that an agent has completed a recursive self-improvement cycle.

**Recommended entry.** Read [`samples/nano-gpt-data-curation/README.md`](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/samples/nano-gpt-data-curation/README.md): select a 12M-token subset for a fixed 30M-parameter model, then verify through training and held-out perplexity. Continue to the task's `instruction.md` and `task.toml`, then follow [Running the Benchmark](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/README.md#running-the-benchmark) for the `harbor run` entry with that task path, agent/model arguments, and Modal runtime.

**Language and running requirements.** English; Python ≥3.12, `pip install -e ".[runner]"`, Harbor, model API access, and configured Modal GPU sandboxes. The reviewed README requires GPUs for its tasks; hardware and timeouts are specified per task. Reading the task contract needs no compute service. Use the Scale repository/website linked above; `recursive-self-improvement-bench.com` and RSIBench-Data are different resources with different task counts.
