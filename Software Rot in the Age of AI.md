# Software Rot in the Age of AI: An Evidence-Based Analysis (2025–2026)

**Technical Analysis Report**

**Compiled by Maxim Glaezer**

**March 15, 2026**

## Goals

This report examines software rot — the progressive decay of software systems — through three connected arguments:

1. **Architecture prevents rot.** Decades of peer-reviewed research establish that modular, well-structured systems resist degradation.
2. **AI generates more code with less architectural awareness.** A growing body of evidence — vendor analyses, preprints, and early peer-reviewed studies — suggests that AI-assisted development increases volume while reducing structural discipline.
3. **Architecture matters more than ever.** If AI amplifies existing practices (as DORA's research indicates), then architectural quality determines whether AI accelerates delivery or accelerates decay.

**Source selection note:** This report excludes vendor blog posts without disclosed methodology, marketing content with conflicts of interest, second-hand citations (blogs citing other blogs), and any source whose claims could not be independently verified from the linked URL. Sources behind paywalls that could not be accessed were also excluded. Each remaining source is categorized by type (peer-reviewed, preprint, industry report, vendor study, or practitioner commentary) in the references section so readers can assess its weight.

**Scope note:** This report focuses on software rot — structural decay, maintainability, and technical debt. Security vulnerabilities in AI-generated code are a significant and well-documented concern, but are outside the scope of this analysis.

---

## 1 What Is Software Rot?

**Software Rot** (or "Bit Rot") refers to the progressive degradation of a software system's usefulness or maintainability over time, even if the code itself remains unchanged. David Parnas formalized this as "software aging" — software degrades as its environment evolves while its internal structure remains static [1].

Lehman's Laws of Software Evolution have been widely validated empirically, confirming that evolving software systems exhibit continuing growth in size and increasing complexity. A study of Apache Tomcat and Apache Ant further found that software quality also degrades over time, consistent with these laws [2].

### 1.1 The Cost

The scale of the problem is well-documented across multiple independent analyses:

- **CAST's 2025 "Coding in the Red" report** analyzed over 10 billion lines of code across 17 countries representing 51% of global GDP: 45% of the world's code is fragile, 32% suffers from bloat, and 31% is too rigid to change efficiently. It would take the world's 25 million developers 9 years of full-time work to pay off current global technical debt [3].
- **McKinsey** (2020) found that tech debt accounts for 20 to 40 percent of companies' entire technology estate value before depreciation, with 10 to 20 percent of the technology budget for new products diverted to resolving debt-related issues [4].
- **CISQ** (2022) estimated the total cost of poor software quality in the US at $2.41 trillion, with $1.52 trillion in accumulated technical debt [5].

**Confidence: ESTABLISHED.** These findings span decades of research and independent analyses. Software rot is not debated — only its rate and remediation.

---

## 2 Architecture Prevents Rot — The Evidence

Before examining AI's effects, it is worth establishing what the research says about architecture's role in preventing software decay. This evidence base is deep, spanning over fifty years.

### 2.1 Modularity (Parnas 1972)

Parnas's foundational work demonstrated that decomposing systems using information hiding — where each module conceals a design decision — produces systems that are significantly more changeable than those decomposed by workflow or data flow [6]. This principle remains the basis of modern software architecture.

### 2.2 Architectural Quality and Defects (Khomh et al. 2012)

An empirical study of change- and fault-proneness found that classes participating in antipatterns are 1.3 to 31 times more fault-prone than classes without antipatterns. This effect holds even when controlling for class size, indicating that architectural quality — not just code volume — drives defect rates [7].

### 2.3 Refactoring as Rot Prevention (ACM 2025)

A study of 207 open-source Java projects identified four release-wise refactoring patterns [8]. The **Late Active pattern** — where teams gradually increase refactoring activity as they approach a release — leads to the best code quality outcomes [8]. This finding quantifies what practitioners have long observed: systematically addressing complexity before each release prevents architectural drift from compounding unchecked.

### 2.4 Architecture Predicts Delivery Performance (DORA 2019)

Google's DORA program measured software delivery performance before the AI era. Elite performers deployed 208 times more frequently and recovered from failures 2,604 times faster than low performers. Loosely coupled architecture was a key predictor of elite performance [9].

**Confidence: STRONG.** These findings come from decades of independent, peer-reviewed research across different teams, methodologies, and codebases. Architecture's role in preventing rot is among the best-established findings in software engineering.

---

## 3 Evidence That AI Accelerates Software Rot

A growing body of evidence suggests that AI-assisted development increases code volume while reducing structural maintenance. The evidence here is newer and more heterogeneous — ranging from vendor analyses to preprints to early peer-reviewed work — so claims are hedged accordingly.

### 3.1 More Code, Less Maintenance

GitClear's analyses of code quality trends reveal a pattern worth noting. Their 2024 report analyzed 153 million changed lines of code (2020–2023) [10], and their 2025 follow-up extended this to 211 million lines through 2024 [11]:

- **Code churn** — the proportion of new code reverted within two weeks — was projected to double in 2024 relative to its 2021, pre-AI baseline [10].
- **Refactoring declined** from 25% of changed lines in 2021 to less than 10% in 2024 [11].
- **Code duplication** (copy-pasted lines) rose from 8.3% to 12.3% [11].

The declining refactoring rate combined with rising duplication suggests that AI tools tend to generate new code rather than restructuring what exists [11]. Practitioner experience corroborates this: Adam Tornhill's research found AI-assisted refactoring correct only 37% of the time [21]. The GitClear analyses are vendor studies and are not peer-reviewed, but the dataset is large and the methodology is disclosed.

### 3.2 Complexity Increases

A Carnegie Mellon study of 806 repositories found that code complexity increased by 41.6% (primary estimator; alternative estimators reported in robustness checks) and static analysis warnings by 30% in AI-assisted repositories after Cursor adoption. Velocity gains were transient, with the only significant gains occurring in the first two months post-adoption [12].

### 3.3 Foundational Debt Persists

An empirical study of 477 repositories found that LLM-related codebases remain debt-free 2.4 times longer than traditional ML repositories (median 492 vs. 204 days), but then accumulate debt rapidly. While the overall debt removal rate in LLM repositories is 49.1%, the first self-admitted technical debt introduced into any file is removed only 4.2% of the time — suggesting that foundational debt tends to become permanent [13].

### 3.4 AI Struggles Architecturally

An empirical study assessing 144 AI-generated microservices found that current agents produce code with inconsistent correctness and require human oversight for system-level concerns such as quality attributes and API contracts. In clean-state generation (from requirements alone), integration tests showed 81–98% pass rates, but incremental generation within existing systems yielded only 50–76% unit test pass rates — suggesting that architectural integration remains a significant challenge [14].

A separate study introduced the concept of **"Hallucinated Coupling"** — when an LLM correctly implements a class but incorrectly imports dependencies, violating inversion of control [15]. AI-generated code can appear correct in isolation while introducing structural debt at the system level.

Kent Beck has reported a related pattern: AI agents sometimes delete tests to make them "pass," undermining the very safety nets that enable confident code changes [22].

### 3.5 The Verification Tax

A randomized controlled trial by METR found that experienced open-source developers took 19% longer to complete tasks when using AI tools in large open-source repositories — despite expecting a 24% speedup [16].

**Confidence: MODERATE.** The GitClear analyses are vendor studies with disclosed methodology but no peer review. The SATD study is a preprint. The CMU and microservices studies are peer-reviewed but recent. The METR RCT is methodologically strong but represents a single study. Practitioner observations from Tornhill [21] and Beck [22] are consistent with the empirical findings but are not controlled studies. Correlation between AI adoption and quality decline does not establish causation — other factors (team composition changes, project maturity) may contribute.

---

## 4 Developer Sentiment Mirrors the Data

The 2025 Stack Overflow Developer Survey — the largest annual survey of professional developers (n=49,000) — reveals a widening trust gap [17]:

- **46% distrust** AI output, versus only 33% who trust it; just 3% "highly trust" it.
- Positive favorability toward AI tools **dropped from over 70% to 60%** year-over-year.
- Approximately **81% of professional developers** currently use AI tools despite this distrust [17].

**Confidence: STRONG.** Large sample, established survey methodology, consistent with the empirical findings in Section 3.

---

## 5 Architecture Matters More Than Ever

### 5.1 AI as Amplifier

Google's DORA program — the longest-running academically rigorous research program on software delivery performance — found in its 2025 report that AI's primary role is as an **amplifier**, magnifying an organization's existing strengths and weaknesses [18]. This finding bridges Sections 2 and 3: if architecture prevents rot (Section 2) and AI amplifies what exists (this finding), then architecture determines whether AI helps or hurts.

### 5.2 Architecture at Scale

Meta's WhatsApp engineering team published their experience deploying AI code generation at enterprise scale over 25 months, producing 3,000+ accepted code changes [19]. Their key finding: architectural guardrails are essential. Their system uses cross-session memory, explicit rules, and retrieval-augmented generation for knowledge grounding to enforce engineering standards [19]. This is a single case study at an organization with exceptional engineering resources, but it illustrates the principle that productive AI-assisted development requires structural constraints.

### 5.3 The Disposable Code Argument

A reasonable counterargument holds that AI-generated code need not resist rot because it can simply be regenerated. If a component decays, discard it and generate a fresh one. This section examines where that argument holds, where it fails, and what it ultimately implies.

**Where it works.** For small, stateless components with stable interface contracts — a 50-line utility function with clear inputs and outputs — disposability is practical. Generate, use, discard, regenerate. No architectural investment required.

**Where it fails.** As components grow in size and accumulated behavior, four problems emerge:

- **The specification problem.** For non-trivial code, the implementation *is* the specification. Edge cases, workarounds, and integration behavior accumulate in the code over time. Regenerating from the original prompt loses this knowledge.
- **Leaky abstractions.** Performance characteristics, resource usage, and error handling are not captured by API contracts. Replacing an implementation can change observable system behavior even when the interface is preserved.
- **Component size.** A 50-line function is safely disposable; a 5,000-line service with dozens of integration points is not. The argument scales inversely with complexity.
- **Test incompleteness.** Tests capture *known* behavior. The edge cases that accumulated organically in the original code — and that no test explicitly verifies — are lost on regeneration.

**The deeper issue: specification is harder than implementation.** The disposable code approach doesn't eliminate complexity — it shifts it from implementation to specification. To safely regenerate a component, you must fully specify its behavioral contract for all edge cases, its performance characteristics, its error semantics, and its side effects. Writing such a complete specification is often harder than writing the implementation itself. This is why formal specification languages (TLA+, Z, Alloy) exist — and why they are rarely used. For most real-world systems, the code *is* the most complete specification available. Hyrum's Law sharpens the point: even with a formally correct interface contract, consumers will depend on incidental implementation behaviors — ordering, timing, error message wording — that no specification captures.

**The problem is recursive.** Specifying a component's external interface does not make its internals disposable. Those internals are composed of sub-components that interact through their own unspecified contracts, which in turn contain further internal relationships, all the way down. You cannot escape the specification problem by drawing a boundary around it; the same problem reappears at every level inside that boundary.

**What about stopping at a practical level?** One might argue for treating everything below some level — functions, classes — as disposable. But the boundary between "safely disposable" and "not safely disposable" depends on how much implicit knowledge has accumulated in a given piece of code, which you cannot assess without understanding the implementation you propose to discard. And even if such a level could be identified, fully specifying all interactions at that level — every function contract, every shared state assumption, every error propagation path — would be impractical for any non-trivial system.

Making code safely disposable — even partially — requires deliberate architectural work at every level: clear interfaces, comprehensive contracts, modular boundaries. This is exactly the discipline that prevents rot in the first place. Disposable code is not an alternative to architecture; it is a consequence of it.

### 5.4 Two Sources of Truth

The analysis above might appear to argue against specification-driven development: if the code is the most complete specification available, why write specs at all? The resolution lies in recognizing that every non-trivial system has *two* sources of truth, not one — and they capture different kinds of knowledge.

Specifications capture **architectural knowledge** — how the system is structured and why. This includes component relationships, design decisions, contracts between modules, constraints that must hold, and the rationale behind structural choices. A specification answers: "How is this designed, and why?" It is deliberately incomplete about implementation details. A good API contract specifies what a component promises to its callers, not how it fulfills that promise. This incompleteness is a feature: it is what allows implementations to change without breaking the system.

Code captures **implementation knowledge** — what the system actually does. This includes everything the specification described, but also everything it did not: the edge case a developer handled after a production incident two years ago, the timing workaround that prevents a race condition nobody documented, the error recovery path that accumulated through three rounds of bug fixes. Over time, the implementation knowledge in a non-trivial component outgrows its specification. The code becomes the authoritative record of what the system does, including things nobody planned or wrote down.

These are not competing sources of truth — they are complementary. The spec answers "how is this designed and why?" The code answers "what does this actually do?" Problems arise when one is mistaken for the other: trusting the spec when the code has diverged leads to bugs in production; treating the code as the design document when the architectural thinking has been buried under years of patches leads to rot.

In a healthy system, architectural knowledge and implementation knowledge are aligned. In a rotting system, they diverge — the code does things the architecture never anticipated, and the specification (if it still exists) describes a design the code no longer follows. This divergence is itself a form of software rot.

This framing connects directly to Parnas's foundational insight. Information hiding is about *design decisions* — each module conceals a design decision from others [6]. The specification captures those decisions. The code implements them. When implementation reveals a design decision that was not anticipated during specification — a new boundary that needs to exist, a constraint that was not obvious until code was written — updating the spec is not capturing behavior. It is capturing architectural knowledge that was *discovered* during implementation.

Specification-driven development works because it forces architectural thinking before implementation. Writing the spec first means deciding on structure, contracts, and boundaries before generating code. The code then fills in everything the spec deliberately left out — the implementation details, the edge cases, the performance optimizations. Good specs make implementations *more* disposable by constraining what a regenerated version must satisfy. But "more disposable" is not "fully disposable." The gap between architectural knowledge (what was designed) and implementation knowledge (what the code actually does) is where regeneration breaks — and where internal design quality still matters.

The disposable code argument fails precisely because it conflates these two sources of truth. It assumes that regenerating from the spec (architectural knowledge) will recover everything in the code (implementation knowledge). It will not. Regeneration recovers the designed structure but loses the accumulated implementation knowledge that the system has come to depend on. No amount of specification discipline closes this gap entirely, because implementation knowledge accumulates through use, not through design.

### 5.5 Spec-Driven Development: The Industry Response

The problems documented in Section 3 — AI generating code without architectural awareness — have not gone unnoticed. A significant industry movement toward **spec-driven development (SDD)** has emerged, with major open-source frameworks (GitHub's spec-kit, OpenSpec, BMAD-METHOD) attracting tens of thousands of GitHub stars, and companies like AWS (Kiro) and Tessl building commercial products around the concept.

Different tools and teams have adopted different levels of specification rigor:

- **Spec-first.** Write a specification before the task, then let AI implement it. The spec may be discarded afterward. This is essentially TDD and API-first design applied to AI-assisted workflows — proven practice with a new interface.
- **Spec-anchored.** The specification persists and evolves alongside the code over its lifecycle. Spec and code are kept in sync through continuous validation. When implementation reveals architectural knowledge that was not anticipated during design — a new boundary, an unforeseen constraint — that knowledge flows back into the spec. This is the alignment problem: maintaining the relationship between architectural knowledge and implementation knowledge as both evolve.
- **Spec-as-source.** Humans maintain *only* the specification. Code is generated, marked as disposable, and regenerated whenever the spec changes. This is the most ambitious vision — and the one that runs directly into the limitations analyzed in Sections 5.3 and 5.4.

Current adoption is concentrated at the spec-first level, which has the widest tooling support and the lowest overhead. Spec-as-source has attracted venture capital (Tessl, $125M) but remains unproven at scale. Spec-anchored — the middle ground that would keep intent and behavior in continuous sync — is the least practiced. A survey of 514 teams using Specification by Example found that only 12% maintain version-controlled specification files as their source of truth, and roughly one-third do not automate their specifications at all, allowing them to go stale. No dominant tool or framework has emerged for this level. Whether this gap reflects inherent difficulty, insufficient tooling, or simply less investment is an open question.

The analysis in this report provides a framework for understanding why the spectrum gets harder as it moves toward full disposability. Spec-first works because it captures architectural knowledge and lets the implementation accumulate its own knowledge through use. Spec-as-source requires specifications to capture *both* architectural and implementation knowledge — the gap that Section 5.4 identifies as fundamentally difficult to close.

**AI's most valuable role may not be generating code.** A parallel trend uses AI to *maintain architectural integrity* rather than produce more code — which is precisely the tooling gap that spec-anchored development needs filled. Tools like CodeScene expose code health metrics as quality gates for AI-generated code. Architecture governance platforms like ArchGuard use AI to analyze and enforce structural constraints. Multi-agent review systems dedicate separate agents to writing, critiquing, testing, and validating architectural alignment. This reframes AI from code producer to architectural integrity tool — using it to detect and repair the divergence between architectural knowledge and implementation knowledge rather than to generate more code. If these tools mature, they could make spec-anchored development practical by automating the continuous sync between specification and implementation that teams currently fail to sustain manually.

**The waterfall risk.** ThoughtWorks and Martin Fowler have noted that rigid specifications could recreate waterfall's problems — slow feedback, premature commitment, specs that calcify before implementation reveals their flaws. The framework from Section 5.4 clarifies this risk: specifications that capture *architectural knowledge* (structure, design decisions, contracts, constraints) remain stable as implementations change. Specifications that attempt to capture *implementation knowledge* (detailed behavioral requirements, edge case handling, performance specifics) calcify because implementation knowledge evolves through use, not through upfront design. The SDD movement will succeed to the extent that it specifies architecture and avoids specifying implementation details.

**The fundamental bet** underlying spec-driven development is that if you can precisely specify what you want, AI becomes a reliable generator. The evidence in this report suggests this bet is partially correct — spec-first and spec-anchored approaches align with the proven practices in Section 2. But complete specification remains impractical for the reasons Sections 5.3 and 5.4 describe. The industry is learning in real time where that ceiling is.

**This report's recommendation: spec-anchored development.** Of the three approaches, spec-anchored is the only one that directly addresses the core problem this report identifies — the divergence between architectural knowledge and implementation knowledge that drives software rot. Spec-first is valuable but incomplete: it front-loads architectural thinking, then lets the specification go stale as the code evolves. Spec-as-source is impractical for non-trivial systems, as Sections 5.3 and 5.4 demonstrate. Spec-anchored development maintains a living specification that evolves alongside the code: architectural knowledge discovered during implementation flows back into the spec, keeping the two sources of truth aligned. That only 12% of teams currently sustain this practice does not argue against it — it argues for better tooling, and for AI to be directed at this alignment problem rather than at generating more code.

### 5.6 Managed vs. Unmanaged: The Performance Gap

| Metric | Unmanaged AI Code | Architecturally Managed |
|---|---|---|
| Initial Build Speed | 55% Faster [20] | Baseline |
| Code Complexity | +41.6% [12] | Baseline |
| Refactoring Rate | Declining (<10%) [11] | Late Active Pattern [8] |
| Delivery Stability | AI amplifies weaknesses [18] | AI amplifies strengths [18] |
| Developer Trust | 46% distrust [17] | Baseline (human-reviewed) |

### 5.7 Synthesis

**The following is an interpretive conclusion drawn from the evidence presented, not a direct empirical finding.**

The logic runs: architecture prevents rot (established across decades of independent research, Section 2) and AI amplifies existing organizational practices (strong finding from DORA's 2025 report [18]). The reasonable inference is that architectural quality is the primary determinant of whether AI-assisted development accelerates delivery or accelerates decay. Teams with strong architectural practices are positioned to benefit from AI's speed advantages while their existing structural discipline constrains the rot that AI-generated code might otherwise introduce. Teams without such practices face the compounding effects documented in Section 3 — rising complexity, declining refactoring, and persistent foundational debt — now amplified by higher code velocity.

**Confidence:** The DORA amplification finding is strong (established research program, large sample). The Meta case study is a single organization. The synthesis is a reasonable inference from the combined evidence, not a directly tested hypothesis.

---

## 6 Summary of Findings

- **Software rot is real and costly.** 45% of the world's code is fragile [3], tech debt accounts for 20–40% of technology estate value [4], and Lehman's Laws confirm that complexity increases continuously in evolving systems [2]. This is established science.
- **Architecture prevents rot.** Classes with antipatterns are up to 31 times more fault-prone [7], the Late Active refactoring pattern produces the best quality outcomes [8], and loosely coupled architecture predicts elite delivery performance [9]. Decades of independent research confirm this.
- **Evidence suggests AI accelerates rot.** Vendor analyses indicate code churn is projected to double [10], refactoring has declined from 25% to less than 10% of changed lines [11], and a peer-reviewed study found 41.6% complexity increase in AI-assisted repositories [12]. These findings warrant attention but require further independent validation.
- **Current AI tools struggle with architectural reasoning.** They require human oversight for system-level concerns [14] and produce "Hallucinated Coupling" that violates design principles [15].
- **AI amplifies existing practices.** DORA research shows AI magnifies both strengths and weaknesses [18]. Meta's enterprise deployment found architectural guardrails essential at scale [19].
- **Developers see it too.** 46% distrust AI output vs. 33% who trust it, and favorability toward AI tools dropped from 70%+ to 60% year-over-year, even as 81% continue using them [17].
- **The industry is responding with spec-driven development.** Frameworks like GitHub's spec-kit and OpenSpec move architectural intent upstream into specifications that constrain AI generation. Spec-first approaches align with proven practice; fully disposable code (spec-as-source) remains limited by the gap between intent and accumulated behavior.

---

## 7 Sources

### Peer-Reviewed Research

[1] **David Parnas (1994):** *Software Aging.* Foundational paper on why software degrades over time as its environment evolves while its internal structure remains static. Published at ICSE '94.
https://doi.org/10.1109/icse.1994.296790

[2] **Lehman's Laws — Quality Evolution:** *An Empirical Study of Lehman's Law on Software Quality Evolution.* Studies software quality degradation over time in Apache Tomcat and Ant projects, treating Lehman's size/complexity laws as established and extending validation to the quality dimension. Published in *International Journal of Software and Informatics*, 2013.
https://www.researchgate.net/publication/259979752_An_Empirical_Study_of_Lehmans_Law_on_Software_Quality_Evolution

[6] **David Parnas (1972):** *On the Criteria To Be Used in Decomposing Systems into Modules.* Foundational work establishing information hiding as the basis for modular design. Published in *Communications of the ACM* 15(12).
https://dl.acm.org/doi/10.1145/361598.361623

[7] **Khomh, Di Penta, Guéhéneuc, Antoniol (2012):** *An Exploratory Study of the Impact of Antipatterns on Class Change- and Fault-Proneness.* Classes with antipatterns 1.3–31x more fault-prone; effect holds controlling for size. Published in *Empirical Software Engineering* 17(3), pp. 243–275.
https://assets.ptidej.net/Publications/Documents/EMSE11b.doc.pdf

[8] **ACM (2025):** *An Empirical Study on Release-Wise Refactoring Patterns.* Study of 207 open-source Java projects identifying four release-wise refactoring patterns. Published in *Proceedings of the ACM on Software Engineering* (FSE 2025).
https://dl.acm.org/doi/10.1145/3715734

[12] **Carnegie Mellon University (2026):** *Speed at the Cost of Quality: How Cursor AI Increases Short-Term Velocity and Long-Term Complexity in Open-Source Projects.* Study of 806 repositories finding +41.6% code complexity (primary estimator) and +30% static analysis warnings in AI-assisted repos. Published at MSR '26.
https://arxiv.org/abs/2511.04427

[14] *Can AI Agents Generate Microservices? How Far Are We?* Assessment of 144 generated microservices showing agents require human oversight for system-level concerns. Accepted at IEEE ICSA 2026.
https://arxiv.org/abs/2603.09004

[19] **Meta (2026):** *WhatsCode: Large-Scale GenAI Deployment for Developer Efficiency at WhatsApp.* 25-month deployment producing 3,000+ accepted code changes with guardrails for knowledge grounding. Accepted at ICSE-SEIP 2026 (industry experience report).
https://arxiv.org/html/2512.05314

### Preprints

[13] *Self-Admitted Technical Debt in LLM Software.* Empirical study of 477 repositories examining how technical debt accumulates in LLM-related codebases. arXiv, January 2026.
https://arxiv.org/html/2601.06266v1

[15] *Quantitative Analysis of Technical Debt and Pattern Violation in LLM Architectures.* Introduces "Hallucinated Coupling" metric for AI-generated code. arXiv, December 2025.
https://arxiv.org/html/2512.04273

### Established Research Programs

[9] **Google DORA (2019):** *Accelerate State of DevOps Report.* Elite performers deploy 208x more frequently, recover 2,604x faster; loosely coupled architecture is a key predictor. Pre-AI era.
https://dora.dev/research/2019/dora-report/ (PDF: https://services.google.com/fh/files/misc/state-of-devops-2019.pdf)

[16] **METR (2025):** *Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity.* Randomized controlled trial finding experienced developers 19% slower with AI tools in large open-source repositories.
https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

[18] **Google DORA (2025):** *State of AI-assisted Software Development 2025.* AI acts as an amplifier of existing organizational practices.
https://dora.dev/research/2025/dora-report/

### Industry Reports and Surveys

[3] **CAST Software Intelligence (2025):** *Coding in the Red: The State of Global Technical Debt.* Industry report analyzing 10 billion lines of code across 17 countries. CAST is a commercial code analysis vendor.
https://www.castsoftware.com/ciu/coding-in-the-red-technical-debt-report-2025

[4] **McKinsey & Company (2020):** *Tech Debt: Reclaiming Tech Equity.* CIO survey on tech debt's impact on technology estate value and budgets.
https://www.mckinsey.com/capabilities/mckinsey-digital/our-insights/tech-debt-reclaiming-tech-equity

[5] **CISQ (2022):** *The Cost of Poor Software Quality in the US.* Estimates $2.41 trillion total cost and $1.52 trillion in accumulated technical debt. CISQ is co-founded by OMG and Carnegie Mellon's Software Engineering Institute.
https://www.it-cisq.org/the-cost-of-poor-quality-software-in-the-us-a-2022-report/

[17] **Stack Overflow (2025):** *2025 Developer Survey — AI Section.* Annual survey of 49,000 developers. 46% distrust AI output vs. 33% who trust it; favorability dropped from 70%+ to 60%.
https://survey.stackoverflow.co/2025/ai/

### Vendor Studies

[10] **GitClear (2024):** *Coding on Copilot: 2023 Data Suggests Downward Pressure on Code Quality.* Analysis of 153 million changed lines (2020–2023). GitClear is a commercial code analytics platform; not peer-reviewed.
https://www.gitclear.com/coding_on_copilot_data_shows_ais_downward_pressure_on_code_quality

[11] **GitClear (2025):** *AI Copilot Code Quality: 2025 Data.* Analysis of 211 million changed lines (2020–2024) showing refactoring decline from 25% to <10% and code duplication increase from 8.3% to 12.3%. Not peer-reviewed.
https://www.gitclear.com/ai_assistant_code_quality_2025_research

[20] **GitHub (2022):** *Research: Quantifying GitHub Copilot's Impact on Developer Productivity.* Vendor-conducted study finding developers completed tasks 55% faster with Copilot (n=95). Not peer-reviewed.
https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/

### Practitioner Commentary

[21] **Adam Tornhill & Martin Fowler / Thoughtworks (2024):** Podcast on refactoring with AI. Tornhill's research found AI refactoring correct only 37% of the time.
https://www.thoughtworks.com/en-us/insights/podcasts/technology-podcasts/refactoring-with-ai

[22] **Kent Beck / Pragmatic Engineer (2025):** Interview covering TDD practices with AI agents. Beck reports that AI agents sometimes delete tests to make them "pass."
https://newsletter.pragmaticengineer.com/p/tdd-ai-agents-and-coding-with-kent
