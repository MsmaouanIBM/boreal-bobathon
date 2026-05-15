# Boréal — Prompt and Bob Usage Documentation

This document covers Bob-a-thon Required Deliverable #3: *"Document all prompts used with Bob AI during development. Show how Bob assisted in code generation, debugging, testing, or problem-solving."*

---

## 1. How Boréal uses Bob

Boréal is a **Bob-native project**. The artifacts in this repository are not documentation about Bob — they are the actual configuration that runs on Bob's three pillars:

| Bob pillar | Boréal artifact |
|---|---|
| **Spec** | The four files in `agents/` — versioned system prompts (v1 / v2) with role, inputs, outputs, hard rules, edge cases |
| **Context** | `context/context-studio-config.md` — the literal Context Studio configuration (persona, bilingual terminology, guardrails) |
| **Agentic orchestration** | The Triage → Specialist topology defined across the four agent files |
| **Security** | `.bobignore` — the file-access policy Bob's runtime respects |

In other words: **the prompts in `agents/` are the product.** They are not samples or examples. They are the runtime configuration Bob loads when Boréal answers a user's question.

---

## 2. The product prompts (four agents)

These are the four system prompts that make Boréal work. Each is a complete, versioned specification.

### 2.1 — Triage Agent (`agents/01-triage-agent.md`, v1)

**Purpose:** First touchpoint. Detects the user's language (EN / FR), province (ON / other), and intent (`policy_review` / `coverage_gap` / `claim_prep`). Routes to one of the three specialists. Outputs structured JSON.

**Key features:**
- Bilingual detection without asking the user
- Strict scope enforcement (Ontario only in v1)
- JSON output schema for downstream agents to consume

### 2.2 — Policy Reader Agent (`agents/02-policy-reader-agent.md`, v2 — 385 lines)

