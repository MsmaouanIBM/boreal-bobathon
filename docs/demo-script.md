# Boréal — Demo Video Script (v2)

**Total runtime:** 4:00
**Format:** Screen recording with voice-over (English narration, French subtitles for the FR demo segment)
**Audience:** Bob-a-thon judging panel (IBM Canada)
**Goal:** Show that Boréal is genuinely agentic, bilingual-native, spec-driven, and demo-ready — using a real test policy (Maple Mutual / Jean-Pierre Tremblay) with **two complete flows** (pre-loss gap analysis + post-loss claim guidance).

---

## Pre-recording setup

Open `prototype/boreal-prototype.html` in Chrome or Edge, full-screen. Have these tabs ready in a second window for context cutaways:

1. `agents/02-policy-reader-agent.md` (line 1 — show the v2 header)
2. `agents/03-coverage-advisor-agent.md` (line 1)
3. `agents/04-claim-prep-agent.md` (line 1)
4. `context/context-studio-config.md` (the bilingual terminology table)
5. `demo/boreal-test-policy.pdf` (the fictional Maple Mutual policy, page 3 — OPCF schedule)

Record at **1080p minimum**. Voice-over recorded separately and synced in post.

---

## Scene-by-scene breakdown

| Scene | Timing | Duration | On-screen | Voice-over |
|---|---|---|---|---|
| 1 | 0:00–0:25 | 25s | Home screen | The hook |
| 2 | 0:25–1:00 | 35s | Upload → agents → policy summary | Policy Reader in action |
| 3 | 1:00–1:50 | 50s | 3 lifestyle Qs → gap report | Coverage Advisor |
| 4 | 1:50–2:30 | 40s | Home → claim entry → deer scenario | Claim Prep — the differentiator |
| 5 | 2:30–3:00 | 30s | Claim guidance, fault caveat, checklist | Calibrated AI |
| 6 | 3:00–3:25 | 25s | Toggle FR, same gap report rendered | Bilingual moat |
| 7 | 3:25–3:50 | 25s | Cutaway: agent specs + context config | Bob's three pillars |
| 8 | 3:50–4:00 | 10s | Logo + tagline | Vision close |

---

## SCENE 1 — Hook (0:00–0:25)

**On screen:** Browser opens to `boreal-prototype.html`. Home screen shows: 🌲 logo, "Boréal" wordmark, tagline *"Your policy. Your gaps. Your claim. In both official languages."* Two cards visible: *Review my policy* and *I just had an accident*.

**Voice-over:**
> "Insurance in Canada has a clarity problem. The average homeowner spends forty-five minutes with their policy and still can't answer one question: *am I actually covered?*
>
> And if you read insurance in French — about a third of Canadians do — the problem multiplies. Most AI tools translate badly. Industry terminology gets lost.
>
> Boréal is a bilingual AI insurance advisor, built natively on IBM Bob. It does two things: it reads your policy and flags your gaps — and when something goes wrong, it tells you what to do."

**Cursor action:** Hover on the *Review my policy* card at 0:23. Tagline visible the entire time.

---

## SCENE 2 — Policy Reader in action (0:25–1:00)

**On screen:**
- Click *Review my policy* → upload screen
- Click *Use the sample policy →* → file preview shows `boreal-test-policy.pdf · 8.7 KB · 3 pages · Ready to analyze`
- Click *Analyze my policy →* → agent thinking screen runs through:
  - ✓ Triage Agent: Ontario, English
  - ✓ Policy Reader Agent: 3 pages parsed · PII redacted
  - ✓ Ready for analysis
- Arrives at Policy at a Glance screen showing Maple Mutual / Jean-Pierre Tremblay

**Voice-over:**
> "I'll upload a sample Ontario auto policy — fictional insured Jean-Pierre Tremblay, Maple Mutual Insurance.
>
> Behind the scenes, the Triage Agent detects the province and language. The Policy Reader Agent extracts coverages — and notice this: *PII redacted.* The agent strips the policyholder's name, address, and VIN before analysis. That's a Boréal hard rule encoded in the agent spec.
>
> In about three seconds, we have a structured coverage summary: one million in liability, Standard accident benefits, Collision with a five-hundred-dollar deductible, OPCF 20 and 39 included, OPCF 44R *not selected*."

