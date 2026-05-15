# Boréal 🌲

> **Your policy. Your gaps. Your claim. In both official languages.**

**A bilingual AI insurance advisor built natively on IBM Bob + Context Studio.**

IBM Bob-a-thon submission · TrueNorth AI Team · May 22, 2026

---

## The problem

Insurance in Canada has a clarity problem. The average homeowner spends 45 minutes with their policy and still can't answer one question: *am I actually covered?* For the ~30% of Canadians who consume insurance in French, the problem multiplies — most consumer tools translate badly, regulatory terminology gets lost, and customers fall through the cracks of a bilingual obligation that every Canadian P&C insurer has but few execute well.

Most AI insurance demos solve half the problem: they summarize a policy. They stop at the moment that matters least. Boréal does both halves — **pre-loss gap analysis and post-loss claim guidance** — bilingually, end-to-end.

---

## The solution

**Four coordinated agents, two complete flows, one bilingual experience.**

| Flow | What it does |
|---|---|
| **Policy Review** *(pre-loss)* | Upload an Ontario auto policy → Policy Reader extracts coverages with PII redacted → 3 lifestyle questions → Coverage Advisor scores 13 gap rules → user gets exact questions to ask their broker. |
| **Claim Prep** *(post-loss)* | User describes what happened (or picks a scenario) → Triage classifies the loss type → Claim Prep Agent applies Ontario Fault Determination Rules → user gets fault assessment, coverage path, 24-hour checklist, and adjuster questions. |

Built and demoed on **Maple Mutual / Jean-Pierre Tremblay** — a fictional Ontario test policy designed to surface meaningful gaps (Rules R1, R2, R4, R7) and three claim scenarios (rear-end, hit-a-deer, vandalism).

---

## Three competitive moats

🇨🇦 **Bilingual moat.** 280+ verified EN/FR regulatory term pairs sourced from the *Manuel du plan statistique automobile* (PSA), GISA / ASAG bulletins, and Ontario Auto Reform documentation. *Avenant FPQ n° 44R. Indemnités d'accident bonifiées. IDDM.* This isn't Google Translate — it's the terminology only an in-domain Canadian P&C practitioner has working access to. Hard to copy. Weeks of work to replicate.

🤖 **Genuinely agentic.** Four specialized agents with versioned system prompts, structured outputs, and clean handoffs — not one chatbot pretending to be smart. The **Claim Prep Agent** is the differentiator: most Bob-a-thon submissions stop at summarize-a-document. Boréal goes to the harder problem — *what do I do now, at the scene, with the adjuster on the phone tomorrow?*

🎯 **Calibrated honesty.** When a user's claim description is ambiguous, Boréal does not guess. It surfaces what it heard and asks the user to clarify. When Ontario's Fault Determination Rules contain edge cases (e.g., swerved-vs-impacted in an animal strike), Boréal flags the caveat explicitly. Production-grade calibration encoded in agent specs, not a chat-prompt afterthought.

---

## How Boréal maps to Bob's three pillars

| Pillar | Evidence |
|---|---|
| **Spec-driven** | Every agent has a versioned system prompt with role, inputs, outputs, hard rules, edge cases (`agents/01-triage-agent.md` → `04-claim-prep-agent.md`). Hard guardrails: no pricing, no legal advice, no policy binding. |
| **Context Studio** | Provincial regulations, bilingual terminology framework, tone & disclaimer guardrails — all in `context/context-studio-config.md`. PII redaction rules encoded in the Policy Reader Agent v2. |
| **Agentic design** | Four coordinated agents with explicit handoffs. Triage routes by language + intent. Policy Reader → Coverage Advisor for pre-loss. Triage → Claim Prep for post-loss. Structured YAML outputs between agents. |

---

## What's in the submission

| Artifact | What to look at |
|---|---|
| `prototype/boreal-prototype.html` | **1,000-line interactive prototype, 10 screens, EN/FR.** Both flows fully clickable, scenario-aware, with calibrated-uncertainty fallback. Open it and play. |
| `agents/` | 4 versioned system prompts (~1,400 lines total). All v2 except Triage (v1 already solid). |
| `context/context-studio-config.md` | Bilingual terminology framework + Boréal persona + hard guardrails. |
| `demo/boreal-test-policy.pdf` | 3-page fictional Maple Mutual / Jean-Pierre Tremblay policy designed to trigger 4 specific gap rules. |
| `docs/demo-script.md` | Word-for-word 4-minute video script with timing marks. |
| `submission/boreal-demo.mp4` | The 4-minute demo video itself. |
| `.bobignore` | Security configuration — prevents Bob from reading raw PII files. |

---

## Reusability for IBM Consulting

Boréal's architecture is **immediately reusable** for Canadian financial services clients:

- Every Canadian P&C insurer has a bilingual obligation under the Official Languages Act and provincial consumer protection laws.
- Every Canadian bank has cross-border bilingual compliance needs.
- The Triage → Specialist agent pattern transfers cleanly to claims triage, underwriting intake, fraud screening, and customer complaint routing.
- The bilingual regulatory terminology framework is an asset-grade reusable IP — instantly applicable to property, tenant, life, and commercial lines.

---

## Scope discipline

**In scope (built and demonstrable):**
- Ontario auto insurance
- English + French
- Four agents (Triage, Policy Reader v2, Coverage Advisor v2, Claim Prep v2)
- Two flows (gap analysis + claim guidance)
- Three claim scenarios (rear-end, animal strike, vandalism)

**Out of scope (architecture-ready, not built):**
- Other provinces (config-driven, would inherit the framework)
- Home, tenant, commercial, life (same agent topology, different context)
- Pricing, quoting, policy binding — *regulatory boundaries Boréal will never cross.* This is education, not advice.

---

## Why a Canadian P&C practitioner built this

Boréal was built by an IBM Consulting practitioner who works on the **Canadian P&C regulatory reporting program** (the Automobile Statistical Plan / GISA / ASAG). The bilingual terminology framework draws on real ERD / DEC documentation, GISA bulletins (including the 2026-04 and 2026-05 Alberta v4.2 releases), and the PSA Manuel du plan statistique — sources only an in-domain practitioner has working access to.

This isn't a generic LLM demo dressed in maple leaves. It's an authentic Canadian insurance product spec, built by someone who lives in the regulatory world it serves.

---

## Suggested evaluation order (for judges)

1. **Read** this pitch — you're here. *(3 min)*
2. **Watch** `submission/boreal-demo.mp4` — the 4-minute demo. *(4 min)*
3. **Open** `prototype/boreal-prototype.html` in a browser. Toggle EN ↔ FR. Click through both flows. Try typing a vague claim description and see the calibrated clarification screen. *(5 min)*
4. **Skim** `agents/04-claim-prep-agent.md` — see the Ontario FDR logic and the bilingual templates. *(3 min)*
5. **Skim** `context/context-studio-config.md` — see the terminology table that powers the bilingual moat. *(2 min)*

**Total: 17 minutes to a complete picture.**

---

**Boréal — built on Bob. Pour vrai.**

*TrueNorth AI Team · May 2026*
