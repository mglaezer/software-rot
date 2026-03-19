# Software Rot in the Age of AI

**A Plain-Language Summary**

**Compiled by Maxim Glaezer | March 2026**

---

## The Problem

Poor software quality costs the US economy $2.4 trillion per year. Companies spend 20–40% of their technology budgets just managing old, decaying systems. It would take 25 million developers working full-time for 9 years to pay off the technical debt that already exists.

This decay is called **software rot** — software degrades over time as the world around it changes, even if nobody touches the code. New requirements, new integrations, new security threats pile up, and the software falls behind.

AI-assisted development was expected to reduce this burden. The early evidence suggests it's making it worse.

---

## What Prevents Rot

Over fifty years of research gives one consistent answer: **good architecture**.

Systems built with clear boundaries, well-defined contracts, and thoughtful structure are easier to change, have fewer bugs, and perform better. The numbers are striking:

- Poorly structured code has up to **31 times more bugs** than well-structured code.
- Teams with good architecture deploy **208 times more often** and recover from failures **2,604 times faster**.
- Improving code health from average to elite **accelerates development by 43%** and **reduces defects up to 15x**.
- Teams that regularly refactor — clean up and restructure their code — produce the best quality outcomes.

Architecture prevents rot. The evidence is deep and consistent.

---

## How AI Changes Things

AI coding tools let developers write code faster. But early evidence suggests they also accelerate rot:

- **More code, less cleanup.** Code duplication is rising. Refactoring — restructuring existing code — has dropped from 25% to less than 10% of code changes.
- **More complexity.** A study of 806 projects found that AI-assisted code was **42% more complex** and had 30% more quality warnings. Speed gains disappeared after just two months.
- **AI struggles with the big picture.** AI can write individual functions well, but doesn't understand how pieces fit together. It creates code that looks correct in isolation but breaks the system's structure.
- **The review bottleneck.** Teams using AI heavily merge 98% more code, but code review time increases by 91% and bugs increase by 9% per developer. Despite feeling faster individually, company-wide delivery metrics stay flat.
- **AI makes bad code worse.** A controlled experiment found that AI increases defect risk by at least 30% when applied to poorly structured code. Good code, on the other hand, produces good AI output.

81% of professional developers now use AI tools. In a survey of 49,000, 46% said they distrust AI-generated code — yet they keep using it.

---

## Two Premises, One Conclusion

The evidence establishes two things:

**Premise 1: Architecture quality determines AI outcomes.** Google's research found that AI acts as an amplifier — it makes good teams better and struggling teams worse. AI increases defect risk on unhealthy code but works well on healthy code. Meta's WhatsApp team found that architectural guardrails were essential to making AI-generated code production-worthy.

**Premise 2: AI without constraints degrades quality.** Every independent study points the same way — complexity up, refactoring down, duplication up, review time up, delivery stability down.

**What follows:** If architecture determines outcomes, and AI without constraints degrades quality, then AI needs externalized architectural knowledge that constrains code *before* it's written.

This isn't a recommendation — it's a logical consequence of the evidence. The question is: what form should those constraints take?

---

## Why Specifications

There are five ways to constrain AI-generated code:

1. **Code quality metrics** (like SonarQube) catch problems *after* code is generated. They can reject bad code, but they can't tell the AI how to structure code in the first place.
2. **Architectural rules** (like ArchUnit) encode constraints as automated checks — "no dependency from A to B." But they capture rules, not the *reasoning* behind those rules.
3. **Tests** verify what code does. They can't guide how code should be structured before it exists.
4. **Human review** provides real architectural guidance — but it doesn't scale. AI adoption already increases review time by 91%.
5. **AI guardrails** — like Meta's WhatsApp deployment with cross-session memory and explicit rules — constrain the generator before code is written. These are, in every functional sense, *specifications*.

The pattern: metrics, rules, and tests are reactive — they evaluate code after it's generated. Human review is proactive but doesn't scale. The only mechanism that is both proactive *and* scalable is externalized architectural knowledge — design decisions, structural constraints, and the rationale behind them, captured in a form that both humans and AI can consult.

That's what a specification is.

Specifications aren't sufficient on their own — you still need tests, metrics, and review as verification layers. But they are *necessary*: no combination of reactive mechanisms can prevent the structural decay the evidence documents, because reactive mechanisms can only reject bad output, not guide good generation.

---

## "Just Regenerate It" — Why That Doesn't Work

Some argue that since AI can generate code so quickly, we don't need to care about quality. If something rots, just throw it away and regenerate it.