**Cursor action:** At 0:55, hover on the red "**No**" next to OPCF 44R (Family Protection) — this is the gap that drives Scene 3.

---

## SCENE 3 — Coverage Advisor (1:00–1:50)

**On screen:**
- Click *Check my coverage gaps →* → 3 lifestyle questions in sequence
- Q1 *Dependents?* → Yes
- Q2 *Homeowner?* → Yes
- Q3 *Commute?* → Highway
- Arrives at three-column gap report: 🟢 COVERED / 🟡 UNDER-PROTECTED / 🔴 CONSIDER ADDING

**Voice-over:**
> "Three lifestyle questions — three taps. Jean-Pierre has two dependents, owns his home, and commutes forty kilometres on the highway.
>
> The Coverage Advisor Agent applies thirteen gap rules against his policy. Look at the result.
>
> **Green** — Collision deductible is appropriate. Comprehensive is reasonable. OPCF 20 is in place.
>
> **Yellow** — Liability of one million is light for a homeowner with dependents. Most Ontario advisors recommend two million. And Standard Accident Benefits cap income replacement at four hundred a week — with two dependents that's tight; Enhanced AB raises it.
>
> **Red** — OPCF 44R, Family Protection. Highway commuters are exposed to underinsured drivers. This is the single most common endorsement gap in Ontario.
>
> And notice — Boréal doesn't tell Jean-Pierre what to buy. It gives him the exact questions to ask his broker. *'Can we raise liability to two million?'* That's a Boréal hard guardrail: educational guidance only, never quoting, never binding."

**Cursor action:** At 1:40, hover slowly over the italicized "Question for your broker" lines in each card.

---

## SCENE 4 — Claim Prep, the differentiator (1:50–2:30)

**On screen:**
- Click the 🌲 Boréal logo (top-left) → home
- Click *I just had an accident*
- Claim intake screen with textarea + 3 scenario chips
- Click *I hit a deer on the highway* chip
- Agent thinking runs:
  - ✓ Triage Agent: Animal strike, English, Ontario
  - ✓ Claim Prep Agent: applying Ontario FDR principles
  - ✓ Building your action checklist

**Voice-over:**
> "Now the other half. Most insurance AI demos stop at *here's a summary of your policy.* Boréal goes further — to the moment that actually matters: when something goes wrong.
>
> Let's say Jean-Pierre hit a deer on the highway. Stressed, late at night, doesn't know what to do.
>
> He picks the scenario. The Triage Agent classifies the loss as an animal strike, not a collision — that distinction matters legally. The Claim Prep Agent applies Ontario's Fault Determination Rules."

---

## SCENE 5 — Calibrated AI (2:30–3:00)

**On screen:** Claim Guidance screen renders, scroll slowly through:
- *What I'm understanding* → Animal strike
- *Preliminary fault assessment* (orange-bordered card)
- The CRITICAL CAVEAT box (red/orange highlight) about swerving
- *Which coverage likely applies* → Comprehensive
- *Your next 24 hours* checklist with the orange warning item

**Voice-over:**
> "Here's what most demos can't do: *calibrated honesty.*
>
> Boréal correctly tells Jean-Pierre an animal strike is a *Comprehensive* claim, not Collision — different deductible, different premium impact.
>
> But look at this caveat. *If you swerved and hit something else instead of the deer, insurers reclassify the whole claim as a Collision — and you may be at fault.* That's a real Ontario adjuster rule. It's the kind of thing only someone inside the regulatory world would think to flag.
>
> Then a complete twenty-four-hour checklist: photograph the scene with the kilometre marker, don't approach the animal, *be precise with your insurer about whether you impacted or swerved.* And four smart questions for his adjuster.
>
> If Jean-Pierre's description had been ambiguous — say, just *'I had a fender bender'* — Boréal would *not* guess. It would ask him to clarify. That's calibrated AI, encoded in the Claim Prep Agent's spec."

