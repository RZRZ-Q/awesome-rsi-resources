# Awesome RSI Resources

**English** | [简体中文](README_zh.md)

Learning and research resources for Recursive Self-Improvement (RSI).

A curated directory of awesome lists, learning guides, tutorials, and courses on recursive self-improvement.

This project brings together RSI resource collections and learning materials to help readers understand who each resource is for, what it offers, where to start, and how current its content is.

**Last reviewed: 2026-10-22.** The collection contains 26 resources spanning awesome lists, books, tutorials, practice projects, courses, workshops, and reproduction materials. The second batch adds 9 resources focused on tutorials, courses, and concrete practice entry points. A project's website, code, and notebooks are grouped into a single entry.

## Where to Start

| What you want to do | Recommended starting point |
| --- | --- |
| Build a conceptual understanding of RSI in Chinese | [Prism's illustrated Chinese guide](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md) |
| Build your first agent improvement loop in Python | [The RSI Book, Chapter 2](https://thersibook.com/chapters/ch02.html) and its companion notebook |
| Understand agent harnesses through code | [L1 of learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop), then follow the lessons in order |
| Optimize a reusable prompt against evaluation data | [GEPA / DSPy AIME notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb) |
| Evolve a small program using evaluator feedback | [ShinkaEvolve tutorial notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) |
| Train an agent from tool feedback with a GPU | [Agent Lightning Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode) |
| Start reading research papers systematically | [natnew's Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths) |
| Follow a course on self-improving agents | The public schedule and readings for [Stanford CS329A](https://cs329a.stanford.edu/) |

Choose a short learning path that fits your goal:

- **Concepts:** Prism's Chinese guide → The RSI Book, Chapters 1–2 → natnew's reading paths.
- **Agent engineering:** The RSI Book's Python loop → the implementations in learn-deepseek-harness → the scaffolding and evaluation sections of the Self-Improving Agents survey.
- **Optimization practice:** GEPA / DSPy → ShinkaEvolve or OpenEvolve → DGM for advanced agent-code evolution.
- **Training and research:** Stanford CS329A's verifier / RL readings → the foundation-model improvement sections of the Self-Improving Agents survey → SEAL's adaptation loop or Agent Lightning's policy training → relevant papers from the ICLR RSI workshop.

## Contents

- [Research Indexes and Awesome Lists](#indexes)
- [Guides, Books, and Learning Paths](#guides)
- [Hands-on Tutorials](#tutorials)
- [Practice Projects](#practice)
- [Courses and Workshops](#courses)
- [Evaluation and Survey Reproduction](#evaluation)
- [Freshness and Review Records](#verification)

<a id="indexes"></a>

## Research Indexes and Awesome Lists

These resources help you find related work, compare research directions, and plan your reading. Each project uses its own RSI definitions and taxonomy; comparing them can be useful.

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [Prism-Shadow/awesome-rsi](https://github.com/Prism-Shadow/awesome-rsi) | Organizes methods and evaluations along nine dimensions, with bilingual illustrations, paper filtering, and a citation graph. A useful starting point for an overview of the field. | Read the [Chinese RSI guide](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md), then explore methods and benchmarks on the [website](https://prism-shadow.github.io/awesome-rsi/#blog/understanding-rsi). | Chinese and English; basic LLM / agent concepts; reading only. |
| [natnew/awesome-recursive-self-improvement](https://github.com/natnew/awesome-recursive-self-improvement) | Combines a field map with three reading paths covering the basics, system building, and safety and limits. Useful for turning scattered papers into a reading sequence. | [Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths): choose a path before exploring the topic sections. | English; LLM / machine learning fundamentals; reading only. |
| [lobehub/awesome-rsi](https://github.com/lobehub/awesome-rsi) | Covers models, harnesses, memory, multi-agent systems, embodied systems, and automated AI research. Explains evidence levels such as task gains, retained gains, and gains in the improver itself. | [Fundamentals & Getting Started](https://github.com/lobehub/awesome-rsi#fundamentals--getting-started) → [Scope & Terminology](https://github.com/lobehub/awesome-rsi#scope--terminology). | English; LLM / agent fundamentals; reading only. |
| [Persdre/awesome-recursive-self-improvement](https://github.com/Persdre/awesome-recursive-self-improvement) | Organizes research by “what is modified × degree of loop closure,” helping readers distinguish what different works mean by RSI. | [What Counts as RSI?](https://github.com/Persdre/awesome-recursive-self-improvement#what-counts-as-rsi), then browse papers by the component being modified. | English; machine learning / agent background. Its level labels are the author's organizing framework. |
| [Token-Rhythm/awesome-rsi](https://github.com/Token-Rhythm/awesome-rsi) | A bilingual literature table with dates, topic labels, summaries, and paper / code links. Useful for browsing by research direction. | [Featured readings in Chinese](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#featured-rsi-readings) → [Category overview](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#category-overview). | Chinese and English; reading only. The upstream last-verification date is **2026-08-13**; consult other indexes for September–October work. |
| [selfimproving-agent/Awesome-Self-Improving-Agents](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents) | A survey companion that separates model-parameter improvement from updates to prompts, memory, tools, and full scaffolds, with indexes of evaluations and application domains. | The Quick Start and Reading Map in the [agent-oriented guide](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/blob/main/README_AGENT.md) point to survey sections by question. | English; machine learning / agent fundamentals; reading only, with manuscript source included. |
| [jacky-leng/awesome-rsi](https://github.com/jacky-leng/awesome-rsi) | Compares improvement loops across six axes: loop locus, feedback, search, persistent state, human role, and evidence type. Useful for comparing methods. | [TAXONOMY.md](https://github.com/jacky-leng/awesome-rsi/blob/main/TAXONOMY.md) → [Landscape](https://github.com/jacky-leng/awesome-rsi#landscape). | English; reading only. The upstream review covers work through **2026-10-07**. |
| [pinkbubblebubble/awesome-rsi](https://github.com/pinkbubblebubble/awesome-rsi) | Uses RSI / Self-improvement / Enabler labels to explain how resources relate to recursive improvement. Includes harnesses, evaluations, and engineering reports for exploring recent practical directions. | [Scope and labels](https://github.com/pinkbubblebubble/awesome-rsi#scope-and-labels) → [Start here](https://github.com/pinkbubblebubble/awesome-rsi#start-here); explore the [harness list](https://github.com/pinkbubblebubble/awesome-rsi#self-improvement-harnesses) for implementation ideas. | English; reading only. The upstream last-review date is **2026-10-21**; linked implementations have their own requirements. |

<a id="guides"></a>

## Guides, Books, and Learning Paths

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi) | Uses one warehouse-inventory question-answering task to introduce tool use, deterministic evaluation, prompt improvement, memory across tasks, and cost tracking. A good first Python experiment. | [Chapter 2: Build Your First Agent Improvement Loop](https://thersibook.com/chapters/ch02.html) + [companion notebook](https://github.com/bhavsarpratik/rsi/blob/master/notebooks/chapter2_build_your_first_loop.ipynb). | English; Python 3.10+, LiteLLM, and access to a model endpoint. The example mainly updates prompts and memory while keeping model weights fixed. |
| [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn) | A Chinese knowledge base, five-stage learning path, architecture diagrams, and evolutionary-search playground for building intuition about “generate–evaluate–select–integrate.” | See the [navigation and setup instructions](https://github.com/Roloria/rsi-learn#页面导航), read the [learning-path content](https://github.com/Roloria/rsi-learn/blob/main/src/data/path.ts), then visit `/#/path` and `/#/lab` after starting the site locally. | Chinese; the interactive site requires Node.js / Vite. The playground is a **rule-based frontend simulation** and does not call a real LLM. |
| [Ashish Kumar: Recursive self-improvement, a three-part series](https://ashishkumar.ai/series/recursive-self-improvement/) | Moves from theoretical foundations to self-play / self-training and then self-modifying code. Includes an illustrative text-to-SQL self-training loop and a discussion of evaluation harnesses. | Read [Part 1: Concepts and theory](https://ashishkumar.ai/blog/recursive-self-improvement-explained/), [Part 2: Self-play and self-training](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/), and [Part 3: Self-modifying code](https://ashishkumar.ai/blog/self-improving-code-alphaevolve-to-aide/) in order. | English; suitable for readers with LLM / machine learning fundamentals. Explanatory articles published on **2026-10-11**; code snippets illustrate the discussion. |

<a id="tutorials"></a>

## Hands-on Tutorials

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness) | Implements agent loops, plugins, persistent session logs, caching, compaction, memory, subagents, and runtime self-modification lesson by lesson. Each lesson is a standalone package for reading and modifying the code. | [L1: The minimal agent loop](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop) → follow the [web course](https://prism-shadow.github.io/learn-deepseek-harness/) in order → [L10: Self-modification](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/advanced/L10_self_modification). | Chinese and English; Node.js, TypeScript fundamentals, and the DeepSeek API. L10 demonstrates generating and registering temporary tools at runtime; it does not yet include a complete evolution loop with automated evaluation, promotion, and persistence. |
| [GEPA / DSPy official tutorials](https://github.com/gepa-ai/gepa) | Teaches reflective prompt evolution through a complete math example: baseline evaluation, textual feedback, candidate selection, and evaluation after optimization. Useful for learning how prompts improve while model weights stay fixed. | Start with the [GEPA for AIME notebook](https://github.com/stanfordnlp/dspy/blob/main/docs/docs/tutorials/gepa_aime/index.ipynb), then read [GEPA optimization](https://dspy.ai/current/getting-started/gepa-optimization/) for split design and saving the optimized program. | English; Python 3.10–3.14, DSPy / GEPA, datasets, and an OpenAI API key for the example. MLflow tracing is optional. |
| [TextGrad official notebooks](https://github.com/zou-group/textgrad) | Introduces textual gradients with a PyTorch-style API, then optimizes a shared prompt on object-counting questions, evaluates it on validation data, and reverts updates that reduce validation performance. Useful for understanding feedback-driven text optimization. | [Primitives](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Primitives.ipynb) → [Prompt Optimization](https://github.com/zou-group/textgrad/blob/main/examples/notebooks/Tutorial-Prompt-Optimization.ipynb). | English; Python 3.9+, Jupyter / Colab, and an OpenAI API key. The notebooks use older model IDs; check compatible model availability before running. Updates prompt text rather than model weights. |

For a first Python improvement loop, start with **The RSI Book, Chapter 2 and its notebook** above. GEPA and TextGrad teach prompt optimization with fixed model weights; their introductory tutorials do not modify the optimizer itself.

<a id="practice"></a>

## Practice Projects

These projects provide concrete examples for program evolution, agent code evolution, or model training. Choose by the object being improved and the available compute.

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [ShinkaEvolve · SakanaAI](https://github.com/SakanaAI/ShinkaEvolve) | A guided notebook connects LLM code mutations, program populations, evaluators, and saved search histories. Circle packing provides a concrete task for learning program evolution and comparing parent-selection strategies. | [Getting Started](https://sakanaai.github.io/ShinkaEvolve/getting_started/) → [interactive tutorial notebook](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/shinka_tutorial.ipynb) → inspect the [circle-packing evaluator](https://github.com/SakanaAI/ShinkaEvolve/blob/main/examples/circle_packing/evaluate.py). | English; Python 3.10+ (3.11 recommended), local Python or Colab, and model API credentials. The introductory example evolves a task program; its evaluator runs locally without a required training GPU. |
| [OpenEvolve](https://github.com/algorithmicsuperintelligence/openevolve) | An open-source AlphaEvolve-inspired program-search framework. The small function-minimization example shows how an initial search algorithm, evaluator feedback, configuration, and checkpoints fit together. | Read [Installation & Setup](https://github.com/algorithmicsuperintelligence/openevolve#installation--setup), obtain the repository examples, then follow [Function Minimization](https://github.com/algorithmicsuperintelligence/openevolve/tree/main/examples/function_minimization), reading `initial_program.py`, `evaluator.py`, and `config.yaml` together. | English; Python 3.10+, NumPy, and a model endpoint. The example defaults to Gemini through an OpenAI-compatible API; Docker is optional. It optimizes task code rather than model weights. |
| [Darwin Gödel Machine (DGM)](https://github.com/jennyzzt/dgm) | The original research implementation for studying agents that modify their own code, evaluate descendants on coding tasks, and retain an archive for further evolution. Best suited to readers ready to trace a complete research loop. | Read [Setup / Running the DGM](https://github.com/jennyzzt/dgm#setup), then trace [DGM_outer.py](https://github.com/jennyzzt/dgm/blob/main/DGM_outer.py) → [self_improve_step.py](https://github.com/jennyzzt/dgm/blob/main/self_improve_step.py). | English; Python, Docker, model API access, and SWE-bench / Polyglot setup. This is a research reproduction path with substantial environment and evaluation work, rather than a small introductory notebook. |
| [SEAL · Self-Adapting Language Models](https://github.com/Continual-Intelligence/SEAL) | **Model adaptation.** The authors' implementation learns to generate self-edits, tests temporary LoRA updates on downstream questions, then uses selected edits to train the edit generator. Useful for studying the inner adaptation / outer learning loop. | Start with the [general-knowledge pipeline](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/README.md): data generation → TTT server → evaluation → ReST-EM training; then inspect the [SFT-data builder](https://github.com/Continual-Intelligence/SEAL/blob/main/general-knowledge/src/EM/build_SFT_dataset.py). | English; advanced Python / fine-tuning background, Python 3.12, PyTorch / vLLM / PEFT. Upstream documents 2 A100/H100 GPUs; adapt SLURM scripts and paths. OpenAI-backed generation / proxy scoring also needs API access. |
| [Microsoft Agent Lightning v1.0](https://github.com/microsoft/agent-lightning) | **Agent policy training.** Calc-X connects an AutoGen agent and MCP calculator to rollout collection, answer-based rewards, and GRPO updates. A concrete entry into learning from tool-using trajectories and saving policy checkpoints. | Follow [Installation](https://github.com/microsoft/agent-lightning/blob/main/docs/00-installation.md), then [Calc-X Local Mode](https://github.com/microsoft/agent-lightning/blob/main/docs/50-example-calc-x.md#local-mode); launch from `examples/calc_x` as that example specifies. | English; Python 3.12+, Linux / WSL, CUDA, `verl` / vLLM, dataset download, and W&B by default. The documented Calc-X setup uses **1 A100 80GB**. This is the v1.0 training path; older APO tutorials target the legacy API. |

<a id="courses"></a>

## Courses and Workshops

| Resource | Distinctive features and audience | Recommended entry point | Language and available materials |
| --- | --- | --- | --- |
| [Stanford CS329A: Self-Improving AI Agents](https://cs329a.stanford.edu/) | Connects test-time compute, verifiers, tool feedback, planning, RL, open-ended evolution, and agent evaluation; useful for organizing a weekly reading plan. | Start with **lectures 2–7** in the official Schedule, then read **lecture 17: Agentic Evaluations & Long-Horizon Tasks**. | English; basic ML / LLM knowledge. The public page covers the **Autumn 2025 course**; this review checked the schedule and paper reading lists. |
| [Harvard CS 2881R: RSI Topics within AI Safety](https://boazbk.github.io/mltheoryseminar/) | Examines RSI through AI R&D automation, the pace of improvement, and safety, adding research questions beyond implementation. | The [2025-10-09 archived lecture](https://boazbk.github.io/mltheoryseminar/fall2025/#lecture-oct-9) links to slides, notes, and a recording; continue with the readings and student experiment materials for [2026-09-24: RSI & AI Trajectories](https://boazbk.github.io/mltheoryseminar/#lecture-sep-24). | English; background in ML, probability / information theory, and Python. These are topics within an AI Safety course; the 2026 lecture currently has no recording listed. |
| [ICLR 2026: AI with Recursive Self-Improvement Workshop](https://recursive-workshop.github.io/) | Brings together research questions about self-improvement methods, systems, and evaluation; useful for moving from the program to specific research papers. | Read the official program and themes, then choose papers from the Oral / Spotlight sections of [Accepted Papers](https://recursive-workshop.github.io/papers.html). | English; research experience is helpful. Held on **2026-04-26**; this review checked the official website and accepted-paper list. |
| [DeepLearning.AI × Oracle: Building Adaptive AI Agents](https://www.deeplearning.ai/courses/building-adaptive-ai-agents) | Teaches three adaptation layers: reusable skills distilled from agent traces, code-graph retrieval, and model adaptation. Useful for learning how experience carries across sessions; extracted skills require human approval. | Start with Overview of Continual Learning, then [Behavior Adaptation: Trajectory-to-Skill Learning](https://learn.deeplearning.ai/courses/building-adaptive-ai-agents/lesson/9i82mn/behavior-adaptation%3A-trajectory-to-skill-learning); continue to the code-graph lessons. | English; Python familiarity recommended. Seven videos and three code examples are listed. Videos are available on the Free plan; hands-on labs and graded activities are in Pro. |
| [Berkeley Advanced LLM Agents MOOC: Self-Improvement Topics](https://llmagents-learning.org/sp25) | Connects self-rewarding, iterative preference optimization, and meta-rewarding with LLM reasoning. Useful for studying how a model can generate training signals and improve its judgments. | Start with Jason Weston's **2025-02-03** lecture, *Learning to reason with LLMs*, and [slides from page 40](https://rdi.berkeley.edu/llm-agents-mooc/slides/Jason-Weston-Reasoning-Alignment-Berkeley-Talk.pdf#page=40), then follow the syllabus readings on iterative reasoning preference optimization. | English; LLM and post-training fundamentals recommended. The **Spring 2025** course has ended; public slides and readings remain available, with recording links listed. |

<a id="evaluation"></a>

## Evaluation and Survey Reproduction

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [deepgrounding/recursive-self-improvement](https://github.com/deepgrounding/recursive-self-improvement) | A survey companion repository with a frozen literature corpus, classification scripts, and workflows for generating figures and bibliographies; places deployment-time improvement, training, self-evaluation, and automated research within one taxonomy. | Read §2 and §5 of the [survey source](https://github.com/deepgrounding/recursive-self-improvement/blob/main/draft/main.md), then explore [Reproducing](https://github.com/deepgrounding/recursive-self-improvement#reproducing) and the [corpus file](https://github.com/deepgrounding/recursive-self-improvement/blob/main/artifacts/corpus_v2.csv). | English; reproduction requires Python 3.11+, NumPy, and Matplotlib; some scripts access arXiv / OpenAlex. The corpus was frozen in **July 2026** and publicly released in September. |
| [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI) | Illustrates improvement loops, evaluation, and change admission, with a small Python example for learning how to accept / reject candidate changes and record their history. | [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python admission-gate example](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py). | English; the example uses the Python 3.10+ standard library. It makes decisions from externally supplied test status, gains, and file paths; it does not generate changes with a model or run evaluations automatically. |

<a id="verification"></a>

## Freshness and Review Records

Both batches were reviewed on **2026-10-22**. New candidates were checked against existing project identities before detailed review; websites, notebooks, and renamed repositories were grouped together. We read project READMEs, recommended chapters or course pages, and inspected relevant code for entries with practical components. **We did not run upstream tutorials, call models, reproduce experiments, or review every paper in the lists.** For videos, we only checked the links provided on course pages.

The table records supported content changes, releases, or review dates reported by the upstream projects. These differ from this directory's review date and do not establish a cutoff for coverage of the entire field. Commit dates use Asia/Taipei; dates stated directly by upstream sources retain their original values.

<details>
<summary>Expand content dates and review scope for all 26 resources</summary>

| Resource | Content dates and evidence | Scope of this review |
| --- | --- | --- |
| Prism Awesome RSI | [Bilingual article added on 2026-10-15](https://github.com/Prism-Shadow/awesome-rsi/commit/6cf55d1bbe224ca1c26c2bb5c8b66e429cce220c); [Chinese guide updated on 09-20](https://github.com/Prism-Shadow/awesome-rsi/commit/775a1bdbe4dc60c55cd9d32e792d36f2ec658534). The 10-19 commit only replaced a QR code. | README, guide source, website routes, and resource configuration; not all interactions on the filtering website were checked. |
| natnew Awesome RSI | [Six research entries added on 2026-10-18](https://github.com/natnew/awesome-recursive-self-improvement/commit/b30c5fd2e36fe8a1f8381444e03377bec16135a1). | README, Reading Paths, and the diff for the new entries. |
| LobeHub Awesome RSI | [Evidence tiers updated on 2026-10-12](https://github.com/lobehub/awesome-rsi/commit/874f5c331c6d2deb70954da12ef9df4b9f255ad0); subsequent sorting and CI changes were not counted as resource additions. | README terminology, getting-started section, directory, and relevant commit diffs. |
| Persdre Awesome RSI | [Taxonomy labels organized and clarified on 2026-09-02](https://github.com/Persdre/awesome-recursive-self-improvement/commit/cde30351387b4abd23373884e90d508f7368b5ef). | Definitions, taxonomy, and learning resources in the README. |
| Token-Rhythm Awesome RSI | Upstream reports Last verified **2026-08-13**; [code links added on the same day](https://github.com/Token-Rhythm/awesome-rsi/commit/87681b460d6420f29f88bc3a2b848ddc6891dd1b). | English directory and maintenance notes, plus Chinese featured readings and category links. |
| Awesome Self-Improving Agents | [RHD entry added on 2026-10-19](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/commit/7ffbe03841e18a21200a0384cb38f868be93bd73). | README; taxonomy, chapter navigation, and evaluation notes in README_AGENT; diff for the latest entry. |
| jacky-leng Awesome RSI | Upstream review covers material through **2026-10-07**; [directory and six-axis taxonomy expanded on 10-08](https://github.com/jacky-leng/awesome-rsi/commit/f41e58bdf14a9a52912eefd85e10215587786c24). | README, TAXONOMY, and commit diffs; source files are the recommended entry points, and the reading website's full interactions were not checked. |
| pinkbubblebubble Awesome RSI | Upstream reports Last reviewed **2026-10-21**; [recent resources added on 10-22, Taipei time](https://github.com/pinkbubblebubble/awesome-rsi/commit/c91823d6ebd9969cea3b7b05e20027988ec5308b). | Labels, Start here, harnesses, related collections, and content commit diffs. |
| The RSI Book | [Chapter 3 added on 2026-07-16](https://github.com/bhavsarpratik/rsi/commit/7ce1c397323d442744be8d75ba584afca5d46afd); the latest August commit updated page design. | README, Chapter 2, agent source, and the setup / agent cells in the companion notebook. |
| Roloria/rsi-learn | [Learning site and simulator added on 2026-09-22](https://github.com/Roloria/rsi-learn/commit/64fa58065410fdc8d0c1c333f2bfc3d74019145b). | README, five-stage learning path, and simulator engine source. |
| Ashish Kumar's three-part guide | The [series page](https://ashishkumar.ai/series/recursive-self-improvement/) and all three articles state a publication date of **2026-10-11**. | Series index, all three articles, and their learning links. |
| learn-deepseek-harness | [Reorganized into Basics L1–L8 and Advanced L9–L10 on 2026-08-23](https://github.com/Prism-Shadow/learn-deepseek-harness/commit/4c3b6492767f8af9d65a2a97776ed3bea8841aec). | Root README, L1 documentation / source / dependencies, and L10 documentation. |
| GEPA / DSPy tutorials | [AIME tutorial added on 2025-08-14](https://github.com/stanfordnlp/dspy/commit/abe6487d6e2091a5a59f901a82d7e84850025d81); [train / validation split guidance added on 2026-08-27](https://github.com/stanfordnlp/dspy/commit/2a67bcc7a53d204ae6c85eee11b73bc898819d56). | Both READMEs, AIME notebook cells, GEPA optimization guide, Python requirements, and relevant commit changes; no model calls or performance reproduction. |
| TextGrad notebooks | Tutorials date from 2024; [renamed to their current Tutorial-* paths on 2024-07-08](https://github.com/zou-group/textgrad/commit/d56d1c1cb50ffe184c46b6ef457bdcd6132c3ace). | README, Primitives and Prompt Optimization notebook cells, dependency files, and rename history; older model IDs were not tested against live endpoints. |
| ShinkaEvolve | [Tutorial examples refreshed on 2026-04-07](https://github.com/SakanaAI/ShinkaEvolve/commit/9b72c250c5c0fccff6e4d5625f4eed76c183e00e); [Azure setup added to Getting Started on 07-16](https://github.com/SakanaAI/ShinkaEvolve/commit/018cea578f1068cadcc617ec1369ee34b3360fe7). | README, Getting Started, notebook setup / configuration / circle-packing / result-inspection cells, circle-packing runner and evaluator, package requirements, and related commit diffs. |
| OpenEvolve | [Example evaluator integrity fixed on 2026-10-19](https://github.com/algorithmicsuperintelligence/openevolve/commit/bc366807fd05720ababd3491fbba0107bf1742e9): the function-minimization evaluator recomputes the objective from the returned point. | README installation and quick start; function-minimization guide, seed program, evaluator, configuration, and the evaluator-fix diff. |
| DGM | [Core research loop released on 2025-05-30, Taipei time](https://github.com/jennyzzt/dgm/commit/682eb38a3eb232f4396924cacd0a083bf1444cf8). | README setup, requirements, outer loop, and self-improvement / evaluation step. Linked experiment logs and benchmark results were not independently reproduced. |
| SEAL | [General-knowledge experiments expanded and paths reorganized on 2025-08-02](https://github.com/Continual-Intelligence/SEAL/commit/6d9c9f9ee392c6cc618e771f399d436d190f6ca4). | Root / general-knowledge READMEs, requirements, TTT server, SFT-data builder, and training launcher; no GPU experiments were run. |
| Agent Lightning | README announces v1.0 in **August 2026**; [tutorial paths reorganized on 2026-08-21](https://github.com/microsoft/agent-lightning/commit/5415d850af20332442fdb0662458f332c7b1e894). | README, installation / Quick Start / Calc-X docs, Python requirements, local launcher, agent reward code, and GRPO configuration. Calc-X Local Mode matches the launcher's working-directory requirement; the root Quick Start differs. No training was run. |
| Stanford CS329A | The official website identifies the course as **Autumn 2025**. | Course overview, Schedule, and public paper reading links. |
| Harvard CS 2881R RSI topics | Archived lecture on **2025-10-09** and the newer lecture on **2026-09-24**. | Official course page and reading / slide / code links for both lectures; videos were not watched. |
| ICLR 2026 RSI Workshop | The official website gives the event date as **2026-04-26**. | Official themes, program, and Accepted Papers page. |
| Building Adaptive AI Agents | [Oracle announced the course on 2026-08-26](https://blogs.oracle.com/developers/we-just-launched-a-new-course-on-how-to-build-adaptive-ai-agents); the course page marks its update as **2026-08-27**. | Official course description, outline, lesson links, access plans, and Oracle's introduction; videos and notebooks were not reviewed. |
| Berkeley Advanced LLM Agents MOOC | The official syllabus identifies **Spring 2025** and dates Jason Weston's lecture **2025-02-03**. | Official syllabus, reading links, and the self-rewarding / iterative optimization / meta-rewarding sections of the linked slides; recordings and Lean labs were not reviewed. |
| deepgrounding survey materials | Corpus frozen in **July 2026**; [public repository released on 09-06](https://github.com/deepgrounding/recursive-self-improvement/commit/aceac9d8a8e46caa702b9651857380a4729202a7). | Reproduction workflow and licensing scope in the README, plus the survey's taxonomy and corpus methodology sections; the corpus and figures were not regenerated. |
| RSI Atlas | [Frozen-path matching fixed on 2026-10-22](https://github.com/aniruddhaadak80/RSI/commit/f4246024469d7e7eadea7a59db64f8289e57eb2a); the Start page is dated 09-18. | README, Start page, Python engine, dependencies, and code diffs. |

</details>

## Curation Principles

- Organize the main directory by resource format, covering model training, agent harnesses, memory and skills, evaluation, and automated research.
- Include adjacent topics, such as self-improving agents, that help readers understand RSI, and explain their specific uses in each entry.
- Provide a recommendation, a concrete starting point, language, prerequisites, and practical requirements.
- Distinguish reading materials, simulations, real model calls, and training; record what was actually read or run during review.
- Prefer original projects; group a project's website, translations, and notebooks together, and do not count ordinary mirrors separately.
- Judge freshness by substantive content and learning value, retaining useful stable textbooks and older courses.

## Contributing

Recommend a resource through an [issue](https://github.com/RZRZ-Q/awesome-rsi-resources/issues) or submit a pull request. See the [contribution guide (Chinese)](CONTRIBUTING.md) for inclusion requirements.

## License

Original content in this repository is available under the [MIT License](LICENSE). Linked third-party materials remain subject to their respective licenses.