This works for simple things — a utility function, a data transformation, a basic API endpoint. For a large fraction of everyday code, disposability is genuinely practical.

But for complex, long-lived systems it breaks down:

- **The code knows things the spec doesn't.** Over time, code accumulates knowledge — edge cases handled, race conditions worked around, quirks accommodated. Regenerating from the original description loses all of this.
- **You can't fully specify complex behavior.** Writing a complete specification of everything a component does is often harder than writing the component itself. The code *is* the most complete description of what the system does.
- **The problem repeats at every level.** Even if you perfectly specify a component's external interface, its internals contain sub-components with their own unspecified relationships, all the way down.

The irony: making code safely disposable requires exactly the architectural discipline — clear interfaces, comprehensive contracts, modular boundaries — that prevents rot in the first place.

---

## Two Sources of Truth

Every non-trivial software system has two sources of truth:

**Specifications** capture **architectural knowledge** — how the system is structured and why. Component relationships, design decisions, contracts between parts, and the reasoning behind choices.

**Code** captures **implementation knowledge** — what the system actually does. This includes everything the spec described, plus everything it didn't: the bug fix from two years ago, the performance workaround nobody documented, the error handling that accumulated through three rounds of patches.

These aren't competing — they're complementary. The spec answers "how is this designed?" The code answers "what does this actually do?"

Problems arise when they diverge. In a healthy system, they're aligned. In a rotting system, the code does things the architecture never intended, and the spec (if it still exists) describes a design the code no longer follows. **This divergence is itself a form of rot.**

---

## The Industry Response: Spec-Driven Development

The software industry has noticed and is responding with **spec-driven development** — writing specifications before generating code with AI. Major frameworks (GitHub's spec-kit, OpenSpec) have attracted tens of thousands of GitHub stars.

Three approaches are emerging:

1. **Spec-first.** Write a spec, let AI generate code, move on. The spec may be discarded afterward. This is the most common approach today.
2. **Spec-anchored.** The spec lives alongside the code and both evolve together. When building reveals new architectural insights, they flow back into the spec. This is the hardest to sustain but the most valuable.
3. **Spec-as-source.** Humans maintain only the spec. Code is generated and treated as fully disposable. This is the most ambitious vision, but runs into the limitations described above.

A related methodology called **compound engineering** has gained traction: each development cycle captures what was learned into structured files that guide future work. Spec-anchored development applies this pattern at the architectural level — instead of compounding task-level heuristics, you compound architectural understanding. Each cycle strengthens the system's structural integrity.

---

## This Report Recommends: Spec-Anchored Development

Of the three approaches, **spec-anchored** is the only one that directly addresses the core problem — the growing gap between what the spec says and what the code actually does.

Spec-first is valuable but incomplete: it captures your thinking upfront, then lets the spec go stale. Spec-as-source is impractical for complex systems. Spec-anchored keeps both sources of truth alive and aligned.

This is not easy. Only about 12% of teams have historically sustained living specifications. Previous attempts at keeping documentation in sync with code have mostly failed.

Two things are different now:

1. **AI makes specs more valuable.** Human developers carry implicit understanding of a system's structure. AI agents don't — they start each session with no context beyond what you explicitly provide. The spec becomes the way you transmit architectural knowledge to the AI.
2. **AI can help maintain specs.** The manual burden of keeping specs current — which killed previous documentation efforts — is exactly the kind of structured task AI could automate.

Whether AI-assisted spec maintenance will actually work at scale is an open question. But the logic is clear: if we want AI to generate structurally sound code, we need to give it structural guidance. Living specifications are how we do that.

---

## The Bottom Line

- Software rots. This is established fact — and it costs trillions.
- Good architecture prevents rot. Decades of research confirm this, with the latest showing 43% faster development and 15x fewer defects for well-structured code.
- AI generates more code with less architectural awareness, accelerating rot. The evidence is consistent across every independent source.
- AI amplifies whatever practices you already have — good or bad. It increases defect risk on unhealthy code and works well on healthy code.
- Two premises lead to one conclusion: if architecture determines AI outcomes, and AI without constraints degrades quality, then AI needs externalized architectural knowledge — specifications — before code is written. No alternative mechanism is both proactive and scalable.
- You can't just "regenerate" complex code. The code knows things the spec doesn't.
- Spec-anchored development — maintaining a living specification alongside the code — is the most promising response, though it remains unproven at scale.

**Architecture was always the antidote to software rot. In the age of AI, it's the prerequisite.**
