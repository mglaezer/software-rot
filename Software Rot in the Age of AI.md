# Software Rot in the Age of AI: An Evidence-Based Analysis (2025–2026)

**Technical Analysis Report**

**Compiled by Maxim Glaezer**

**March 15, 2026**

## The Problem

Poor software quality costs the US economy $2.41 trillion per year [5]. Technical debt consumes 20–40% of companies' entire technology budgets [4]. It would take 25 million developers working full-time for 9 years to pay off the debt that already exists [3].

AI-assisted development was expected to reduce this burden. The early evidence suggests it is increasing it:

- **Code complexity increased 41.6%** in repositories after adopting AI tools, compared to the same repositories before adoption [12].
- **Refactoring declined from 25% to less than 10%** of changed lines over the period AI tools reached mainstream use [11].
- **Delivery stability drops 7.2%** for every 25% increase in AI tool adoption [31].
- **Review time increases 91%** in teams with high AI adoption, while delivery metrics remain flat [34].

81% of professional developers now use these tools [17]. The debt is growing. The tools meant to help are making the structural problems worse.

---

## Goals

This report examines software rot — the progressive decay of software systems — through four connected arguments:

1. **Architecture prevents rot.** Decades of peer-reviewed research establish that modular, well-structured systems resist degradation.
2. **AI generates more code with less architectural awareness.** A growing body of evidence — vendor analyses, preprints, and early peer-reviewed studies — suggests that AI-assisted development increases volume while reducing structural discipline.
3. **Architecture matters more than ever.** If AI amplifies existing practices (as DORA's research indicates), then architectural quality determines whether AI accelerates delivery or accelerates decay.
4. **Specification preserves architectural knowledge.** Every non-trivial system has two sources of truth — specifications capture architectural knowledge (structure and design decisions), code captures implementation knowledge (what the system actually does). Keeping both aligned through spec-anchored development is the most promising response to AI-accelerated rot, though empirical validation of this approach remains limited.

The first three arguments are empirically grounded (Sections 2–5). The fourth follows by elimination: if architecture determines whether AI helps or hurts, and AI without architectural constraints degrades quality, then AI needs externalized architectural knowledge that constrains code before it is written. Section 7 examines every alternative constraint mechanism and finds that each either is a specification by another name or is reactive rather than generative.

**Source selection note:** This report excludes vendor blog posts without disclosed methodology, marketing content with conflicts of interest, second-hand citations (blogs citing other blogs), and any source whose claims could not be independently verified from the linked URL. Sources behind paywalls that could not be accessed were also excluded. Each remaining source is categorized by type (peer-reviewed, preprint, industry report, vendor study, or practitioner commentary) in the references section so readers can assess its weight.

**Scope note:** This report focuses on software rot — structural decay, maintainability, and technical debt. Security vulnerabilities in AI-generated code are a significant and well-documented concern, but are outside the scope of this analysis.

**A plain-language summary** of this report is available in Appendix A at the end of this document for readers who prefer a less technical overview.

---

## 1 What Is Software Rot?

**Software Rot** (or "Bit Rot") refers to the progressive degradation of a software system's usefulness or maintainability over time, even if the code itself remains unchanged. David Parnas formalized this as "software aging" — software degrades as its environment evolves while its internal structure remains static [1].

Lehman's Laws of Software Evolution — confirmed across many studies — show that evolving software systems keep growing in size and complexity. A study of Apache Tomcat and Apache Ant found that software quality degrades over time too, not just size [2].

### 1.1 The Cost

The scale of the problem is well-documented across multiple independent analyses:

- **CAST's 2025 "Coding in the Red" report** analyzed over 10 billion lines of code across 17 countries representing 51% of global GDP: 45% of the world's code is fragile, 32% suffers from bloat, and 31% is too rigid to change efficiently. It would take the world's 25 million developers 9 years of full-time work to pay off current global technical debt [3].
- **McKinsey** (2020) found that tech debt accounts for 20 to 40 percent of companies' entire technology estate value before depreciation, with 10 to 20 percent of the technology budget for new products diverted to resolving debt-related issues [4].
- **CISQ** (2022) estimated the total cost of poor software quality in the US at $2.41 trillion, with $1.52 trillion in accumulated technical debt [5].

**Confidence: ESTABLISHED.** These findings span decades of research and independent analyses. Software rot is not debated — only its rate and remediation.

---

## 2 Architecture Prevents Rot — The Evidence

Before examining AI's effects, we need to establish what the research says about architecture's role in preventing decay. The evidence goes back over fifty years.

### 2.1 Modularity (Parnas 1972)

Parnas showed that if you decompose systems by information hiding — where each module conceals a design decision — the result is significantly easier to change than systems decomposed by workflow or data flow [6]. This principle still underpins modern software architecture.

### 2.2 Architectural Quality and Defects (Khomh et al. 2012)

A study of how often code changes and breaks found that classes with antipatterns are 1.3 to 31 times more likely to have bugs than clean classes. This holds even after accounting for class size — it's the architecture that drives defect rates, not the amount of code [7].

### 2.3 Refactoring as Rot Prevention (ACM 2025)

A study of 207 open-source Java projects identified four release-wise refactoring patterns [8]. The **Late Active pattern** — where teams gradually increase refactoring activity as they approach a release — leads to the best code quality outcomes [8]. This confirms what practitioners have long seen: cleaning up complexity regularly, rather than letting it accumulate, prevents architectural drift from spiraling.

### 2.4 Architecture Predicts Delivery Performance (DORA 2019)

Google's DORA program measured software delivery performance before the AI era. Elite performers deployed 208 times more frequently and recovered from failures 2,604 times faster than low performers. Loosely coupled architecture was a key predictor of elite performance [9].

### 2.5 Code Health Accelerates Development (Borg et al. 2024)

A study of 46,000 source code files found that the returns on code quality are increasing, not diminishing: improving code health from industry average to elite levels accelerates development by 43% and reduces defects up to 15x [32]. This finding — which won Best Paper at the International Conference on Technical Debt — puts numbers on what the preceding studies describe: high architectural quality is not a cost center but a development accelerator.

**Confidence: STRONG.** These findings come from decades of independent, peer-reviewed research across different teams, methodologies, and codebases. Architecture's role in preventing rot is among the best-established findings in software engineering.

---

## 3 Evidence That AI Accelerates Software Rot

A growing body of evidence suggests that AI-assisted development produces more code while reducing structural upkeep. The evidence here is newer and more mixed — ranging from vendor analyses to preprints to early peer-reviewed work — so claims are stated carefully.

### 3.1 More Code, Less Maintenance

GitClear's analyses of code quality trends reveal a pattern worth noting. Their 2024 report analyzed 153 million changed lines of code (2020–2023) [10], and their 2025 follow-up extended this to 211 million lines through 2024 [11]:

- **Code churn** — the proportion of new code reverted within two weeks — was projected to double in 2024 relative to its 2021, pre-AI baseline [10].
- **Refactoring declined** from 25% of changed lines in 2021 to less than 10% in 2024 [11].
- **Code duplication** (copy-pasted lines) rose from 8.3% to 12.3% [11].

The declining refactoring rate combined with rising duplication suggests that AI tools tend to generate new code rather than restructuring what exists [11]. Practitioner experience extends the point: even when developers do refactor, Adam Tornhill's research found AI-assisted refactoring correct only 37% of the time [21]. The GitClear analyses are vendor studies and are not peer-reviewed, but the dataset is large and the methodology is disclosed.

### 3.2 Complexity Increases

A Carnegie Mellon study of 806 repositories found that code complexity increased by 41.6% (primary estimator; alternative estimators reported in robustness checks) and static analysis warnings by 30% in AI-assisted repositories after Cursor adoption. Speed gains were short-lived — significant only in the first two months after adoption [12].

### 3.3 Foundational Debt Persists

A study of 477 repositories found that LLM-related codebases stay debt-free 2.4 times longer than traditional ML repositories (median 492 vs. 204 days), but then accumulate debt fast. While the overall debt removal rate in LLM repositories is 49.1%, the *first* technical debt introduced into any file is removed only 4.2% of the time — suggesting that once debt takes root, it tends to stay [13].

### 3.4 AI Struggles Architecturally

A study of 144 AI-generated microservices found that current agents produce inconsistently correct code and need human oversight for system-level concerns like quality attributes and API contracts. When generating from scratch, integration tests pass 81–98% of the time. But when generating into existing systems, unit test pass rates drop to 50–76% — suggesting that fitting into an existing architecture remains a major challenge for AI [14].

A separate study introduced the concept of **"Hallucinated Coupling"** — when an LLM correctly implements a class but incorrectly imports dependencies, violating inversion of control [15]. AI-generated code can appear correct in isolation while introducing structural debt at the system level.

### 3.5 The Verification Tax

Kent Beck has reported a pattern where AI agents sometimes delete tests to make them "pass," undermining the very safety nets that enable confident code changes [22].

A randomized controlled trial by METR found that experienced open-source developers took 19% longer to complete tasks when using AI tools in large open-source repositories — despite expecting a 24% speedup [16].

Telemetry from over 10,000 developers across 1,255 teams reveals the same pattern at organizational scale: teams with high AI adoption merge 98% more pull requests, but code review time increases by 91% and bugs per developer increase by 9%. Despite individual developers reporting that they feel faster, company-wide delivery metrics remain flat [34]. The bottleneck shifts from writing code to verifying it.

**Confidence: MODERATE.** The GitClear analyses are vendor studies with disclosed methodology but no peer review. The SATD study is a preprint. The CMU and microservices studies are peer-reviewed but recent. The METR RCT is methodologically strong but represents a single study. The Faros telemetry [34] covers a large dataset but is a vendor study without peer review. Practitioner observations from Tornhill [21] and Beck [22] are consistent with the empirical findings but are not controlled studies. Correlation between AI adoption and quality decline does not establish causation — other factors (team composition changes, project maturity) may contribute. However, the pattern is consistent across every independent source.

---

## 4 Developer Sentiment Mirrors the Data

The 2025 Stack Overflow Developer Survey — the largest annual survey of professional developers (n=49,000) — reveals a widening trust gap [17]:

- **46% distrust** AI output, versus only 33% who trust it; just 3% "highly trust" it.
- Positive favorability toward AI tools **dropped from over 70% to 60%** year-over-year.
- Approximately **81% of professional developers** currently use AI tools despite this distrust [17].

**Confidence: STRONG.** Large sample, established survey methodology, consistent with the empirical findings in Section 3.

---

## 5 The Two Premises

The preceding sections established two empirical claims. This section states them explicitly, because everything that follows depends on them.

### 5.1 Premise 1: Architecture Quality Determines AI Outcomes

The evidence for this premise comes from three independent sources.

Google's DORA program — the longest-running rigorous research program on software delivery performance — found in its 2025 report that AI primarily acts as an **amplifier**: it magnifies an organization's existing strengths and weaknesses [18]. If your practices are strong, AI makes them stronger. If they're weak, AI makes them worse. DORA describes this amplification broadly — process maturity, testing discipline, architectural quality. Since this report focuses on architecture specifically, the inference that architecture determines whether AI helps or hurts is reasonable but narrower than DORA's finding.

A controlled experiment on 5,000 Python files found that AI coding assistants increase defect risk by at least 30% when applied to code with poor structural health. Well-structured code produces healthier AI output — code that is good for humans is also good for AI [33]. Combined with the finding in Section 2.5 that elite code health accelerates development by 43% and reduces defects up to 15x [32], the picture is clear: architectural quality doesn't merely correlate with better AI outcomes — it determines them.

Meta's WhatsApp engineering team reported on their experience deploying AI code generation at enterprise scale over 25 months, producing 3,000+ accepted code changes [19]. Their key finding: architectural guardrails are essential. Their system uses cross-session memory, explicit rules, and retrieval-augmented generation to enforce engineering standards [19]. This is a single case study at an organization with exceptional engineering resources, but it shows the same pattern: productive AI-assisted development requires structural constraints.

### 5.2 Premise 2: AI Without Constraints Degrades Quality

The evidence for this premise is documented in detail in Section 3 and summarized here:

- Code complexity increases 41.6% in repositories after AI tool adoption [12].
- Refactoring — the primary defense against structural decay — declines from 25% to less than 10% of changed lines [11].
- Code duplication rises from 8.3% to 12.3% [11].
- Foundational technical debt, once introduced, is removed only 4.2% of the time [13].
- AI-generated code requires human oversight for system-level concerns and achieves only 50–76% test pass rates when integrated into existing systems [14].
- Experienced developers take 19% longer with AI tools on complex tasks, despite expecting a 24% speedup [16].
- Teams merging 98% more AI-assisted pull requests see review time increase 91% and bugs increase 9% per developer, with no improvement in overall delivery metrics [34].
- A 25% increase in AI tool adoption correlates with a 7.2% decrease in delivery stability [31].

This evidence comes from peer-reviewed studies [12][14], established research programs [16][18][31], vendor analyses with disclosed methodology [10][11][34], and practitioner experience [21][22]. No single study is conclusive, but every independent source points the same way: AI increases code volume while reducing structural quality.

### 5.3 What Follows

If architecture determines AI outcomes (Premise 1) and AI without constraints degrades quality (Premise 2), then AI-assisted development requires externalized architectural knowledge that constrains code before it is written.

This is not a recommendation — it is a logical consequence of the evidence. The open question is not *whether* AI needs architectural constraints, but *what form* those constraints should take. Section 7 examines every candidate mechanism.

**Confidence: The premises are empirically supported across multiple independent studies (Sections 2–4). The inference follows logically from the premises. Whether the specific practice of spec-anchored development is the best implementation of this inference remains an open empirical question (Section 8).**

---

## 6 The Limits of Disposable Code

The preceding sections presented evidence. What follows — through this section and Section 8.1 — is primarily analysis: reasoning from that evidence and from established software engineering principles, rather than reporting new findings.

### 6.1 The Disposable Code Argument

A reasonable counterargument holds that AI-generated code need not resist rot because it can simply be regenerated. If a component decays, discard it and generate a fresh one. This section examines where that argument holds, where it fails, and what it ultimately implies.

**Where it works.** For components where the specification fully captures the implementation — where there is no gap between what was designed and what the code actually does — disposability is practical. This includes more than edge cases. A large fraction of professional software is CRUD applications, glue code, data transformations, and API integrations where the behavior is straightforward and the specification is complete: read from here, write to there, validate these fields, return that format. For these systems, disposability may be the correct default approach. The argument in this section applies specifically to systems where implementation knowledge significantly outgrows specification knowledge over time — long-lived, mission-critical systems with accumulated edge cases, performance-sensitive paths, and emergent behavioral contracts. These systems are a minority of all code written, but they represent a disproportionate share of the economic value and operational risk described in Section 1.1.

**Where it fails.** As components grow in size and accumulated behavior, four problems emerge:

- **The specification problem.** For non-trivial code, the implementation *is* the specification. Edge cases, workarounds, and integration behavior accumulate in the code over time. Regenerating from the original prompt loses this knowledge.
- **Leaky abstractions.** Performance characteristics, resource usage, and error handling are not captured by API contracts. Replacing an implementation can change observable system behavior even when the interface is preserved.
- **Component size.** A 50-line function is safely disposable; a 5,000-line service with dozens of integration points is not. The argument scales inversely with complexity.
- **Test incompleteness.** Tests capture *known* behavior. The edge cases that accumulated organically in the original code — and that no test explicitly verifies — are lost on regeneration. The microservices study [14] provides empirical support: AI-generated code achieved 81–98% integration test pass rates in clean-state generation but only 50–76% in existing systems, suggesting that accumulated system knowledge escapes test coverage.

**The deeper issue: complete specification is impractical.** The disposable code approach doesn't eliminate complexity — it shifts it from implementation to specification. To safely regenerate a component, you must fully specify its behavioral contract for all edge cases, its performance characteristics, its error semantics, and its side effects. Writing such a complete specification is impractical for non-trivial systems. This is why formal specification languages (TLA+, Z, Alloy) exist — and why they are rarely used. For most real-world systems, the code *is* the most complete specification available. Hyrum's Law [27] sharpens the point: even with a formally correct interface contract, consumers will depend on incidental implementation behaviors — ordering, timing, error message wording — that no specification captures.

**The problem is recursive.** For components with accumulated state and side effects, specifying a component's external interface does not make its internals disposable. Those internals are composed of sub-components that interact through their own unspecified contracts, which in turn contain further internal relationships, all the way down. You cannot escape the specification problem by drawing a boundary around it; the same problem reappears at every level inside that boundary.

**What about stopping at a practical level?** One might argue for treating everything below some level — functions, classes — as disposable. But the boundary between "safely disposable" and "not safely disposable" depends on how much implicit knowledge has accumulated in a given piece of code, which you cannot assess without understanding the implementation you propose to discard. And even if such a level could be identified, fully specifying all interactions at that level — every function contract, every shared state assumption, every error propagation path — would be impractical for any non-trivial system.

Making code safely disposable — even partially — requires deliberate architectural work at every level: clear interfaces, comprehensive contracts, modular boundaries. Meta's WhatsApp deployment [19] illustrates this in practice: making AI-generated code production-worthy required explicit architectural guardrails, cross-session memory, and knowledge grounding — precisely the structural investment the disposable-code argument claims to avoid. Disposable code is not an alternative to architecture; it is a consequence of it.

### 6.2 Two Sources of Truth

The analysis above might seem to argue against specification-driven development: if the code is the most complete specification available, why write specs at all? The answer is that every non-trivial system has at least *two* sources of truth — and they capture different kinds of knowledge.

Specifications capture **architectural knowledge** — how the system is structured and why. This includes component relationships, design decisions, contracts between modules, constraints that must hold, and the rationale behind structural choices. A specification answers: "How is this designed, and why?" It is deliberately incomplete about implementation details. A good API contract specifies what a component promises to its callers, not how it fulfills that promise. This incompleteness is a feature: it is what allows implementations to change without breaking the system.

Code captures **implementation knowledge** — what the system actually does. This includes everything the specification described, but also everything it did not: the edge case a developer handled after a production incident two years ago, the timing workaround that prevents a race condition nobody documented, the error recovery path that accumulated through three rounds of bug fixes. Over time, the implementation knowledge in a non-trivial component outgrows its specification. The code becomes the authoritative record of what the system does, including things nobody planned or wrote down. The SATD study [13] provides empirical support: foundational technical debt — the first implementation decisions embedded in a file — is removed only 4.2% of the time, suggesting that early implementation knowledge tends to become permanent.

The line between architectural and implementation knowledge is not sharp. Performance characteristics, error handling strategies, and resource management often straddle both. The distinction is useful not because the boundary is clean, but because the extremes are clear: some knowledge obviously belongs in specifications (system structure, module contracts, design rationale) and some obviously belongs in code (algorithmic details, format parsing, data transformation). The gray zone requires engineering judgment.

These are not competing sources of truth — they are complementary. The spec answers "how is this designed and why?" The code answers "what does this actually do?" Problems arise when one is mistaken for the other: trusting the spec when the code has diverged leads to bugs in production; treating the code as the design document when the architectural thinking has been buried under years of patches leads to rot.

In a healthy system, architectural knowledge and implementation knowledge are aligned. In a rotting system, they diverge — the code does things the architecture never anticipated, and the specification (if it still exists) describes a design the code no longer follows. This divergence is itself a form of software rot.

**What about tests as specifications?** A comprehensive test suite is itself a form of executable specification — one that captures behavioral contracts more precisely than prose. Tests verify that a component produces the correct outputs for given inputs, handles edge cases, and respects integration contracts. In this sense, tests partially bridge the gap between architectural knowledge and implementation knowledge: they encode accumulated behavioral expectations that would otherwise exist only in the code. However, tests and specifications capture different things. Tests constrain *what* a component does (validation); specifications capture *how* the system is structured and *why* — design rationale, structural relationships across components, and the reasoning behind architectural boundaries. For AI-assisted development specifically, a test suite can verify whether generated code is correct (it validates output), but it cannot guide how code should be structured before it exists (it does not tell the generator where to place boundaries, which patterns to use, or how to decompose a problem). Tests are a verification tool; specifications are a generation tool. Tests and specifications serve complementary roles: together they narrow the gap between architectural and implementation knowledge more than either achieves alone.

This connects directly to Parnas's original insight. Information hiding is about *design decisions* — each module conceals a design decision from others [6]. The specification captures those decisions. The code implements them. When implementation reveals a design decision that wasn't anticipated — a new boundary that needs to exist, a constraint that only became obvious while writing code — updating the spec isn't capturing behavior. It's capturing architectural knowledge that was *discovered* during implementation.

Specification-driven development works because it forces architectural thinking before implementation. Writing the spec first means deciding on structure, contracts, and boundaries before generating code. The code then fills in everything the spec deliberately left out — the implementation details, the edge cases, the performance optimizations. Good specs make implementations *more* disposable by constraining what a regenerated version must satisfy. But "more disposable" is not "fully disposable." The gap between architectural knowledge (what was designed) and implementation knowledge (what the code actually does) is where regeneration breaks — and where internal design quality still matters.

The disposable code argument fails precisely because it conflates these two sources of truth. It assumes that regenerating from the spec (architectural knowledge) will recover everything in the code (implementation knowledge). It will not. Regeneration recovers the designed structure but loses the accumulated implementation knowledge that the system has come to depend on. No amount of specification discipline closes this gap entirely, because implementation knowledge accumulates through use, not through design — a pattern observable across the evidence in this report: software ages as its environment evolves while its structure remains static [1], evolving systems exhibit continuing growth in size and complexity [2], and the first technical debt introduced into a file is removed only 4.2% of the time [13].

---

## 7 Why Specifications

Section 5 established that AI-assisted development requires externalized architectural knowledge that constrains code before it is written. This section examines what form those constraints can take.

Five mechanisms are available:

**Code health metrics and quality gates** (CodeScene, SonarQube) detect structural problems after code is generated. A quality gate can reject code that falls below a threshold — but it cannot tell the generator how to structure code in the first place. Metrics are reactive: they evaluate output, they do not guide generation. They answer "is this code healthy?" not "how should this system be designed?"

**Architectural fitness functions** (ArchUnit, ArchGuard) encode structural rules as automated checks — "no dependency from layer A to layer B," "all services must communicate through defined interfaces." These are closer to specifications: they capture some architectural constraints in executable form. But they capture only constraints expressible as testable rules, not design rationale. They can enforce that a boundary exists, but not explain why the boundary was drawn there or what trade-off it reflects. When a fitness function fails, a human knows what to fix; an AI agent without access to the rationale may "fix" the violation by restructuring in a way that breaks a different, unstated constraint.

**Tests** validate what code does — they constrain outputs for given inputs. As Section 6.2 established, a test suite can verify whether generated code is correct, but it cannot guide how code should be structured before it exists. Tests are a verification tool; they do not tell the generator where to place boundaries, which patterns to use, or how to decompose a problem.

**Human review** provides both architectural knowledge and generative guidance — a reviewer can say "this should be a separate service" or "this violates our layering model." But human review does not scale. Telemetry from over 10,000 developers shows that AI adoption increases code review time by 91% [34]. The verification tax documented in Section 3.5 makes human review an increasingly expensive bottleneck, not a sustainable constraint mechanism.

**AI guardrails** — such as Meta's WhatsApp deployment [19] — use cross-session memory, explicit rules, and retrieval-augmented generation for knowledge grounding. These constrain the generator before code is written. They encode architectural knowledge in a form the AI can consult. They are, in every functional sense, specifications: externalized architectural knowledge that guides and constrains code generation.

The pattern is clear. Metrics, fitness functions, and tests are reactive — they evaluate code after generation. Human review is generative but does not scale. The only mechanism that is both generative (guides code before it exists) and scalable (does not require human intervention on every change) is externalized architectural knowledge — design decisions, component relationships, structural constraints, and the rationale behind them, captured in a form that both humans and AI can consult.

That is what a specification is.

This is not a claim that specifications are sufficient. They are not — quality gates, tests, and review remain necessary as verification layers. The claim is that specifications are *necessary*: no combination of reactive mechanisms alone can prevent the architectural degradation documented in Section 3, because reactive mechanisms can only reject bad output, not guide good generation. The evidence in Sections 2–5 establishes that AI needs architectural constraints; the analysis above establishes that specifications are the only constraint mechanism that operates before code is written.

---

## 8 Toward Spec-Anchored Development

### 8.1 Compound Engineering: The Broader Pattern

A practitioner methodology called **compound engineering** (Shipper & Klaassen, 2025) has gained significant traction in the AI-assisted development community [28]. The core idea: each development cycle should make the next one better. The methodology has four steps: plan (agents research the codebase and produce a detailed implementation plan), work (agents execute the plan), assess (multi-agent review from multiple perspectives), and compound (learnings are captured into structured files that future agents consult). The key step is the last one — systematically capturing knowledge so it compounds over time.

Will Larson characterized compound engineering as comprising "two extremely well-known patterns, one moderately well-known pattern, and one pattern that many practitioners have intuited but have not found a consistent mechanism to implement" [29]. He found it "not shocking" but "extremely effective" at converting intuitive best practices into something "specific, concrete, and largely automatic."

As originally practiced, compound engineering captures **operational knowledge** — bug patterns, coding conventions, failure modes, problem-solving heuristics. This makes each *task* more efficient but does not maintain a structural model of the system. A team could practice compound engineering perfectly and still have its architecture rot — it would simply rot more efficiently.

The pattern becomes architecturally significant when what gets captured isn't operational heuristics but design decisions, component relationships, and structural constraints. At that level, the compounding effect shifts from task efficiency to structural integrity — each cycle strengthens the system's architecture rather than just making the next task easier. The next section explores how the industry is applying this insight.

### 8.2 Spec-Driven Development: The Industry Response

The problems documented in Section 3 — AI generating code without architectural awareness — have not gone unnoticed. A significant industry movement toward **spec-driven development (SDD)** has emerged [25][26], with major open-source frameworks (GitHub's spec-kit [23], OpenSpec, BMAD-METHOD) attracting tens of thousands of GitHub stars, and companies like AWS (Kiro) and Tessl building commercial products around the concept.

Different tools and teams have adopted different levels of specification rigor:

- **Spec-first.** Write a specification before the task, then let AI implement it. The spec may be discarded afterward. This is essentially TDD and API-first design applied to AI-assisted workflows — established practice (TDD, API-first design) applied through a new interface.
- **Spec-anchored.** The specification persists and evolves alongside the code over its lifecycle. Spec and code are kept in sync through continuous validation. When implementation reveals architectural knowledge that was not anticipated during design — a new boundary, an unforeseen constraint — that knowledge flows back into the spec. This is compound engineering (Section 8.1) applied to design and architecture: the same plan-work-assess-compound cycle, but what gets captured is not operational heuristics but design decisions, component relationships, and structural constraints. This is the alignment problem: maintaining the relationship between architectural knowledge and implementation knowledge as both evolve.
- **Spec-as-source.** Humans maintain *only* the specification. Code is generated, marked as disposable, and regenerated whenever the spec changes. This is the most ambitious vision — and the one that runs directly into the limitations analyzed in Sections 6.1 and 6.2.

Current adoption is concentrated at the spec-first level, which has the widest tooling support and the lowest overhead. Spec-as-source has attracted venture capital but remains unproven at scale. Spec-anchored — the middle ground that would keep architectural and implementation knowledge in continuous sync — is the least practiced. A survey of 514 respondents about Specification by Example — of whom 339 used SBE — found that only 12% maintain version-controlled specification files as their source of truth, and roughly one-third of those using examples do not automate their specifications at all, allowing them to go stale [24]. This survey measured pre-AI BDD/SbE teams rather than AI-era spec-anchored workflows, so the figure is indicative rather than directly applicable. No dominant tool or framework has emerged for this level. Whether this gap reflects inherent difficulty, insufficient tooling, or simply less investment is an open question.

The analysis in this report provides a framework for understanding why the spectrum gets harder as it moves toward full disposability. Spec-first works because it captures architectural knowledge and lets the implementation accumulate its own knowledge through use. Spec-as-source requires specifications to capture *both* architectural and implementation knowledge — the gap that Section 6.2 identifies as fundamentally difficult to close.

**AI's most valuable role may not be generating code.** A parallel trend uses AI to *maintain architectural integrity* rather than produce more code — which is precisely the tooling gap that spec-anchored development needs filled. Tools like CodeScene expose code health metrics as quality gates for AI-generated code. Architecture governance platforms like ArchGuard use AI to analyze and enforce structural constraints. Multi-agent review systems dedicate separate agents to writing, critiquing, testing, and validating architectural alignment. This reframes AI from code producer to architectural integrity tool — using it to detect and repair the divergence between architectural knowledge and implementation knowledge rather than to generate more code.

A reasonable objection: if AI can extract architecture from code — as tools like ArchGuard already do — why maintain a separate specification? Because extraction recovers architecture *as-is*, not *as-intended*. It can't tell the difference between a deliberate design decision and accidental coupling that built up over years of patches. It can't recover *why* two services are separated or what failure mode the separation prevents. The specification's value is precisely this: it records how the system *should* be structured and why, giving you something to compare the actual architecture against.

If these tools mature, they could make spec-anchored development practical by automating the continuous sync between specification and implementation that teams currently fail to sustain manually. Whether AI-assisted spec maintenance can deliver on this promise is an empirical question that current evidence cannot answer.

**The waterfall risk.** ThoughtWorks [26] and Martin Fowler [25] have warned that rigid specifications could recreate waterfall's problems — slow feedback, premature commitment, specs that become outdated before implementation reveals their flaws. The framework from Section 6.2 clarifies this: specifications that capture *architectural knowledge* (structure, design decisions, contracts, constraints) stay stable as implementations change. Specifications that try to capture *implementation knowledge* (detailed behavioral requirements, edge case handling, performance specifics) go stale because implementation knowledge evolves through use, not through upfront design. The waterfall comparison is misleading: waterfall specifies once, implements, then discovers the spec was wrong. Spec-anchored development specifies continuously alongside implementation, with discoveries flowing back into the spec. The real concern isn't waterfall-style rigidity but ongoing maintenance cost. The SDD movement will succeed to the extent that it specifies architecture and avoids specifying implementation details.

**The fundamental bet** underlying spec-driven development is that if you can precisely specify what you want, AI becomes a reliable generator. The evidence in this report suggests this bet is partially correct — spec-first and spec-anchored approaches align with the established practices in Section 2. But complete specification remains impractical for the reasons Sections 6.1 and 6.2 describe. The industry is learning in real time where that ceiling is.

**This report's recommendation: spec-anchored development.** Of the three approaches, spec-anchored is the only one that directly addresses the core problem this report identifies — the divergence between architectural knowledge and implementation knowledge that drives software rot. Spec-first is valuable but incomplete: it front-loads architectural thinking, then lets the specification go stale as the code evolves. Spec-as-source is impractical for non-trivial systems, as Sections 6.1 and 6.2 demonstrate. Spec-anchored development maintains a living specification that evolves alongside the code: architectural knowledge discovered during implementation flows back into the spec, keeping the two sources of truth aligned. This parallels the refactoring finding from Section 2.3: the Late Active pattern succeeds because it maintains continuous structural discipline rather than treating quality as a one-time upfront investment [8].

The resemblance to documentation-driven development is not superficial — it's historically grounded. Decades of attempts to keep design documents synchronized with code have failed, from CASE tools in the 1980s to UML round-tripping in the 2000s. Two things are different now. First, AI code generation makes architectural knowledge *more* valuable, not less: human developers carry implicit understanding of a system's structure into every coding session, but AI agents start each session with no context beyond what's explicitly provided. The spec becomes the way to transmit architectural knowledge to the generator. Second, the maintenance burden that killed previous documentation efforts — the manual labor of keeping specs current as code evolves — is precisely the kind of structured, diff-aware task that AI itself could automate.

That only 12% of teams currently sustain this practice has two honest interpretations. It might be a tooling gap — existing Specification by Example tools like Cucumber and SpecFlow require manual maintenance of spec-to-code mappings, which is exactly the overhead that causes teams to give up. If AI can automate this maintenance, the 12% figure reflects a solvable problem. Or it might reflect fundamental impracticality — that keeping specs synchronized with evolving code is just too costly regardless of tooling. This report can't resolve which is correct. It can note that previous SbE tools automated *running* specs but left *maintaining* specs to humans. AI-assisted spec maintenance is a genuinely new capability, not yet validated at scale. The recommendation for spec-anchored development depends on this capability maturing.

This recommendation follows from the analytical framework developed in Sections 6.1 and 6.2. It has not been empirically validated against alternatives — no study compares outcomes of spec-anchored versus spec-first teams in AI-assisted development. Empirical comparison is a critical gap in the current evidence base.

### 8.3 Managed vs. Unmanaged: The Performance Gap

| Metric | Unmanaged AI Code | Architecturally Managed |
|---|---|---|
| Initial Build Speed | 55% Faster [20] | Pre-AI levels |
| Code Complexity | +41.6% [12] | Pre-AI levels |
| Refactoring Rate | Declining (<10%) [11] | Late Active Pattern [8] |
| Delivery Stability | AI amplifies weaknesses [18] | AI amplifies strengths [18] |
| Developer Trust | 46% distrust [17] | Pre-AI levels (human-reviewed) |

### 8.4 Synthesis

**What follows is an interpretive conclusion drawn from the evidence presented, not a direct empirical finding.**

The logic runs: architecture prevents rot (established across decades of independent research, Section 2), AI without constraints degrades quality (consistent across every independent source, Section 3), and architecture determines AI outcomes (Section 5). The logical consequence — that AI needs externalized architectural knowledge — leads to specifications by elimination of alternatives (Section 7). Architectural quality is the primary determinant of whether AI-assisted development accelerates delivery or accelerates decay. Teams with strong architectural practices are positioned to benefit from AI's speed advantages while their existing structural discipline constrains the rot that AI-generated code might otherwise introduce. Teams without such practices face the compounding effects documented in Section 3 — rising complexity, declining refactoring, and persistent foundational debt — now amplified by higher code velocity.

**Confidence: ANALYTICAL.** The two premises — that architecture determines AI outcomes (Section 5.1) and that AI without constraints degrades quality (Section 5.2) — are empirically supported across multiple independent studies. The inference that AI needs externalized architectural knowledge follows logically from these premises. The elimination of alternative constraint mechanisms (Section 7) is an analytical argument. The SDD industry analysis (8.2) reflects current developments as of early 2026, with adoption data drawn from practitioner surveys rather than controlled studies. The specific recommendation for spec-anchored development has not been empirically compared against alternatives — that remains a critical gap in the evidence base.

---

## 9 Summary of Findings

- **Software rot is real and costly.** 45% of the world's code is fragile [3], tech debt accounts for 20–40% of technology estate value [4], and Lehman's Laws confirm that complexity increases continuously in evolving systems [2]. This is established science.
- **Architecture prevents rot.** Classes with antipatterns are up to 31 times more fault-prone [7], the Late Active refactoring pattern produces the best quality outcomes [8], loosely coupled architecture predicts elite delivery performance [9], and elite code health accelerates development by 43% while reducing defects up to 15x [32]. Decades of independent research confirm this.
- **Evidence suggests AI accelerates rot.** Vendor analyses indicate code churn is projected to double [10], refactoring has declined from 25% to less than 10% of changed lines [11], and a peer-reviewed study found 41.6% complexity increase in AI-assisted repositories [12]. These findings warrant attention but require further independent validation.
- **Current AI tools struggle with architectural reasoning.** They require human oversight for system-level concerns [14] and produce "Hallucinated Coupling" that violates design principles [15].
- **AI amplifies existing practices.** DORA research shows AI magnifies both strengths and weaknesses [18]. AI increases defect risk by at least 30% on unhealthy code [33]. Meta's enterprise deployment found architectural guardrails essential at scale [19].
- **Developers see it too.** 46% distrust AI output vs. 33% who trust it, and favorability toward AI tools dropped from 70%+ to 60% year-over-year, even as 81% continue using them [17].
- **Two premises, one conclusion.** Architecture quality determines AI outcomes (Premise 1, Section 5.1). AI without constraints degrades quality (Premise 2, Section 5.2). The logical consequence: AI needs externalized architectural knowledge that constrains code before it is written. Every alternative constraint mechanism — metrics, tests, fitness functions, human review — is either reactive or does not scale. Specifications are the only mechanism that is both generative and scalable (Section 7).
- **Code is not fully disposable.** Every non-trivial system has two sources of truth: specifications capture architectural knowledge (structure, design decisions, contracts), and code captures implementation knowledge (edge cases, workarounds, accumulated behavior). Regenerating from the spec recovers the designed structure but loses the implementation knowledge the system has come to depend on.
- **Spec-anchored development is the most promising response.** Of the three emerging approaches — spec-first, spec-anchored, and spec-as-source — spec-anchored is the only one that directly addresses the divergence between architectural and implementation knowledge. Current adoption is low, arguing not against the approach but for better tooling — and for directing AI at the alignment problem rather than at generating more code. The premises are empirically supported and the conclusion follows logically; the specific practice of spec-anchored development has not been compared against alternatives in a controlled study.

---

## 10 Sources

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

[32] **Borg, Mones, Tornhill, Pruvost (2024):** *Increasing, not Diminishing: Investigating the Returns of Highly Maintainable Code.* Study of 46,000 source code files finding that improving code health from average to elite accelerates development by 43% and reduces defects up to 15x. Best Paper Award at the 7th ACM/IEEE International Conference on Technical Debt 2024. Authors are affiliated with CodeScene and Lund University.
https://arxiv.org/abs/2401.13407

### Preprints

[13] *Self-Admitted Technical Debt in LLM Software.* Empirical study of 477 repositories examining how technical debt accumulates in LLM-related codebases. arXiv, January 2026.
https://arxiv.org/html/2601.06266v1

[15] *Quantitative Analysis of Technical Debt and Pattern Violation in LLM Architectures.* Introduces "Hallucinated Coupling" metric for AI-generated code. arXiv, December 2025.
https://arxiv.org/html/2512.04273

[33] **Borg, Hagatulah, Tornhill, Soderberg (2026):** *Code for Machines, Not Just Humans: Quantifying AI-Friendliness with Code Health Metrics.* LLM-based refactoring experiments on 5,000 Python files finding AI increases defect risk by at least 30% on unhealthy code. Authors affiliated with CodeScene and Lund University. arXiv, January 2026.
https://arxiv.org/abs/2601.02200

### Established Research Programs

[9] **Google DORA (2019):** *Accelerate State of DevOps Report.* Elite performers deploy 208x more frequently, recover 2,604x faster; loosely coupled architecture is a key predictor. Pre-AI era.
https://dora.dev/research/2019/dora-report/ (PDF: https://services.google.com/fh/files/misc/state-of-devops-2019.pdf)

[16] **METR (2025):** *Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity.* Randomized controlled trial finding experienced developers 19% slower with AI tools in large open-source repositories.
https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/

[18] **Google DORA (2025):** *State of AI-assisted Software Development 2025.* AI acts as an amplifier of existing organizational practices.
https://dora.dev/research/2025/dora-report/

[31] **Google DORA (2024):** *Accelerate State of DevOps Report 2024.* A 25% increase in AI tool adoption correlates with a 7.2% decrease in delivery stability and a 1.5% decrease in throughput.
https://dora.dev/research/2024/dora-report/ (PDF: https://services.google.com/fh/files/misc/2024_final_dora_report.pdf)

### Industry Reports and Surveys

[3] **CAST Software Intelligence (2025):** *Coding in the Red: The State of Global Technical Debt.* Industry report analyzing 10 billion lines of code across 17 countries. CAST is a commercial code analysis vendor.
https://www.castsoftware.com/ciu/coding-in-the-red-technical-debt-report-2025

[4] **McKinsey & Company (2020):** *Tech Debt: Reclaiming Tech Equity.* CIO survey on tech debt's impact on technology estate value and budgets.
https://www.mckinsey.com/capabilities/mckinsey-digital/our-insights/tech-debt-reclaiming-tech-equity

[5] **CISQ (2022):** *The Cost of Poor Software Quality in the US.* Estimates $2.41 trillion total cost and $1.52 trillion in accumulated technical debt. CISQ is co-founded by OMG and Carnegie Mellon's Software Engineering Institute.
https://www.it-cisq.org/the-cost-of-poor-quality-software-in-the-us-a-2022-report/

[17] **Stack Overflow (2025):** *2025 Developer Survey — AI Section.* Annual survey of 49,000 developers. 46% distrust AI output vs. 33% who trust it; favorability dropped from 70%+ to 60%.
https://survey.stackoverflow.co/2025/ai/

[24] **Gojko Adzic (2020):** *Specification by Example — 10 Years Later.* Survey of 514 respondents on Specification by Example adoption; 339 used SBE, roughly one-third did not automate specifications.
https://gojko.net/2020/03/17/sbe-10-years.html

### Vendor Studies

[10] **GitClear (2024):** *Coding on Copilot: 2023 Data Suggests Downward Pressure on Code Quality.* Analysis of 153 million changed lines (2020–2023). GitClear is a commercial code analytics platform; not peer-reviewed.
https://www.gitclear.com/coding_on_copilot_data_shows_ais_downward_pressure_on_code_quality

[11] **GitClear (2025):** *AI Copilot Code Quality: 2025 Data.* Analysis of 211 million changed lines (2020–2024) showing refactoring decline from 25% to <10% and code duplication increase from 8.3% to 12.3%. Not peer-reviewed.
https://www.gitclear.com/ai_assistant_code_quality_2025_research

[20] **GitHub (2022):** *Research: Quantifying GitHub Copilot's Impact on Developer Productivity.* Vendor-conducted study finding developers completed tasks 55% faster with Copilot (n=95). Not peer-reviewed.
https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/

[23] **GitHub (2025):** *spec-kit — Spec-Driven Development with AI.* Open-source framework for structuring AI-assisted development around specifications.
https://github.com/github/spec-kit

[34] **Faros AI (2025):** *The AI Productivity Paradox.* Engineering telemetry from 10,000+ developers across 1,255 teams. High-AI-adoption teams merge 98% more PRs but review time increases 91%, bugs increase 9% per developer, and delivery metrics remain flat. Faros AI is an engineering intelligence vendor; not peer-reviewed.
https://www.faros.ai/blog/ai-software-engineering

### Practitioner Commentary

[21] **Adam Tornhill & Martin Fowler / Thoughtworks (2024):** Podcast on refactoring with AI. Tornhill's research found AI refactoring correct only 37% of the time.
https://www.thoughtworks.com/en-us/insights/podcasts/technology-podcasts/refactoring-with-ai

[22] **Kent Beck / Pragmatic Engineer (2025):** Interview covering TDD practices with AI agents. Beck reports that AI agents sometimes delete tests to make them "pass."
https://newsletter.pragmaticengineer.com/p/tdd-ai-agents-and-coding-with-kent

[25] **Martin Fowler (2025):** *Exploring Generative AI — Spec-Driven Development: Tools.* Analysis of SDD tooling including Kiro, spec-kit, and Tessl.
https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html

[26] **ThoughtWorks (2025):** *Spec-Driven Development: Unpacking 2025's New Engineering Practice.* Industry analysis of SDD trends, including waterfall risk.
https://www.thoughtworks.com/en-us/insights/blog/agile-engineering-practices/spec-driven-development-unpacking-2025-new-engineering-practices

### Practitioner Formulations

[27] **Hyrum Wright:** *Hyrum's Law.* "With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody."
https://www.hyrumslaw.com/

[28] **Dan Shipper & Kieran Klaassen / Every (2025):** *Compound Engineering: How Every Codes With Agents.* Practitioner methodology where each development cycle compounds knowledge for the next. Four-step workflow: plan, work, assess, compound.
https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents

[29] **Will Larson / Irrational Exuberance (2026):** *Learning from Every's Compound Engineering.* Independent analysis characterizing compound engineering as effective systematization of intuitive practices.
https://lethain.com/everyinc-compound-engineering/