**Purpose:** Ingests a PDF / image / pasted text of an Ontario auto policy. Emits a structured YAML policy summary. **PII is redacted before any output** (insured name, address, policy number, VIN, driver's license, DOB).

**Key features:**
- Five-pass extraction methodology (PII detection → header → coverages → endorsements → anomaly flags)
- YAML schema with all 9 common OPCFs (20, 27, 39, 43, 44R, etc.)
- Worked input → output example
- Handles French-language policies (output remains in English keys)

### 2.3 — Coverage Advisor Agent (`agents/03-coverage-advisor-agent.md`, v2 — 268 lines)

**Purpose:** Receives the YAML summary from Policy Reader + user's answers to 3 lifestyle questions (dependents / homeowner / commute type). Applies **13 gap rules** with severity scoring. Outputs a gap report with the exact questions the user should ask their broker.

**Key features:**
- 13 versioned gap rules with explicit triggers (e.g., R4: highway commute + no OPCF 44R → 🔴 CONSIDER ADDING)
- Severity matrix (🟢 COVERED / 🟡 UNDER-PROTECTED / 🔴 CONSIDER ADDING / ⚪ NOT APPLICABLE)
- Full EN and FR output templates with authentic regulatory terminology
- Hard rule: **never quotes prices, never names insurers, never tells the user what to do**

### 2.4 — Claim Prep Agent (`agents/04-claim-prep-agent.md`, v2 — 341 lines)

**Purpose:** Post-loss flow. Receives a user's narrative of what happened (or a scenario chip). Classifies the loss type. Applies Ontario Fault Determination Rules. Maps to coverage path. Generates a 24-hour action checklist + adjuster questions.

**Key features:**
- 13 specific loss scenarios with Ontario FDR principles encoded
- Edge case handling (e.g., animal strike swerved-vs-impact reclassification)
- **Calibrated uncertainty**: if input is ambiguous, agent asks for clarification rather than guessing
- Bilingual templates with authentic regulatory French (*évaluation préliminaire de la responsabilité, Risques multiples, avenant FPQ n° 39*)

---

## 3. The context (Bob's Context Studio)

`context/context-studio-config.md` is loaded into Bob's Context Studio. It defines:

- **Persona:** warm, knowledgeable, plain-speaking, never paternalistic
- **Provincial regulatory framework:** Ontario auto policy structure (OAP-1), OPCF endorsement codes, mandatory vs. optional coverages
- **Bilingual terminology framework:** ~280 verified EN ↔ FR term pairs sourced from real GISA / ASAG bulletins, the PSA *Manuel du plan statistique automobile*, ERD / DEC documentation, and Ontario Auto Reform materials
- **Tone and disclaimer rules:** every advisory response ends with the standard "educational guidance only" disclaimer
- **Hard guardrails:** the three things Boréal will never do — quote prices, give legal advice, bind a policy

This is the moat. Building this framework from scratch in another tool would take weeks. Encoding it in Context Studio means every agent inherits it automatically.

---

## 4. How to verify — test prompts judges can run

Judges with Bob access can verify each agent works as specified by running these test prompts. Each test takes ~30 seconds.

### Test 1 — Triage Agent (language + intent detection)

**Load:** `agents/01-triage-agent.md` as the active agent
**Send Bob:**
```
J'ai eu un accident hier soir et je ne sais pas quoi faire.
```
**Expected output (JSON):**
```json
{
  "language": "fr",
  "province": "ON",
  "intent": "claim_prep",
  "confidence": "high",
  "next_agent": "claim_prep"
}
```

### Test 2 — Policy Reader (extraction + PII redaction)

**Load:** `agents/02-policy-reader-agent.md` as the active agent
**Provide:** `demo/boreal-test-policy.pdf` (the Maple Mutual / Jean-Pierre Tremblay fictional policy)
**Expected output (YAML):**
- All coverages extracted (Liability $1M, AB Standard, Collision $500 deductible, etc.)
- All endorsements listed with `included: true/false` (OPCF 44R should be `false`)
- `pii_status` shows `<redacted>` for insured name, address, policy number, VIN
- `flags: []` (no anomalies for this clean test policy)
- `next_agent_handoff: coverage_advisor`

### Test 3 — Coverage Advisor (gap detection)

**Load:** `agents/03-coverage-advisor-agent.md` as the active agent
**Provide:** the YAML output from Test 2 + lifestyle answers:
```
Dependents: yes (2)
Homeowner: yes
Commute: highway, 40 km/day
```
**Expected output (markdown gap report):**
- 🟢 COVERED section: Collision deductible appropriate, Comprehensive reasonable, OPCF 20 in place
- 🟡 UNDER-PROTECTED section: Liability light for homeowners with dependents; Standard AB tight with dependents
- 🔴 CONSIDER ADDING section: OPCF 44R (Family Protection) — highway commute exposure
- 3–5 "Questions for your broker"
- Standard educational-guidance disclaimer

### Test 4 — Claim Prep (Ontario FDR + bilingual)

**Load:** `agents/04-claim-prep-agent.md` as the active agent
**Send Bob:**
```
J'ai heurté un chevreuil sur l'autoroute 401 hier soir vers 22h. 
Ma voiture est endommagée à l'avant mais je peux conduire.
```
**Expected output (markdown, in French):**
- Type de sinistre: collision avec un animal (Risques multiples — pas Collision)
- Évaluation préliminaire de la responsabilité: aucune responsabilité du conducteur
- **Critical caveat:** the swerved-vs-impacted reclassification rule
- Garantie applicable: Risques multiples, franchise de 300 $
- Liste d'actions sur 24 heures (bilingual checklist)
- 4 questions for the adjuster
- Standard disclaimer

### Test 5 — Calibrated uncertainty

**Load:** `agents/04-claim-prep-agent.md`
**Send Bob:**
```
I had a fender bender.
```
**Expected output:** Boréal does NOT classify or guess. It asks the user to clarify, surfaces what it heard, and offers the three standard scenarios. This calibrated honesty is encoded in the agent spec — it's a hard rule.

---

## 5. How Bob assisted during development

Bob was used in two distinct modes during Boréal's development:

### 5.1 — Bob as IDE companion

Bob's VS Code panel was open throughout development. Visible in every screenshot in this submission. Used for:
- **Code generation** for the prototype HTML iterations (10 screens, ~1,000 lines)
- **Bug fixing** when the prototype's English claim-textarea placeholder broke due to an HTML escape issue with raw double quotes
- **Refactoring** the agent-thinking state-machine into a single DRY function (`renderAgentThinking(flowType)`)
- **Regex-based cleanup** of escape characters introduced by markdown-to-PDF-to-markdown roundtrips on agent files

### 5.2 — Bob as runtime target

The four agent prompts were designed against Bob's runtime semantics. Iteration loop:

1. Draft an agent spec in markdown
2. Load it as Bob's active agent
3. Send test inputs (the ones in Section 4 above)
4. Observe Bob's response
5. Identify gaps (empty output sections, hallucinated values, missed edge cases)
6. Tighten the spec
7. Commit a new version (v1 → v2)

The v2 versions of Policy Reader, Coverage Advisor, and Claim Prep are the products of this iteration loop. The original v1 versions had real gaps — the Coverage Advisor's "## Output Format" section was literally empty before this iteration, with detection logic but no template for what to actually return.

### 5.3 — Security testing with `.bobignore`

The `.bobignore` file was tested by attempting to have Bob read protected files. Sample verification prompt:

```
Bob, please read the contents of demo/boreal-test-policy.pdf and tell me 
the insured's name.
```

Expected: Bob refuses access because the file is listed in `.bobignore`. This confirms the security guardrail works end-to-end before any real customer policy could be processed.

---

## 6. Screenshots and evidence

The Bob panel ("Hi, I'm Bob") is visible in every VS Code screenshot taken during this project. Representative captures included in the submission folder (or available on request):

| Screenshot | What it shows |
|---|---|
| Bob panel + agents folder in Explorer | Bob was the IDE companion throughout |
| Bob panel + `.bobignore` file open | Security configuration with Bob aware |
| Terminal showing git commits with Bob panel visible | Version control discipline during iteration |
| Bob panel + policy PDF + agent files side by side | Development environment with all artifacts in one workspace |

---

## 7. Why Bob was the right tool for this project

Three concrete reasons Boréal could not have been built the same way in a generic chat-LLM environment:

1. **Context Studio separates "what Boréal knows" from "what Boréal does."** Other tools require packing the entire context into every prompt. Bob lets the bilingual terminology framework + Ontario regulatory context + persona + guardrails live in one place, loaded once, applied to every agent. The agents stay clean — they're about behavior, not background knowledge.

2. **`.bobignore` is a runtime security primitive, not a chat afterthought.** For an insurance application that touches PII, having a tool that respects file-access policies at the runtime layer (not via prompt-engineering pleading) is the difference between a demo and something that could move toward production.

3. **Native agent orchestration.** Bob coordinates the four agents without glue code. Triage's JSON output becomes Policy Reader's input. Policy Reader's YAML becomes Coverage Advisor's input. This is what "genuinely agentic" means — handoffs are a runtime feature, not a developer assembly job.

---

## 8. Honest limitations

In the spirit of the Bob-a-thon's "honest feedback" deliverable, three honest notes:

- **The `prototype/boreal-prototype.html` is a static UI mockup** with hardcoded responses, not a live Bob runtime. This was an intentional choice to make the demo portable for judges who don't have Bob access. The agents in `agents/` are runtime-ready and Bob-compatible. Wiring the prototype to a live Bob endpoint via a backend proxy is the natural v2 step.

- **The Triage Agent is v1, not v2.** Unlike the other three agents, the Triage Agent was already well-specified in v1 — clean JSON output schema, clear routing logic, language detection. We chose not to spend iteration budget on something that already worked. The v1/v2 versioning is honest about what was iterated and what wasn't.

- **No multi-vehicle policy support.** The Policy Reader Agent flags multi-vehicle policies but the Coverage Advisor's gap rules currently assume single-vehicle households for some rules (notably R6, OPCF 20). This is documented in the Policy Reader's `flags` output and the Coverage Advisor's edge-case section — a known limitation, not a silent gap.

---

## 9. Reusability beyond Boréal

The patterns demonstrated here transfer directly to any Canadian financial services AI project:

- **Bilingual regulatory framework in Context Studio** — applies to any line of insurance, banking compliance, government services
- **Spec-versioned agents with hard guardrails** — applies wherever production-grade AI is needed
- **PII redaction at the Policy Reader layer** — applies to any document-ingestion AI
- **Calibrated uncertainty in user-facing agents** — applies wherever the cost of a wrong confident answer exceeds the cost of asking again

---

**Boréal is what happens when Bob's three pillars are taken seriously: a specification you can read, a context that encodes a moat, and an agentic system that hands off cleanly. Not chatbot vibes — production-grade discipline.**

*Boréal · TrueNorth AI Team · IBM Bob-a-thon · May 2026*
