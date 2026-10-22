# Awesome RSI Resources

**English** | [简体中文](README_zh.md)

Learning and research resources for Recursive Self-Improvement (RSI).

A curated directory of awesome lists, learning guides, tutorials, and courses on recursive self-improvement.

This project brings together RSI resource collections and learning materials to help readers understand who each resource is for, what it offers, where to start, and how current its content is.

**Last reviewed: 2026-10-22.** The initial collection contains 17 resources spanning awesome lists, books, tutorials, courses, workshops, and reproduction materials. A project's website, code, and notebooks are grouped into a single entry.

## Where to Start

| What you want to do | Recommended starting point |
| --- | --- |
| Build a conceptual understanding of RSI in Chinese | [Prism's illustrated Chinese guide](https://github.com/Prism-Shadow/awesome-rsi/blob/main/site/src/data/blog/rsi-guide.zh.md) |
| Build your first agent improvement loop in Python | [The RSI Book, Chapter 2](https://thersibook.com/chapters/ch02.html) and its companion notebook |
| Understand agent harnesses through code | [L1 of learn-deepseek-harness](https://github.com/Prism-Shadow/learn-deepseek-harness/tree/main/basics/L01_agent_loop), then follow the lessons in order |
| Start reading research papers systematically | [natnew's Reading Paths](https://github.com/natnew/awesome-recursive-self-improvement#reading-paths) |
| Follow a course on self-improving agents | The public schedule and readings for [Stanford CS329A](https://cs329a.stanford.edu/) |

Choose a short learning path that fits your goal:

- **Concepts:** Prism's Chinese guide → The RSI Book, Chapters 1–2 → natnew's reading paths.
- **Agent engineering:** The RSI Book's Python loop → the implementations in learn-deepseek-harness → the scaffolding and evaluation sections of the Self-Improving Agents survey.
- **Training and research:** Stanford CS329A's verifier / RL readings → the foundation-model improvement sections of the Self-Improving Agents survey → relevant papers from the ICLR RSI workshop.

## Contents

- [Research Indexes and Awesome Lists](#indexes)
- [Guides, Books, and Learning Paths](#guides)
- [Hands-on Tutorials](#tutorials)
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

For a Python path, use **The RSI Book, Chapter 2 and its notebook** above. The two projects focus on improvement loops and harness engineering, respectively.

<a id="courses"></a>

## Courses and Workshops

| Resource | Distinctive features and audience | Recommended entry point | Language and available materials |
| --- | --- | --- | --- |
| [Stanford CS329A: Self-Improving AI Agents](https://cs329a.stanford.edu/) | Connects test-time compute, verifiers, tool feedback, planning, RL, open-ended evolution, and agent evaluation; useful for organizing a weekly reading plan. | Start with **lectures 2–7** in the official Schedule, then read **lecture 17: Agentic Evaluations & Long-Horizon Tasks**. | English; basic ML / LLM knowledge. The public page covers the **Autumn 2025 course**; this review checked the schedule and paper reading lists. |
| [Harvard CS 2881R: RSI Topics within AI Safety](https://boazbk.github.io/mltheoryseminar/) | Examines RSI through AI R&D automation, the pace of improvement, and safety, adding research questions beyond implementation. | The [2025-10-09 archived lecture](https://boazbk.github.io/mltheoryseminar/fall2025/#lecture-oct-9) links to slides, notes, and a recording; continue with the readings and student experiment materials for [2026-09-24: RSI & AI Trajectories](https://boazbk.github.io/mltheoryseminar/#lecture-sep-24). | English; background in ML, probability / information theory, and Python. These are topics within an AI Safety course; the 2026 lecture currently has no recording listed. |
| [ICLR 2026: AI with Recursive Self-Improvement Workshop](https://recursive-workshop.github.io/) | Brings together research questions about self-improvement methods, systems, and evaluation; useful for moving from the program to specific research papers. | Read the official program and themes, then choose papers from the Oral / Spotlight sections of [Accepted Papers](https://recursive-workshop.github.io/papers.html). | English; research experience is helpful. Held on **2026-04-26**; this review checked the official website and accepted-paper list. |

<a id="evaluation"></a>

## Evaluation and Survey Reproduction

| Resource | Distinctive features and audience | Recommended entry point | Language and prerequisites |
| --- | --- | --- | --- |
| [deepgrounding/recursive-self-improvement](https://github.com/deepgrounding/recursive-self-improvement) | A survey companion repository with a frozen literature corpus, classification scripts, and workflows for generating figures and bibliographies; places deployment-time improvement, training, self-evaluation, and automated research within one taxonomy. | Read §2 and §5 of the [survey source](https://github.com/deepgrounding/recursive-self-improvement/blob/main/draft/main.md), then explore [Reproducing](https://github.com/deepgrounding/recursive-self-improvement#reproducing) and the [corpus file](https://github.com/deepgrounding/recursive-self-improvement/blob/main/artifacts/corpus_v2.csv). | English; reproduction requires Python 3.11+, NumPy, and Matplotlib; some scripts access arXiv / OpenAlex. The corpus was frozen in **July 2026** and publicly released in September. |
| [RSI Atlas · aniruddhaadak80/RSI](https://github.com/aniruddhaadak80/RSI) | Illustrates improvement loops, evaluation, and change admission, with a small Python example for learning how to accept / reject candidate changes and record their history. | [Start With Simple Words](https://aniruddhaadak-rsi.vercel.app/docs/start) → [Python admission-gate example](https://github.com/aniruddhaadak80/RSI/blob/main/engine/rsi_loop.py). | English; the example uses the Python 3.10+ standard library. It makes decisions from externally supplied test status, gains, and file paths; it does not generate changes with a model or run evaluations automatically. |

<a id="verification"></a>

## Freshness and Review Records

This batch was reviewed on **2026-10-22**. We read project READMEs, recommended chapters or course pages, and inspected relevant code for entries with practical components. **We did not run upstream tutorials, call models, reproduce experiments, or review every paper in the lists.** For videos, we only checked the links provided on course pages.

The table records supported content changes, releases, or review dates reported by the upstream projects. These differ from this directory's review date and do not establish a cutoff for coverage of the entire field. Commit dates use Asia/Taipei; dates stated directly by upstream sources retain their original values.

<details>
<summary>Expand content dates and review scope for all 17 resources</summary>

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
| Stanford CS329A | The official website identifies the course as **Autumn 2025**. | Course overview, Schedule, and public paper reading links. |
| Harvard CS 2881R RSI topics | Archived lecture on **2025-10-09** and the newer lecture on **2026-09-24**. | Official course page and reading / slide / code links for both lectures; videos were not watched. |
| ICLR 2026 RSI Workshop | The official website gives the event date as **2026-04-26**. | Official themes, program, and Accepted Papers page. |
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
