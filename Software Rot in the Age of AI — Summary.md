# Software Rot in the Age of AI

**A Plain-Language Summary**

**Compiled by Maxim Glaezer | March 2026**

---

## The Problem

Software decays over time. Even if nobody touches the code, the world around it changes — new requirements, new integrations, new security threats — and the software falls behind. This is called **software rot**.

It is expensive. Nearly half the world's code is fragile. The US alone loses an estimated $2.4 trillion per year to poor software quality. Companies spend 20–40% of their technology budgets just managing old, decaying systems.

---

## What Prevents Rot

Over fifty years of research has established one consistent answer: **good architecture**.

Systems built with clear boundaries between components, well-defined contracts, and thoughtful structure are easier to change, have fewer bugs, and perform better. The numbers are striking:

- Poorly structured code has up to **31 times more bugs** than well-structured code.
- Teams with good architecture deploy **208 times more often** and recover from failures **2,604 times faster**.
- Teams that regularly refactor — clean up and restructure their code — produce the best quality outcomes.

None of this is controversial. Architecture prevents rot. The evidence is deep and consistent.

---

## How AI Changes Things

AI coding tools let developers write code faster. But early evidence suggests they also accelerate rot:

- **More code, less cleanup.** Code duplication is rising. Refactoring — the practice of restructuring existing code — has dropped sharply.
- **More complexity.** One study of 806 projects found that AI-assisted code was **42% more complex** and had 30% more quality warnings.
- **Speed gains fade.** The initial productivity boost from AI tools disappears after about two months, as the accumulated mess slows teams down.
- **AI struggles with the big picture.** AI can write individual functions well, but it doesn't understand how pieces fit together. It creates code that looks correct in isolation but breaks the system's structure.

This evidence is early — some studies are from vendors, some are preprints — so we should treat it as a strong signal rather than settled science.

Meanwhile, developers are noticing. In a survey of 49,000 developers, 46% said they distrust AI-generated code — yet 81% keep using it.

---

## The Key Insight: AI Amplifies What You Already Have

Google's research program on software delivery found that AI acts as an **amplifier**. It makes good teams better and struggling teams worse.

If your architecture is strong, AI generates code within good boundaries and your structure contains the mess. If your architecture is weak, AI generates more mess, faster, with nobody steering.

**Architecture was always important. With AI, it's the deciding factor.**

---

## "Just Regenerate It" — Why That Doesn't Work

Some argue that since AI can generate code so quickly, we don't need to care about code quality. If something rots, just throw it away and regenerate it.

This works for simple things — a small utility function, a data transformation, a basic API endpoint. For a large fraction of everyday code, disposability is genuinely practical.

But for complex, long-lived systems it breaks down:

- **The code knows things the spec doesn't.** Over time, code accumulates knowledge — edge cases handled, race conditions worked around, quirks accommodated. Regenerating from the original description loses all of this.
- **You can't fully specify complex behavior.** Writing a complete specification of everything a component does is often harder than writing the component itself. In practice, the code *is* the most complete description of what the system does.
- **The problem repeats at every level.** Even if you perfectly specify a component's external interface, its internals contain sub-components with their own unspecified relationships, all the way down.

The irony: making code safely disposable requires exactly the architectural discipline — clear interfaces, comprehensive contracts, modular boundaries — that prevents rot in the first place.

---

## Two Sources of Truth

Every non-trivial software system has two sources of truth:

**Specifications** capture **architectural knowledge** — how the system is structured and why. Component relationships, design decisions, contracts between parts, and the reasoning behind choices.

**Code** captures **implementation knowledge** — what the system actually does. This includes everything the spec described, plus everything it didn't: the bug fix from two years ago, the performance workaround nobody documented, the error handling that accumulated through three rounds of patches.

These aren't competing — they're complementary. The spec answers "how is this designed?" The code answers "what does this actually do?"

Problems arise when they diverge. In a healthy system, they're aligned. In a rotting system, the code does things the architecture never intended, and the spec (if it still exists) describes a design the code no longer follows. **This divergence is itself a form of rot.**

Tests play a complementary role: they verify that code behaves correctly, but they don't capture *why* the system is structured a certain way or guide how new code should be organized. Specs guide generation; tests validate it.

---

## The Industry Response: Spec-Driven Development

The software industry has noticed these problems and is responding with **spec-driven development** — writing specifications before generating code with AI. Major frameworks (GitHub's spec-kit, OpenSpec) have attracted tens of thousands of GitHub stars.

Three approaches are emerging:

1. **Spec-first.** Write a spec, let AI generate code, move on. The spec may be discarded afterward. This is the most common approach today.
2. **Spec-anchored.** The spec lives alongside the code and both evolve together. When building reveals new architectural insights, they flow back into the spec. This is the hardest to sustain but the most valuable.
3. **Spec-as-source.** Humans maintain only the spec. Code is generated and treated as fully disposable. This is the most ambitious vision, but runs into the limitations described above.

---

## This Report Recommends: Spec-Anchored Development

Of these three, **spec-anchored** is the only approach that directly addresses the core problem — the growing gap between what the spec says and what the code actually does.

Spec-first is valuable but incomplete: it captures your thinking upfront, then lets the spec go stale. Spec-as-source is impractical for complex systems. Spec-anchored keeps both sources of truth alive and aligned.

This is not easy. Only about 12% of teams have historically sustained living specifications. Previous attempts at keeping documentation in sync with code have mostly failed.

Two things are different now:

1. **AI makes specs more valuable.** Human developers carry implicit understanding of a system's structure. AI agents don't — they start each session with no context beyond what you explicitly provide. The spec becomes the way you transmit architectural knowledge to the AI.
2. **AI can help maintain specs.** The manual burden of keeping specs current — which killed previous documentation efforts — is exactly the kind of structured task AI could automate.

Whether AI-assisted spec maintenance will actually work at scale is an open question. But the logic is clear: if we want AI to generate structurally sound code, we need to give it structural guidance. Living specifications are how we do that.

---

## The Bottom Line

- Software rots. This is established fact.
- Good architecture prevents rot. Decades of research confirm this.
- AI generates more code with less architectural awareness, which early evidence suggests accelerates rot.
- AI amplifies whatever practices you already have — good or bad.
- You can't just "regenerate" complex code. The code knows things the spec doesn't.
- Every system has two sources of truth: the spec (architecture) and the code (implementation). Keeping them aligned is the challenge.
- Spec-anchored development — maintaining a living specification alongside the code — is the most promising response, though it remains unproven at scale.

**Architecture was always the antidote to software rot. In the age of AI, it's the prerequisite.**
