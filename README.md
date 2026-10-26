# Awesome RSI Resources

**English** | [简体中文](README_zh.md)

A learning and research directory for Recursive Self-Improvement (RSI), with distinctive features, recommended entry points, and prerequisites for each resource.

**62 resources; latest source review: 2026-10-25.** A project’s website, code, and notebooks count as one resource. See the [verification archive](docs/verification.md) for individual dates and the scope of each review.

<a id="resource-scope"></a>

## Resource Scope and Labels

This directory covers both recursive improvement and the mechanisms and tools needed to study it. The following labels describe the **recommended practical entry**, with its demonstrated scope. They are our learning-oriented classification, informed by [Modern Agentic Systems §3.2](https://arxiv.org/html/2607.13104v1#S3.SS2) and [The Last AI §§2.2–2.3](https://arxiv.org/html/2609.11873v3#S2.SS2); individual papers use different definitions.

| Label | What the entry teaches | Examples in this directory |
| --- | --- | --- |
| **Recursive improvement method** | Changes to an agent implementation or improvement policy are retained and used in subsequent improvement work. We distinguish teaching prototypes from research implementations; neither label promises sustained acceleration. | [RSI Labs](#rsi-labs): a small improvement-policy experiment; [STOP / SICA](#recursive-methods): source routes through executable inheritance; [Harness²](#harness2) / [HyperAgents](#hyperagents): improver experience or meta-agent code; [DGM](#dgm): inherited agent code participates in later self-modification. |
| **Related self-improvement mechanism** | Prompt optimization, program search, learned adaptation, reusable experience, or co-adaptation; also introductory components and simulations. The entry explains what changes and what remains fixed. | [Meta-Harness / AHO](#harness-optimization), [GEPA / TextGrad](#tutorials), [ShinkaEvolve / SEAL / Agent Lightning](#practice), [ACE / Voyager](#memory-skills), [co-evolution](#coevolution-projects), and [self-play](#adversarial-self-play). |
| **Evaluation tool** | Measures a component or illustrates acceptance criteria for a candidate change. | [LongMemEval-V2 and RSI Atlas](#evaluation); Atlas is an acceptance-gate teaching example. |

Indexes, surveys, books, and comprehensive courses remain reading resources and may span several categories. A memory benchmark or a fixed-optimizer tutorial can be useful preparation for RSI without demonstrating a recursive improvement loop. Start with the [prerequisite course](#prerequisite-courses) if needed, then compare the concrete mechanisms below.

<a id="start-here"></a>

## Quick Start

| Goal | Starting point |
| --- | --- |
| Build a conceptual map | [Prism’s Chinese guide](#prism) → [RL and RSI distinctions](#rl-and-rsi) → [survey reading path](docs/learning-guide.md#survey-reading-path) |
| Learn through Chinese explanations and code | [Hello-Agents Reflection](#hello-agents) → [Hung-yi Lee’s self-improvement lectures](#hung-yi-lee); choose [WalkingLabs](#walkinglabs) for broader prerequisites |
| Understand recursive improvement | [RSI Labs §4](#rsi-labs) → [STOP / SICA source routes](#recursive-methods) → [DGM](#dgm) or [HyperAgents](#hyperagents) |
| Build and optimize agents | [Harness component lessons](#learn-deepseek-harness) → [Harness² workflow demo](#harness2), then choose [harness optimization](#harness-optimization) or [program search](#program-search) |
| Study training and research | [Stanford CS329A](#cs329a) → [model training projects](#model-training); choose [co-evolution](#coevolution-projects) or [self-play](#adversarial-self-play) for your research goal |
| Study experience reuse and evaluation | [ACE / Voyager](#memory-skills) → [LongMemEval-V2](#longmemeval-v2); start with [RSI Atlas](#rsi-atlas) for acceptance gates |

Read further: [Learning guide](docs/learning-guide.md) for routes and project mappings · [Practice guide](docs/practice-guide.md) for source walkthroughs, runnable entries, and full requirements · [Verification archive](docs/verification.md) for dates, coverage, and source evidence.

## Contents

- [Research Indexes and Awesome Lists](#indexes)
- [Surveys and Reading Routes](#surveys)
- [RL and RSI](#rl-and-rsi)
- [Learning Materials](#learning-materials)
  - [Guides and Books](#guides)
  - [Prerequisite Course](#prerequisite-courses)
  - [Hands-on Tutorials](#tutorials)
  - [Courses and Workshops](#courses)
  - [Chinese Videos and Talks](#videos)
- [Practice Projects](#practice)
  - [Program Search](#program-search)
  - [Agent and Improver Code](#recursive-methods)
  - [Harness Optimization](#harness-optimization)
  - [Model Training](#model-training)
  - [Memory and Skills](#memory-skills)
  - [Co-Evolution](#coevolution-projects)
  - [Adversarial Self-Play](#adversarial-self-play)
- [Evaluation Tools](#evaluation)
- [Verification and Contribution](#verification)

<a id="indexes"></a>

## Research Indexes and Awesome Lists

These resources help you find related work, compare research directions, and plan your reading. Each project uses its own RSI definitions and taxonomy; comparing them can be useful.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="prism"></a> [Prism-Shadow/awesome-rsi](https://github.com/Prism-Shadow/awesome-rsi) | Organizes methods and evaluations along nine dimensions, with bilingual illustrations, paper filtering, and a citation graph. A useful starting point for an overview of the field. | Read the [Chinese RSI guide](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md), then explore methods and benchmarks on the [website](https://prism-shadow.github.io/awesome-rsi/#blog/understanding-rsi). Its [author-hosted survey](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/public/papers/rsi-survey.pdf) offers a deeper path: §2.3 loop → §3 taxonomy → §4 connections to deep learning → §5 evaluation. | Chinese and English guides; English survey; basic LLM / agent concepts; reading only. |
| <a id="natnew"></a> [natnew/awesome-recursive-self-improvement](https://github.com/natnew/awesome-recursive-self-improvement) | Combines a field map with three reading paths covering the basics, system building, and safety and limits. Useful for turning scattered papers into a reading sequence. | [Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths): choose a path before exploring the topic sections. | English; LLM / machine learning fundamentals; reading only. |
| <a id="lobehub"></a> [lobehub/awesome-rsi](https://github.com/lobehub/awesome-rsi) | Covers models, harnesses, memory, multi-agent systems, embodied systems, and automated AI research. Explains evidence levels such as task gains, retained gains, and gains in the improver itself. | [Fundamentals & Getting Started](https://github.com/lobehub/awesome-rsi#fundamentals--getting-started) → [Scope & Terminology](https://github.com/lobehub/awesome-rsi#scope--terminology). | English; LLM / agent fundamentals; reading only. |
| <a id="persdre"></a> [Persdre/awesome-recursive-self-improvement](https://github.com/Persdre/awesome-recursive-self-improvement) | Organizes research by “what is modified × degree of loop closure,” helping readers distinguish what different works mean by RSI. | [What Counts as RSI?](https://github.com/Persdre/awesome-recursive-self-improvement#what-counts-as-rsi), then browse papers by the component being modified. | English; machine learning / agent background. Its level labels are the author's organizing framework. |
| <a id="token-rhythm"></a> [Token-Rhythm/awesome-rsi](https://github.com/Token-Rhythm/awesome-rsi) | A bilingual literature table with dates, topic labels, summaries, and paper / code links. Useful for browsing by research direction. | [Featured readings in Chinese](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#featured-rsi-readings) → [Category overview](https://github.com/Token-Rhythm/awesome-rsi/blob/main/README_zh.md#category-overview). | Chinese and English; reading only. The upstream last-verification date is **2026-08-13**; consult other indexes for September–October work. |
| <a id="jacky-leng"></a> [jacky-leng/awesome-rsi](https://github.com/jacky-leng/awesome-rsi) | Compares improvement loops across six axes: loop locus, feedback, search, persistent state, human role, and evidence type. Useful for comparing methods. | [TAXONOMY.md](https://github.com/jacky-leng/awesome-rsi/blob/main/TAXONOMY.md) → [Landscape](https://github.com/jacky-leng/awesome-rsi#landscape). | English; reading only. The upstream review covers work through **2026-10-07**. |
| <a id="pinkbubblebubble"></a> [pinkbubblebubble/awesome-rsi](https://github.com/pinkbubblebubble/awesome-rsi) | Uses RSI / Self-improvement / Enabler labels to explain how resources relate to recursive improvement. Includes harnesses, evaluations, and engineering reports for exploring recent practical directions. | [Scope and labels](https://github.com/pinkbubblebubble/awesome-rsi#scope-and-labels) → [Start here](https://github.com/pinkbubblebubble/awesome-rsi#start-here); explore the [harness list](https://github.com/pinkbubblebubble/awesome-rsi#self-improvement-harnesses) for implementation ideas. | English; reading only. The upstream last-review date is **2026-10-21**; linked implementations have their own requirements. |

<a id="surveys"></a>

## Surveys and Research Overviews

Selected surveys with specific chapter entry points. Papers use their own definitions and taxonomies; version and index-coverage records are linked below.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="modern-agentic-systems"></a> [selfimproving-agent/Awesome-Self-Improving-Agents](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents) · [paper](https://arxiv.org/abs/2607.13104) | A survey companion that separates model-parameter improvement from updates to prompts, memory, tools, and full scaffolds, with indexes of evaluations and application domains. | Read [§3 definitions → §4 taxonomy → §5 model / §6 scaffold improvement → §8 evaluation](https://arxiv.org/html/2607.13104); use the [agent-oriented guide](https://github.com/selfimproving-agent/Awesome-Self-Improving-Agents/blob/main/README_AGENT.md) for question-based navigation. | English; machine learning / agent fundamentals; reading only, with manuscript source included. |
| <a id="bounded-refinement"></a> [deepgrounding/recursive-self-improvement](https://github.com/deepgrounding/recursive-self-improvement) · [paper](https://arxiv.org/abs/2607.07663) | A survey companion repository with a frozen literature corpus, classification scripts, and workflows for generating figures and bibliographies; places deployment-time improvement, training, self-evaluation, and automated research within one taxonomy. | Read §2 and §5 of the [survey source](https://github.com/deepgrounding/recursive-self-improvement/blob/main/draft/main.md), then explore [Reproducing](https://github.com/deepgrounding/recursive-self-improvement#reproducing) and the [corpus file](https://github.com/deepgrounding/recursive-self-improvement/blob/main/artifacts/corpus_v2.csv). | English; reproduction requires Python 3.11+, NumPy, and Matplotlib; some scripts access arXiv / OpenAlex. The corpus was frozen in **July 2026** and publicly released in September. |
| <a id="llm-overview"></a> [Self-Improvement of Large Language Models: A Technical Overview and Future Outlook](https://arxiv.org/abs/2603.25681) · [author repository](https://github.com/Zesearch/self-improvement-llm) | Organizes model improvement as data acquisition, selection, model optimization, inference refinement, and autonomous evaluation. Useful for connecting isolated techniques into a full learning lifecycle. | Read the [paper's introduction and §4](https://arxiv.org/html/2603.25681v3), especially §4.3–4.4 on self-generated versus self-evolving optimization; then §6 on autonomous evaluation. | English; ML / LLM training background. TMLR survey; the reviewed camera-ready version is v3. |
| <a id="self-evolving-agents"></a> [A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve](https://arxiv.org/abs/2507.21046) · [CharlesQ9/Self-Evolving-Agents](https://github.com/CharlesQ9/Self-Evolving-Agents) | Compares what changes, when adaptation occurs, and how feedback or populations drive updates. Especially helpful for distinguishing adaptation within a task from learning across tasks. | [§2 definitions → §3–5 taxonomy → §7 evaluation](https://arxiv.org/html/2507.21046v4); use the companion list to find implementations after choosing a branch. | English; agent / ML fundamentals. TMLR 2026; the reviewed paper is v4, newer than the companion README's last content update. |
| <a id="comprehensive-survey"></a> [A Comprehensive Survey of Self-Evolving AI Agents](https://arxiv.org/abs/2508.07407) · [ANative-Lab/Awesome-Self-Evolving-Agents](https://github.com/ANative-Lab/Awesome-Self-Evolving-Agents) | Explains an optimization loop through system inputs, agent systems, environments, and optimizers, then separates single-agent, multi-agent, and domain-specific optimization. | Read [§3 and Figure 3](https://arxiv.org/pdf/2508.07407v2#page=9) first, then §4–5 for methods and §7 for evaluation. | English; basic agent / optimization knowledge. The former EvoAgentX repository URL redirects to ANative-Lab; these are one resource. |
| <a id="frontis-survey"></a> [Self-Improving Agents in the Era of Experience: A Survey of Self- to Meta-Evolution](https://github.com/FrontisAI/Awesome-Self-Improving-Agents) | Follows deployment traces into reusable skills, persistent memory, environments, model updates, and meta-level control. A system-oriented bridge from harness engineering to experience-driven improvement. | Start with the [author-hosted PDF](https://github.com/FrontisAI/Awesome-Self-Improving-Agents/blob/main/Self_Improving_Agents.pdf), §2 (p. 5), then §3–4 and §7–8; continue with Che Jiang’s Chinese [Qingke Talk 146 recording](https://www.bilibili.com/video/BV13ZgA64Ept/) and [organizer’s outline](https://www.qingkeai.online/blog/AI4AI-RSI). | English paper; Chinese talk. Agent / LLM fundamentals. Paper text and structure were checked through the author's PDF; OpenReview returned a browser-verification page. |
| <a id="last-ai"></a> [The Last AI Built by Humans: Toward Genuine Recursive Self-Improvement](https://arxiv.org/abs/2609.11873) · [theseus-labs-rsi/awesome-rsi](https://github.com/theseus-labs-rsi/awesome-rsi) | A survey and roadmap that compares autonomy over execution, strategies, future experience, deployment adaptation, and the improvement mechanism. Connects the framework to application domains and industry cases. | Read [§2.2 improvement-loop definitions → §3 autonomy levels](https://arxiv.org/html/2609.11873v3); then use the repository's [Start Here](https://github.com/theseus-labs-rsi/awesome-rsi#start-here). | English; agent / ML background. L1–L5 are this paper's framework, not a field-wide standard; industry examples are author-reported evidence. |
| <a id="coevolution-survey"></a> [Co-Evolution in Agentic Systems: Toward Self-Directed Evolution Beyond Human Design](https://arxiv.org/abs/2608.10299) | Focuses on mutually adapting agents, environments, and evolution mechanisms, explaining what co-evolution adds beyond a fixed-context improvement loop. | [§2.2–2.3 definitions and three-stage map → §3–5](https://arxiv.org/html/2608.10299v1); Appendix A separates co-evolution from adjacent concepts. | English; multi-agent / RL fundamentals. A survey and conceptual roadmap; meta co-evolution is discussed as an emerging direction. |
| <a id="coding-agents-survey"></a> [Self-Evolving Coding Agents](https://arxiv.org/abs/2608.03392) | Organizes persistent coding-agent updates into assets, architecture, and model parameters, with code-specific feedback and evaluation. Helps distinguish improving a task's code from improving the agent that will solve later tasks. | Read [§2.3 operational boundary → §3 taxonomy → §7–8 feedback and evaluation](https://arxiv.org/html/2608.03392v4). | English; coding-agent / software-engineering fundamentals. Reviewed v4; reading material, not a runnable tutorial. |
| <a id="safety-survey"></a> [Safety in Self-Evolving Agents: A Survey](https://arxiv.org/abs/2610.00093) · [author repository](https://github.com/xaddwell/awesome-self-evolving-agent-safety) | Studies how safety properties change as experience becomes reusable memory, skills, tools, workflows, or model state. The SAVER framework connects the state carrier, adaptation, violation, exposure, and response. | Start with [§2.3–2.4: transition tests and SAVER](https://arxiv.org/html/2610.00093v1), then the companion repository's [Overview and Corpus](https://github.com/xaddwell/awesome-self-evolving-agent-safety#overview). | English; agent / security background. The companion corpus includes machine-initialized labels with confidence levels; it is not an entirely manually verified bibliography. |
| <a id="towards-ai"></a> [Towards AI That Improves Itself: A Survey of Recursive Self-Improvement](https://lee1003-lee.github.io/Awesome-RSI-Research/) · [author repository](https://github.com/Lee1003-lee/Awesome-RSI-Research) | Distinguishes inherited improvements from gains in the improver itself, connecting this distinction to verification, update policies, and memory reuse. Useful for designing and evaluating persistent improvement loops. | Read [§3 definitions and claim protocol](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5), then §4.3 (p. 14) and §5.2 (p. 21) for updates and agent-system evolution. | English; agent / ML fundamentals. The distinctions are the authors' framework; the bibliography also includes enabling methods. Author-hosted survey manuscript. |

<a id="survey-reading-path"></a>

**[Recommended Survey Reading Path](docs/learning-guide.md#survey-reading-path)**: overviews → methods, with reliability and safety controls as an optional branch.

<a id="survey-project-map"></a>

**[From Surveys to Practice Projects](docs/learning-guide.md#survey-project-map)**.

<a id="survey-coverage"></a>

**[Recent Survey Coverage](docs/verification.md#survey-coverage)**.

<a id="rl-and-rsi"></a>

## RL and RSI: Connections, Distinctions, and Reading Route

**RL is a way to learn behavior from reward; RSI concerns how retained improvements contribute to subsequent improvement.** They overlap, but describe different aspects of a system. Existing literature already discusses the connection: start with [Modern Agentic Systems §§3.2–3.3](https://arxiv.org/html/2607.13104v1#S3.SS3), then compare the definitions in [Towards AI §3](https://lee1003-lee.github.io/Awesome-RSI-Research/assets/rsi-survey.pdf#page=5). Some frameworks include self-generated training loops; stronger claims require improvement to the improver itself. The comparison below is this directory's synthesis, not a universal hierarchy or a claim that all RL uses a fixed architecture.

| Mechanism | What changes | What to learn from the example |
| --- | --- | --- |
| Policy learning | Policy parameters under a specified update procedure | [Agent Lightning](#agent-lightning): trace rollouts → rewards → checkpoints. Higher task reward alone does not establish that the update procedure improved. |
| Adversarial self-play | Policies and the opponents / experience they generate for one another | [OpenSpiel and SPIRAL](#adversarial-self-play): study an adaptive learning signal. Self-play specifies how experience is produced; it does not by itself specify RL, preference optimization, or changes to the learning rule. |
| Learning the RL update rule | A parameterized rule for training other agents | DiscoRL below: compare learning a better policy with learning how to update policies. A learned rule does not imply its discovery process also rewrites itself. |
| Coupled system improvement | Reusable harness procedures together with model weights | ScienceBuddy below: harness refinement shapes the next RL stage, and the updated model changes subsequent harness adaptation. |
| Self-modifying learning machinery | Policy programs that can modify their own learning behavior | Schmidhuber's self-modifying policies below: study how credit is assigned to modifications that affect later modifications. |

RL can therefore power part of an RSI loop, while code search or retained skill edits can supply other updates; [DGM](#dgm) is a useful comparison without an RL weight-training step. For any project, identify **what persists, what generates the next learning signal, and whether the update procedure itself changes**. To investigate gains in the improver, compare later learning with and without the retained change under comparable tasks and budgets.

**Reading route:** Modern Agentic Systems §3.3 → the already-listed [Ashish Kumar Part 2](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/) (the self-play template, then “Learning to learn”) → one hands-on self-play project → the three readings below. The research readings require no execution; the project tables separately specify runtime requirements.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="schmidhuber-rsi"></a> [Schmidhuber: Recursive Self-Improvement (RSI) Since 1987](https://people.idsia.ch/~juergen/recursive-self-improvement.html) | Author retrospective on policies that can modify their learning procedure. Makes the stronger “improve the improver” interpretation concrete; its definitions and historical framing are the author's perspective. | [§2: self-modifying policies](https://people.idsia.ch/~juergen/recursive-self-improvement.html#secSMP) → [§7: recent work](https://people.idsia.ch/~juergen/recursive-self-improvement.html#secLouis); follow the [1997 chapter](https://people.idsia.ch/~juergen/ssabook/ssabook.html) for formal concepts. | Technical Note **September 2026**; English; RL and algorithm fundamentals. Historical / conceptual reading, not a modern installation tutorial. |
| <a id="discorl"></a> [DiscoRL: Discovering state-of-the-art reinforcement learning algorithms](https://www.nature.com/articles/s41586-025-09761-x) | Learns an RL update rule through meta-optimization, then uses it to train new agents. A bridge from policy improvement to improving the training machinery. | [Authors' illustrated project page](https://google-deepmind.github.io/disco_rl/), Method → paper Figure 1, Discovery method / Meta-optimization → Generalization. | Nature first published **2025-10-22**; version of record **2025-11-26**. English; RL, neural networks, and meta-gradients. Reading entry; code / reproduction requirements were not audited here. |
| <a id="sciencebuddy"></a> [ScienceBuddy: Recursive-in-Recursive Self-Improvement for Interactive Scientific Agents](https://arxiv.org/abs/2609.17523) | Couples harness edits with model RL across cycles. The auxiliary editor and GRPO rule stay fixed, making the changing components easy to distinguish. | [§§2.3–2.5 and Algorithm 1](https://arxiv.org/html/2609.17523v1#S2.SS3) → §4.2's two-cycle study. | arXiv **v1, 2026-09-15**. English; agent architecture and RL background. Paper reading; product, code, and experimental results were not independently reproduced. |

<a id="learning-materials"></a>

## Learning Materials

<a id="guides"></a>

### Guides, Books, and Learning Paths

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="rsi-book"></a> [The RSI Book · bhavsarpratik/rsi](https://github.com/bhavsarpratik/rsi) | **Related self-improvement mechanism.** Build a first Python loop with evaluation, prompt changes, and reusable memory. | [Chapter 2 and notebook](docs/practice-guide.md#rsi-book) | English; Python 3.10+, LiteLLM, model endpoint. |
| <a id="rsi-learn"></a> [Roloria/rsi-learn](https://github.com/Roloria/rsi-learn) | **Related self-improvement mechanism.** A Chinese learning path and rule-based evolutionary-search simulation. | [Learning path and local playground](docs/practice-guide.md#rsi-learn) | Chinese; Node.js / Vite; no model calls in the simulation. |
| <a id="ashish-kumar"></a> [Ashish Kumar: Recursive self-improvement, a three-part series](https://ashishkumar.ai/series/recursive-self-improvement/) | Moves from theoretical foundations to self-play / self-training and then self-modifying code. Includes an illustrative text-to-SQL self-training loop and a discussion of evaluation harnesses. | Read [Part 1: Concepts and theory](https://ashishkumar.ai/blog/recursive-self-improvement-explained/), [Part 2: Self-play and self-training](https://ashishkumar.ai/blog/self-improving-ai-self-play-self-training/), and [Part 3: Self-modifying code](https://ashishkumar.ai/blog/self-improving-code-alphaevolve-to-aide/) in order. | English; suitable for readers with LLM / machine learning fundamentals. Explanatory articles published on **2026-10-11**; code snippets illustrate the discussion. |
| <a id="rsi-research-notes"></a> [RSI Research Notes · asimfish/awesome_rsi](https://github.com/asimfish/awesome_rsi) | Chinese paper walkthroughs and a synthesis comparing changes to model weights, harness code, and text-based skills, with particular attention to evaluation. Useful for moving from a field overview to individual papers. | Follow [Start Here](https://github.com/asimfish/awesome_rsi#1-start-here), read [Report 10: Synthesis](https://github.com/asimfish/awesome_rsi/blob/main/reports/10_synthesis_insights.md), then [Report 12: Self-Evolving Agents survey](https://github.com/asimfish/awesome_rsi/blob/main/reports/12_self_evolving_agents_survey.md). For harness optimization, read [Report 13 §4: Meta-Harness](https://github.com/asimfish/awesome_rsi/blob/63f83e581ff3161932b62ab5fbe845fdf03cf84b/reports/13_meta_harness.md) before the [official code entry](#harness-optimization). | Chinese; LLM / agent fundamentals; reading only. Reports contain the curator's analysis; bundled Chinese paper translations are machine-generated, so use original papers for citations and technical details. |
| <a id="weng-harness"></a> [Lilian Weng: Harness Engineering for Self-Improvement](https://lilianweng.github.io/posts/2026-07-04-harness/) | A research overview connecting context management, workflow search, self-modifying harnesses, evolutionary search, and joint harness / weight updates. Useful for comparing the mechanisms behind the practice projects in this directory. | Read [Harness Optimization](https://lilianweng.github.io/posts/2026-07-04-harness/#harness-optimization), focusing on Self-Improving Harness and Evolutionary Search, then the Future Challenges section. | English; familiarity with agents and evaluation; reading only. A survey-style technical blog, distinct from a peer-reviewed survey paper. |

<a id="prerequisite-courses"></a>

### Prerequisite Course

Use this optional course to learn the components behind agent improvement before the recursive-method examples. The already-listed [Hello-Agents and harness tutorials](#tutorials) provide shorter introductions.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="walkinglabs"></a> [WalkingLabs: Self-Improving Agent Notebooks](https://github.com/walkinglabs/self-improving-agent-notebook) | **Related self-improvement mechanism.** Bilingual notebooks covering agent loops, evaluation, code search, and archives; a community course inspired by CS329A. | [L01 foundations → L07 code search](docs/practice-guide.md#walkinglabs) | Chinese / English; Python, Jupyter and model API; optional prerequisite. |

<a id="tutorials"></a>

### Hands-on Tutorials

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="rsi-labs"></a> [rsi_labs · weilinear](https://github.com/weilinear/rsi_labs) | **Recursive improvement method.** A teaching prototype changes the improver’s instructions and evaluates later repair selection. | [Notebook §4 and configuration](docs/practice-guide.md#rsi-labs) | English; Colab / Jupyter and Google API key; no training GPU. |
| <a id="learn-deepseek-harness"></a> [Prism-Shadow/learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness) | **Related self-improvement mechanism.** Build agent harness components lesson by lesson, then inspect runtime self-modification. | [L1 agent loop → L10 self-modification](docs/practice-guide.md#learn-deepseek-harness) | Chinese / English; Node.js, TypeScript and DeepSeek API. |
| <a id="gepa"></a> [GEPA / DSPy official tutorials](https://github.com/gepa-ai/gepa) | **Related self-improvement mechanism.** Optimize reusable prompts with textual feedback, candidate selection, and held-out evaluation. | [DSPy AIME notebook](docs/practice-guide.md#gepa) | English; Python and model API; no weight training. |
| <a id="textgrad"></a> [TextGrad official notebooks](https://github.com/zou-group/textgrad) | **Related self-improvement mechanism.** Use textual gradients to optimize a shared prompt and inspect validation-based rollback. | [Primitives → object-counting notebook](docs/practice-guide.md#textgrad) | English; Python and model API. |
| <a id="hello-agents"></a> [Datawhale Hello-Agents: Reflection and self-evolution](https://github.com/datawhalechina/hello-agents) | **Related self-improvement mechanism.** Learn the generate–review–revise reflection loop through Chinese explanations and code. | [Chapter 4 §4.4 → Extra10](docs/practice-guide.md#hello-agents) | Chinese; Python and model API for real inference. |
| <a id="hello-generic-agent"></a> [Datawhale Hello Generic Agent](https://github.com/datawhalechina/hello-generic-agent) | **Related self-improvement mechanism.** Turn task experience into discoverable SOPs and scripts for later sessions. | [Chapters 4 and 12; installation](docs/practice-guide.md#hello-generic-agent) | Chinese; Python 3.11/3.12 recommended, model API and selected tool dependencies; Beta. |

<a id="courses"></a>

### Courses and Workshops

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="cs329a"></a> [Stanford CS329A: Self-Improving AI Agents](https://cs329a.stanford.edu/) | Connects test-time compute, verifiers, tool feedback, planning, RL, open-ended evolution, and agent evaluation; useful for organizing a weekly reading plan. | Start with **lectures 2–7** in the official Schedule, then read **lecture 17: Agentic Evaluations & Long-Horizon Tasks**. | English; basic ML / LLM knowledge. The public page covers the **Autumn 2025 course**; this review checked the schedule and paper reading lists. |
| <a id="harvard-rsi"></a> [Harvard CS 2881R: RSI Topics within AI Safety](https://boazbk.github.io/mltheoryseminar/) | Examines RSI through AI R&D automation, the pace of improvement, and safety, adding research questions beyond implementation. | The [2025-10-09 archived lecture](https://boazbk.github.io/mltheoryseminar/fall2025/#lecture-oct-9) links to slides, notes, and a recording; continue with the readings and student experiment materials for [2026-09-24: RSI & AI Trajectories](https://boazbk.github.io/mltheoryseminar/#lecture-sep-24). | English; background in ML, probability / information theory, and Python. These are topics within an AI Safety course; the 2026 lecture currently has no recording listed. |
| <a id="iclr-rsi"></a> [ICLR 2026: AI with Recursive Self-Improvement Workshop](https://recursive-workshop.github.io/) | Brings together research questions about self-improvement methods, systems, and evaluation; useful for moving from the program to specific research papers. | Read the official program and themes, then choose papers from the Oral / Spotlight sections of [Accepted Papers](https://recursive-workshop.github.io/papers.html). | English; research experience is helpful. Held on **2026-04-26**; this review checked the official website and accepted-paper list. |
| <a id="adaptive-agents-course"></a> [DeepLearning.AI × Oracle: Building Adaptive AI Agents](https://www.deeplearning.ai/courses/building-adaptive-ai-agents) | Teaches three adaptation layers: reusable skills distilled from agent traces, code-graph retrieval, and model adaptation. Useful for learning how experience carries across sessions; extracted skills require human approval. | Start with Overview of Continual Learning, then [Behavior Adaptation: Trajectory-to-Skill Learning](https://learn.deeplearning.ai/courses/building-adaptive-ai-agents/lesson/9i82mn/behavior-adaptation%3A-trajectory-to-skill-learning); continue to the code-graph lessons. | English; Python familiarity recommended. Seven videos and three code examples are listed. Videos are available on the Free plan; hands-on labs and graded activities are in Pro. |
| <a id="berkeley-agents"></a> [Berkeley Advanced LLM Agents MOOC: Self-Improvement Topics](https://llmagents-learning.org/sp25) | Connects self-rewarding, iterative preference optimization, and meta-rewarding with LLM reasoning. Useful for studying how a model can generate training signals and improve its judgments. | Start with Jason Weston's **2025-02-03** lecture, *Learning to reason with LLMs*, and [slides from page 40](https://rdi.berkeley.edu/llm-agents-mooc/slides/Jason-Weston-Reasoning-Alignment-Berkeley-Talk.pdf#page=40), then follow the syllabus readings on iterative reasoning preference optimization. | English; LLM and post-training fundamentals recommended. The **Spring 2025** course has ended; public slides and readings remain available, with recording links listed. |

<a id="videos"></a>

### Chinese Video Courses and Research Talks

For a Chinese author lecture on experience-driven self- to meta-evolution, see Qingke Talk 146, grouped with the FrontisAI paper in [Surveys and Research Overviews](#surveys).

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="hung-yi-lee"></a> [Hung-yi Lee: Machine Learning 2026 — Self-Improvement](https://speech.ee.ntu.edu.tw/~hylee/ml/2026-spring.php) | Chinese lectures connect answer correction, self-generated training signals, harness optimization, and learning how to improve. The accompanying slides distinguish changes to outputs, prompts / code, and model parameters. | Watch [Self-Correction](https://youtu.be/m3i2mk5hs8U) → [Self-Improving, Part 1](https://youtu.be/s06mSAGN4gM) → [Part 2](https://youtu.be/cQLKVzbwN7I); read the [Part 1 slides](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2026-course-data/Self-Improving.pdf) and [Part 2 slides, pp. 11–18 and 33–46](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2026-course-data/self-evolving-agent.pdf#page=11) alongside them. | Chinese lectures and slides with English technical terms; LLM / ML fundamentals recommended. Public lecture links and PDFs; some course assignments use NTUCOOL. These are selected topics within a broader ML course. |
| <a id="baai-forum"></a> [2026 BAAI Conference: AI Self-Evolution Forum](https://www.bilibili.com/video/BV1Bijw65Ec9/) | Research talks connect agent-generated experience, reusable memory, and verifiable feedback with self-improvement. The official multipart upload makes individual talks easy to follow. | Start with [P3: Shaokun Zhang — Recursive Self-Learning through Scalable Agentic Experience](https://www.bilibili.com/video/BV1Bijw65Ec9/?p=3), then [P5: Yu Gu — The Illusion of Self-Improving Agents](https://www.bilibili.com/video/BV1Bijw65Ec9/?p=5); use the [organizer's written recap](https://hub.baai.ac.cn/view/55536) to connect the talks. | Chinese talks with English technical titles; LLM / agent and basic RL knowledge recommended. Public Bilibili research presentations, rather than a lab-based course. |

<a id="practice"></a>

## Practice Projects

Grouped by the main learning topic; each entry’s label describes its relationship to RSI. Each project appears once in the catalog. The [practice guide](docs/practice-guide.md) holds detailed goals, commands, and environment requirements. GPU configurations are upstream examples, not tested minimums; we have not run the upstream projects.

<a id="program-search"></a>

### Program Search

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="shinkaevolve"></a> [ShinkaEvolve · SakanaAI](https://github.com/SakanaAI/ShinkaEvolve) | **Related self-improvement mechanism.** Study program mutation, evaluator feedback, parent selection, and saved search history. | [Tutorial notebook](docs/practice-guide.md#shinkaevolve) | English; Python 3.10+ (3.11 recommended), model API and evaluator dependencies. |
| <a id="openevolve"></a> [OpenEvolve](https://github.com/algorithmicsuperintelligence/openevolve) | **Related self-improvement mechanism.** Evolve a task program with evaluation, configuration, and checkpoints. | [Function-minimization example](docs/practice-guide.md#openevolve) | English; Python 3.10+, NumPy and model endpoint; no training GPU. |

<a id="recursive-methods"></a>

### Agent and Improver Code

After RSI Labs, follow **STOP → SICA → DGM** to trace inherited implementations into later improvement, then compare meta-agent code inheritance in HyperAgents.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="stop"></a> <a id="stop-source-route"></a> [STOP · Self-Taught Optimizer](https://github.com/microsoft/stop) · [paper](https://arxiv.org/abs/2310.02304) | **Recursive improvement method.** Accepted Python improver code becomes the executable improver used in the next round. | [Four-step source route](docs/practice-guide.md#stop) | English; reading needs no API; execution needs Python, legacy SDK/model adaptation and isolation. |
| <a id="sica"></a> <a id="sica-source-route"></a> [SICA · Self-Improving Coding Agent](https://github.com/MaximeRobeyns/self_improving_coding_agent) · [paper](https://arxiv.org/abs/2504.15228) | **Recursive improvement method.** Distinguish the edited parent, the agent performing improvement, and successor selection. | [Five-step source route](docs/practice-guide.md#sica) | English; reading needs no API; execution needs Python, Docker/buildx, benchmark data and model APIs. |
| <a id="dgm"></a> [Darwin Gödel Machine (DGM)](https://github.com/jennyzzt/dgm) | **Recursive improvement method.** Archived agent implementations participate in later self-modification and offspring evaluation. | [Outer loop → self-improvement step](docs/practice-guide.md#dgm) | English; Python, Docker, model API and benchmark environments/data. |
| <a id="hyperagents"></a> [HyperAgents · Meta and collaborators](https://github.com/facebookresearch/HyperAgents) · [paper](https://arxiv.org/abs/2603.19461) | **Recursive improvement method.** Inherited meta-agent code edits later candidates alongside an editable task agent. | [DGM-Hyperagent loop and source route](docs/practice-guide.md#hyperagents) | English; Python 3.12, Docker/build environment, domain data and model API. |

<a id="harness-optimization"></a>

### Harness Optimization

Compare reusable improvement experience with harness search under a fixed optimizer. [HyperAgents](#hyperagents), with editable meta-agent code, is grouped above.

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="harness2"></a> [Harness² · Google Cloud AI Research / Northwestern](https://github.com/google-research/harness2) · [paper](https://arxiv.org/abs/2610.14224) | **Recursive improvement method.** Retained improvement experience informs later harness edits; start with the scripted workflow demo. | [Local demo → experience-library source](docs/practice-guide.md#harness2) | English; demo: Python 3.12/3.13 and uv, no model credentials; real improvement requires model access. |
| <a id="meta-harness"></a> [Meta-Harness · Stanford IRIS and collaborators](https://github.com/stanford-iris-lab/meta-harness) · [paper](https://arxiv.org/abs/2603.28052) | **Related self-improvement mechanism.** A fixed coding proposer uses source, scores, and traces to search task-specific harness programs. | [Text-classification example](docs/practice-guide.md#meta-harness) | English; Python, proposer/task-model access and datasets; setup differs by model provider. |
| <a id="aho"></a> [Agent Harness Optimizer (AHO) · Airbnb](https://github.com/airbnb/agent-harness-optimizer) · [paper](https://arxiv.org/abs/2609.05736) | **Related self-improvement mechanism.** Optimize prompts and tool middleware; distinguish candidate acceptance from final evaluation. | [BetterHarness BFCL example](docs/practice-guide.md#aho) | English; Python, model API and separately downloaded BFCL data; check scorecard settings. |

<a id="model-training"></a>

### Model Training

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="seal"></a> [SEAL · Self-Adapting Language Models](https://github.com/Continual-Intelligence/SEAL) | **Related self-improvement mechanism.** Compare temporary LoRA adaptation with outer-loop learning to generate self-edits. | [General-knowledge workflow](docs/practice-guide.md#seal) | English; Python 3.12, Linux/CUDA; example uses 2 A100/H100 GPUs plus API and script adaptation. |
| <a id="agent-lightning"></a> [Microsoft Agent Lightning v1.0](https://github.com/microsoft/agent-lightning) | **Related self-improvement mechanism.** Trace tool-use rollouts, rewards, GRPO updates, and policy checkpoints under a fixed trainer. | [Calc-X Local Mode](docs/practice-guide.md#agent-lightning) | English; Python 3.12+, Linux/WSL, CUDA; example uses 1 A100 80GB. |

<a id="memory-skills"></a>

### Memory and Skill Learning

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="ace"></a> [ACE: Agentic Context Engineering](https://github.com/ace-agent/ace) | **Related self-improvement mechanism.** Convert feedback into a persistent text playbook; compare adaptation and reloaded evaluation. | [Formula CLI and playbook reload](docs/practice-guide.md#ace) | English; Python ≥3.10, uv and model API; no training GPU. |
| <a id="voyager"></a> [Voyager](https://github.com/MineDojo/Voyager) | **Related self-improvement mechanism.** Save, retrieve, and compose executable Minecraft skills across sessions. | [Skill manager → saved-skill example](docs/practice-guide.md#voyager) | English; Python, Node, Minecraft Java/Fabric and model APIs; legacy dependencies. |

<a id="coevolution-projects"></a>

### Co-Evolution

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="coral"></a> [CORAL](https://github.com/Human-Agent-Society/CORAL) | **Related self-improvement mechanism.** Shared scored attempts and notes influence other agents’ subsequent search. | [Two-agent circle-packing example](docs/practice-guide.md#coral) | English docs + Chinese README; Python 3.11–3.13, Git, uv, Docker and model API; no training GPU for this evaluator. |
| <a id="comas"></a> [CoMAS](https://github.com/xxyQwQ/CoMAS) | **Related self-improvement mechanism.** Peer solutions and criticism become interaction rewards and separate policy updates. | [Training launcher and controller](docs/practice-guide.md#comas) | English; Python 3.10, CUDA; upstream recommends 2 A100 80GB GPUs per agent, four agents by default. |
| <a id="r-zero"></a> [R-Zero](https://github.com/Chengsong-Huang/R-Zero) | **Related self-improvement mechanism.** Alternate task generation and solver learning, carrying both checkpoints into later rounds. | [Challenger–Solver loop](docs/practice-guide.md#r-zero) | English; Linux/CUDA, 8-GPU script configuration, HF/W&B and evaluation API. |
| <a id="jaxued"></a> [JaxUED](https://github.com/DramaCow/jaxued) | **Related self-improvement mechanism.** Use policy performance to retain and mutate environments, then train on the resulting curriculum. | [Maze ACCEL → PAIRED](docs/practice-guide.md#jaxued) | English; JAX/Flax; no LLM API; full RL training requires substantial compute. |

<a id="adversarial-self-play"></a>

### Adversarial Self-Play

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="open-spiel"></a> [OpenSpiel: Kuhn poker NFSP](https://github.com/google-deepmind/open_spiel) — classical self-play | **Related self-improvement mechanism.** Compare best responses, historical average policies, and exploitability in Kuhn poker. | [Fictitious play → NFSP](docs/practice-guide.md#open-spiel) | English; Python, OpenSpiel and PyTorch; CPU entry. |
| <a id="spiral"></a> [SPIRAL](https://github.com/spiral-rl/spiral) — multi-turn zero-sum game RL | **Related self-improvement mechanism.** Learn a shared policy from both roles in multi-turn zero-sum games. | [Game training script](docs/practice-guide.md#spiral) | English; Linux/CUDA and distributed LLM RL dependencies; inspect the upstream GPU configuration. |
| <a id="sppo"></a> [SPPO](https://github.com/uclaml/SPPO) — preference-game self-play | **Related self-improvement mechanism.** Iteratively train on preference games scored by a fixed PairRM evaluator. | [Iterative SPPO training](docs/practice-guide.md#sppo) | English; CUDA, model/data access and multi-GPU configuration; fixed evaluator and learning rule. |

<a id="evaluation"></a>

## Evaluation Tools

| Resource | Features and learning goals | Recommended entry | Language and requirements |
| --- | --- | --- | --- |
| <a id="rsi-atlas"></a> [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI) | **Evaluation tool.** A teaching example for acceptance gates and change history. | [Simple explanations → Python example](docs/practice-guide.md#rsi-atlas) | English; Python for the example; demonstrates gates rather than full RSI. |
| <a id="longmemeval-v2"></a> [LongMemEval-V2](https://github.com/xiaowu0162/LongMemEval-V2) · [paper](https://arxiv.org/abs/2605.12493) | **Evaluation tool.** Evaluate memory accuracy and query latency using retained agent traces. | [No-retrieval and RAG baselines](docs/practice-guide.md#longmemeval-v2) | English; Python ≥3.11, data, reader/embedding endpoints and paid judges for some tasks. |

<a id="verification"></a>

## Verification and Maintenance

Source-review dates, survey versions and coverage, per-resource review scope, and expansion records live in the [verification archive](docs/verification.md). Reading documentation or source is distinct from execution; consult the full requirements for each practical entry before running it.

## Curation Principles

- Organize learning materials by format and practice projects by their main topic. Maintain detailed runtime instructions in one place and link to them from learning routes.
- Label practical entries as recursive improvement methods, related self-improvement mechanisms, or evaluation tools; describe what changes and how it is reused. Keep prerequisite lessons distinct from demonstrated recursive improvement, and do not force broad surveys or courses into one category.
- Provide a recommendation, a concrete starting point, language, prerequisites, and practical requirements.
- Distinguish reading materials, simulations, real model calls, and training; record what was actually read or run during review.
- Prefer original projects; group a project's website, translations, and notebooks together, and do not count ordinary mirrors separately.
- Judge freshness by substantive content and learning value, retaining useful stable textbooks and older courses.

## Contributing

Recommend a resource through an [issue](https://github.com/RZRZ-Q/awesome-rsi-resources/issues) or submit a pull request. See the [contribution guide (Chinese)](CONTRIBUTING.md) for inclusion requirements.

## License

Original content in this repository is available under the [MIT License](LICENSE). Linked third-party materials remain subject to their respective licenses.
