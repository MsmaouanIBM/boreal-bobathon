# Honest Feedback on Bob Usage

This is my personal reflection, not marketing copy. I'd rather be useful to the Bob team than be polite to it.

— **Mohamed Maouan**, TrueNorth AI Team
*May 2026*

---

## My overall verdict


Bob enabled me, a non-developer business transformation consultant, to ship working code I could not have written alone. The architecture is genuine engineering — but the developer experience has rough edges at predictable moments."*

---

## What worked well

### 1. Bob in VS Code as a constant companion

Bob's panel was visible an easy It became my default "what should I do next?" surface. I never had to switch to a separate AI chat window or copy-paste context across tools.


### 2. Spec-driven workflow with approval gates

The TODO list → approve → diff-by-diff approval workflow was the single feature that let me, as a non-developer, ship real code changes. Every change went through a review gate before being applied. For someone who can't write 200 lines of TypeScript fluently, this was the difference between "I might break the app" and "I can see exactly what changed before saving."


### 3. Context Studio and `.bobignore` (Boréal-specific)

For Boréal, Context Studio is the architectural feature that made the bilingual moat possible. Building 280+ EN/FR regulatory term pairs in a single configuration file — loaded once, applied to every agent — is a fundamentally different workflow than packing context into every prompt.

The `.bobignore` mechanism working as a runtime security primitive (not as prompt-engineering pleading) gave me confidence to handle PII without anxiety.


### 4. Speed — objective measurements

- **Galaxium Mandatory Task:** 21 commits across infant booking, cancellation flow, IBM Carbon re-theme, multiple bug fixes — over a handful of focused sessions
- **Boréal:** ~3,600 lines of agent specs, prototype code, and documentation committed in 8 days
- **Bob session costs:** ~$3.50 across the Mandatory Task — negligible


## What could be improved

###  Misdiagnosis on hard bugs

When the booking 500 error appeared (the `cancelled_at` type mismatch), Bob's first hypothesis was a CORS issue — the symptom looked like it, but the real root cause was a SQLAlchemy schema cache mismatch. It took multiple debug rounds to land on the actual fix (changing the column type and switching to `setattr()`).
---

## How Bob impacted my development speed and quality

### Speed impact

For tasks where I knew clearly what I wanted (e.g., "add infant booking end-to-end with validation"), Bob compressed days of work into a single afternoon session. For tasks where I needed to think (designing Boréal's agent topology), Bob was about as fast as just thinking — but still faster than starting from blank pages.


### Quality impact — where Bob delivered

- The IBM Carbon Design System re-theme: Bob used proper semantic tokens (`support-success`, `support-error`, `support-info`), not just color swaps. This is something I might have done wrong on my own.
- The infant-booking validation logic with proper error responses and a sensible 2:1 infants-per-adult ratio.
- Unit tests added unprompted for the booking-time validation fix.

### Quality impact — where I had to push back

The Coverage Advisor agent v1 had a literally empty "## Output Format" section — detection logic was complete, but there was no template for what to return to the user. Bob can produce specs that look complete at a glance but have hollow spots in the middle. This was caught and fixed in v2, but it's a real failure mode worth flagging.


### Quality of my own work, with Bob

For me as a non-developer business transformation consultant, Bob is closer to 'produces output I couldn't have produced myself' than 'makes me a better developer.' I can read the diffs, understand what changed, and approve or reject. I cannot yet write that code from scratch. Bob is a force multiplier for my domain knowledge, not a teacher — at least at the speed I was working."*

---

## Would I use Bob again?


Yes, for sure. I would use Bob again, and I would recommend it to others. It's a powerful tool that can help you get things done faster and more efficiently."*
---

## Final note


Boréal could not have been built at this quality, by me, in two weeks, without Bob. That's the honest verdict. Everything above is the truthful caveat."*

— Mohamed Maouan, TrueNorth AI Team
