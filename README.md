# A Systematic Survey of Large Language Model Routing

A survey of LLM routing methods organised by what the router does at decision time: predict, try and adjust, reason as an LLM, or study routing from the outside.

Citation-aligned reading list for **A Systematic Survey of Large Language Model Routing** — Chang Jiangeng, Xingyu Wu, Kay Chen Tan, Mengling Feng (Findings of EMNLP 2026).

[Paper](https://aclanthology.org/2026.findings-emnlp.2072/) · [PDF](https://aclanthology.org/2026.findings-emnlp.2072.pdf) · [BibTeX](https://aclanthology.org/2026.findings-emnlp.2072.bib)

**97/97 references accounted for.** 34 predictive · 20 adaptive · 6 generative · 17 infrastructure · 14 adjacent/hybrid · 8 background. Every entry keeps the survey's paradigm label and its own description of what the method does.

## How this list is built

- Rows come from the survey's master inventory (Figure 2 and Tables 2–3) plus the per-paradigm appendix tables (C.1–C.4, Tables 4–7), which give a *Primary contribution* line for each method.
- Each row is resolved to exactly one entry of the paper's reference list by first author + year, so the mapping is checkable. Links use the arXiv/DOI printed in that entry, otherwise a Google Scholar lookup.
- Labels are the survey's own: **P** predictive · **A** adaptive · **G** generative · **I** infrastructure · **Adj** adjacent · **Ext** extension · **H** hybrid.
- References cited only for framing (classical algorithm selection, related surveys, side-channel attacks, model merging) are listed in the last section instead of being forced into a paradigm.
- Machine-readable version with the reference index and the section where each work is cited: [`data/papers.json`](data/papers.json).

## Contents

1. [Predictive routing](#1-predictive-routing) — 34
2. [Adaptive routing](#2-adaptive-routing) — 20
3. [Generative routing](#3-generative-routing) — 6
4. [Infrastructure](#4-infrastructure) — 17
5. [Adjacent work and aggregation](#5-adjacent-work-and-aggregation) — 14
6. [Background and related surveys](#6-background-and-related-surveys) — 8
7. [Full bibliography](#full-bibliography)

## 1. Predictive routing

Score every candidate before its answer exists, then commit to one cost-adjusted choice per query (survey §3.1).

### Classification and heuristic

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Tryage** `P` | [Tryage: Real-time, intelligent routing of user prompts to large language models](https://arxiv.org/abs/2308.11601) | 2023 | arXiv:2308.11601 | Gold | *22 models, API* — Real-time prompt classifier dispatching to a pool of expert LLMs |
| **CoE** `P` | [Composition of experts: A modular compound AI system leveraging large language models](https://arxiv.org/abs/2412.01868) | 2024 | arXiv:2412.01868 | Gold | *5+ models, API* — Two-step routing: classify input into category, then map category to expert LLM |
| **Hybrid LLM** `P` | [Hybrid LLM: Cost-efficient and quality-aware query routing](https://scholar.google.com/scholar?q=Hybrid+LLM:+Cost-efficient+and+quality-aware+query+routing+Ding) | 2024 | ICLR 2024 | Gold | Binary query-difficulty classifier that chooses between a small and a large model; evaluated on MixInstruct. |
| **MoDEM** `P` | [MoDEM: Mixture of domain expert models](https://scholar.google.com/scholar?q=MoDEM:+Mixture+of+domain+expert+models+Simonds) | 2024 | ALTA 2024 | Gold | *5 models, API* — DeBERTa-v3-large classifier routing to one of five domain expert LLMs (math/health/science/coding/other) |
| **OptLLM** `P` | [OptLLM: Optimal assignment of queries to large language models](https://scholar.google.com/scholar?q=OptLLM:+Optimal+assignment+of+queries+to+large+language+models+Liu) | 2024 | ICWS 2024 | Gold | *12 models, API* — Multi-label classifier with uncertainty plus iterative non-dominated assignment |
| **BEST-Route** `P/H` | [BEST-Route: Adaptive LLM routing with test-time optimal compute](https://scholar.google.com/scholar?q=BEST-Route:+Adaptive+LLM+routing+with+test-time+optimal+compute+Ding) | 2025 | ICML 2025 | Gold | *8 models, API* — Joint pre-inference choice of model identity and sample count |
| **GraphRouter** `P` | [GraphRouter: A graph-based router for LLM selections](https://scholar.google.com/scholar?q=GraphRouter:+A+graph-based+router+for+LLM+selections+Feng) | 2025 | ICLR 2025 | Gold | *10+ models, GPU* — Heterogeneous-graph router with HGT message passing for inductive new-model attachment |
| **One-Head** `P` | [One head, many models: Cross-attention routing for cost-aware LLM selection](https://arxiv.org/abs/2509.09782) | 2025 | arXiv:2509.09782 | Gold | *5 models, GPU* — Single cross-attention head over the candidate-LLM pool |
| **RouteLLM (SW/MF/CLS + LLM)** `P` | [RouteLLM: Learning to route LLMs from preference data](https://scholar.google.com/scholar?q=RouteLLM:+Learning+to+route+LLMs+from+preference+data+Ong) | 2025 | ICLR 2025 | Preference | *2 models, API* — Preference-driven router family — Bradley–Terry similarity weighting, matrix factorization and a BERT classifier — plus a causal-LLM scorer at full-LLM scale. |
| **Select-then-Route** `P/A` | [Select-then-Route: Taxonomy guided routing for LLMs](https://scholar.google.com/scholar?q=Select-then-Route:+Taxonomy+guided+routing+for+LLMs+Shah) | 2025 | EMNLP 2025 | Gold | *22 models, API* — Two-stage taxonomy classifier narrows pool, then confidence-based cascade routes within (EMNLP 2025 Industry) |
| **SkewRoute** `P` | [SkewRoute: Training-free LLM routing for knowledge graph retrieval-augmented generation via score skewness of retrieved context](https://scholar.google.com/scholar?q=SkewRoute:+Training-free+LLM+routing+for+knowledge+graph+retrieval-augmented+generation+via+score+skewness+of+retrieved+context+Wang) | 2025 | Findings of EMNLP 2025 | Confidence | *2 models, API* — Training-free score-skewness rule selects a smaller or larger LLM for KG-RAG |

### Performance regression

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Eagle** `P` | [Eagle: Efficient training-free router for multi-LLM inference](https://arxiv.org/abs/2409.15518) | 2024 | arXiv:2409.15518 | Pairwise | *11 models, API* — Training-free ELO ranker using global plus local pairwise outcomes |
| **Zooter** `P` | [Routing to the expert: Efficient reward-guided ensemble of large language models](https://scholar.google.com/scholar?q=Routing+to+the+expert:+Efficient+reward-guided+ensemble+of+large+language+models+Lu) | 2024 | NAACL 2024 | Preference | *6 models, API* — Distills reward-model signal into a lightweight router via knowledge distillation |
| **CARROT** `P` | [CARROT: A cost aware rate optimal router](https://arxiv.org/abs/2502.03261) | 2025 | arXiv:2502.03261 | Gold | *14 models, API* — Minimax rate-optimal cost-accuracy router; introduces SPROUT benchmark |
| **InferenceDynamics** `P` | [InferenceDynamics: Efficient routing across LLMs through structured capability and knowledge profiling](https://arxiv.org/abs/2505.16303) | 2025 | arXiv:2505.16303 | Gold | *8 models, API* — Decomposes LLMs into capability and knowledge dimensions combined as a weighted score |
| **IPR** `P` | [IPR: Intelligent prompt routing with user-controlled quality-cost trade-offs](https://scholar.google.com/scholar?q=IPR:+Intelligent+prompt+routing+with+user-controlled+quality-cost+trade-offs+Feng) | 2025 | EMNLP 2025 | Gold | *6 models, API* — Quality-cost regression with user-controlled tolerance; deployed on AWS workload (EMNLP 2025 Industry) |
| **Causal LLM Routing** `P` | [Causal LLM Routing: End-to-end regret minimization from observational data](https://scholar.google.com/scholar?q=Causal+LLM+Routing:+End-to-end+regret+minimization+from+observational+data+Tsiourvas) | 2026 | NeurIPS 2026 | — | *13 models, API* — End-to-end regret minimization via classification + softmax-weighted surrogates with cost-sensitivity conditioning |
| **RouteMoA** `P/H` | [RouteMoA: Dynamic routing without pre-inference boosts efficient mixture-of-agents](https://arxiv.org/abs/2601.18130) | 2026 | arXiv:2601.18130 | Gold | Lightweight scorer plus LLM-judge refinement to pick models and sample counts for mixture-of-agents pools. |
| **SEMIROUTER** `P` | [SEMIROUTER: Sparse-data enhanced routing for adaptive multi-LLM system](https://scholar.google.com/scholar?q=SEMIROUTER:+Sparse-data+enhanced+routing+for+adaptive+multi-LLM+system+Wang) | 2026 | EACL 2026 | Gold (sparse) | *API* — Adaptive scorer trained under sparse query-by-model annotations; integrates new candidates with limited supervision (EACL 2026) |

### Query similarity

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **RouterDC** `P` | [RouterDC: Query-based router by dual contrastive learning for assembling large language models](https://scholar.google.com/scholar?q=RouterDC:+Query-based+router+by+dual+contrastive+learning+for+assembling+large+language+models+Chen) | 2024 | NeurIPS 2024 | — | *7 models, GPU* — Dual contrastive learning over (query, LLM) and (query, query) pairs |
| **EmbedLLM** `P` | [EmbedLLM: Learning compact representations of large language models](https://scholar.google.com/scholar?q=EmbedLLM:+Learning+compact+representations+of+large+language+models+Zhuang) | 2025 | ICLR 2025 | Gold | *112 models, GPU* — Learnable LLM embeddings; bilinear (q,m) scoring |
| **Model-SAT** `P` | [Capability instruction tuning](https://scholar.google.com/scholar?q=Capability+instruction+tuning+Zhang) | 2025 | AAAI 2025 | Gold | *66 models, GPU* — Capability-instruction-tuning encoder; learned skill profiles for matching |
| **RadialRouter** `P` | [RadialRouter: Structured representation for efficient and robust large language models routing](https://scholar.google.com/scholar?q=RadialRouter:+Structured+representation+for+efficient+and+robust+large+language+models+routing+Jin) | 2025 | Findings of EMNLP 2025 | Gold | *11 models, GPU* — RadialFormer Transformer with structured query-LLMs interaction; cost-aware evaluation (Findings EMNLP 2025) |
| **UniRoute** `P` | [Universal model routing for efficient LLM inference](https://arxiv.org/abs/2502.08773) | 2025 | arXiv:2502.08773 | Gold | *30+ models, GPU* — Probe-set fingerprints + cluster mapping; excess-risk bound for unseen models |
| **ContextualRouter** `P` | [Generalising LLM routing using past performance retrieval: A few-shot router is sufficient](https://scholar.google.com/scholar?q=Generalising+LLM+routing+using+past+performance+retrieval:+A+few-shot+router+is+sufficient+Varangot-Reille) | 2026 | EACL 2026 | Gold | *5+ models, API* — Past-performance retrieval with attention reweighting; effective with 1% historical data (EACL 2026 SRW) |

### Recommender system

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **IRT-Router** `P` | [IRT-Router: Effective and interpretable multillm routing via item response theory](https://scholar.google.com/scholar?q=IRT-Router:+Effective+and+interpretable+multillm+routing+via+item+response+theory+Song) | 2025 | ACL 2025 | Gold | *20 models, GPU* — Item-Response-Theory psychometric router; interpretable difficulty / discrimination |
| **RADAR** `P` | [RADAR: Reasoning-ability and difficulty-aware routing for reasoning LLMs](https://arxiv.org/abs/2509.25426) | 2025 | arXiv:2509.25426 | Gold | *35 models, API* — IRT-style joint modelling of per-LLM reasoning ability and per-query difficulty |
| **LLMRec** `P` | [Let the LLM stick to its strengths: Learning to route economical LLM](https://scholar.google.com/scholar?q=Let+the+LLM+stick+to+its+strengths:+Learning+to+route+economical+LLM+Zhang) | 2026 | NeurIPS 2026 | Gold | Recommender-system formulation that routes over 52 training and 10 evaluation LLMs. |

### Other / extensions

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **OmniRouter** `P` | [OmniRouter: Budget and performance controllable multi-LLM routing](https://scholar.google.com/scholar?q=OmniRouter:+Budget+and+performance+controllable+multi-LLM+routing+Mei) | 2025 | SIGKDD Explorations | Gold | *12 models, API* — Joint budget and performance controls; explicit Pareto-frontier coverage |
| **ThriftLLM** | [ThriftLLM: On cost-effective selection of large language models for classification queries](https://scholar.google.com/scholar?q=ThriftLLM:+On+cost-effective+selection+of+large+language+models+for+classification+queries+Huang) | 2025 | VLDB | — | Hard-budget variant of the standard routing objective, for classification queries (§2, Eq. 1). |
| **ICL Router** | [ICL Router: In-context learned model representations for LLM routing](https://scholar.google.com/scholar?q=ICL+Router:+In-context+learned+model+representations+for+LLM+routing+Wang) | 2026 | AAAI 2026 | — | Builds in-context capability profiles from query vectors and correctness labels, so new models can be added without retraining the router (§3.1). |
| **Meta-Router** `P` | [Meta-Router: Bridging gold-standard and preference-based evaluations in LLM routing](https://scholar.google.com/scholar?q=Meta-Router:+Bridging+gold-standard+and+preference-based+evaluations+in+LLM+routing+Zhang) | 2026 | ICLR 2026 | Causal | *2 models, API* — CATE estimation combining gold-standard and biased preference signals (pairwise routing) |
| **MTRouter** | [MTRouter: Cost-aware multi-turn LLM routing with history-model joint embeddings](https://scholar.google.com/scholar?q=MTRouter:+Cost-aware+multi-turn+LLM+routing+with+history-model+joint+embeddings+Zhang) | 2026 | ACL 2026 | — | Jointly embeds dialogue history and candidates; a stateful predictive router under a conversation budget (§2). |

## 2. Adaptive routing

Try a model, observe the feedback, then commit, defer or update (§3.2).

### Cascade

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **FrugalGPT** | [FrugalGPT: How to use large language models while reducing cost and improving performance](https://arxiv.org/abs/2305.05176) | 2023 | arXiv:2305.05176 | — | *12 models, API* — First confidence-based cascade; popularized the cheap-to-expensive escalation pattern |
| **AutoMix** `A` | [AutoMix: Automatically mixing language models](https://scholar.google.com/scholar?q=AutoMix:+Automatically+mixing+language+models+Aggarwal) | 2024 | NeurIPS 2024 | Confidence | *5 models, API* — Self-verification cascade; cheaper LLM verifies its own answer before escalating |
| **MoT-Cascade** `A` | [Large language model cascades with mixture of thought representations for cost-efficient reasoning](https://scholar.google.com/scholar?q=Large+language+model+cascades+with+mixture+of+thought+representations+for+cost-efficient+reasoning+Yue) | 2024 | ICLR 2024 | Confidence | *2 models, API* — Cascade with mixed Chain-of-Thought and Program-of-Thought consistency check as escalation trigger |
| **Cascadia** `A` | [Cascadia: An efficient cascade serving system for large language models](https://arxiv.org/abs/2506.04203) | 2025 | arXiv:2506.04203 | Confidence | *3 models, API* — Cascade serving system; queries flow through a chain of LLMs of increasing capability |
| **SATER** `P/A` | [SATER: A self-aware and token-efficient approach to routing and cascading](https://scholar.google.com/scholar?q=SATER:+A+self-aware+and+token-efficient+approach+to+routing+and+cascading+Shen) | 2025 | EMNLP 2025 | Confidence | *3 models, API* — Self-aware combined routing+cascade; >50% cost and >80% latency reduction (EMNLP 2025) |
| **Unified R&C** `A` | [A unified approach to routing and cascading for LLMs](https://scholar.google.com/scholar?q=A+unified+approach+to+routing+and+cascading+for+LLMs+Dekoninck) | 2025 | ICML 2025 | Gold | *11 models, API* — Theoretical unification of routing and cascading; Pareto-optimality proof |
| **MESS+** `A` | [MESS+: Dynamically learned inference-time LLM routing in model zoos with service level guarantees](https://scholar.google.com/scholar?q=MESS+:+Dynamically+learned+inference-time+LLM+routing+in+model+zoos+with+service+level+guarantees+Woisetschläger) | 2026 | NeurIPS 2026 | Gold | *2 models, API* — Service-level-agreement guarantees; routes to satisfy SLA with high probability |
| **TRIM** `A` | [TRIM: Hybrid inference via targeted stepwise routing in multi-step reasoning tasks](https://arxiv.org/abs/2601.10245) | 2026 | arXiv:2601.10245 | RL | *2+ models, API* — Per-step routing inside chain-of-thought; escalates only uncertainty-critical reasoning steps under a budget |

### Bandit and online

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **BaRP** `A` | [Learning to route LLMs from bandit feedback: One policy, many trade-offs](https://arxiv.org/abs/2510.07429) | 2025 | arXiv:2510.07429 | Bandit | *8 models, API* — Trade-off-conditioned bandit; one policy covers entire Pareto frontier |
| **Dueling Feedback** `A` | [LLM routing with dueling feedback](https://arxiv.org/abs/2510.00841) | 2025 | arXiv:2510.00841 | CDB | *11 models, API* — Contextual Dueling Bandit formalization; sublinear regret bound for FGTS.CDB |
| **LLM Bandit** `A` | [LLM Bandit: Cost-efficient LLM generation via preference-conditioned dynamic routing](https://arxiv.org/abs/2502.02743) | 2025 | arXiv:2502.02743 | Bandit | *15+ models, API* — Preference-conditioned multi-armed bandit; large LLM pool |
| **MixLLM (Wang)** `A` | [MixLLM: Dynamic routing in mixed large language models](https://scholar.google.com/scholar?q=MixLLM:+Dynamic+routing+in+mixed+large+language+models+Wang) | 2025 | NAACL 2025 | Bandit | *API* — Contextual-bandit dynamic routing balancing quality, cost, latency; supports continual learning (NAACL 2025) |
| **PickLLM** `A` | [PickLLM: Context-aware rl-assisted large language model routing](https://scholar.google.com/scholar?q=PickLLM:+Context-aware+rl-assisted+large+language+model+routing+Sikeridis) | 2025 | International Workshop on AI for Transportation | RL | *4 models, API* — Q-learning router that adapts on the fly to the runtime query distribution and observed reward |
| **Reward Routing** `A/Ext` | [Reward model routing in alignment](https://arxiv.org/abs/2510.02850) | 2025 | arXiv:2510.02850 | Bandit | *API* — Contextual bandit over candidate reward models during DPO and online alignment (component-level routing) |
| **StageRoute** `A` | [Near-optimal online deployment and routing for streaming LLMs](https://arxiv.org/abs/2506.17254) | 2025 | arXiv:2506.17254 | Bandit | *API* — Online deployment + routing for streaming queries; near-optimal regret under periodic pool redeployment |
| **LinUCB** `A` | [Online multillm selection via contextual bandits under unstructured context evolution](https://scholar.google.com/scholar?q=Online+multillm+selection+via+contextual+bandits+under+unstructured+context+evolution+Poon) | 2026 | AAAI 2026 | Bandit | *6 models, API* — Unstructured-context LinUCB; sublinear regret without context-distribution assumptions |
| **MixLLM (Ding)** `A` | [MixLLM: Selecting large language models with high-quality results and minimum inference cost for multi-stage complex tasks](https://scholar.google.com/scholar?q=MixLLM:+Selecting+large+language+models+with+high-quality+results+and+minimum+inference+cost+for+multi-stage+complex+tasks+Ding) | 2026 | Preprint | Gold | Model selection across multi-stage tasks under a quality target, trained on gold multi-stage outcomes. |
| **Not-a-Bandit** `A/Ext` | [Not-a-Bandit: Provably noregret drafter selection in speculative decoding for LLMs](https://scholar.google.com/scholar?q=Not-a-Bandit:+Provably+noregret+drafter+selection+in+speculative+decoding+for+LLMs+Liu) | 2026 | ICLR 2026 | Full information | *7 models, Local* — HedgeSpec full-information no-regret drafter selection inside speculative decoding |

### Confidence deferral

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Self-Route** `A/G/Ext` | [Retrieval augmented generation or long-context LLMs? a comprehensive study and hybrid approach](https://scholar.google.com/scholar?q=Retrieval+augmented+generation+or+long-context+LLMs?+a+comprehensive+study+and+hybrid+approach+Li) | 2024 | EMNLP 2024 | Confidence | Confidence-triggered cascade between retrieval-augmented generation and a long-context LLM, with an LLM judge; NarrativeQA and HotpotQA. |
| **Self-REF (deferral)** `A/G` | [Learning to route LLMs with confidence tokens](https://scholar.google.com/scholar?q=Learning+to+route+LLMs+with+confidence+tokens+Chuang) | 2025 | ICML 2025 | Confidence | *3 models, GPU* — Native confidence tokens drive a learned deferral cascade · Native confidence-token decoding as the routing primitive |

## 3. Generative routing

The router is an LLM emitting a routing trajectory, or the decision is distributed across candidates (§3.3).

### LLM as router

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Arch-Router** `G` | [Arch-Router: Aligning LLM routing with human preferences](https://arxiv.org/abs/2506.16655) | 2025 | arXiv:2506.16655 | SFT | *6 models, GPU* — SFT 1.5B model for domain-and-action matching; intent-aligned routing |
| **Generalized Routing** `G/H` | [Towards generalized routing: Model and agent orchestration for adaptive and efficient inference](https://arxiv.org/abs/2509.07571) | 2025 | arXiv:2509.07571 | Gold | *5+ models, GPU* — Mixture of Models and Agents (MoMA) routing layer for unified orchestration over LLMs and agents |
| **MasRouter** `G` | [MasRouter: Learning to route LLMs for multi-agent systems](https://scholar.google.com/scholar?q=MasRouter:+Learning+to+route+LLMs+for+multi-agent+systems+Yue) | 2025 | ACL 2025 | Gold | *5 models, GPU* — Constructs a multi-agent system through cascaded decisions over collaboration mode, role allocation, and LLM choice |
| **Router-R1** `G/H` | [Router-R1: Teaching LLMs multi-round routing and aggregation via reinforcement learning](https://scholar.google.com/scholar?q=Router-R1:+Teaching+LLMs+multi-round+routing+and+aggregation+via+reinforcement+learning+Zhang) | 2026 | NeurIPS 2026 | RL | *6 models, GPU* — PPO-trained 3B LLM-as-router with multi-round <think>, <search>, <info>, and <answer> actions |

### Distributed self-routing

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **DiSRouter** `G` | [DiSRouter: Distributed self-routing for LLM selections](https://arxiv.org/abs/2510.19208) | 2025 | arXiv:2510.19208 | — | *5 models, GPU* — Distributed self-routing via PPO and self-awareness SFT; no central router |

### Strategy extensions

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **DeepSieve** `G/Ext` | [DeepSieve: Information sieving via LLM-as-a-knowledge-router](https://scholar.google.com/scholar?q=DeepSieve:+Information+sieving+via+LLM-as-a-knowledge-router+Guo) | 2026 | Findings of ACL 2026 | Confidence | LLM-as-knowledge-router that progressively filters candidate answers using a confidence signal; multi-hop QA and RAG. |

## 4. Infrastructure

Work that does not route but studies routing from outside: benchmarks, attacks, serving systems, theory (§3.4).

### Benchmarks

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **MixInstruct** | [LLM-blender: Ensembling large language models with pairwise ranking and generative fusion](https://scholar.google.com/scholar?q=LLM-blender:+Ensembling+large+language+models+with+pairwise+ranking+and+generative+fusion+Jiang) | 2023 | ACL 2023 | — | Benchmark · Pairwise preference benchmark seeded from LLM-Blender; widely reused |
| **RouterBench** `I` | [RouterBench: A benchmark for multi-LLM routing system](https://arxiv.org/abs/2403.12031) | 2024 | arXiv:2403.12031 | Gold | Benchmark · Early widely used routing benchmark; 405k responses across 11 LLMs and 8 task suites |
| **RouterEval** `I` | [RouterEval: A comprehensive benchmark for routing LLMs to explore model-level scaling up in LLMs](https://arxiv.org/abs/2503.10657) | 2025 | arXiv:2503.10657 | Gold | Benchmark · More than 200 million performance records from over 8,500 LLMs across 12 evaluations |
| **LLMRouterBench** `I` | [LLMRouterBench: A massive benchmark and unified framework for LLM routing](https://arxiv.org/abs/2601.07206) | 2026 | arXiv:2601.07206 | Gold | Benchmark · More than 400K instances from 21 datasets and 33 models; unified evaluation of ten routing baselines |
| **RouterArena** `I` | [RouterArena: An open platform for comprehensive comparison of LLM routers](https://scholar.google.com/scholar?q=RouterArena:+An+open+platform+for+comprehensive+comparison+of+LLM+routers+Lu) | 2026 | ICLR 2026 | Gold | Benchmark · Multi-domain (9 top-level, 44 categories); three empirical difficulty bands plus Bloom-taxonomy cognitive labels; continuously updated open platform |

### Adversarial

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **InputSnatch** | [InputSnatch: Stealing input in LLM services via timing side-channel attacks](https://arxiv.org/abs/2411.18191) | 2024 | arXiv:2411.18191 | — | Timing side-channel that steals inputs from shared LLM serving infrastructure (§3.4). |
| **Rerouting Routers** `I` | [Rerouting LLM routers](https://arxiv.org/abs/2501.01818) | 2025 | arXiv:2501.01818 | – | Attack · White-box and transfer attacks using query-independent confounder gadgets |
| **Whisper Leak** | [Whisper Leak: A side-channel attack on large language models](https://arxiv.org/abs/2511.03675) | 2025 | arXiv:2511.03675 | — | Side-channel on commercial LLM APIs leaking prompt content from encrypted-traffic metadata; an adjacent serving risk, not a router attack (§3.4). |
| **R2A** `I` | [Route to rome attack: Directing LLM routers to expensive models via adversarial suffix optimization](https://arxiv.org/abs/2604.15022) | 2026 | arXiv:2604.15022 | – | Attack · Query-limited black-box attack evaluated on seven open routers and two commercial services |
| **RerouteGuard** `I` | [RerouteGuard: Understanding and mitigating adversarial risks for LLM routing](https://arxiv.org/abs/2601.21380) | 2026 | arXiv:2601.21380 | – | Defence · Embedding-based anomaly detection with adaptive thresholding |
| **Router Fragility** `I` | [How robust are router-LLMs? analysis of the fragility of LLM routing capabilities](https://scholar.google.com/scholar?q=How+robust+are+router-LLMs?+analysis+of+the+fragility+of+LLM+routing+capabilities+Kassem) | 2026 | EACL 2026 | – | Audit · Demonstrates that off-the-shelf routers route jailbreaks to weakly aligned models |
| **Routing Collapse** `I` | [When routing collapses: On the degenerate convergence of LLM routers](https://arxiv.org/abs/2602.03478) | 2026 | arXiv:2602.03478 | – | Analysis · Diagnoses training-time pathology where routers collapse to a single dominant model |

### Systems

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Eff. Scheduling** `I/Adj` | [Efficient LLM scheduling by learning to rank](https://scholar.google.com/scholar?q=Efficient+LLM+scheduling+by+learning+to+rank+Fu) | 2024 | NeurIPS 2024 | Rank | Learning-to-rank scheduler that exploits predicted output lengths to raise serving throughput; evaluated on serving traces. |
| **vLLM Semantic Router / Workload-Router-Pool** `I` | [The workload-router-pool architecture for LLM inference optimization: A vision paper from the vllm semantic router project](https://arxiv.org/abs/2603.21354) | 2026 | arXiv:2603.21354 | – | System · Vision paper (references open-source components: vLLM Semantic Router, OpenClaw); workload–router–pool architecture |

### Theory

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **Routing & Cascades** `I` | [Routing, cascades, and user choice for LLMs](https://arxiv.org/abs/2602.09902) | 2026 | arXiv:2602.09902 | – | Theory · Game-theoretic analysis of provider-side routing/cascades vs. user choice |

### Other / extensions

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **TensorOpera Router** `I` | [TensorOpera Router: A multi-model router for efficient LLM inference](https://scholar.google.com/scholar?q=TensorOpera+Router:+A+multi-model+router+for+efficient+LLM+inference+Stripelis) | 2024 | EMNLP 2024 | – | System · Predictive multi-model interface evaluated on throughput, monetary cost, and answer performance |
| **SPROUT** | [Carrot: A cost aware rate optimal router](https://arxiv.org/abs/2502.03261) | 2025 | arXiv:2502.03261 | — | Benchmark · Approximately 45K prompts from six suites evaluated across 14 LLMs |

## 5. Adjacent work and aggregation

Broader model-selection targets the survey labels Adj / Ext / H: aggregation, model merging, component-level routing (§3.5).

### Adjacent work and extensions

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **LLM-Blender** `Adj` | [LLM-Blender: Ensembling large language models with pairwise ranking and generative fusion](https://scholar.google.com/scholar?q=LLM-Blender:+Ensembling+large+language+models+with+pairwise+ranking+and+generative+fusion+Jiang) | 2023 | ACL 2023 | Pairwise | Pairwise ranker plus a generative fuser over a pool of LLM outputs — ensembling rather than single-model routing; evaluated on MixInstruct. |
| **Smoothie** `Adj` | [Smoothie: Label free language model routing](https://scholar.google.com/scholar?q=Smoothie:+Label+free+language+model+routing+Guha) | 2024 | NeurIPS 2024 | Unsupervised | Unsupervised latent quality model that predicts the winning model per query without labels; AlpacaEval, SQuAD, MixInstruct, GSM8K. |
| **Team formation (RL)** | [Team formation in large organizations: A deep reinforcement learning approach](https://scholar.google.com/scholar?q=Team+formation+in+large+organizations:+A+deep+reinforcement+learning+approach+Lv) | 2024 | Decision Support Systems | — | RL team formation; explicitly not an LLM routing method because the selected entities are people and no query is dispatched (§3.5). |
| **LLM Selector** `Adj` | [Active model selection for large language models](https://scholar.google.com/scholar?q=Active+model+selection+for+large+language+models+Durmazkeser) | 2025 | NeurIPS 2025 Workshop | — | Active labelling chooses which (query, model) pairs to evaluate, then a router is fitted; 6 benchmarks over 151 LLMs. |
| **Mordal** `Ext` | [Mordal: Automated pretrained model selection for vision language models](https://arxiv.org/abs/2502.00241) | 2025 | arXiv:2502.00241 | Gold | Learned scorer over VLM backbones that ranks vision-language models per query; VLM benchmarks. |
| **Adaptive continual merging** | [Towards adaptive continual model merging via manifold-aware expert evolution](https://arxiv.org/abs/2604.22464) | 2026 | arXiv:2604.22464 | — | Evolves expert sets by manifold-based subspace affinity and activates them without a learned gate (§3.5). |
| **Fine-grained model merging** | [Fine-grained model merging via modular expert recombination](https://arxiv.org/abs/2602.06552) | 2026 | arXiv:2602.06552 | — | Expert library plus a lightweight router that assembles a model per input under a storage constraint (§3.5). |
| **HM3** | [HM3: Hierarchical multiobjective model merging for pretrained models](https://scholar.google.com/scholar?q=HM3:+Hierarchical+multiobjective+model+merging+for+pretrained+models+Zhou) | 2026 | NeurIPS 2026 | — | Hierarchical multi-objective merging that optimises parameter and architecture spaces jointly (§3.5). |
| **HotelQuEST** `Adj` | [HotelQuEST: Balancing quality and efficiency in agentic search](https://scholar.google.com/scholar?q=HotelQuEST:+Balancing+quality+and+efficiency+in+agentic+search+Hadad) | 2026 | EACL 2026 | Gold | Benchmark and audit of 214 hotel queries for cost-aware routing. |
| **JiSi** | [Beyond gemini3-pro: Revisiting LLM routing and aggregation at scale](https://arxiv.org/abs/2601.01330) | 2026 | arXiv:2601.01330 | — | Switches between a directly routed answer and an aggregation strategy learned from a support set; hybrid routing + aggregation (§3.5). |
| **LEGO reassembly** | [Building LLMs like lego: Two-dimensional architecture reassembly of large language models](https://scholar.google.com/scholar?q=Building+LLMs+like+lego:+Two-dimensional+architecture+reassembly+of+large+language+models+Wu) | 2026 | ACL 2026 | — | Two-dimensional architecture reassembly across depth and within layers (§3.5). |
| **The Avengers** | [The Avengers: A routing recipe for collective intelligence in language models](https://scholar.google.com/scholar?q=The+Avengers:+A+routing+recipe+for+collective+intelligence+in+language+models+Zhang) | 2026 | AAAI 2026 | — | Learns a routing recipe that chooses candidates and may combine repeated samples by voting; routing + aggregation (§3.5). |

### Other / extensions

| Method | Paper | Year | Venue | Signal | Survey's one-line description |
|---|---|---|---|---|---|
| **HuggingGPT** `Adj` | [HuggingGPT: Solving AI tasks with chatgpt and its friends in hugging face](https://scholar.google.com/scholar?q=HuggingGPT:+Solving+AI+tasks+with+chatgpt+and+its+friends+in+hugging+face+Shen) | 2023 | NeurIPS 2023 | ICL | An LLM planner decomposes a request and calls specialist HuggingFace models; 24 HF tasks. |
| **Gorilla** `Adj` | [Gorilla: Large language model connected with massive apis](https://scholar.google.com/scholar?q=Gorilla:+Large+language+model+connected+with+massive+apis+Patil) | 2024 | NeurIPS 2024 | SFT | Fine-tuned LLM that emits the right API call from a large API set (APIBench, 1.6k+ APIs). |

## 6. Background and related surveys

Lineage and related surveys cited for framing, not as routing methods (§1).

| Reference | Year | Venue | Where | Why it is in the survey |
|---|---|---|---|---|
| [The algorithm selection problem](https://scholar.google.com/scholar?q=The+algorithm+selection+problem+Rice) — John R Rice | 1976 | Advances in computers | §1 | The classical algorithm-selection problem that the paper treats as the ancestor of LLM routing (§1). |
| [The llama 3 herd of models](https://arxiv.org/abs/2407.21783) — Aaron Grattafiori et al. | 2024 | arXiv:2407.21783 | §1 | Open-weight family used to show how broad the candidate pool has become (§1). |
| [Large language modelenhanced algorithm selection: Towards comprehensive algorithm representation](https://scholar.google.com/scholar?q=Large+language+modelenhanced+algorithm+selection:+Towards+comprehensive+algorithm+representation+Wu) — Xingyu Wu et al. | 2024 | IJCAI 2024 | §1 | Encodes algorithm code, selects task-relevant dimensions and matches them to problem features (§1). |
| [Doing more with lessimplementing routing strategies in large language model-based systems: An extended survey](https://scholar.google.com/scholar?q=Doing+more+with+lessimplementing+routing+strategies+in+large+language+model-based+systems:+An+extended+survey+Varangot-Reille) — Clovis Varangot-Reille et al. | 2025 | Preprint | §1 | Treats routing as one item on a broader resource-optimisation menu (§1). |
| [A unifying perspective on model reuse: From small to large pretrained models](https://scholar.google.com/scholar?q=A+unifying+perspective+on+model+reuse:+From+small+to+large+pretrained+models+Zhou) — Da-Wei Zhou and Han-Jia Ye | 2025 | IJCAI 2025 | §1 | Unifies model reuse from small to large pretrained models; cited in the algorithm-selection lineage (§1). |
| [Llmdriven evolutionary algorithm selection: Bidirectional framework and sampling paradigm](https://scholar.google.com/scholar?q=Llmdriven+evolutionary+algorithm+selection:+Bidirectional+framework+and+sampling+paradigm+Wu) — Xingyu Wu et al. | 2025 | ICML 2025 | §1 | Bidirectional LLM-driven evolutionary search over algorithm portfolios (§1). |
| [Towards robustness and explainability of automatic algorithm selection](https://scholar.google.com/scholar?q=Towards+robustness+and+explainability+of+automatic+algorithm+selection+Wu) — Xingyu Wu et al. | 2025 | ICML 2025 | §1 | Models conditional mechanisms with a DAG for robust, explainable algorithm selection (§1). |
| [Dynamic model routing and cascading for efficient LLM inference: A survey](https://arxiv.org/abs/2603.04445) — Yasmin Moslem and John D Kelleher | 2026 | arXiv:2603.04445 | §1 | Survey of dynamic model routing and cascading; one of the two starting points the paper contrasts with (§1, §6). |

<a id="full-bibliography"></a>

## Full bibliography

- Pranjal Aggarwal, Aman Madaan, Ankit Anand, Srividya Pranavi Potharaju, Swaroop Mishra, Pei Zhou, Aditya Gupta, Dheeraj Rajagopal, Karthik Kappaganthu, Yiming Yang, and 1 others (2024). *AutoMix: Automatically mixing language models*. NeurIPS 2024. [link](https://scholar.google.com/scholar?q=AutoMix:+Automatically+mixing+language+models+Aggarwal)
- Lingjiao Chen, Matei Zaharia, and James Zou (2023). *FrugalGPT: How to use large language models while reducing cost and improving performance*. arXiv:2305.05176. [link](https://arxiv.org/abs/2305.05176)
- Shuhao Chen, Weisen Jiang, Baijiong Lin, James Kwok, and Yu Zhang (2024). *RouterDC: Query-based router by dual contrastive learning for assembling large language models*. NeurIPS 2024. [link](https://scholar.google.com/scholar?q=RouterDC:+Query-based+router+by+dual+contrastive+learning+for+assembling+large+language+models+Chen)
- Huamin Chen, Xunzhuo Liu, Bowei He, Fuyuan Lyu, Yankai Chen, Xue Liu, Yuhan Liu, and Junchen Jiang (2026). *The workload-router-pool architecture for LLM inference optimization: A vision paper from the vllm semantic router project*. arXiv:2603.21354. [link](https://arxiv.org/abs/2603.21354)
- Chao-Kai Chiang, Takashi Ishida, and Masashi Sugiyama (2025). *LLM routing with dueling feedback*. arXiv:2510.00841. [link](https://arxiv.org/abs/2510.00841)
- Yu-Neng Chuang, Prathusha Kameswara Sarma, Parikshit Gopalan, John Boccio, Sara Bolouki, Xia Hu, and Helen Zhou (2025). *Learning to route LLMs with confidence tokens*. ICML 2025. [link](https://scholar.google.com/scholar?q=Learning+to+route+LLMs+with+confidence+tokens+Chuang)
- Jasper Dekoninck, Maximilian Baader, and Martin Vechev (2025). *A unified approach to routing and cascading for LLMs*. ICML 2025. [link](https://scholar.google.com/scholar?q=A+unified+approach+to+routing+and+cascading+for+LLMs+Dekoninck)
- Dujian Ding, Ankur Mallick, Chi Wang, Robert Sim, Subhabrata Mukherjee, Victor Rühle, Laks Lakshmanan, and Ahmed H Awadallah (2024). *Hybrid LLM: Cost-efficient and quality-aware query routing*. ICLR 2024. [link](https://scholar.google.com/scholar?q=Hybrid+LLM:+Cost-efficient+and+quality-aware+query+routing+Ding)
- Dujian Ding, Ankur Mallick, Shaokun Zhang, Chi Wang, Daniel Madrigal, Mirian Del Carmen Hipolito Garcia, Menglin Xia, Laks VS Lakshmanan, Qingyun Wu, and Victor Rühle (2025). *BEST-Route: Adaptive LLM routing with test-time optimal compute*. ICML 2025. [link](https://scholar.google.com/scholar?q=BEST-Route:+Adaptive+LLM+routing+with+test-time+optimal+compute+Ding)
- Mengsu Ding, Rong Zhu, Bolin Ding, and Jingren Zhou (2026). *MixLLM: Selecting large language models with high-quality results and minimum inference cost for multi-stage complex tasks*. Preprint. [link](https://scholar.google.com/scholar?q=MixLLM:+Selecting+large+language+models+with+high-quality+results+and+minimum+inference+cost+for+multi-stage+complex+tasks+Ding)
- Yavuz Durmazkeser, Patrik Okanovic, Andreas Kirsch, Torsten Hoefler, and Nezihe Merve Gürel (2025). *Active model selection for large language models*. NeurIPS 2025 Workshop. [link](https://scholar.google.com/scholar?q=Active+model+selection+for+large+language+models+Durmazkeser)
- Aosong Feng, Balasubramaniam Srinivasan, Yun Zhou, Zhichao Xu, Kang Zhou, Sheng Guan, Yueyan Chen, Xian Wu, Ninad Kulkarni, Yi Zhang, and 1 others (2025a). *IPR: Intelligent prompt routing with user-controlled quality-cost trade-offs*. EMNLP 2025. [link](https://scholar.google.com/scholar?q=IPR:+Intelligent+prompt+routing+with+user-controlled+quality-cost+trade-offs+Feng)
- Tao Feng, Yanzhen Shen, and Jiaxuan You (2025b). *GraphRouter: A graph-based router for LLM selections*. ICLR 2025. [link](https://scholar.google.com/scholar?q=GraphRouter:+A+graph-based+router+for+LLM+selections+Feng)
- Nigel Fernandez, Branislav Kveton, Ryan A Rossi, Andrew S Lan, and Zichao Wang (2025). *RADAR: Reasoning-ability and difficulty-aware routing for reasoning LLMs*. arXiv:2509.25426. [link](https://arxiv.org/abs/2509.25426)
- Yichao Fu, Siqi Zhu, Runlong Su, Aurick Qiao, Ion Stoica, and Hao Zhang (2024). *Efficient LLM scheduling by learning to rank*. NeurIPS 2024. [link](https://scholar.google.com/scholar?q=Efficient+LLM+scheduling+by+learning+to+rank+Fu)
- Aaron Grattafiori, Abhimanyu Dubey, Abhinav Jauhri, Abhinav Pandey, Abhishek Kadian, Ahmad AlDahle, Aiesha Letman, Akhil Mathur, Alan Schelten, Alex Vaughan, and 1 others (2024). *The llama 3 herd of models*. arXiv:2407.21783. [link](https://arxiv.org/abs/2407.21783)
- Neel Guha, Mayee F Chen, Trevor Chow, Ishan S Khare, and Christopher Re (2024). *Smoothie: Label free language model routing*. NeurIPS 2024. [link](https://scholar.google.com/scholar?q=Smoothie:+Label+free+language+model+routing+Guha)
- Xiyu Guo, Shan Wang, Chunfang Ji, Xuefeng Zhao, Wenhao Xi, Yaoyao Liu, Qinglan Li, Chao Deng, and Junlan Feng (2025). *Towards generalized routing: Model and agent orchestration for adaptive and efficient inference*. arXiv:2509.07571. [link](https://arxiv.org/abs/2509.07571)
- Minghao Guo, Qingcheng Zeng, Xujiang Zhao, Yanchi Liu, Wenchao Yu, Mengnan Du, Haifeng Chen, and Wei Cheng (2026). *DeepSieve: Information sieving via LLM-as-a-knowledge-router*. Findings of ACL 2026. [link](https://scholar.google.com/scholar?q=DeepSieve:+Information+sieving+via+LLM-as-a-knowledge-router+Guo)
- Guy Hadad, Shadi Iskander, Sofia Tolmach, Oren Kalinsky, Haggai Roitman, and Ran Levy (2026). *HotelQuEST: Balancing quality and efficiency in agentic search*. EACL 2026. [link](https://scholar.google.com/scholar?q=HotelQuEST:+Balancing+quality+and+efficiency+in+agentic+search+Hadad)
- Surya Narayanan Hari and Matt Thomson (2023). *Tryage: Real-time, intelligent routing of user prompts to large language models*. arXiv:2308.11601. [link](https://arxiv.org/abs/2308.11601)
- Shiqi He, Insu Jang, and Mosharaf Chowdhury (2025). *Mordal: Automated pretrained model selection for vision language models*. arXiv:2502.00241. [link](https://arxiv.org/abs/2502.00241)
- Qitian Jason Hu, Jacob Bieker, Xiuyu Li, Nan Jiang, Benjamin Keigwin, Gaurav Ranganath, Kurt Keutzer, and Shriyash Kaustubh Upadhyay (2024). *RouterBench: A benchmark for multi-LLM routing system*. arXiv:2403.12031. [link](https://arxiv.org/abs/2403.12031)
- Keke Huang, Yimin Shi, Dujian Ding, Yifei Li, Yang Fei, Laks Lakshmanan, and Xiaokui Xiao (2025a). *ThriftLLM: On cost-effective selection of large language models for classification queries*. VLDB. [link](https://scholar.google.com/scholar?q=ThriftLLM:+On+cost-effective+selection+of+large+language+models+for+classification+queries+Huang)
- Zhongzhan Huang, Guoming Ling, Yupei Lin, Yandong Chen, Shanshan Zhong, Hefeng Wu, and Liang Lin (2025b). *RouterEval: A comprehensive benchmark for routing LLMs to explore model-level scaling up in LLMs*. arXiv:2503.10657. [link](https://arxiv.org/abs/2503.10657)
- Swayambhoo Jain, Ravi Raju, Bo Li, Zoltan Csaki, Jonathan Li, Kaizhao Liang, Guoyao Feng, Urmish Thakkar, Anand Sampat, Raghu Prabhakar, and 1 others (2024). *Composition of experts: A modular compound AI system leveraging large language models*. arXiv:2412.01868. [link](https://arxiv.org/abs/2412.01868)
- Dongfu Jiang, Xiang Ren, and Bill Yuchen Lin (2023). *LLM-blender: Ensembling large language models with pairwise ranking and generative fusion*. ACL 2023. [link](https://scholar.google.com/scholar?q=LLM-blender:+Ensembling+large+language+models+with+pairwise+ranking+and+generative+fusion+Jiang)
- Youhe Jiang, Fangcheng Fu, Wanru Zhao, Stephan Rabanser, Jintao Zhang, Nicholas D Lane, and Binhang Yuan (2025). *Cascadia: An efficient cascade serving system for large language models*. arXiv:2506.04203. [link](https://arxiv.org/abs/2506.04203)
- Ruihan Jin, Pengpeng Shao, Zhengqi Wen, Jinyang Wu, Mingkuan Feng, Shuai Zhang, and Jianhua Tao (2025). *RadialRouter: Structured representation for efficient and robust large language models routing*. Findings of EMNLP 2025. [link](https://scholar.google.com/scholar?q=RadialRouter:+Structured+representation+for+efficient+and+robust+large+language+models+routing+Jin)
- Wittawat Jitkrittum, Harikrishna Narasimhan, Ankit Singh Rawat, Jeevesh Juneja, Congchao Wang, Zifeng Wang, Alec Go, Chen-Yu Lee, Pradeep Shenoy, Rina Panigrahy, and 1 others (2025). *Universal model routing for efficient LLM inference*. arXiv:2502.08773. [link](https://arxiv.org/abs/2502.08773)
- Vansh Kapoor, Aman Gupta, Hao Chen, Anurag Beniwal, Jing Huang, and Aviral Kumar (2026). *TRIM: Hybrid inference via targeted stepwise routing in multi-step reasoning tasks*. arXiv:2601.10245. [link](https://arxiv.org/abs/2601.10245)
- Aly M Kassem, Bernhard Schölkopf, and Zhijing Jin (2026). *How robust are router-LLMs? analysis of the fragility of LLM routing capabilities*. EACL 2026. [link](https://scholar.google.com/scholar?q=How+robust+are+router-LLMs?+analysis+of+the+fragility+of+LLM+routing+capabilities+Kassem)
- Guannan Lai and Han-Jia Ye (2026). *When routing collapses: On the degenerate convergence of LLM routers*. arXiv:2602.03478. [link](https://arxiv.org/abs/2602.03478)
- Zhuowan Li, Cheng Li, Mingyang Zhang, Qiaozhu Mei, and Michael Bendersky (2024). *Retrieval augmented generation or long-context LLMs? a comprehensive study and hybrid approach*. EMNLP 2024. [link](https://scholar.google.com/scholar?q=Retrieval+augmented+generation+or+long-context+LLMs?+a+comprehensive+study+and+hybrid+approach+Li)
- Yang Li (2025). *LLM Bandit: Cost-efficient LLM generation via preference-conditioned dynamic routing*. arXiv:2502.02743. [link](https://arxiv.org/abs/2502.02743)
- Shaoang Li and Jian Li (2025). *Near-optimal online deployment and routing for streaming LLMs*. arXiv:2506.17254. [link](https://arxiv.org/abs/2506.17254)
- Hao Li, Yiqun Zhang, Zhaoyan Guo, Chenxu Wang, Shengji Tang, Qiaosheng Zhang, Yang Chen, Biqing Qi, Peng Ye, Lei Bai, and 1 others (2026). *LLMRouterBench: A massive benchmark and unified framework for LLM routing*. arXiv:2601.07206. [link](https://arxiv.org/abs/2601.07206)
- Yueyue Liu, Hongyu Zhang, Yuantian Miao, Van-Hoang Le, and Zhiqiang Li (2024). *OptLLM: Optimal assignment of queries to large language models*. ICWS 2024. [link](https://scholar.google.com/scholar?q=OptLLM:+Optimal+assignment+of+queries+to+large+language+models+Liu)
- Hongyi Liu, Jiaji Huang, Zhen Jia, Youngsuk Park, and Yu-Xiang Wang (2026). *Not-a-Bandit: Provably noregret drafter selection in speculative decoding for LLMs*. ICLR 2026. [link](https://scholar.google.com/scholar?q=Not-a-Bandit:+Provably+noregret+drafter+selection+in+speculative+decoding+for+LLMs+Liu)
- Keming Lu, Hongyi Yuan, Runji Lin, Junyang Lin, Zheng Yuan, Chang Zhou, and Jingren Zhou (2024). *Routing to the expert: Efficient reward-guided ensemble of large language models*. NAACL 2024. [link](https://scholar.google.com/scholar?q=Routing+to+the+expert:+Efficient+reward-guided+ensemble+of+large+language+models+Lu)
- Yifan Louie Lu, Rixin Liu, Jiayi Yuan, Xingqi Cui, Shenrun Zhang, Hongyi Liu, and Jiarong Xing (2026). *RouterArena: An open platform for comprehensive comparison of LLM routers*. ICLR 2026. [link](https://scholar.google.com/scholar?q=RouterArena:+An+open+platform+for+comprehensive+comparison+of+LLM+routers+Lu)
- Bing Lv, Junji Jiang, Likang Wu, and Hongke Zhao (2024). *Team formation in large organizations: A deep reinforcement learning approach*. Decision Support Systems. [link](https://scholar.google.com/scholar?q=Team+formation+in+large+organizations:+A+deep+reinforcement+learning+approach+Lv)
- Rafid Mahmood (2026). *Routing, cascades, and user choice for LLMs*. arXiv:2602.09902. [link](https://arxiv.org/abs/2602.09902)
- Geoff McDonald and Jonathan Bar Or (2025). *Whisper Leak: A side-channel attack on large language models*. arXiv:2511.03675. [link](https://arxiv.org/abs/2511.03675)
- Kai Mei, Wujiang Xu, Minghao Guo, Shuhang Lin, and Yongfeng Zhang (2025). *OmniRouter: Budget and performance controllable multi-LLM routing*. SIGKDD Explorations. [link](https://scholar.google.com/scholar?q=OmniRouter:+Budget+and+performance+controllable+multi-LLM+routing+Mei)
- Yasmin Moslem and John D Kelleher (2026). *Dynamic model routing and cascading for efficient LLM inference: A survey*. arXiv:2603.04445. [link](https://arxiv.org/abs/2603.04445)
- Isaac Ong, Amjad Almahairi, Vincent Wu, Wei-Lin Chiang, Tianhao Wu, Joseph E Gonzalez, Mohammed Kadous, and Ion Stoica (2025). *RouteLLM: Learning to route LLMs from preference data*. ICLR 2025. [link](https://scholar.google.com/scholar?q=RouteLLM:+Learning+to+route+LLMs+from+preference+data+Ong)
- Shishir G Patil, Tianjun Zhang, Xin Wang, and Joseph E Gonzalez (2024). *Gorilla: Large language model connected with massive apis*. NeurIPS 2024. [link](https://scholar.google.com/scholar?q=Gorilla:+Large+language+model+connected+with+massive+apis+Patil)
- Manhin Poon, XiangXiang Dai, Xutong Liu, Fang Kong, John CS Lui, and Jinhang Zuo (2026). *Online multillm selection via contextual bandits under unstructured context evolution*. AAAI 2026. [link](https://scholar.google.com/scholar?q=Online+multillm+selection+via+contextual+bandits+under+unstructured+context+evolution+Poon)
- Roshini Pulishetty, Mani Kishan Ghantasala, Keerthy Kaushik Dasoju, Niti Mangwani, Vishal Garimella, Aditya Mate, Somya Chatterjee, Yue Kang, Ehi Nosakhare, Sadid Hasan, and 1 others (2025). *One head, many models: Cross-attention routing for cost-aware LLM selection*. arXiv:2509.09782. [link](https://arxiv.org/abs/2509.09782)
- Haiyun Qiu, Xingyu Wu, Liang Feng, and Kay Chen Tan (2026a). *Fine-grained model merging via modular expert recombination*. arXiv:2602.06552. [link](https://arxiv.org/abs/2602.06552)
- Haiyun Qiu, Xingyu Wu, and Kay Chen Tan (2026b). *Towards adaptive continual model merging via manifold-aware expert evolution*. arXiv:2604.22464. [link](https://arxiv.org/abs/2604.22464)
- John R Rice (1976). *The algorithm selection problem*. Advances in computers. [link](https://scholar.google.com/scholar?q=The+algorithm+selection+problem+Rice)
- Avital Shafran, Roei Schuster, Thomas Ristenpart, and Vitaly Shmatikov (2025). *Rerouting LLM routers*. arXiv:2501.01818. [link](https://arxiv.org/abs/2501.01818)
- Soham Shah and Kumar Shridhar (2025). *Select-then-Route: Taxonomy guided routing for LLMs*. EMNLP 2025. [link](https://scholar.google.com/scholar?q=Select-then-Route:+Taxonomy+guided+routing+for+LLMs+Shah)
- Yongliang Shen, Kaitao Song, Xu Tan, Dongsheng Li, Weiming Lu, and Yueting Zhuang (2023). *HuggingGPT: Solving AI tasks with chatgpt and its friends in hugging face*. NeurIPS 2023. [link](https://scholar.google.com/scholar?q=HuggingGPT:+Solving+AI+tasks+with+chatgpt+and+its+friends+in+hugging+face+Shen)
- Yuanzhe Shen, Yide Liu, Zisu Huang, Ruicheng Yin, Xiaoqing Zheng, and Xuan-Jing Huang (2025). *SATER: A self-aware and token-efficient approach to routing and cascading*. EMNLP 2025. [link](https://scholar.google.com/scholar?q=SATER:+A+self-aware+and+token-efficient+approach+to+routing+and+cascading+Shen)
- Haochen Shi, Tianshi Zheng, Weiqi Wang, Baixuan Xu, Chunyang Li, Chunkit Chan, Tao Fan, Yangqiu Song, and Qiang Yang (2025). *InferenceDynamics: Efficient routing across LLMs through structured capability and knowledge profiling*. arXiv:2505.16303. [link](https://arxiv.org/abs/2505.16303)
- Dimitrios Sikeridis, Dennis Ramdass, and Pranay Pareek (2025). *PickLLM: Context-aware rl-assisted large language model routing*. International Workshop on AI for Transportation. [link](https://scholar.google.com/scholar?q=PickLLM:+Context-aware+rl-assisted+large+language+model+routing+Sikeridis)
- Toby Simonds, Kemal Kurniawan, and Jey Han Lau (2024). *MoDEM: Mixture of domain expert models*. ALTA 2024. [link](https://scholar.google.com/scholar?q=MoDEM:+Mixture+of+domain+expert+models+Simonds)
- Seamus Somerstep, Felipe Maia Polo, Allysson Flavio Melo de Oliveira, Prattyush Mangal, Mírian Silva, Onkar Bhardwaj, Mikhail Yurochkin, and Subha Maity (2025). *CARROT: A cost aware rate optimal router*. arXiv:2502.03261. [link](https://arxiv.org/abs/2502.03261)
- Wei Song, Zhenya Huang, Cheng Cheng, Weibo Gao, Bihan Xu, GuanHao Zhao, Fei Wang, and Runze Wu (2025). *IRT-Router: Effective and interpretable multillm routing via item response theory*. ACL 2025. [link](https://scholar.google.com/scholar?q=IRT-Router:+Effective+and+interpretable+multillm+routing+via+item+response+theory+Song)
- Dimitris Stripelis, Zhaozhuo Xu, Zijian Hu, Alay Dilipbhai Shah, Han Jin, Yuhang Yao, Jipeng Zhang, Tong Zhang, Salman Avestimehr, and Chaoyang He (2024). *TensorOpera Router: A multi-model router for efficient LLM inference*. EMNLP 2024. [link](https://scholar.google.com/scholar?q=TensorOpera+Router:+A+multi-model+router+for+efficient+LLM+inference+Stripelis)
- Haochun Tang, Yuliang Yan, Jiahua Lu, Huaxiao Liu, and Enyan Dai (2026a). *Route to rome attack: Directing LLM routers to expensive models via adversarial suffix optimization*. arXiv:2604.15022. [link](https://arxiv.org/abs/2604.15022)
- Shengji Tang, Weihao Lin, Peng Ye, Jingqi Ye, Hao Li, Yiqun Zhang, Xiaosong Wang, Bo Zhang, Shuyue Hu, Tao Chen, and 1 others (2026b). *Beyond gemini3-pro: Revisiting LLM routing and aggregation at scale*. arXiv:2601.01330. [link](https://arxiv.org/abs/2601.01330)
- Co Tran, Salman Paracha, Adil Hafeez, and Shuguang Chen (2025). *Arch-Router: Aligning LLM routing with human preferences*. arXiv:2506.16655. [link](https://arxiv.org/abs/2506.16655)
- Asterios Tsiourvas, Wei Sun, and Georgia Perakis (2026). *Causal LLM Routing: End-to-end regret minimization from observational data*. NeurIPS 2026. [link](https://scholar.google.com/scholar?q=Causal+LLM+Routing:+End-to-end+regret+minimization+from+observational+data+Tsiourvas)
- Clovis Varangot-Reille, Christophe Bouvard, Antoine Gourru, Mathieu Ciancone, Marion Schaeffer, and François Jacquenet (2025). *Doing more with lessimplementing routing strategies in large language model-based systems: An extended survey*. Preprint. [link](https://scholar.google.com/scholar?q=Doing+more+with+lessimplementing+routing+strategies+in+large+language+model-based+systems:+An+extended+survey+Varangot-Reille)
- Clovis Varangot-Reille, Christophe Bouvard, and Antoine Gourru (2026). *Generalising LLM routing using past performance retrieval: A few-shot router is sufficient*. EACL 2026. [link](https://scholar.google.com/scholar?q=Generalising+LLM+routing+using+past+performance+retrieval:+A+few-shot+router+is+sufficient+Varangot-Reille)
- Hairu Wang, Yuan Feng, Yukun Cao, Xike Xie, and S Kevin Zhou (2025a). *SkewRoute: Training-free LLM routing for knowledge graph retrieval-augmented generation via score skewness of retrieved context*. Findings of EMNLP 2025. [link](https://scholar.google.com/scholar?q=SkewRoute:+Training-free+LLM+routing+for+knowledge+graph+retrieval-augmented+generation+via+score+skewness+of+retrieved+context+Wang)
- Xinyuan Wang, Yanchi Liu, Wei Cheng, Xujiang Zhao, Zhengzhang Chen, Wenchao Yu, Yanjie Fu, and Haifeng Chen (2025b). *MixLLM: Dynamic routing in mixed large language models*. NAACL 2025. [link](https://scholar.google.com/scholar?q=MixLLM:+Dynamic+routing+in+mixed+large+language+models+Wang)
- Chenxu Wang, Hao Li, Yiqun Zhang, Linyao Chen, Jianhao Chen, Ping Jian, Qiaosheng Zhang, and Shuyue Hu (2026a). *ICL Router: In-context learned model representations for LLM routing*. AAAI 2026. [link](https://scholar.google.com/scholar?q=ICL+Router:+In-context+learned+model+representations+for+LLM+routing+Wang)
- Jize Wang, Han Wu, Zhiyuan You, Yiming Song, Yijun Wang, Zifei Shan, Yining Li, Songyang Zhang, Xinyi Le, Cailian Chen, and 1 others (2026b). *RouteMoA: Dynamic routing without pre-inference boosts efficient mixture-of-agents*. arXiv:2601.18130. [link](https://arxiv.org/abs/2601.18130)
- Zijie Wang, Xinyu Yan, Che Wang, Zihao Zeng, Lei Xiao, and Wei Yang Bryan Lim (2026c). *SEMIROUTER: Sparse-data enhanced routing for adaptive multi-LLM system*. EACL 2026. [link](https://scholar.google.com/scholar?q=SEMIROUTER:+Sparse-data+enhanced+routing+for+adaptive+multi-LLM+system+Wang)
- Wang Wei, Tiankai Yang, Hongjie Chen, Yue Zhao, Franck Dernoncourt, Ryan A Rossi, and Hoda Eldardiry (2025). *Learning to route LLMs from bandit feedback: One policy, many trade-offs*. arXiv:2510.07429. [link](https://arxiv.org/abs/2510.07429)
- Herbert Woisetschläger, Ryan Zhang, Shiqiang Wang, and Hans Arno Jacobsen (2026). *MESS+: Dynamically learned inference-time LLM routing in model zoos with service level guarantees*. NeurIPS 2026. [link](https://scholar.google.com/scholar?q=MESS+:+Dynamically+learned+inference-time+LLM+routing+in+model+zoos+with+service+level+guarantees+Woisetschläger)
- Xingyu Wu, Yan Zhong, Jibin Wu, Bingbing Jiang, and Kay Chen Tan (2024). *Large language modelenhanced algorithm selection: Towards comprehensive algorithm representation*. IJCAI 2024. [link](https://scholar.google.com/scholar?q=Large+language+modelenhanced+algorithm+selection:+Towards+comprehensive+algorithm+representation+Wu)
- Xinle Wu and Yao Lu (2025). *Reward model routing in alignment*. arXiv:2510.02850. [link](https://arxiv.org/abs/2510.02850)
- Xingyu Wu, Yinglan Feng, and Jibin Wu (2025a). *Llmdriven evolutionary algorithm selection: Bidirectional framework and sampling paradigm*. ICML 2025. [link](https://scholar.google.com/scholar?q=Llmdriven+evolutionary+algorithm+selection:+Bidirectional+framework+and+sampling+paradigm+Wu)
- Xingyu Wu, Jibin Wu, Yu Zhou, Liang Feng, and Kay Chen Tan (2025b). *Towards robustness and explainability of automatic algorithm selection*. ICML 2025. [link](https://scholar.google.com/scholar?q=Towards+robustness+and+explainability+of+automatic+algorithm+selection+Wu)
- Xingyu Wu, Yu Zhou, and Kay Chen Tan (2026). *Building LLMs like lego: Two-dimensional architecture reassembly of large language models*. ACL 2026. [link](https://scholar.google.com/scholar?q=Building+LLMs+like+lego:+Two-dimensional+architecture+reassembly+of+large+language+models+Wu)
- Murong Yue, Jie Zhao, Min Zhang, Liang Du, and Ziyu Yao (2024). *Large language model cascades with mixture of thought representations for cost-efficient reasoning*. ICLR 2024. [link](https://scholar.google.com/scholar?q=Large+language+model+cascades+with+mixture+of+thought+representations+for+cost-efficient+reasoning+Yue)
- Yanwei Yue, Guibin Zhang, Boyang Liu, Guancheng Wan, Kun Wang, Dawei Cheng, and Yiyan Qi (2025). *MasRouter: Learning to route LLMs for multi-agent systems*. ACL 2025. [link](https://scholar.google.com/scholar?q=MasRouter:+Learning+to+route+LLMs+for+multi-agent+systems+Yue)
- Yi-Kai Zhang, De-Chuan Zhan, and Han-Jia Ye (2025a). *Capability instruction tuning*. AAAI 2025. [link](https://scholar.google.com/scholar?q=Capability+instruction+tuning+Zhang)
- Yiqun Zhang, Hao Li, Jianhao Chen, Hangfan Zhang, Peng Ye, Lei Bai, and Shuyue Hu (2025b). *Beyond GPT-5: Making LLMs cheaper and better via performance-efficiency optimized routing*. DAI 2025. [link](https://scholar.google.com/scholar?q=Beyond+GPT-5:+Making+LLMs+cheaper+and+better+via+performance-efficiency+optimized+routing+Zhang)
- Yichi Zhang, Fangzheng Xie, Shu Yang, and Chong Wu (2026). *Meta-Router: Bridging gold-standard and preference-based evaluations in LLM routing*. ICLR 2026. [link](https://scholar.google.com/scholar?q=Meta-Router:+Bridging+gold-standard+and+preference-based+evaluations+in+LLM+routing+Zhang)
- Haozhen Zhang, Tao Feng, and Jiaxuan You (2026a). *Router-R1: Teaching LLMs multi-round routing and aggregation via reinforcement learning*. NeurIPS 2026. [link](https://scholar.google.com/scholar?q=Router-R1:+Teaching+LLMs+multi-round+routing+and+aggregation+via+reinforcement+learning+Zhang)
- Wenhui Zhang, Huiyu Xu, Zhibo Wang, Zhichao Li, Zeqing He, Xuelin Wei, and Kui Ren (2026b). *RerouteGuard: Understanding and mitigating adversarial risks for LLM routing*. arXiv:2601.21380. [link](https://arxiv.org/abs/2601.21380)
- Yi-Kai Zhang, Shiyin Lu, Qingguo Chen, Weihua Luo, De-Chuan Zhan, and Han-Jia Ye (2026c). *Let the LLM stick to its strengths: Learning to route economical LLM*. NeurIPS 2026. [link](https://scholar.google.com/scholar?q=Let+the+LLM+stick+to+its+strengths:+Learning+to+route+economical+LLM+Zhang)
- Yiqun Zhang, Hao Li, Chenxu Wang, Linyao Chen, Qiaosheng Zhang, Peng Ye, Shi Feng, Xinrun Wang, Jia Xu, Lei Bai, and 1 others (2026d). *The Avengers: A routing recipe for collective intelligence in language models*. AAAI 2026. [link](https://scholar.google.com/scholar?q=The+Avengers:+A+routing+recipe+for+collective+intelligence+in+language+models+Zhang)
- Yiqun Zhang, Hao Li, Zihan Wang, Shi Feng, Xiaocui Yang, Daling Wang, Bo Zhang, Lei Bai, and Shuyue Hu (2026e). *MTRouter: Cost-aware multi-turn LLM routing with history-model joint embeddings*. ACL 2026. [link](https://scholar.google.com/scholar?q=MTRouter:+Cost-aware+multi-turn+LLM+routing+with+history-model+joint+embeddings+Zhang)
- Zesen Zhao, Shuowei Jin, and Z Morley Mao (2024). *Eagle: Efficient training-free router for multi-LLM inference*. arXiv:2409.15518. [link](https://arxiv.org/abs/2409.15518)
- Xinyao Zheng, Husheng Han, Shangyi Shi, Qiyan Fang, Zidong Du, Xing Hu, and Qi Guo (2024). *InputSnatch: Stealing input in LLM services via timing side-channel attacks*. arXiv:2411.18191. [link](https://arxiv.org/abs/2411.18191)
- Hang Zheng, Hongshen Xu, Yongkai Lin, Shuai Fan, Lu Chen, and Kai Yu (2025). *DiSRouter: Distributed self-routing for LLM selections*. arXiv:2510.19208. [link](https://arxiv.org/abs/2510.19208)
- Da-Wei Zhou and Han-Jia Ye (2025). *A unifying perspective on model reuse: From small to large pretrained models*. IJCAI 2025. [link](https://scholar.google.com/scholar?q=A+unifying+perspective+on+model+reuse:+From+small+to+large+pretrained+models+Zhou)
- Yu Zhou, Xingyu Wu, Jibin Wu, Liang Feng, and Kay Chen Tan (2026). *HM3: Hierarchical multiobjective model merging for pretrained models*. NeurIPS 2026. [link](https://scholar.google.com/scholar?q=HM3:+Hierarchical+multiobjective+model+merging+for+pretrained+models+Zhou)
- Richard Zhuang, Tianhao Wu, Zhaojin Wen, Andrew Li, Jiantao Jiao, and Kannan Ramchandran (2025). *EmbedLLM: Learning compact representations of large language models*. ICLR 2025. [link](https://scholar.google.com/scholar?q=EmbedLLM:+Learning+compact+representations+of+large+language+models+Zhuang)

## Notes

- **Adj / Ext / H** entries are not core routing methods by the survey's own scope rules; they are listed because the paper discusses them next to the core inventory.
- 97/97 reference entries are mapped. Two references (Meta-Router, LLM Selector) have no year inside the citation parenthesis in the PDF text; their years were taken from the inventory tables.
- Year suffixes (`2025a`, `2026a`…) are the survey's own disambiguation between same-author, same-year entries and are kept so every row traces back to exactly one reference entry.
- **Model-SAT** is listed under the reference the survey actually cites for it (Zhang et al., 2025a, *Capability Instruction Tuning*), following the paper rather than substituting a similar-looking paper.
- Where the survey reuses one reference for a method and its benchmark (e.g. Somerstep et al. for CARROT/SPROUT, Jiang et al. for LLM-Blender/MixInstruct), both rows point at the same reference entry, exactly as the paper does.
- Descriptions are condensed from the survey's tables and prose. Please cite the survey, not this list.

## Citation

```bibtex
@inproceedings{jiangeng-etal-2026-systematic,
  title     = {A Systematic Survey of Large Language Model Routing},
  author    = {Jiangeng, Chang and Wu, Xingyu and Tan, Kay Chen and Feng, Mengling},
  booktitle = {Findings of the Association for Computational Linguistics: EMNLP 2026},
  year      = {2026},
  pages     = {44102--44134},
  url       = {https://aclanthology.org/2026.findings-emnlp.2072/}
}
```