**Cursor action:** Pause briefly on the orange CRITICAL CAVEAT box at 2:42. Scroll continues at 2:50.

---

## SCENE 6 — Bilingual flip (3:00–3:25)

**On screen:**
- Click the **FR** toggle in the header
- Same Claim Guidance screen instantly re-renders in French
- *Vos conseils Boréal pour la réclamation*
- *Évaluation préliminaire de la responsabilité*
- Slow scroll through showing the same caveat in authentic regulatory French
- *Quelle garantie s'applique probablement* → Risques multiples (avenant FPQ n° 39)

**Voice-over:**
> "One toggle.
>
> *Évaluation préliminaire de la responsabilité. Risques multiples. Avenant FPQ numéro trente-neuf.*
>
> This isn't Google Translate. It's authentic Canadian regulatory French — the same terminology used in the *Manuel du plan statistique automobile*, in *GISA / ASAG bulletins*, in actual Ontario insurance documents. Two hundred and eighty verified term pairs. That terminology framework is hard-coded into Boréal's Context Studio.
>
> That's the moat. Building this in any other language would take a team months."

---

## SCENE 7 — Bob's three pillars (3:25–3:50)

**On screen:** Quick cutaway montage:
- VS Code: `agents/04-claim-prep-agent.md` — header showing v2, 341 lines
- Pan to `context/context-studio-config.md` — bilingual terminology table
- Pan to file tree: `agents/` folder with all four agent files
- Return to prototype home screen

**Voice-over:**
> "Boréal maps to Bob's three pillars.
>
> **Spec-driven**: every agent has a versioned system prompt — role, inputs, outputs, hard rules, edge cases. Nothing improvised.
>
> **Context Studio**: provincial regulations, bilingual terminology, tone rules, hard guardrails — *no pricing, no legal advice, no policy binding* — all loaded as context.
>
> **Genuinely agentic**: four coordinated agents. Triage routes by language and intent. Policy Reader extracts and redacts. Coverage Advisor scores gaps. Claim Prep guides post-loss. Real handoffs. Structured outputs."

---

## SCENE 8 — Vision close (3:50–4:00)

**On screen:** Home screen, 🌲 logo centered. Tagline visible: *"Your policy. Your gaps. Your claim. In both official languages."* Header reads *Built on IBM Bob · TrueNorth AI Team.*

**Voice-over:**
> "Built on Bob. Today: Ontario auto. Architecture-ready for every province, every line — home, tenant, life. Like the forest it's named after.
>
> Boréal. By the TrueNorth AI Team."

**Final frame** holds for 2 seconds with the tagline visible before fade-out.

---

## Recording checklist

Before pressing record:
- [ ] Browser zoom at 100% (default)
- [ ] Full-screen, no bookmarks bar
- [ ] Cursor visibility enabled (highlight on click)
- [ ] Tabs prepared in second monitor for cutaways
- [ ] `boreal-test-policy.pdf` open at page 3 (OPCF schedule)
- [ ] EN/FR toggle tested — Boréal v6 prototype confirmed working
- [ ] Microphone tested — voice-over recorded in a separate audio file
- [ ] Stopwatch visible in second monitor to hit the timing marks

After recording:
- [ ] Sync voice-over to screen capture
- [ ] Add subtle lower-third when scenes change (Scene name + agent invoked)
- [ ] French subtitles for Scene 6 (so non-French-speaking judges can follow the bilingual moment)
- [ ] Export to MP4, 1080p, target file size under 100 MB
- [ ] Place final file at `demo/boreal-demo.mp4`

---

## Timing flexibility

If you go long on Scene 5 (the deer caveat is the demo's strongest moment), trim from Scene 7 — the agent file pan is a "nice to have," not the climax. The climax is the bilingual flip in Scene 6 and the caveat in Scene 5.

If you go short and have spare seconds, extend Scene 8 with one extra sentence: *"Built by a Canadian insurance specialist, for the Canadian market that's been waiting for it."*

---

*Demo script v2 — May 15, 2026. Replaces v1 (4-min policy-only flow).*
*Boréal · TrueNorth AI Team · IBM Bob-a-thon submission*
