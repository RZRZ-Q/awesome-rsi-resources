# Practice Guide

**English** | [简体中文](practice-guide_zh.md)

[Back to the resource directory](../README.md) · [Learning guide](learning-guide.md) · [Verification records](verification.md)

This guide collects learning goals, source entry points, and running requirements for specific examples. Choose a project by topic; use the [learning guide](learning-guide.md#survey-project-map) to connect it to survey chapters. The [three resource labels](../README.md#resource-scope) describe the recommended entry point; topic groups are not RSI capability levels.

These notes come from upstream documentation and selected source reviews on **2026-10-22–2026-11-25**. The [verification records](verification.md#verification) give the scope of each review, including which local examples ran. API examples require model access and a call budget. Training configurations describe the authors' setups.

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

<a id="real-lab-rsi-tutorial"></a>

### [RSI Interactive Tutorial · REAL Lab](https://github.com/REAL-Lab-NU/rsi-interactive-tutorial)

**Interactive introduction.** In an open-day scheduling example, follow a solver's proposed plan, a verifier's conflict report, and the improver's revision. The general course uses a scripted browser simulation.

1. Open [Base Agent](https://real-lab-nu.github.io/rsi-interactive-tutorial/general/#base-agent), then [SI](https://real-lab-nu.github.io/rsi-interactive-tutorial/general/#si). Change the scheduling priority or room availability. Check which task fails and which change to the solver carries forward.
2. Open [RSI](https://real-lab-nu.github.io/rsi-interactive-tutorial/general/#rsi). Compare a fixed setup buffer with looking up how long a shared resource needs. Follow the comparison into a rule the improver can reuse on later tasks.
3. Use the [research atlas](https://real-lab-nu.github.io/rsi-interactive-tutorial/general/#atlas) to compare solver and improver roles across ten papers. Each card points to primary evidence.

**Requirements and evidence.** Chinese and English. The online tutorial needs only a browser. At the [pinned revision](https://github.com/REAL-Lab-NU/rsi-interactive-tutorial/tree/134733b92427650c36b68cad9ae392d252db3212), seven upstream Node checks passed, including the scheduling controls and paper atlas coverage.

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

<a id="sage"></a>

### [Sage · Agent-package optimization](https://github.com/ZHangZHengEric/Sage)

**Related self-improvement mechanism · workflow tutorial.** Compare versioned instructions and skills through separate target, tuner and evaluator invocations. Accepted packages become later parents; model weights, tuner implementation and selection logic remain fixed. Selection returns a candidate; using it in the active Agent is a separate action.

**Recommended entry.** Read the [first-run guide](https://github.com/ZHangZHengEric/Sage/blob/be0499cdc1a5902ea14f085573608852253bc35f/docs/en/applications/FIRST_RSI_RUN.md) alongside the [current example source](https://github.com/ZHangZHengEric/Sage/blob/be0499cdc1a5902ea14f085573608852253bc35f/examples/v2/package_optimizer.py). In a checkout of that revision:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -e .
python -m examples.v2.package_optimizer
```

Find the rejected second round and the selected package hash. All three roles use scripted responses: scores are predefined as 0.4 → 0.6 → 0.5 → 0.8, and the target returns a guidance label rather than solving unit conversions. The script prints JSON, uses temporary Session storage and removes it on normal exit. It makes no model calls and enables no tools.

**Version detail.** The guide's old output uses `final_passed`; current source prints `goal_verified`. Its fixed-validation mode has no independent final exam. Read [`_select_adaptive` and retained-parent updates](https://github.com/ZHangZHengEric/Sage/blob/be0499cdc1a5902ea14f085573608852253bc35f/sagents/v2/optimization/optimizer.py) instead of treating the old output as the current selection contract.

**Requirements and next step.** Python **3.12+**, Git and dependency installation; no API key, Flutter or training GPU for this example. Continue with the [optimizer API](https://github.com/ZHangZHengEric/Sage/blob/be0499cdc1a5902ea14f085573608852253bc35f/sagents/v2/optimization/README.md). [Real-model domain experiments](https://github.com/ZHangZHengEric/Sage/blob/be0499cdc1a5902ea14f085573608852253bc35f/examples/v2/README.md) require a Responses-compatible model catalog, credentials, explicit domain and a new output directory; they incur API costs and use a different, legacy selection / final-evaluation protocol.

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

<a id="infrarsi"></a>

### [InfraRSI](https://github.com/TokenRhythm/InfraRSI) · [paper](https://arxiv.org/abs/2611.11558)

**Related self-improvement mechanism · retained optimization experience.** Verified training-system trials become experience that seeds later search configurations and performance / memory priors. Within a run, measurements revise those priors and guide configuration / code proposals. The task contract, search implementation and verifier remain fixed; the retained asset improves subsequent optimization choices.

**Recommended entry.** Read [§§2.1, 3 → §§4–5](https://arxiv.org/html/2611.11558v1), then trace [experience write-back](https://github.com/TokenRhythm/InfraRSI/blob/512f8ea784054f4ca3331d03cc6589267a4cbdf5/infrarsi/experience/runs.py) → [next-search initialization](https://github.com/TokenRhythm/InfraRSI/blob/512f8ea784054f4ca3331d03cc6589267a4cbdf5/infrarsi/search/bcomp.py#L570). From the pinned repository root, start with the [CPU toy](https://github.com/TokenRhythm/InfraRSI/blob/512f8ea784054f4ca3331d03cc6589267a4cbdf5/examples/toy_cpu/train.py):

```bash
python -m pip install -e .
infrarsi doctor examples/toy_cpu
infrarsi run examples/toy_cpu --strategy random --llm none --screens 2
infrarsi report examples/toy_cpu
```

This example simulates time, memory and loss to teach contracts, rejected candidates and reports; it neither trains a model nor exercises LLM-guided B-Comp. Continue with the [real-job workflow](https://github.com/TokenRhythm/InfraRSI/blob/512f8ea784054f4ca3331d03cc6589267a4cbdf5/README.md#-getting-started): `init` → `doctor` → `run --strategy bcomp --llm codex-cli` → `report` → preview `apply`. Compare `--experience off` with retained experience under the same workload and budget.

**Requirements.** Bilingual README; Python ≥3.10. The toy needs no GPU or model credentials. Real optimization needs an already working training job, its framework / GPUs and an authenticated coding CLI or model API. Search caps exclude baseline checks, diagnosis and final verification. The [Claude Code / Codex Skill](https://github.com/TokenRhythm/InfraRSI/blob/512f8ea784054f4ca3331d03cc6589267a4cbdf5/agent_skill/README.md) is an optional interface, added November 12; the paper first appeared November 8 UTC. The reported 8–16 H100/H200 configurations are experiment setups, not minimum requirements.

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

<a id="skill-infinity"></a>

### [Skill∞](https://github.com/taowangcheng/Skill-Infinity) · [paper](https://arxiv.org/abs/2610.35434)

**Recursive improvement method · editable optimization procedure.** A meta agent follows a meta-skill to improve task skills. When that meta-skill becomes the target, the current parent meta-skill governs its own revision; the selected version then guides later optimization. Pair with [VERSE](#verse) and the [experience / meta-evolution survey](../README.md#frontis-survey).

**Recommended entry.** Read [§§3.2–3.4 → §4.3 → Appendix C → Appendix G](https://arxiv.org/html/2610.35434v1): recursive loop, self-improvement ablation, changed selection rule, and seed meta-skill. Track the retained procedure separately from task-specific skills and compare the cost of learning it with the cost of reuse.

**Language and requirements.** English; agent and skill-optimization fundamentals; reading requires no API or GPU. The [official snapshot](https://github.com/taowangcheng/Skill-Infinity/tree/78197d69784665d38a74a327940783c48c8b4897) contains a README, license and artwork, with code still pending release as of **2026-11-02**. No runnable implementation, installation command or hardware minimum was verified.

<a id="rsi-env"></a>

### [RSI-Env](https://arxiv.org/abs/2611.01736) — method reading

**Recursive improvement method.** Read [§§3.1–3.3 → §4.5 → Appendix A](https://arxiv.org/html/2611.01736v1). Trace the Self successor into the next improver and contrast it with a fixed Teacher. Registration checks validity and executability; capability evaluation is separate, so registration alone does not establish improvement.

**Requirements.** English; reading needs no compute. No official runnable repository was located through the paper and repository searches on **2026-11-04**. Appendix A reports 32 A800 80GB GPUs for training and another 32 for inference, with ten three-hour rounds; this is the study setup, not a verified minimum.

<a id="exo"></a>

### [Exo](https://github.com/exoharness/exo) · [paper](https://arxiv.org/abs/2611.00463)

**Recursive improvement method · runtime self-modification.** The self-improving agent can edit its harness and instructions for later improvement, then activate the changed implementation while retaining conversation history. The current root README describes a general runtime; start with the separate self-improving-agent example.

**Source route.** Read [paper §§3–4 → §5.4](https://arxiv.org/html/2611.00463v1) → [example README](https://github.com/exoharness/exo/blob/d7fb6d2ee477dec48d272461b4c534152939ad22/examples/self-improving-agent/README.md) → [harness prompt assembly](https://github.com/exoharness/exo/blob/d7fb6d2ee477dec48d272461b4c534152939ad22/examples/self-improving-agent/harness.ts) → [rebuild tool](https://github.com/exoharness/exo/blob/d7fb6d2ee477dec48d272461b4c534152939ad22/examples/self-improving-agent/tools/guardian-tools.ts). Follow source edits into the guardian's build / restart operation and the next agent turn. Inspect `.exo/guardian-updates/` and conversation events to connect a requested update with its recorded outcome.

**Running entry.** Use a dedicated checkout at the reviewed revision. From its root, run `pnpm install`, copy `.env.example` to `.env`, and configure `OPENAI_API_KEY` and an accessible model using the example's settings. On a new instance only:

```bash
./examples/self-improving-agent/exo.sh fresh --control
```

`fresh` deletes existing agents, conversations and adapters for this checkout. Resume with `./examples/self-improving-agent/exo.sh --control` to keep state; the control wrapper restarts the REPL child when a guardian update requests it.

**Requirements.** English; Docker, model API access and a Rust / Node / pnpm build environment. The reviewed [mise.toml](https://github.com/exoharness/exo/blob/d7fb6d2ee477dec48d272461b4c534152939ad22/mise.toml) pins Rust 1.95, Node 22.15.0, pnpm 10.26.2 and Python 3.11. The agent edits the mounted checkout; use an instance dedicated to this experiment. Build success is not a quality gate. [Self-control documentation](https://github.com/exoharness/exo/blob/d7fb6d2ee477dec48d272461b4c534152939ad22/examples/self-improving-agent/docs/SELF-CONTROL.md) describes separate validation / rollback primitives; cloning and a canary comparison path remain planned.

<a id="elite"></a>

### [ELITE · Evaluation-Free Recursive Self-Improvement for Coding Agents](https://arxiv.org/abs/2611.21056) — method reading

**Related self-improvement mechanism.** ELITE implements several proposals from one parent, then reimplements a compatible subset as one descendant. A descendant that passes validity checks supplies the source and starting point for the next round. Model weights and the outer search procedure stay fixed.

**Recommended entry.** Read §§4.1–4.2 and Appendix A.6 to trace the parent, exploratory implementations and integrated descendant. Appendix A.5.2 describes compilation, interface checks and smoke tests used to admit changes. Then read §§5.1–5.3 and Table 2 to compare selection feedback, final evaluation and search cost. [Paper v1](https://arxiv.org/html/2611.21056v1#S4)

**Evidence and requirements.** The loop uses implementation inspection and deterministic validity checks. Downstream task outcomes are measured after evolution on 60 SWE-bench Pro tasks and 50 tasks each from SWE-bench Verified and Polyglot. Verified and Polyglot serve as transfer tests. Runtime comparisons use different search budgets and concurrency. The paper describes Docker sandboxes and DeepSeek or Qwen model access for the main experiments. No official runnable implementation was verified. [Experimental setup](https://arxiv.org/html/2611.21056v1#S5.SS1) · [Runtime settings](https://arxiv.org/html/2611.21056v1#A1.SS5)

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

<a id="sim"></a>

### SIM · Self-Improvement Memory ([paper](https://arxiv.org/abs/2611.18856) · [author explainer](https://lucasxinyu.github.io/sim/))

**Recursive improvement method · paper reading.** SIM carries forward the reasons, predictions, and observed outcomes behind earlier harness edits. When a compatible benchmark or policy model changes, the proposer and selector read the carried memory. They append findings for selected edits, including missed predictions and regressions, so later rounds can revise how inherited edits are used.

1. Start with [the illustrated memory record](https://lucasxinyu.github.io/sim/#method). Follow a diagnosis through an edit, selection on the evolve split, and an appended outcome. Then read [§3](https://arxiv.org/html/2611.18856v1#S3) and Appendix D for the stored fields and who reads them.
2. Read [§4.4 and Table 3](https://arxiv.org/html/2611.18856v1#S4.SS4). Ten evolved Terminus-2 harnesses each seed two ten-round TB4 continuations with matched starting code, policy and round/candidate budgets. Carrying and updating SIM gives a mean final-score gain of 2.36 points over harness-only continuation. Nine of ten pairs favor SIM.
3. Compare Appendix F with the [Harness² experience-library route](#harness2). Identify which earlier rationales transfer, which edits need revision, and why giving the proposer and selector the full memory adds context cost.

**Requirements.** The author explainer and paper are readable without a model or GPU. The explainer's record illustrates the format. This review located no author-provided runnable release for the reported experiments.

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

<a id="rsihub"></a>

### [RSIHub](https://github.com/simple-agent-lab/RSIHub) · [framework paper](https://arxiv.org/abs/2610.32253)

**Related self-improvement mechanism · experiment framework.** Compare methods through reusable operators and a common evaluation lifecycle. Its HyperAgents recipe permits changes to both `target/**` and `operators/**`, including the mutation procedure; retained operator code can participate in later improvement work. The evaluator, framework mechanism and model weights stay fixed. Other recipes use narrower mutable surfaces.

**Recommended entry.** Read [§§3.1–3.3 → §4.1 / Appendix D](https://arxiv.org/html/2610.32253v1), then trace the [recipe](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/recipes/hyperagents/evolve.yaml) → [mutation operator](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/library/mutate/hyperagents.py) → [parent snapshot inheritance](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/src/evolve/driver.py#L681) → [operator loading](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/src/evolve/operators.py#L66). Changed operators take effect when next invoked; earlier-stage changes affect later generations, while an unexecuted gate may change within the current generation.

Start with the documented [deterministic baseline check](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/docs/getting-started.md#run-a-deterministic-baseline-check). Its `EVAL_STUB=1` and `--max-generations 0` exercise workspace creation, generation-zero evaluation and archive integrity without a model or Docker; no mutation occurs. After configuring credentials and Docker as in the [quick start](https://github.com/simple-agent-lab/RSIHub/blob/d6554299c58bf0fe2db04ddda0277f9db67ea680/docs/QUICKSTART.md), run from the pinned repository root:

```bash
./scripts/setup_terminal_bench.sh hyperagents
./scripts/run_recipe_demo.sh hyperagents
```

The launcher defaults to one generation. This recipe uses all 30 curated tasks as a shared optimization set; its optimization curve is not a held-out transfer result.

**Companion evaluation reading.** [Beneath the Surface §§3.2–4 → §§5–6 → §7](https://arxiv.org/html/2611.07624v1) uses RSIHub to distinguish repeated success, task-coverage gains and losses, deployment cost, and transfer. Follow the diagnostics into EvoAudit's operator redesign; AGE installs four revised operators that stay fixed during each reported run. The checked repository exposes the framework and existing recipes, but no named EvoAudit / AGE reproduction entry was verified. The two papers and repository are grouped as one resource here.

**Requirements.** Bilingual repository; Python ≥3.12, uv and Git. The real launcher additionally needs Bash, Git ≥2.25, Docker, Harbor task downloads and model access / budget. Harbor is pinned to 0.18.0; the HyperAgents mutation container uses Codex 0.146.0. This source route does not establish a minimum machine specification or reproduce the reported gains.

<a id="flashrsi"></a>

### [FlashRSI · RUC-NLPIR](https://github.com/RUC-NLPIR/FlashRSI)

**Related self-improvement mechanism · experiment framework.** Configure the algorithm, target harness, editing worker and benchmark separately; follow candidate resources through execution, selection and saved snapshots. Whether the improver changes depends on the chosen algorithm. The quickstart uses SkillOpt to revise skills with fixed model weights.

**Recommended entry.** Read the pinned [quickstart](https://github.com/RUC-NLPIR/FlashRSI/blob/1d3f4d3703cc7c90eba01968626d0873158f2e24/docs/index.md) → [configuration](https://github.com/RUC-NLPIR/FlashRSI/blob/1d3f4d3703cc7c90eba01968626d0873158f2e24/examples/quickstart.yaml). It includes 12 SearchQA questions split **6 / 3 / 3** for train / dev / test and one fast update. Check out that revision, create a Python virtual environment and install `python -m pip install -e ".[all]"`. From the repository root:

```bash
flashrsi run --config examples/quickstart.yaml --check-only
```

This checks startup and may prepare data / dependencies; it makes no model calls and does not test remote authentication. Configure `TARGET_API_KEY` and `WORKER_API_KEY` separately, then use model names available to your account:

```bash
flashrsi run --config examples/quickstart.yaml \
  --model YOUR_TARGET_MODEL --worker-model YOUR_WORKER_MODEL \
  --output-dir runs/quickstart \
  --set agent.llm.api_key="$TARGET_API_KEY" \
  --set algorithm.worker.llm.api_key="$WORKER_API_KEY"
```

For custom endpoints, set `agent.llm.base_url` and `algorithm.worker.llm.base_url`. Inspect `snapshots/`, `trajectories/`, `result.json` and `end-summary.md`; compare initial and selected snapshots on the same held-out tasks. This small run teaches the experiment workflow, not a research-level improvement estimate.

**Requirements.** English / Chinese documentation; Python **≥3.11**, with **3.12** recommended, a running **Docker Linux daemon**, and model API budget. Docker is required even for this quickstart: target tasks run in containers that must reach the model endpoint. Hosted-model use requires no local training GPU; full benchmarks add their own data and dependencies. Compare with [Hermit](#hermit) for external adapters and [Beagle](#beagle) for evolution interfaces.

<a id="emoharness"></a>

### [EmoHarness](https://github.com/Emo-Harness/EmoHarness) · [paper](https://arxiv.org/abs/2611.11994)

**Related self-improvement mechanism · multimodal harness search.** A Builder edits prompts, configuration and restricted verification code from a frozen student's failures. Validation gates choose the next harness; Builder logic, gates and student weights stay fixed. Learn to separate gains from audio evidence, a human-written scaffold and evolved edits.

**Recommended entry.** Read [§§3.1–3.3 → §5.1](https://arxiv.org/html/2611.11994v1), then the [construction loop](https://github.com/Emo-Harness/EmoHarness/blob/f8da94134ef0c164d6b9556ed3da7b56abfbf050/src/emoharness/builder/loop.py) and [selection gates](https://github.com/Emo-Harness/EmoHarness/blob/f8da94134ef0c164d6b9556ed3da7b56abfbf050/src/emoharness/builder/gates.py). At this revision, start from the repository root:

```bash
poetry install
poetry run emoharness reproduce --fake --root tmp/emoharness-fake
```

The fake pipeline exercises preparation, evaluation, construction and reporting without models, GPUs or external datasets; it skips real IntentQA. Its scores illustrate workflow wiring. For real runs, follow the [README](https://github.com/Emo-Harness/EmoHarness/blob/f8da94134ef0c164d6b9556ed3da7b56abfbf050/README.md): `prepare` → `evaluate --student qwen3vl_4b` → `evolve --student qwen3vl_4b --builder sol` (prefix each with `poetry run emoharness`).

**Requirements and interpretation.** English; Python **≥3.10,<3.13**, Poetry. Real runs add `poetry install --with api,audio`, datasets, ffmpeg, separate vLLM environments, GPUs for the student / perception models and an API budget for evolution. The paper attributes most gains to audio evidence; no MHE increment survives its Holm correction. Humans inspected 986 evaluation items during development, although the Builder never saw evaluation items: “held-out task types” does not mean an untouched evaluation set.

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

<a id="pce"></a>

### [PCE · Population-Centered Agent Evolution](https://github.com/YanShuo1992/PCE) · [paper](https://arxiv.org/abs/2610.36660)

**Recursive improvement method · inherited harness and population evidence.** Learn how the archive becomes evidence for the next edit: compare population-wide task coverage with the best single agent, then trace distilled observations into a selected parent's harness. Parent patches are restored before the edited agent performs the next self-modification; the population-distillation procedure stays fixed. Pair with the [coding-agent survey](../README.md#coding-agents-survey) and [DGM](#dgm).

**Recommended entry.** Read [§§3.1–3.3 → §§4.3, 5.2–5.4](https://arxiv.org/html/2610.36660v2), then follow the pinned source: [run_swe.sh](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/run_swe.sh) → [GEA_outer.py](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/GEA_outer.py) → [group_distill.py](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/group_distill.py). Inspect `render_block` / `run_for` to see how population observations become reusable context. Then read [self_improve_step.py, parent-patch restoration](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/self_improve_step.py#L342-L371) → [execution of the inherited coding agent](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/self_improve_step.py#L449-L462). This is the recursion boundary, distinct from the fixed population summary mechanism.

**Running entry and requirements.** Complete the [pinned README setup](https://github.com/YanShuo1992/PCE/blob/afe623953f8b1d66336c53502096288fe0e0efb9/README.md), including the specified SWE-bench revision / patches or Polyglot image preparation. Run `./run_swe.sh distill` or `./run_polyglot.sh polyglot_distill`; the corresponding `gea` / `polyglot_gea` modes provide the comparison. Requires Linux, Docker, Conda / Python 3.11, a DeepSeek key and paid API calls, and at least 500 GB free disk (1 TB recommended). Authors estimate roughly four days for SWE-bench and one for Polyglot, depending on workers. Start with source reading; these launchers run full experiments, not a small local demo. No upstream execution was performed in this review.

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

<a id="sol-pi"></a>

### [SoL-Pi · NVIDIA](https://github.com/NVlabs/SoL-Pi) · [paper](https://arxiv.org/abs/2609.20519)

**Related self-improvement mechanism · deploying discovered harness changes.** The research searches for reusable efficiency changes; the public Pi extension packages four selected mechanisms. It does not expose an autonomous recursive search merely by being installed. Pair with [HarnessMM](#harnessmm), [HarnessPro](#harnesspro) and the [harness survey](../README.md#harness-rsi-survey).

**Recommended entry.** Read [paper §2 → §3](https://arxiv.org/html/2609.20519v1), then [src/sol-pi/index.ts](https://github.com/NVlabs/SoL-Pi/blob/219568034fa54ed121ede80961655e33dfb9d0e3/src/sol-pi/index.ts) and the [configuration guide](https://github.com/NVlabs/SoL-Pi/blob/219568034fa54ed121ede80961655e33dfb9d0e3/docs/configuration.md). Trace which feature changes a tool result or context, then compare task completion and cost with that feature enabled and disabled under the same model and tasks.

**Running entry and requirements.** Follow the [pinned Getting Started](https://github.com/NVlabs/SoL-Pi/blob/219568034fa54ed121ede80961655e33dfb9d0e3/README.md#getting-started): Node.js ≥22.19, npm and a tested Pi version. Upstream recommends Pi **1.3.0** for fresh installs; see [compatibility](https://github.com/NVlabs/SoL-Pi/blob/219568034fa54ed121ede80961655e33dfb9d0e3/docs/compatibility.md). The documented project-scoped extension command is `pi install git:github.com/NVlabs/SoL-Pi --local --approve`. Features default to off; configure `.pi/sol-pi.json` in a trusted project. Begin with `actionFusion` and `observationPack`, which add no extra model calls; the agent itself still needs model access. The reducer uses its configured model, and context compaction can continue the active task in a new turn. Source reading needs no runtime; applying the extension requires API budget but no model training. Installing the current branch can differ from the reviewed snapshot.

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

<a id="modular-gated-harness"></a>

### [Harnesses That Improve Themselves · Modular Gated Evolution](https://arxiv.org/abs/2611.22299)

**Related self-improvement mechanism · paper reading.** The framework separates context and state, agent control, action interfaces, and verification and recovery. An external optimizer proposes one module edit at a time. Code-path execution, validation performance and a runtime token cap govern acceptance. The task model stays frozen.

**Recommended entry.** Read §§II–III for the editable components and how traces are used to diagnose failures, §IV for the validation gate, then §VII and Table IV. Identify which data informs the proposal, which selects an edit, and which measures transfer. [Paper v1](https://arxiv.org/html/2611.22299v1)

**Evidence and requirements.** English. Agent engineering and software evaluation fundamentals. Table IV uses 60 SWE-bench Lite issues, with 12 for development, 8 for validation and 40 for final testing. On the original model, modular evolution solves 16/40 at 46.7k runtime tokens per task. The full rewrite solves 17/40 at 451.6k. The search uses 100 versus 24 rollouts and the turn limits differ, so compare search and deployment costs separately. The second model is evaluated using frozen harnesses. No official runnable release was verified.

<a id="guard"></a>

### [GUARD](https://arxiv.org/abs/2611.23476) — method reading

**Recursive improvement method.** GUARD separates new regressions from unresolved gaps using paired trajectory checks. Soft-HURT screens candidate playbook updates. Comparing the best and worst candidates also rewrites the strategy prompts that the distiller uses to propose edits in the next round. Model weights and the update algorithm stay fixed.

**Recommended entry.** Read [§§4.1–4.4 and Algorithm 1](https://arxiv.org/html/2611.23476v1#S4) to trace one edit from a task checklist through candidate scoring, promotion and the next proposer prompts. Then compare [§4.5](https://arxiv.org/html/2611.23476v1#S4.SS5) with [§§6.2–6.4](https://arxiv.org/html/2611.23476v1#S6.SS2). The gate constrains observed self-review scores on its task buffer, while held-out performance is measured separately. Test-time evaluation uses a frozen harness and one rollout per task.

**Requirements and evidence.** English. Agent evaluation and continual learning fundamentals. The reported 54.5% reduction is deployment tokens per task versus the base harness on hosted EvoHarnessBench (43 test tasks), excluding adaptation, review and candidate-evaluation cost. [Appendix B.3](https://arxiv.org/html/2611.23476v1#A2.SS3) describes the model configurations and prompts. The authors plan to release the reference harness subject to approval, and this review located no official executable release.

<a id="jevrsi"></a>

### [JevRSI](https://github.com/usail-hkust/JevRSI) · [paper](https://arxiv.org/abs/2611.22432)

**Related self-improvement mechanism · asynchronous decision harness.** A fast System-1 model selects actions. An asynchronous System-2 LLM uses interaction feedback to revise procedures, state memory and action-effect predictors. Admitted revisions are available to System-1 on later decisions. Those decisions generate the evidence for the next revision, while both models' weights stay fixed.

**Recommended entry.** Read [§3](https://arxiv.org/html/2611.22432v3#S3), then follow a low-confidence action from the [decision loop](https://github.com/usail-hkust/JevRSI/blob/825a4e83e6c6805c7b7255d514e62b3668a20a76/jevmaster/agent.py#L212) through [System-2 review and publication](https://github.com/usail-hkust/JevRSI/blob/825a4e83e6c6805c7b7255d514e62b3668a20a76/jevmaster/system2/service.py#L614) and back to a store reload. Try the [offline example](https://github.com/usail-hkust/JevRSI/blob/825a4e83e6c6805c7b7255d514e62b3668a20a76/README.md#running) with two deterministic stubs and a mock environment. The documented command exited successfully in our check, running one episode and recording one System-2 rejection and zero module publications.

**Requirements and evidence.** English. The mock uses Python and core dependencies, with no GPU or API key. Benchmark runs need S1/S2 endpoints and the relevant environment dependencies and assets. Check [the split protocol](https://github.com/usail-hkust/JevRSI/blob/825a4e83e6c6805c7b7255d514e62b3668a20a76/scripts/run_protocol.py#L234) before interpreting ID/OOD scores. Under the official profile, each split starts from a copy of the same training snapshot and can continue evolving by default. [§4.3](https://arxiv.org/html/2611.22432v3#S4.SS3) reports S1 model-call latency, evaluation token expenditure and training-time S2 activity separately.

<a id="hookevo"></a>

### [HookEvo](https://github.com/HuangShengZeBlueSky/HookEvo) · [paper](https://arxiv.org/abs/2611.27294)

**Related self-improvement mechanism · coordinated runtime plugins.** A separate improver reads execution traces and proposes changes to a frozen executor's harness. A patch can coordinate how one hook records a tool result and how another uses it in a later action. The controller compares the candidate and parent on matched tasks. The retained harness and comparison feedback carry into the next round.

**Recommended entry.** Read [§3](https://arxiv.org/html/2611.27294v1#Sx3) and [Algorithm 1](https://arxiv.org/html/2611.27294v1#Sx6.SSx3), then follow an ALFWorld receipt into the episode state and a later action check in the [released plugin](https://github.com/HuangShengZeBlueSky/HookEvo/blob/6322d7448b297a1553b79b3532a429aacd9ade36/artifacts/alfworld/plugins/action-hint.mjs). Read the [search controller](https://github.com/HuangShengZeBlueSky/HookEvo/blob/6322d7448b297a1553b79b3532a429aacd9ade36/evolution/src/dsh_evolve/abc.py#L243) to see where candidate scores and hook changes determine promotion.

**Requirements and evidence.** English. The [synthetic smoke example](https://github.com/HuangShengZeBlueSky/HookEvo/blob/6322d7448b297a1553b79b3532a429aacd9ade36/README.md#installation) runs a scripted actor and toy task with the actual DeepSeek Harness runtime. It needs Linux or macOS, Python 3.10–3.12 and Node.js 22.19+ with npm. A model account is unnecessary. In our check, all three edit scopes (A/B/C) passed. The pinned release includes the controller and selected ALFWorld, DBBench and WebShop harnesses. For the reported OSBench narrow run it supplies 80 training task IDs. The README's linked reproduction guide was absent at this revision. [Table 2](https://arxiv.org/html/2611.27294v1#Sx4.T2) reports 70.56% versus 64.11% for the local Life-Harness rerun on DBBench, across 300 test tasks and three executions. The authors report the checkpoint with the highest observed test mean.

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

<a id="care"></a>

### [CARE](https://arxiv.org/abs/2611.02839) — production-loop reading

**Related self-improvement mechanism.** Read [§3.3 → §5 → §§6.1–6.3 → §7](https://arxiv.org/html/2611.02839v1): separate model faults from component faults, construct repairs at the first wrong decision, then study teacher-only hindsight and candidate promotion. The current model supplies experience and the self-teacher; external models diagnose failures and people approve deployment. This entry teaches a bounded production learning loop.

**Requirements.** English; distillation and agent fundamentals. Reading needs no API. No public reproduction package was verified on **2026-11-04**; reproducing the loop requires business traces, versioned policies, simulation / inspection infrastructure and model training. No minimum hardware recommendation is established here.

<a id="jomoha"></a>

### [JoMoHa](https://github.com/xudongwu-0/coevolve) · [paper](https://arxiv.org/abs/2611.11499)

**Recursive improvement method · joint policy training.** An Engineer generates an executable harness; the Solver acts under it. Their shared task outcome trains both policies on their own generated tokens, so later harness construction uses an updated Engineer alongside the updated Solver. The RL implementation, environment and validation / fallback rules remain fixed.

**Recommended entry.** Read [§4 → §§5.1–5.3 → §6.2](https://arxiv.org/html/2611.11499v1), then [paired rollouts](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/whale_local/sao_bridge/joint_workflow.py) → [partner weighting](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/whale_local/sao_bridge/joint_updates.py) → [role scheduling](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/whale_local/sao_bridge/joint_schedule.py). Start from the pinned checkout with the documented [offline evidence audit](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/docs/REPRODUCE_MA_SAO.md):

```bash
python3 -B scripts/reproduce_ma_progress.py --best97
```

Python ≥3.10 and the standard library suffice; this checks released files and recomputes archived outcomes without models, APIs, GPUs or initialized submodules. The official archive identifies selection/evaluation overlap: `best97` is 194/200 on reused development data, while Full144's 186/200 belongs to a different run. Treat this as result inspection, not a new held-out evaluation.

**Requirements for new runs.** Follow [source restoration](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/docs/REPRODUCE_MA_SAO.md#restoring-the-training-source) and the [benchmark guide](https://github.com/xudongwu-0/coevolve/blob/5d6c7fdbff3b65d3fbb60e68cd68b4d9042f5cf6/docs/BENCHMARK_IMPLEMENTATIONS.md): pinned submodules, patched AReaL, task assets and GPU inference / training. The recorded 9B stack uses Python 3.12, PyTorch 2.10.0+cu129 and vLLM 0.19.1; the Full144 run used two eight-GPU nodes, not a verified minimum. Released best97 actors total about 35.09 GiB and omit critics / optimizer state needed for training continuation; historical launchers require environment-specific configuration.

<a id="ace-rl"></a>

### [ACE-RL: Experience-Handoff Reinforcement Learning](https://arxiv.org/abs/2611.16409) · [author repository](https://github.com/doyoungkim-ml/ehrl)

**Related self-improvement mechanism · learning to write useful experience.** A shared model learns acting, reflection and playbook editing under a fixed ACE harness. During training, a candidate playbook receives credit from a fresh actor rollout; at inference, the next attempt reads the edited playbook with weights frozen. The memory is local to one task, rather than a cross-task experience bank.

**Recommended entry.** Read [§§2.1–2.2 → §§3.1–3.2 / Algorithm 1 → §4.2 and §5.2](https://arxiv.org/pdf/2611.16409v1). Trace which role receives which reward, then compare actor-only RL inside the same harness. Use Appendix C for role prompts and Appendices E / F.1 / H for evaluation and cost accounting. Equal actor-episode counts still leave extra reflection / curation calls; the paper's compute comparison counts update FLOPs, not total generation cost. Compare with the [ACE practice entry](#ace) to distinguish learning a writer from retaining its output.

**Requirements and release status.** English; RL and agent fundamentals; reading needs no compute. The [verified repository snapshot](https://github.com/doyoungkim-ml/ehrl/tree/f2d04dc4c8be112db0456b423a8518903ab80fab) contains a README and paper, with implementation announced. There is no runnable training entry at this snapshot. Table 5 reports two H100/H200 GPUs per experiment; this is the authors' setup, not a verified minimum.

<a id="no-second-run"></a>

### [No Second Run: Does RSI Stop at Frontier Pre-training?](https://arxiv.org/abs/2611.10719) · [801-30B repository](https://github.com/GAIR-NLP/801-30B)

**Engineering report · improvement within a pre-training project.** Learn how teams split a long training run into smaller loops: infrastructure / data debugging, post-training-headroom measurement, and conversion of experience into measurable data-pipeline criteria. Shared records retain rejected hypotheses and diagnoses for subsequent work. The improving system includes researchers, agents and infrastructure.

**Recommended entry.** Read [§2 / Table 2 → §3.3 → §4.1 → §5](https://arxiv.org/html/2611.10719v1), then §8.1 for the evaluation protocol. For each loop, identify the trial, feedback and retained artifact. Compare base models under the same SFT protocol; the separate comparison with vendor post-trained models is a headroom reference, not matched training. The report studies one full pre-training project, not repeated autonomous end-to-end training cycles.

**Requirements and release status.** English; pre-training and evaluation fundamentals; reading needs no hardware. The [verified repository](https://github.com/GAIR-NLP/801-30B/tree/8b5dc7dc50abf1b896afa8e0488dc081006e243b) supplies the report and figures and links a Tiny-SFT dataset; its README still marks base weights as forthcoming. A full training / improvement pipeline is not present in this snapshot. The reported 30B-total / 3B-active model used 11.8T tokens over three months; this is a research case study, not a small runnable tutorial.

<a id="esi"></a>

### [ESI](https://github.com/ZERITH-ZLab/ESI) · [paper](https://arxiv.org/abs/2611.18176)

**Related self-improvement mechanism · embodied policy learning.** Teacher corrections and useful student actions become replay data for the next robot-policy update. The design also revises guidance and skills with the LLM frozen; the reported three-round VLA experiment keeps prompts and the skill catalog fixed across policy updates.

**Recommended entry.** Read [§§3.4, 4.3 → §§5.3–5.5 → §6.1](https://arxiv.org/html/2611.18176v1), then follow the Chinese [installation](https://github.com/ZERITH-ZLab/ESI/blob/bc29d46f38378eb5058aeab40397f5a44c494eb2/docs/INSTALLATION.md) and [configuration](https://github.com/ZERITH-ZLab/ESI/blob/bc29d46f38378eb5058aeab40397f5a44c494eb2/docs/CONFIGURATION.md) guides. Configure the single-worker deployment template and preview from the repository root:

```bash
bash scripts/eval.sh --set run.name=esi_preview --show-config
```

This resolves configuration without launching models, SSH or simulation. Follow `collect.sh` → `annotate.sh` → `data.sh` → `train.sh`, then explicitly pass the new checkpoint to the next collection round. Optional [prompt evolution](https://github.com/ZERITH-ZLab/ESI/blob/bc29d46f38378eb5058aeab40397f5a44c494eb2/hybrid_rollout/robodojo/prompt_evolution/README.md) publishes a reviewed bundle selected by hash for a later run; automatic updates are disabled by default. Appendix C distinguishes collection-suite evaluation from the transfer case study.

**Requirements.** Bilingual README / Chinese deployment guides; Linux, Python 3.11, separate simulator and OpenPI environments, pinned RoboDojo / Isaac Sim 5.1.0 dependencies, assets, RTX rendering GPU, policy compute and model-account access. Deployment uses SSH even locally; multiple nodes need shared storage at matching paths. The [released model](https://huggingface.co/Embodied-Self-Improvement/ESI-pi05) is approximately 11.6 GiB. Training's 8/16-GPU templates are examples, not verified minima.

<a id="recurir"></a>

### [RecurIR: Learning When and How to Revise Restoration Policies](https://arxiv.org/abs/2611.18006)

**Recursive improvement method · paper reading.** A learned revision operator changes tool selection, order, strength and image regions when degradation conditions shift. Accepted updates improve both the restoration policy and its revision mechanism, which guide the next round of hypothesis discovery and task generation. The restoration-tool library stays frozen; transfer and retention checks control acceptance.

**Recommended entry.** Read [§§3.1–3.4 → §4.4 → §§7.3–7.4 and 8.2](https://arxiv.org/html/2611.18006v1). Follow a conditional rule through matched tool comparisons, targeted counterexamples, learned revision and acceptance. Separate the learned gate deciding whether to edit a plan from the validation gate deciding whether to retain a policy update. Reference images provide training supervision; inference estimates degradation conditions without those references.

**Requirements and release status.** English; image restoration and policy-learning fundamentals; reading only. No official implementation or launch command was verified on **2026-11-16**. Section 7.3 refers to MAIR settings and a shared pretrained tool library; reproducing the loop additionally requires restoration datasets, controlled degradation generation and revision training. A tested environment or minimum hardware requirement is not established by this directory.

<a id="g-cast"></a>

### [G-CAST: Governed Continual Self-Training](https://arxiv.org/abs/2611.17814)

**Related self-improvement mechanism · production training case study.** An accepted checkpoint generates trajectories that are routed to SFT, RL or regression monitoring. Contract changes and scoring errors trigger validated revisions of executable training rewards; accepted checkpoints and reward versions carry into later rounds. Product requirements and the promotion procedure remain externally specified, with human reward audits still part of the system.

**Recommended entry.** Read [§3 / Table 1 → §4 → §5 / Tables 2–4](https://arxiv.org/html/2611.17814v1). Trace one rollout through routing, training and checkpoint admission. Distinguish the evolving training reward from the common frozen evaluation reward, then compare new-demand adaptation with retained performance on earlier periods. The cumulative evaluation slices also govern promotion; they are not a separately untouched final test.

**Requirements.** English; SFT / RL and agent-evaluation fundamentals; paper reading. No official runnable implementation was verified in this review. The study uses Qwen3-4B-Thinking-2507, production queries, eight rollouts per query and versioned business tools; reading needs no compute, while reproduction requires the application data, reward rules and training infrastructure. No public minimum hardware configuration was verified.

<a id="basersi"></a>

### [BaseRSI](https://github.com/beita6969/BaseRSI) · [paper](https://arxiv.org/abs/2611.24578)

**Related self-improvement mechanism · harness internalization.** The stock Qwen3.8-27B proposes and evaluates harness entries. The inner loop compiles accepted entries into a patch embedding and selected MLP weights through forward passes and regression. A student with the previous edit generates responses for a later refit under a fixed procedure. The published pipeline uses the original checkpoint for outer-loop proposals and exports an edited checkpoint that answers with the original input.

**Recommended entry.** Read [§§4.1–4.3](https://arxiv.org/html/2611.24578v1#S4) and trace [the pipeline](https://github.com/beita6969/BaseRSI/blob/ecafed335b96298b46a864b8004af5f0c8a8bd55/basersi/config/pipeline.yaml) from data preparation and entry acceptance to the [student replay and refits](https://github.com/beita6969/BaseRSI/blob/ecafed335b96298b46a864b8004af5f0c8a8bd55/basersi/procedure_edit/rounds.py#L460). Install the package from the pinned checkout to inspect the stage list:

```bash
python -m pip install .
basersi pipeline --list
```

**Requirements and evidence.** English. Python 3.12 for the preview. With the source extra and the pinned benchmark files, the [data stage](https://github.com/beita6969/BaseRSI/blob/ecafed335b96298b46a864b8004af5f0c8a8bd55/README.md#running) can prepare the 640 development items without loading a model. The full pipeline adds the stock 27B checkpoint, the GPU extra and 80 GB cards in the documented setup. The authors report 45.5 H800 GPU-hours for the improvement run with zero external API tokens. They reuse one improved checkpoint for three test-sampling seeds and separate fitting and validation from 640 ID and 640 OOD test items. The released workflow ends with checkpoint export and acceptance on development data. The [edited weights](https://huggingface.co/beita6969/BaseRSI-27B) and [test data](https://huggingface.co/datasets/beita6969/BaseRSI-Dataset) are available separately. [Appendix D](https://arxiv.org/html/2611.24578v1#A4)

<a id="automaster"></a>

### [AutoMaster](https://github.com/RUCAIBox/AutoMaster) · [paper](https://arxiv.org/abs/2611.26510)

**Related self-improvement mechanism · skill-guided post-training.** An LLM research agent designs skills for a fixed teacher, tests them in pilot rollouts and selects demonstrations for SFT. Student scores and trajectories guide the next round's skills and data selection. Every student starts from the same initial checkpoint and is evaluated without the generated skills.

**Recommended entry.** Read [§§3.1–3.3 and §5.2](https://arxiv.org/html/2611.26510v2), then use the [behavioral examples](https://github.com/RUCAIBox/AutoMaster/blob/116c295dfdb7729e8f8684d85dea867c5fd9806e/docs/method.md#behavioral-shaping-in-practice) to compare what the teacher demonstrates with what the verifier scores. Trace how skill context is retained in SFT inputs while supervision stays on the assistant outputs.

**Requirements and evidence.** English. Reading the examples requires no model. To evaluate a [released student checkpoint](https://huggingface.co/collections/RUC-AIBOX/automaster) with the [Doc2Repo recipe](https://github.com/RUCAIBox/AutoMaster/blob/116c295dfdb7729e8f8684d85dea867c5fd9806e/recipes/inference/README.md), use Python 3.11+, the pinned AweAgent submodule, an OpenAI-compatible endpoint or a local SGLang deployment, Docker and benchmark assets. The release covers skills and inference, while the research controller, teacher rollout service and SFT orchestration are outside the release. [Table 1](https://arxiv.org/html/2611.26510v2#S4.SS2) reports mean gains of 1.42–8.99 percentage points across six benchmark/model settings against Vanilla SFT, controlling for the teacher, task pool, demonstration count and SFT recipe. This comparison controls the SFT setup while AutoMaster additionally searches over teacher interventions across rounds.

<a id="finevo"></a>

### [FinEvo](https://github.com/pcj-sudo/FinEvo) · [paper](https://arxiv.org/abs/2611.28239)

**Related self-improvement mechanism · solver-guided curriculum.** Use fresh solver attempts to decide which spreadsheet challenges to harden or repair. An executable verifier checks target cells and supplies a binary task reward. FinEvo then uses rollouts on the selected tasks for synchronous GRPO. The reported study evaluates one challenge-generation and policy-learning cycle.

**Recommended entry.** Start with [the twenty released examples](https://github.com/pcj-sudo/FinEvo/blob/c94868d3246047e4dbd04133a5e72ccc34831baa/examples/README.md). Compare one modeling task and one formula-repair task. Identify what the solver sees and what the verifier checks. Then read [§§3.2–3.3 and §4.3](https://arxiv.org/html/2611.28239v1) for curriculum selection, on-policy training and held-out scoring.

**Requirements and evidence.** Chinese and English docs. The official [release check](https://github.com/pcj-sudo/FinEvo/blob/c94868d3246047e4dbd04133a5e72ccc34831baa/README.md#2-validate-the-example) passed on Python 3.12, checking 20 task packages, file hashes and the synchronous training configuration. It validates artifacts without recalculating workbooks or calling a model. Solver runs need Docker, LibreOffice and a model endpoint. The [training guide](https://github.com/pcj-sudo/FinEvo/blob/c94868d3246047e4dbd04133a5e72ccc34831baa/training/README.md) uses six eight-GPU nodes. The paper's 88 training and 22 held-out tasks come from 11 source workbooks. The release contains two example workbooks and their tasks.

<a id="memory-skills"></a>

## Memory and Skills

<a id="agent-qa"></a>

### [agent-qa](https://vostride.com) · [code](https://github.com/vostride/agent-qa)

**Related self-improvement mechanism.** Inspect persistent memidex app memory for web, Android and iOS QA. Run evidence becomes candidates for reusable facts, cautions and procedures; admission gates control what later runs can trust. The updated object is app knowledge, not model weights or the improvement implementation. CI proposes candidates only.

**Recommended entry.** Read the [memory](https://vostride.com/docs/agent-qa/memory) and [self-improvement](https://vostride.com/docs/agent-qa/self-improvement) docs, then trace the pinned v0.3.1 [promotion gate](https://github.com/vostride/agent-qa/blob/2d56b09304b000034a1ab1c9a5ef2fb4c546c66e/packages/knowledge-local/src/curator/commit.ts#L1181) → [staged-file write](https://github.com/vostride/agent-qa/blob/2d56b09304b000034a1ab1c9a5ef2fb4c546c66e/packages/knowledge-local/src/bundle-publish.ts#L199) → [durable publication](https://github.com/vostride/agent-qa/blob/2d56b09304b000034a1ab1c9a5ef2fb4c546c66e/packages/knowledge-local/src/bundle-publish.ts#L312). Follow candidate evidence, admission outcomes and retained files; the docs explain how later runs receive relevant records.

**Language and requirements.** English; this source-reading route needs only a browser. Execution requires [Node.js ≥24](https://github.com/vostride/agent-qa/blob/2d56b09304b000034a1ab1c9a5ef2fb4c546c66e/package.json), a configured model provider and target-specific app setup. [FSL-1.1-ALv2](https://github.com/vostride/agent-qa/blob/2d56b09304b000034a1ab1c9a5ef2fb4c546c66e/LICENSE.md); model/API and environment costs are separate. Sources reviewed on 2026-11-07; no installation, runtime test, benchmark reproduction or measured memory-benefit claim.

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

<a id="evorepair"></a>

### [EvoRepair](https://github.com/iSEngLab/Learn-from-Repair-Experience) · [paper](https://arxiv.org/abs/2605.30105)

**Related self-improvement mechanism · repair experience.** Start with [paper §III → §VI-A](https://arxiv.org/html/2605.30105v3), then [multi_turn_runner.py](https://github.com/iSEngLab/Learn-from-Repair-Experience/blob/d0d885513e750d3c5bbed183e839f0c709dfbf60/multi_turn_runner.py) and `expbank/`: repair → experience extraction / scoring → database update → later retrieval. The retained experience bank evolves under a fixed orchestration process. Compare with [ACE](#ace); track same-instance learning separately from cross-vulnerability transfer.

**Running entry.** Follow the [pinned setup](https://github.com/iSEngLab/Learn-from-Repair-Experience/blob/d0d885513e750d3c5bbed183e839f0c709dfbf60/README.md), configure both extraction and repair endpoints, and prepare the embedding model and evaluation images. First inspect one bounded configuration:

```bash
python multi_turn_runner.py -o output_preview -n 1 --workers 1 --eval-workers 1 --dry-run
```

This validates configuration rather than repairing a vulnerability. For real runs, explicitly set `-o` and `-n`: the source requires an output directory, and omitting `-n` enables automatic iteration. Start with baseline mode to build `turn_1/cold-start/vec_DB`, then pass that path through `--exp-db` in a separate retrieve-only run. Despite its name, retrieve-only updates the bank after each turn. The [embedding downloader](https://github.com/iSEngLab/Learn-from-Repair-Experience/blob/d0d885513e750d3c5bbed183e839f0c709dfbf60/expbank/script/download_model.py) requires a model repository argument and `--local-dir`; align that directory with the runner configuration instead of copying the README's argument-free command.

**Requirements.** English; [Python ≥3.10](https://github.com/iSEngLab/Learn-from-Repair-Experience/blob/d0d885513e750d3c5bbed183e839f0c709dfbf60/pyproject.toml), API budget, local embedding dependencies and Docker. Upstream recommends at least **500 GB** free space for the full 230-image PatchEval set; a smaller task subset needs its corresponding images. No training-GPU minimum was verified.

<a id="specforge"></a>

### [SpecForge · ccsnow127](https://github.com/ccsnow127/SpecForge) · [paper](https://arxiv.org/abs/2610.15708)

**Related self-improvement mechanism · reusable behavioral specifications.** Test failures refine natural-language descriptions of functions and classes; the descriptions then guide new code generation. Learn how a Pareto archive, dependency-aware entity selection and different failure subsets reduce interference between edits. The search procedure and model weights stay fixed.

**Recommended entry.** Read [§§2–3 → §4.5](https://arxiv.org/html/2610.15708v1), then the [two-stage README](https://github.com/ccsnow127/SpecForge/blob/5ed001d759fb5db408308c367e1ae25d238f31df/README.md) and [runner](https://github.com/ccsnow127/SpecForge/blob/5ed001d759fb5db408308c367e1ae25d238f31df/scripts/run_specforge.py). At that revision, install `python -m pip install -r requirements.txt` in a virtual environment and set `OPENAI_API_KEY` for the documented example:

```bash
python scripts/generate_llm_tests.py \
  --module data/deveval_plus/stocktrends/indicators.py \
  --model gpt-4o --branch-coverage 0.90
python scripts/run_specforge.py \
  --module data/deveval_plus/stocktrends/indicators.py \
  --model gpt-4o --output-dir artifacts/quickstart
```

Stage 1 checks generated tests against the reference implementation. Confirm that Stage 2 prints `LLM-generated` for `Search-time tests`: if those tests are missing, the runner falls back to ground-truth tests, exposing final-evaluation information during search. `--no-llm-tests` also uses ground truth for both stages. Inspect `nodes/` for revised specifications and failures, then `result.json` / `summary.json` for evaluation and usage.

**Requirements.** English; Python, [repository dependencies](https://github.com/ccsnow127/SpecForge/blob/5ed001d759fb5db408308c367e1ae25d238f31df/requirements.txt) and model API budget; no explicit minimum Python version was verified. This example uses local test execution and hosted inference rather than weight training. Use a disposable workspace because generated code executes locally. Default search settings are budget 50 and width 3; test synthesis and other stages also make calls, so this is not an end-to-end spending cap. Python → Java transfer adds JDK / Maven. Use this exact repository; other projects share the SpecForge name.

<a id="roboscript"></a>

### [RoboScript](https://github.com/ArcheOne-AI/RoboScript) · [paper](https://arxiv.org/abs/2611.12885)

**Related self-improvement mechanism · embodied skills and memory.** A fixed driver accepts executable skills from demonstration gaps, then freezes the skillset. Rehearsal builds Task Memory; later reflection adds guidance for new evaluation blocks. Model weights and the driver stay fixed.

**Recommended entry.** Read [§4.1 and Appendix C.2 → §§4.2, 4.4, 5.5](https://arxiv.org/pdf/2611.12885v1), then the [Mock tutorial](https://github.com/ArcheOne-AI/RoboScript/blob/fad0496a773ea9fee66addf43e44af5095982b78/examples/tutorials/quickstart_mock/README.md). From the fixed revision's root:

```bash
uv sync --all-packages
cd examples/tutorials
uv run python -m quickstart_mock.run ../../tmp/quickstart
```

This CPU example uses `ScriptedBrain` without a model or simulator. It deliberately holds still, so `success=False` is expected. Inspect `events.jsonl` to learn tool visibility, action budgets and the environment's independent verdict; this is not a learning run.

Continue with the [skill builder's gates](https://github.com/ArcheOne-AI/RoboScript/blob/fad0496a773ea9fee66addf43e44af5095982b78/packages/methods/src/roboscript_methods/skill_builder/builder/README.md) → [RoboTwin build / freeze entry](https://github.com/ArcheOne-AI/RoboScript/blob/fad0496a773ea9fee66addf43e44af5095982b78/examples/simBenchmarks/RoboTwin/p1/README.md), and [learning stages](https://github.com/ArcheOne-AI/RoboScript/blob/fad0496a773ea9fee66addf43e44af5095982b78/docs/concepts/learning.md). Compare skill acceptance with memory revision and reflection; skills freeze before task learning.

**Requirements.** English; Python **≥3.10** and uv for the tutorial. Real skill building adds Linux / bubblewrap, the pinned RoboTwin 2.0 simulator in a separate environment, demonstrations, cuRobo / vision GPU services and model-gateway credentials / budget. The [vision service's approximately 8 GiB](https://github.com/ArcheOne-AI/RoboScript/blob/fad0496a773ea9fee66addf43e44af5095982b78/packages/vision/README.md) is component usage, not a whole-pipeline minimum. Real-robot deployment code remains on the upstream TODO list.

<a id="mixua"></a>

### [MixUA: Who Remembers What?](https://arxiv.org/abs/2611.10439)

**Related self-improvement mechanism · paper reading.** Learn how independent users and agents share experience through four memory scopes: Pair, User, Agent and Global. A fixed writing / retrieval pipeline retains lessons across rounds; protected evidence is routed separately from shareable evidence. Model weights and the memory-update procedure are not evolved.

**Recommended entry.** Read [§§3.2–3.4 → §4 → §5.3](https://arxiv.org/html/2611.10439v1), then Appendix C's population-learning algorithm and Appendix G's disclosure matrix. Trace one lesson from a trajectory into its permitted audience, then compare a frozen store on held-out tasks with the learning rounds. CrossLearnBench measures task success, preference retention and planted-fact leakage separately. Its privacy probes test the stated boundary contract; they are not a general privacy guarantee.

**Requirements.** English; reading only. No official runnable implementation or standalone reproduction entry was verified. Appendix D describes Linux / Python 3.12, Harbor task containers, several model / agent services and an embedding service; these are the study's configuration, not a verified minimum setup. Read its full-cost accounting before attempting a reproduction: table cost columns include only the writer on the memory side, while other memory operations also incur cost.

<a id="wikitrace"></a>

### [WikiTrace](https://github.com/yukyeongleee/wikitrace) · [paper](https://arxiv.org/abs/2611.14320)

**Related self-improvement mechanism · evidence-linked memory.** A compiler extracts insights from training runs and links each insight to a summary and the original trajectory. During later tasks the agent can check the evidence and reconsider how a lesson applies. The corpus is built once and mounted read-only during testing, with the model and memory construction procedure fixed.

**Recommended entry.** Read [§§3.1, 3.3–3.4 → §§4.1, 4.3 → Appendix B](https://arxiv.org/html/2611.14320v1). Follow an insight to the source outcome and tool observations, then trace the [memory layout](https://github.com/yukyeongleee/wikitrace/blob/dc06570f2fc69e20d36fede62128a806e35edfcd/src/wikitrace/memory/README.md) and [read-only mounting](https://github.com/yukyeongleee/wikitrace/blob/dc06570f2fc69e20d36fede62128a806e35edfcd/src/wikitrace/memory/mount.py). After [repository setup](https://github.com/yukyeongleee/wikitrace/blob/dc06570f2fc69e20d36fede62128a806e35edfcd/README.md#install) and the ALFWorld installer, follow the documented suite example from the repository root:

```bash
uv run wikitrace build --config configs/alfworld.yaml --benchmark alfworld --suite valid-seen --trial 0
uv run wikitrace run --config configs/alfworld.yaml --benchmark alfworld --suite valid-seen --trial 0 --method wikitrace
```

**Requirements and evaluation.** English. Python ≥3.11, uv, Node 20, Docker, ALFWorld assets and OpenRouter access with call budget. The sample commands build one trial's corpus and evaluate a suite. The paper uses 50 training games and 101 test games for `valid-seen`. Start with the source walkthrough if you want to avoid model calls. The [analysis guide](https://github.com/yukyeongleee/wikitrace/blob/dc06570f2fc69e20d36fede62128a806e35edfcd/src/wikitrace/analysis/README.md) requires matched rows across methods and three no-memory trials for the reference majority. Compare newly solved tasks (Gain) and lost successes (Regression), then use additional no-memory reruns to estimate ordinary variation.

<a id="altk-evolve"></a>

### [ALTK-Evolve](https://github.com/AgentToolkit/altk-evolve) · [deployment study](https://arxiv.org/abs/2611.26361)

**Related self-improvement mechanism · reusable procedural memory.** The same model acts, extracts lessons from its training trajectories and merges equivalent advice. Later runs receive all guidelines or a selected subset. Model weights and the extraction and consolidation procedure stay fixed.

**Recommended entry.** Follow the [arithmetic agent tutorial](https://github.com/AgentToolkit/altk-evolve/blob/03f83be7480bf0be3f4aa6e868b832486e064718/docs/tutorials/guidelines-loop.md). Trace a run into local Phoenix, sync it to a filesystem namespace, list the stored guideline entities, then inspect which guidelines a fresh run receives. The task demonstrates the handoff between runs. To study effectiveness, read *The System* → *Measurement Setting* → *Insights 1, 3, 5 and 6* in the [paper](https://arxiv.org/html/2611.26361v1).

**Requirements and evidence.** English. The tutorial uses Python ≥3.12, uv, local Phoenix, an embedding backend and model access. It uses a filesystem store and needs no AppWorld data. The study mines from AppWorld train/dev and reports a fixed injection rule alongside configurations selected on `test_normal`. Check the chosen memory size, repeat variation and per-task tokens. In the ACE comparison, the no-memory baselines use different scaffolds, so the headline score gap includes scaffold effects.

<a id="perplexity-skills"></a>

### [Perplexity: Self-improving skills](https://www.perplexity.ai/en-GB/hub/blog/self-improving-skills)

**Related self-improvement mechanism · production case study.** Perplexity's Brain uses session traces to propose procedural skill changes. Personal updates undergo eligibility and version checks before activation for later sessions. Shared built-in updates undergo paired replay against failure and control scenarios, followed by engineer approval. The retained asset is the skill used in subsequent sessions.

**Recommended entry.** Read Figures 2, 4 and 5, then the production experiment and offline results. Use Figure 5 to see how replay can catch regressions outside the targeted scenario. The eight-week randomized test reports tool-failure and user-dissatisfaction outcomes. The separate offline skill comparison uses 16 paired instances across nine task families. [Author report](https://www.perplexity.ai/en-GB/hub/blog/self-improving-skills)

**Requirements.** English. Reading needs only a browser. The post describes internal implementation and experiments. For a separate public evaluation exercise, inspect one task and its evaluation dimensions in the benchmark the authors reference. [SkillLearnBench at `726e1f7`](https://github.com/cxcscmu/SkillLearnBench/blob/726e1f79b96b0cb3d729d0e55a1c847e0b5353ae/README.md#2-evaluation-dimensions)

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

<a id="mas-loop"></a>

### [MAS-Loop](https://arxiv.org/abs/2610.38946) — method reading

**Recursive improvement method · learned refinement policy.** The Orchestrator builds a multi-agent graph; the Refiner diagnoses its trajectory and patches roles, connections or execution settings. Re-execution supplies rewards to train both policies, so the learned Refiner participates in later improvements. The RL update rule and task evaluator stay fixed. Pair with the [co-evolution survey](../README.md#coevolution-survey); compare the learned Refiner with [EAT](#eat)'s team-editing supervisor.

**Recommended entry.** Read [§§3.1–3.3 → Algorithm 1 in Appendix B → Appendix D.1](https://arxiv.org/html/2610.38946v1): structured patch → source / revised execution pair → separate policy rewards → execution-budget-matched comparison.

**Language and running requirements.** English; multi-agent systems and RL fundamentals. No official code or runnable command was confirmed in the paper and targeted search on **2026-11-01**. Appendix C.3 reports verl, two trainable Qwen3-8B policies, a frozen Qwen3-30B-A3B executor and **8 × H100**; this describes the experiment, not a verified minimum. Reading requires no model calls.

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

<a id="rsi-anything"></a>

### [RSI-Anything · Gen-Verse](https://github.com/Gen-Verse/RSI-Anything) · [paper](https://arxiv.org/abs/2610.13912)

**Related self-improvement mechanism · policy–world-model co-adaptation.** A policy proposes actions, a world model predicts consequences, and observed feedback supports persistent updates. The GUI implementation updates both components under fixed training and selection rules; follow retained checkpoints into later interaction, without assuming that the update algorithm rewrites itself.

**Recommended entry.** Read [paper §§2.3–2.5 → Table 4](https://arxiv.org/html/2610.13912v1) → [GUI guide](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/README.md) → [`rsi.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/rsi.py) → [`policy_train.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/policy_train.py) / [`gui_world.py`](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/tasks/gui/src/rsi_anything_gui/gui_world.py). Trace successful-action SFT plus replay, world-model updates from browser transitions and expert continuations, then development-set promotion of the policy/model pair. Both candidate generations freeze before crossed policy/world tests. The reported selected controller uses `alpha=0` (policy ranking); distinguish it from pure world-model ranking.

Start with this CPU browser check from a pinned checkout. Install the shared CLI and browser runtime in separate environments:

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

This executes rule-controlled checkbox actions in Chromium, with no model credentials or GPU. It checks the environment and report path, not learning or RSI performance. On Linux, missing browser system libraries require the Playwright dependencies described in the GUI guide.

**Language and running requirements.** English guides and a Chinese README. Full GUI training uses Linux, Python 3.10, CUDA and roughly **22 GB** of base-model downloads, plus storage for traces and checkpoints. The default assigns **three GPUs** to separate roles; A800 80 GB is the recorded environment, not a verified minimum. Follow the GUI guide for model acquisition, resource configuration and the full workflow. The separate [code-repair route](https://github.com/Gen-Verse/RSI-Anything/blob/8ba44cd73ec6f57b151ec06e2f71a0726adfb687/docs/reproduction.en.md) keeps the coder fixed; its evaluation entry does not update parameters.

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

<a id="metr-acceleration"></a>

### [METR: AI R&D Acceleration Assessment](https://metr.org/blog/2026-11-05-anthropic-ai-rd-acceleration-assessment/) — research reading

**Evaluation reading.** This November 5 report assesses Anthropic's October 2026 research progress. Read Key findings → Appendices: Methodology / Benchmark scores (AECI) → Limitations. Distinguish historical, current and counterfactual growth, then separate measured acceleration from attribution to AI use.

**Requirements.** English; basic statistics; no runtime or API. Some underlying evidence is private or redacted, so the public report is not a complete reproduction package or a demonstration of autonomous RSI.

<a id="rsi-tax"></a>

### [The RSI Tax: When Recursive Self-Improvement Is Not Worth the Cost](https://arxiv.org/abs/2611.13524) — evaluation reading

**Evaluation reading · accounting for improvement overhead.** Learn to compare task accuracy against total tokens, including the calls spent verifying, exploring and writing updates. Rejected updates still incur cost. The paper adapts six methods to a common online protocol across two task streams and two model backbones; tasks are scored before their feedback can update later state. Its findings concern those configurations, rather than a universal ranking of RSI methods.

**Recommended entry.** Read [§§2.2–2.3 → §3 → §4 → §5.1](https://arxiv.org/html/2611.13524v1), then Appendix A.2–A.3 for update schedules and implementation choices. Contrast the total-cost accounting with SRN, a simple reflection-and-notes baseline. Use the [evaluation route](learning-guide.md#survey-project-map) to compare the starting agent, a lightweight notes baseline and a fuller improvement loop under the same task order and budget. Record task-execution and update tokens separately, retaining failed attempts. Whether an artifact is later used is descriptive evidence, not proof that it caused a gain or that unused work can be removed without affecting accuracy.

**Language and running requirements.** English; the paper is directly readable without compute. No official reproduction package or standalone execution entry was verified in this review. Reproducing its experiments would require the task environments and model access described in the paper; this entry is a reading exercise, not a runnable evaluation tool.

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

<a id="exlabel"></a>

### [ExLabel / SWE-TQ](https://github.com/ZJU-CTAG/ExLabel) · [paper](https://arxiv.org/abs/2610.39417)

**Evaluation tool · evolving assessment experience.** Learn to inspect the quality of the task and tests before using pass rates to judge agent improvement. ExLabel retains assessment experience from labeled training cases and retrieves it for later judgments; it does not rewrite its learning algorithm. Pair with the [coding-agent survey's feedback / evaluation chapters](../README.md#coding-agents-survey).

**Recommended entry.** Read [§2.1 → §§3.1–3.2 → §4](https://arxiv.org/html/2610.39417v1), then [core/app.py](https://github.com/ZJU-CTAG/ExLabel/blob/cef7b443ce2f991f721f1975d266e286b911c1b2/core/app.py) → [core/agent/agent.py](https://github.com/ZJU-CTAG/ExLabel/blob/cef7b443ce2f991f721f1975d266e286b911c1b2/core/agent/agent.py). Follow `accumulation` on `train` into saved memories, then `inference` on `test`. Assessments use task / patch text; they do not replace executing a candidate solution's tests.

**Running entry and requirements.** Follow the [pinned setup and two-stage commands](https://github.com/ZJU-CTAG/ExLabel/blob/cef7b443ce2f991f721f1975d266e286b911c1b2/README.md). Use Python 3.12, the repository requirements, configured LLM / embedding endpoints and `API_KEY` / `EMBEDDER_API_KEY`. Start with the `issue` task and `data/SWE-bench-issue`; build a bank with `python core/app.py --mode accumulation`, then query the same bank with `--mode inference`, supplying the README's dataset, model, bank and experiment arguments. Banks are not bundled. A fresh accumulation run clears its target bank; use distinct paths for `issue` and `test`, keep the same embedder, and use a new experiment ID when changing settings because outputs resume by instance ID. Hosted endpoints need API budget but no local GPU training; downstream fine-tuning is a separate experiment. Source and commands were inspected, not executed.

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

<a id="clr-bench"></a>

### [CLR-Bench](https://github.com/yausankit/clr-bench) · [paper](https://arxiv.org/abs/2610.40758)

**Evaluation tool · rule learning from retained feedback.** Compare learning a category with memorizing its revealed members, then test unseen members and similar non-members. Connect [ACE](#ace)'s playbook updates to the [self-evolving-agent survey's evaluation branch](../README.md#self-evolving-agents).

**Recommended entry.** Read [§§3–5 → §7.2](https://arxiv.org/html/2610.40758v1), then follow the [bilingual README](https://github.com/yausankit/clr-bench/blob/098d2a36cc9cd362ffd63208b998c30376ea3fbe/README.md) and [run_condition.sh](https://github.com/yausankit/clr-bench/blob/098d2a36cc9cd362ffd63208b998c30376ea3fbe/harness/run_condition.sh): practice → retained state → test replay. Compare `self`, `hint` and raw-history conditions before attributing gains to the update method.

**Running entry and requirements.** Python 3.12. Start with the bundled TR1 reference program after installing the README dependencies:

```bash
python data/unpack_chains.py TR1
cd data/chains/TR1
python score_k1_v3.py --version 0 --program L1=controls/reference_L1.py --diagnostics
```

This local scorer executes the supplied reference program without a model API; it does not run agent learning. The [scorer's runner](https://github.com/yausankit/clr-bench/blob/098d2a36cc9cd362ffd63208b998c30376ea3fbe/data/chains/TR1/harness_k1_test/runner.py) uses local Python subprocesses, distinct from the full evaluation harness's Docker execution. Full method runs additionally need Docker, the upstream method dependencies and an OpenAI-compatible endpoint; follow the README's gateway and `harness/run_condition.sh` instructions. Constructing new probe-certified chains also calls a model. The repository's license is still marked undecided; inspect its terms before redistribution.

<a id="selfimprove-bench"></a>

### [SelfImprove-Bench](https://github.com/theseus-labs-rsi/SelfImprove-Bench) · [paper](https://arxiv.org/abs/2611.02797)

**Evaluation tool · generalization after adaptation.** Read [§§3.1–3.4 → §4.2](https://arxiv.org/html/2611.02797v1), then [the README](https://github.com/theseus-labs-rsi/SelfImprove-Bench/blob/99b07d7da9e2dda4bdd0b460ac58951c3c15108f/README.md). G0 checks encountered-instance retention; G1–G4 extend to unseen instances, difficulty, tasks and capabilities. Pair with [ACE](#ace) or [HyperAgents](#hyperagents), retaining initial and evolved evaluations on identical holdouts.

**Recommended entry.** After the documented Python **3.13.12** environment and requirements installation, follow [examples/minimal_rsi.py](https://github.com/theseus-labs-rsi/SelfImprove-Bench/blob/99b07d7da9e2dda4bdd0b460ac58951c3c15108f/examples/minimal_rsi.py):

```bash
python -m benchmark configs/examples/minimal_rsi.json
```

The example returns a fixed action and records refinement rounds; it makes no model calls and demonstrates lifecycle / state handling, not learned improvement. Then configure the method's model/backend in `rsi_methods/ACE/config.toml` and use the [Farm experiment](https://github.com/theseus-labs-rsi/SelfImprove-Bench/blob/99b07d7da9e2dda4bdd0b460ac58951c3c15108f/configs/main/farm_ace.json):

```bash
python -m benchmark configs/main/farm_ace.json --initial
python -m benchmark configs/main/farm_ace.json
```

**Requirements.** English; real methods require their backend credentials / CLI and model budget. Farm's main configuration has 20 adaptation tasks plus 60 holdouts and replay; it is not a one-call example. HyperAgents adds Docker; AHE needs Linux bubblewrap and unprivileged user namespaces; Minecraft / Astray add GameWorld and Chromium. Trajectory analysis also calls a model. No model-training GPU is required for the fixed-action example; inspect each backend before a full run.

<a id="flex-rsi"></a>

### [Flex-RSI](https://github.com/flex-rsi/rsi-bench) · [paper](https://arxiv.org/abs/2611.08946)

**Evaluation tool · separating executor and improver gains.** Compare `base` (executor only), `fixed-i` (improver changes the executor), and `full` (improver also changes itself). Learn which gains survive held-out evaluation under the same model, task and budget. The orchestrator, task definitions and evaluation splits remain fixed; test scores are produced after the run ends. This complements the [evaluation learning route](learning-guide.md#survey-project-map).

**Recommended entry.** Read [paper §§3.1–3.3 → §5.4](https://arxiv.org/html/2611.08946v1), then the [testing guide](https://github.com/flex-rsi/rsi-bench/blob/ebff61558d15dfd0ad64f636ca8318aec0386adb/docs/testing-guide.md) and [harness interfaces](https://github.com/flex-rsi/rsi-bench/blob/ebff61558d15dfd0ad64f636ca8318aec0386adb/docs/harness.md). At this revision, create a virtual environment and install `python -m pip install -e ".[all,tasks]"` using the [README setup](https://github.com/flex-rsi/rsi-bench/blob/ebff61558d15dfd0ad64f636ca8318aec0386adb/README.md). After task-data preparation and site configuration, the documented first check is:

```bash
rsib run new --task <task> --model mock:finish --mode base \
  --max-rounds 1 --budget wall_hours=0.5
rsib run start <worktree> --backend local
rsib report <worktree>
```

This checks the runtime and starter evaluation; it does not exercise model-driven improvement. Continue with a real model and compare the three modes. Reduced-budget exercises do not reproduce standard benchmark results.

**Language and running requirements.** English; Python ≥3.11, Git ≥2.30, Linux unprivileged user namespaces for the sandbox, task data, a compute profile, and model API access or an authenticated Claude Code / Codex CLI. [Spatial-VSI](https://github.com/flex-rsi/rsi-bench/blob/ebff61558d15dfd0ad64f636ca8318aec0386adb/docs/tasks.md#spatial-vsi) needs no local GPU but downloads about 5.4 GB and uses model calls. Other tasks require task-specific GPUs / containers; standard runs can take 10–72 hours. Public code is available; the result-submission channel was not yet open at review.

<a id="scale-rsi-bench"></a>

### [Scale RSI Bench · scaleapi/rsi-benchmark](https://github.com/scaleapi/rsi-benchmark) · [website](https://www.rsi-benchmark.com)

**Evaluation tool · AI R&D tasks.** The README's four public sample types cover self-distillation, jailbreak robustness, agent-swarm optimization, and nanoGPT data curation. Start by learning how a research task specifies editable artifacts, compute limits, and verification. These are task examples, not evidence that an agent has completed a recursive self-improvement cycle.

**Recommended entry.** Read [`samples/nano-gpt-data-curation/README.md`](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/samples/nano-gpt-data-curation/README.md): select a 12M-token subset for a fixed 30M-parameter model, then verify through training and held-out perplexity. Continue to the task's `instruction.md` and `task.toml`, then follow [Running the Benchmark](https://github.com/scaleapi/rsi-benchmark/blob/d9f7dcba7412ccc99dc0d97ad92f26e40f1b2354/README.md#running-the-benchmark) for the `harbor run` entry with that task path, agent/model arguments, and Modal runtime.

**Language and running requirements.** English; Python ≥3.12, `pip install -e ".[runner]"`, Harbor, model API access, and configured Modal GPU sandboxes. The reviewed README requires GPUs for its tasks; hardware and timeouts are specified per task. Reading the task contract needs no compute service. Use the Scale repository/website linked above; `recursive-self-improvement-bench.com` and RSIBench-Data are different resources with different task counts.

<a id="autorse"></a>

### [AutoRSE](https://github.com/Ray-Tiann/AutoRSE) · [paper](https://arxiv.org/abs/2610.37228)

**Evaluation tool · recommendation research.** Study whether an agent's gains come from training settings, ensembles or new algorithms, using six recommendation tasks. This evaluates research actions; improving a recommender alone does not establish that the research agent improves itself. Pair with the [AI R&D evaluation route](learning-guide.md#survey-project-map).

**Recommended entry.** Read [§§2.2–2.3 → §§3.3–3.4](https://arxiv.org/html/2610.37228v1), then the [pinned README](https://github.com/Ray-Tiann/AutoRSE/blob/9711faddc2d684f15243fd0d871bb8633098d666/README.md) → [tools/run_agent.py](https://github.com/Ray-Tiann/AutoRSE/blob/9711faddc2d684f15243fd0d871bb8633098d666/tools/run_agent.py) → [runtime contract](https://github.com/Ray-Tiann/AutoRSE/blob/9711faddc2d684f15243fd0d871bb8633098d666/benchmark/RUNTIME.md). Begin with HSTU; trace experiment branches, public-validation selection, predictions and exported provenance.

**Running entry and requirements.** Python 3.12+. After checkout and dependency setup, preview the documented command with `python tools/run_agent.py --task hstu --agent codex --model YOUR_MODEL_ID --gpu 0 --seed 2024 --dry-run`; this prints a launch plan and does not run research. Full trials require public task inputs, Linux, an NVIDIA GPU / CUDA 12.1-compatible driver, Docker / NVIDIA Container Toolkit, Harbor 0.18.0 and configured model credentials. The default research budget is 12 hours plus finalization; GPU memory depends on the task. `tools/run_baseline.py` offers training without an LLM agent, while `tools/validate_submission.py` checks prediction format only. Hidden-test scores depend on the hosted evaluator. The published [dataset](https://huggingface.co/datasets/RayTian/AutoRSE) and [scoring Space](https://huggingface.co/spaces/RayTian/AutoRSE) could not be verified as accessible in this review; source availability does not establish an end-to-end usable hosted service.

<a id="justrua"></a>

### [JustRUA](https://github.com/ZefanW/JustRUA) · [paper](https://arxiv.org/abs/2611.16009)

**Evaluation tool · controlled robot-harness baseline.** Compare full episode history, motion length, experience reuse and scene geometry on one evaluation set. The released policy keeps fixed model weights and uses no self-improvement loop. The paper separately studies a five-round loop that edits shared Python operations and guidance; its final policy does not inherit that library. Use this comparison to identify which component produces a gain.

**Recommended entry.** Read [§§2.4–2.5 → §§4.2–4.3 and Appendix G → §5](https://arxiv.org/html/2611.16009v1), then the [repository setup](https://github.com/ZefanW/JustRUA/blob/7429b76ffc765b9feee95e2ffb4340f09163e930/README.md#use-with-xpolicylab) and [adapter instructions](https://github.com/ZefanW/JustRUA/blob/7429b76ffc765b9feee95e2ffb4340f09163e930/policy/JustRUA/README.md). After installing the adapter in the documented XPolicyLab checkout and setting `SERVER_PY` / `EVAL_PY`, run from the XPolicyLab root:

```bash
EVAL_ENV_TYPE=debug DEBUG_OBS_ENCODED=1 bash policy/JustRUA/eval.sh \
  RoboDojo insert_tubes no-checkpoint arx_x5 joint 0 0 0 "$SERVER_PY" "$EVAL_PY"
```

This exercises WebSocket transport and a 20-step joint-hold loop without the simulator, model account or depth weights. It does not test robot task solving or improvement. Follow [policy.py](https://github.com/ZefanW/JustRUA/blob/7429b76ffc765b9feee95e2ffb4340f09163e930/policy/JustRUA/policy.py) into the 20-control motion cap before attempting the documented real task evaluation.

**Requirements and interpretation.** English documentation / bilingual project page. The pinned [XPolicyLab package](https://github.com/XPolicyLab/XPolicyLab/blob/6baccd57ff958570d0db1588370289ee36c8bb70/pyproject.toml) requires Python ≥3.10. Real evaluation adds RoboDojo / Isaac, robot assets, the Cartesian planner, compatible GPU / PyTorch dependencies, Apple's Depth Pro weights and Codex **0.153.4** with access to the selected actor. Keep the coding Python environment separate as documented. The 111-episode subset differs from the official leaderboard protocol; the experience experiment uses tasks that are later scored. Compare its measured behavior and cost within that protocol, rather than crediting the static policy's score gain to RSI.

<a id="trust-gate"></a>

### [TRUST: Trustworthy Recursive Updates with Statistical Testing](https://arxiv.org/abs/2611.10787)

**Evaluation tool · acceptance-method reading.** Study when to retain a proposed harness update. TRUST combines sequential evidence, a tolerated loss margin, correction for reused validation samples and an error budget allocated across rounds. An LLM uses past context to guide allocation; the statistical procedure itself stays fixed. This belongs to the [optional reliability branch](learning-guide.md#reliability-safety).

**Recommended entry.** Read [§3 → §4 / Algorithm 1 → §5 / Assumption 1 → §6.1](https://arxiv.org/html/2611.10787v1), then Appendix G.1 for the shared protocol and Appendix I for validation-overfitting examples. Separate the expected proportion of harmful accepted updates from a guarantee that every update improves. The guarantee depends on a bound on reuse bias; the paper does not establish how to identify that bound from data.

**Requirements.** English; probability, hypothesis testing and agent evaluation. Reading needs no API; no official runnable implementation was verified. The reported protocol uses HotpotQA, DROP and APPS, two model services, separate 200-item validation / 300-item test sets, and 30 rounds across five seeds. These describe the study, not a packaged reproduction or a minimum budget.

<a id="continual-arc"></a>

### [Continual-ARC](https://github.com/unifyai/continual-arc) · [paper](https://arxiv.org/abs/2611.14505)

**Evaluation tool · continual skill acquisition.** ARC tasks return after gaps with fresh instances. The benchmark charges for demonstrations and incorrect attempts, then compares the learner's final state with the same learner reset under the same model and Harness. The frozen seen test measures reuse of rules on new instances. The frozen held-out test measures transfer to tasks absent from the stream.

**Recommended entry.** Read [§§2.1–2.4 → §§3–4](https://arxiv.org/html/2611.14505v3) and step through a returning task in the [public replay](https://continual-arc.unify.ai/runs). From the pinned checkout, install the core package and rescore the [archived run](https://github.com/unifyai/continual-arc/blob/513dd67f6e9b7bb1224a57d64c7f66c4e3828fea/runs/README.md#reading-them):

```bash
python -m pip install -e .
continual-arc report runs/arc1/H-prime-agent-luna6-low-ws0
continual-arc transfer runs/arc1/H-prime-agent-luna6-low-ws0/frozen/held-out/play \
  runs/arc1/H0-prime-agent-luna6-low-fresh0/frozen/held-out-reference/play
```

Compare the memory and program-library controls before interpreting budget savings. The benchmark scores feedback usage and separately records model and compute costs. The public ARC-AGI-1 held-out tasks were withheld from the stream and may have appeared in model training.

**Requirements.** English. The browser replay needs only a browser. Local rescoring uses Python ≥3.10 and the downloaded records without model calls. Fresh [baseline runs](https://github.com/unifyai/continual-arc/blob/513dd67f6e9b7bb1224a57d64c7f66c4e3828fea/baselines/README.md#install) add Python 3.12/3.13, uv, benchmark data, and the selected Harness and sandbox. Model-backed runs require provider access and budget. ARC-AGI-3 adds its pinned game engine and toolkit.

<a id="rsi-pdebench"></a>

### [RSI-PDEbench](https://arxiv.org/abs/2611.14949) · [project site](https://jeremylu916.github.io/RSI-PDE/)

**Evaluation tool · protocol reading.** Study how an agent identifies an equation family, fits coefficients and builds a solver from samples. The harness retains solver code, policy text and memory after validation. The foundation model and executable supervisor stay fixed.

**Recommended entry.** Read [§2.4 → §3.2 → §4 → §§5.4, 6](https://arxiv.org/html/2611.14949v1). Compare Full (210 test cases), Noisy (160) and Hard-OOD (278) with the 1,001-case inventory. Trace candidate-equation residuals into the shortlist, then compare public relative error and the final scoring protocol. Agents do not receive hidden-test feedback during runs, but the authors used benchmark results to inform design choices. Treat the reported comparisons as developmental evidence. Some dollar costs come from a retrospective stopping-rule replay paired with full-budget scores.

**Requirements.** English. Numerical PDE and agent-evaluation fundamentals. The [upstream setup](https://jeremylu916.github.io/RSI-PDE/#start) describes a GPU node, bubblewrap and model access for a built-in entrant. The paper-linked GitHub repository and Hugging Face dataset API returned 404 and 401 respectively on November 18, so the verified entry is the paper and project site.

<a id="repofactory"></a>

### [RepoFactory](https://huggingface.co/datasets/IQuestLab/RepoFactory) · [paper](https://arxiv.org/abs/2611.21152)

**Evaluation tool.** The public release packages 200 environments before evolution. Each asks the agent to reconstruct a software project from a specification and API guide. Its verifier scores a submitted implementation against tests, while the reference solution stays outside the solving workspace. [Release contents](https://huggingface.co/datasets/IQuestLab/RepoFactory/blob/efdcaa8f6ea1bfa55eed2263e39186b928c7da88/README.md#release-contents)

**Recommended entry.** Download instance `000001` and load its supplied image using the official quickstart. Run the Harbor `oracle` and `nop` agents. The intended results are full reward for the reference implementation and zero reward for the unchanged workspace. Inspect verifier logs to confirm those outcomes. [Pinned quickstart](https://github.com/IQuestLab/RepoFactory/blob/133f7cd998a049c94f86d420491e462456478320/README.md#quickstart)

**Method reading.** In §3.2, follow how a construction agent uses verifier output and code metrics to revise the specification, reference implementation and tests. §5.6 examines recovery of valid environments separately from the downstream training value of scope and coupling. The paper reports 10,159 environments. The public files support checking the initial tasks. The checked GitHub snapshot supplies documentation and figures. [Paper v2](https://arxiv.org/html/2611.21152v2#S3.SS2) · [Ablation](https://arxiv.org/html/2611.21152v2#S5.SS6)

**Requirements.** Docker with Linux/amd64 support, Python ≥3.12 for Harbor 0.26.0 and `huggingface_hub`. The oracle and no-op checks require no model calls. The example image archive is about 720 MB and the task config assigns 2 CPUs, 8 GiB of RAM and 20 GiB of storage. A solving agent adds model access and call budget. [Instance files](https://huggingface.co/datasets/IQuestLab/RepoFactory/tree/efdcaa8f6ea1bfa55eed2263e39186b928c7da88/instances/000001) · [Harbor installation](https://docs.harborframework.com/getting-started/installation)

<a id="skilldiff"></a>

### [SkillDiff · How Feedback-Free Self-Evolution Reshapes Agent Skills](https://github.com/LitaoGuo/How-Self-Evolution-Reshapes-Skills) · [paper](https://arxiv.org/abs/2611.25534)

**Evaluation tool · skill rewrite diagnostics.** Compare the original expert skill with successive rewrites that receive no task results. The same model rewrites and uses each skill, and companion scripts and references stay fixed. In 87 SkillsBench tasks across six models, the authors report an average 14.6 percentage point drop after 30 rewrites. SkillDiff marks expert items absent from all ten topic-only drafts to focus the agent's attention on them.

**Recommended entry.** Read [§§2.1–2.2 → §§3.2–3.3 → §4 and Appendices C.4 / E](https://arxiv.org/html/2611.25534v1). Compare original, rewritten and restored conditions before interpreting the marking result. Run the [published chart commands](https://github.com/LitaoGuo/How-Self-Evolution-Reshapes-Skills/blob/db2cdbde29e752ebc9cc81817f17400b64056c40/README.md#evaluation) from the pinned repository root after installing `requirements.txt`:

```bash
python3 -m experiments.evaluate performance
python3 -m experiments.evaluate retention
```

**Requirements and evidence.** Chinese and English docs. The charts need Python ≥3.10 and use the bundled aggregate CSV without model calls or GPUs. New SkillsBench runs need the selected original skills, task assets, BenchFlow, Docker and the corresponding harness and model access. In the reported setup, marking a skill for one model costs 21 preparation calls (one topic, ten drafts and ten judgments). The original skills and per-run outputs are absent from the [release](https://github.com/LitaoGuo/How-Self-Evolution-Reshapes-Skills/blob/db2cdbde29e752ebc9cc81817f17400b64056c40/EXPERIMENTS.md#data).

<a id="coevobench"></a>

### [CoEvoBench](https://github.com/AlibabaResearch/CoEvoBench) · [paper](https://arxiv.org/abs/2611.27116)

**Evaluation tool · model–harness co-evolution.** Follow how a researcher agent can revise model weights, the harness, or both under one budget. Compare the paired controls and the roles of Visible, Selection and Test to distinguish the first working candidate from gains produced by later feedback. [Paper §§3.2–3.4, 5.1–5.3](https://arxiv.org/html/2611.27116v1)

**Recommended entry.** Read the AppWorld example in §15.2 and the evaluation audits in §19. To follow the development evaluator in code, use the [pinned quickstart](https://github.com/AlibabaResearch/CoEvoBench/blob/d39a924c8985806933c94777d8e969d6e756262c/README.md#quickstart-no-gpu-smoke-run) and run this from the checkout root.

```bash
uv run --locked --no-dev ceb eval --bench toy --split visible
```

**Requirements and evidence.** Chinese and English documentation. The toy uses Python ≥3.11, uv and local Docker with `python:3.11-slim`, with no model credentials or GPUs. Both scripted sum-of-squares tasks passed locally (`score=1.0000`, `n_bad=0`), verifying the toy scoring path. The reference protocol budgets four GPUs, 24 hours and a $100 teacher-model allowance per run, with three independent runs per researcher–benchmark pair. Full runs also need benchmark assets, model access and training infrastructure. The pinned checkout documents gaps in current Docker/GPU acceptance and final evaluation. [Quickstart and implementation status](https://github.com/AlibabaResearch/CoEvoBench/blob/d39a924c8985806933c94777d8e969d6e756262c/README.md)

<a id="rsibench-infra"></a>

### [RSIBench-Infra](https://rsibench-infra.github.io/) · [paper](https://arxiv.org/abs/2611.24395)

**Evaluation tool · infrastructure optimization.** Study how task-specific quality checks qualify throughput gains from changing the infrastructure for 16 inference and four training workloads. The five-task Lite Set uses single-H20 inference workloads also measured in the full suite. [Paper §§3–5](https://arxiv.org/pdf/2611.24395v1)

**Recommended entry.** Start with Qwen3.8-27B and open Kimi K3's run in the [public results explorer](https://rsibench-infra.github.io/#results). Compare validated speedup and the analytical speed-of-light (SOL) score, then inspect the published trajectory. In §5, check how the authors estimate the analytical reference. Claude Opus 5.5 has formal scores for 10 of 20 tasks and three of the five Lite tasks. Use those denominators when comparing aggregates. [Lite Set](https://rsibench-infra.github.io/#lite-set) · [Paper §§4–5](https://arxiv.org/pdf/2611.24395v1)

**Requirements and evidence.** English paper and results explorer. Reviewing scores and traces only needs a browser. The paper describes workloads using one to 32 accelerators. The [pinned source](https://github.com/rsibench-infra/rsibench-infra.github.io/tree/5bb554a6d622736a31cc9d711168ab8f041e3b30) publishes the site, results data and trace viewer. The [project site](https://rsibench-infra.github.io/#about) lists the benchmark runner as forthcoming.

<a id="computewise"></a>

### [ComputeWise](https://github.com/SalesforceAIResearch/computewise) · [paper](https://arxiv.org/abs/2611.31027)

**Evaluation tool · experimental compute efficiency.** Study how a simulated GPU replays recorded jobs and how the scoring distinguishes work needed for the answer, unneeded work and idle capacity. The fixed scheduling harness provides a control for measuring research efficiency. Read §§4–5 for the reference schedules and §§7.2–8 for the harness comparison and simulator limitations. [Paper v1](https://arxiv.org/html/2611.31027v1)

**Recommended entry.** Filter the [public runs](https://huggingface.co/datasets/Salesforce/computewise/blob/9bdd145383a7d823ca9d3125da69e04e5374e1dc/data/runs/results.jsonl) to `pkg-filter-yield`, `sonnet`, `claude-code`, simulator `r7` and valid runs with an `over_ref` reading. For `L0` (no help) and `A5` (released harness), the three runs per arm give median times of 1.423× and 1.065× the reference. The median fillable-idle shares are 28.2% and 6.8%, with zero unneeded GPU time in both arms. Follow the definitions in the [data card](https://huggingface.co/datasets/Salesforce/computewise/blob/9bdd145383a7d823ca9d3125da69e04e5374e1dc/README.md) to see what changed in this example.

**Requirements and evidence.** English. Reading the data uses a browser or a JSONL reader without model calls. The archive contains 748 scored runs across 45 tasks, which includes runs beyond the paper's nine-task suite. Some paper comparisons use different simulator builds across arms. New simulated runs need Linux x86_64, Docker with cgroup v2, the `loop` module, Python ≥3.9, roughly 200 GB of free space and model access. The upstream commands use root and the simulator uses CPU resources. [Pinned setup](https://github.com/SalesforceAIResearch/computewise/blob/ed097953b307f5ef8a0bc28048b21641272d804f/README.md#running-the-benchmark)

<a id="intervention-failure"></a>

### [Which Failure Does an Intervention Repair?](https://arxiv.org/abs/2611.29290) · [code](https://github.com/Zihan-Zoe/same-skill-different-harness)

**Evaluation tool · matched intervention comparisons.** Study how to change one axis at a time across model, skill, execution harness and inference budget on the same task instances. Read §2 for the matched design, §§4–5 for failure labels and skill transfer across models, and §6 for how the authors use a labeled pilot to choose a configuration. [Paper v1](https://arxiv.org/html/2611.29290v1)

**Recommended entry.** Download `ledger/executions.parquet`, `examples/pilot.py` and `examples/reproduce_pilot.py` from the [pinned dataset](https://huggingface.co/datasets/Zihan-Zoe/same-skill-different-harness/tree/e9b538f93a16647ddd38dd1f9bb5cf6a139fb8d9), keeping the directory layout. Run the published replay from its root.

```bash
python examples/reproduce_pilot.py
```

**Requirements and evidence.** English. The replay needs Python, NumPy, pandas and PyArrow. It uses the public ledger of 718,848 executions without model calls or GPUs. A local replay returned 57.39 for the 20-task pilot and 53.47 for always using GPT-5.6-sol on the paper's five-benchmark pilot subset. The ledger prices local Qwen inference at zero and omits hardware costs. The release includes a 3,939-row failure cohort and frozen skills, while raw trajectories and benchmark payloads are absent. New experiments need the source benchmarks, model endpoints or local vLLM, and the upstream Python 3.10 setup. [Pinned code](https://github.com/Zihan-Zoe/same-skill-different-harness/tree/183fa2a0012e07f7e2678a3fba626bc882900454) · [Dataset card](https://huggingface.co/datasets/Zihan-Zoe/same-skill-different-harness/blob/e9b538f93a16647ddd38dd1f9bb5cf6a139fb8d9/README.md)
