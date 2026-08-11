# Joint Whitepaper Process — OCEANS Sim × AQUASIM

Working process outline (discussion draft) for producing a **joint community whitepaper / roadmap** for maritime robotic simulation, as the shared output of the OCEANS 2026 Sim workshop and AQUASIM v.2 (IROS 2026). 

## How to contribute

This is a living draft. To contribute:

- **Edit or comment directly** in the repo (a wording fix as a pull request; a reaction as an inline comment).
- **Raise a larger objection** — to a principle, a milestone, or the whole structure — as a GitHub issue or in the standing meeting, so it's tracked rather than lost in a thread. The structure here is not settled.
- **Bring project-specific input** (topics, questions, speakers) to the shared planning doc.

## Goal and fixed points

- **Deliverable:** joint whitepaper/roadmap, released to arXiv, with an optional journal submission to follow.
- **Target release:** end of December 2026 — roughly three months after the workshops.
- **Two half-day workshops feed it:**
  - **OCEANS Sim** — Mon 21 Sep 2026, Monterey (~4 hr). Emphasis: higher-TRL, production / community-tested simulators.
  - **AQUASIM v.2** — ~1 Oct 2026, IROS, Pittsburgh (half day). Emphasis: cutting-edge / prototype research simulators.
 

## What the workshops produce

The workshops' objectives are to move the community toward a shared plan. Through focused discussion, project comparison, and prioritization, participants build alignment on the highest-value directions for maritime robotic simulation. The output is a citable roadmap that records those shared priorities and the collaborations formed to act on them.


## Guiding principles

- **Curate enough to move, not enough to pre-decide.** Organizers supply the *vocabulary and the questions*; the *priorities and the roadmap content* are developed by the workshops. 
- **Convergence and commitment.** The room is experts; the highest-value work is to prioritize, decide, and commit. Where the experts genuinely disagree on priorities is the signal to surface and resolve.
- **Discussion-first format.** Minimal lecturing, mostly small-group work against pre-defined topics with key questions, with small groups reporting back to the whole room.
- **Two-layer taxonomy.** A clean *seed* set of topics organizes the sessions; expect the *write-up* to reorganize around whatever cross-cutting problems actually emerge. Design note-taking so that regrouping is possible afterward.
- **Pre-work is decisive.** Each event is only a half day; whatever isn't framed beforehand won't get resolved in the room.
- **Transparent, lead-driven drafting** (MARE model, not the opaque "roadmap synthesis" model): a named lead editor drives, section owners write, the broad group reviews, and every key step is circulated.
- **Speed over polish for v1:** arXiv first (weeks, not the ~year a journal took MARE), refine toward a journal version afterward if we want one.

## Timeline (planned backwards)

| When | Milestone | Owner(s) |
| --- | --- | --- |
| **late Dec 2026** | v1.0 whitepaper posted to arXiv | Lead editor(s) |
| mid-Dec 2026 | Camera-ready circulated to all coauthors; final coherence/voice/length pass | Lead editor(s) |
| late Nov – early Dec | Full draft assembled; cross-section integration and revision | Lead + core |
| Nov 2026 | Section owners draft assigned sections async (2–3 wk); broad review adds/edits | Section owners + broad group |
| mid–late Oct 2026 | Consolidate both workshops' notes → agreed outline → assign section owners | Core group |
| **~1 Oct 2026** | **AQUASIM v.2 workshop** (research / cutting-edge sessions) | AQUASIM organizers |
| 22 Sep – 1 Oct | Harvest OCEANS outputs; brief AQUASIM so it builds on, not repeats | Bridge (Mabel + core) |
| **21 Sep 2026** | **OCEANS Sim workshop** (production / community sessions) | OCEANS organizers |
| Aug – mid-Sep 2026 | Pre-workshop framing: scope doc, seed topics + questions, talk template, governance | Organizing committee |


## Milestone 1 — Pre-workshop framing (now → 21 Sep)

The curation the organizers commit to *before* the room convenes. The question "how far down the definition route do we go?" is answered here.

**We (organizers) curate:**
- A **working definition** and bounding box for "maritime robotic simulation" — the `scope_and_framework.md` draft (definition, the three axes, gates vs. priorities). Offered as a *starting frame to react to*, not a settled position.
- A **seed set of discussion topics** with a few key questions each — scaffolding to organize breakouts. Draw candidates from the capability areas already sketched (multi-domain coverage, fidelity-to-purpose, stack interoperability / shared substrate, extensibility, project health & sustainment, sim-to-real / validation) and the maritime-distinctive requirements (long-endurance / faster-than-real-time, underwater sensing).
- A **common lightning-talk template** (≈5 min, status update per project) with the same per-project questions, so project inputs are comparable.
- The **split of labor** between OCEANS (production) and AQUASIM (research) mapped onto the seed topics, so the two half-days compound.

**We deliberately leave open (for the workshops to develop):**
- The **ranking of priorities** and what the roadmap should push funders toward.
- The **final structure** of the whitepaper (expected to emerge from cross-cutting problems).
- **Contested definitions / scope edges** — surfaced as questions, not resolved by fiat.
- Which projects/approaches matter most — described, not judged, going in.

## Milestone 2 — OCEANS workshop activities (21 Sep)

Proposed format for the **OCEANS** session, adapted from MARE-Madeira and compressed to a half day. (OCEANS proposal only — AQUASIM runs its own agenda and may reuse parts of this, but the two are not formally coupled; they simply share the paper as an output.) 

- **Whole-group opening (short):** scope frame + the seed topics, so everyone is oriented to all of them before splitting. State ground rules so all voices are heard, and that the aim is to prioritize, decide, and commit.
- **Lightning talks:** brief, templated project status updates — context, not the main event.
- **Small-group working sessions** on the seed topics, each with a moderator + scribe and key questions, driving toward *decisions*: the top gaps, how they rank, and where the group disagrees. Then **report-back to the whole room** to converge — or to record the disagreement.
- **Capture discipline:** standardized notes per group, ideally audio + auto-transcript, because the write-up will regroup the raw material later.
- **Close:** each group names the cross-cutting problems and the one or two things the roadmap must say; volunteers self-identify for section authorship.
- **OCEANS → AQUASIM handoff (informal):** in the ~10-day gap, share a short brief of OCEANS outputs (research questions raised, production gaps found) so AQUASIM can build on it if useful — a courtesy, not a dependency.

## Milestone 3 — Post-workshop writing (Oct → Dec)

Adopt the MARE drafting model, transparent and lead-driven:

1. **Consolidate (mid–late Oct):** core group merges both workshops' notes/transcripts into a single problem-oriented map; draft an outline in a shared Google Doc; open inline questions for the broad group.
2. **Assign (late Oct):** 5–8 **section owners** put their names on sections; confirm the lead editor(s) and the broad reviewer list (workshop participants + interested community).
3. **Draft (Nov):** section owners write async over 2–3 weeks; anyone can add ideas or edits; keep it in the open doc.
4. **Integrate (late Nov – early Dec):** lead editor(s) assemble the full draft, revise for one coherent voice and a firm length target, resolve overlaps.
5. **Typeset (early–mid Dec):** convert the agreed draft from the shared Google Doc to LaTeX; circulate formatted proofs to all coauthors.
6. **Camera-ready (mid-Dec):** collect sign-off on the proofs — circulate even a trusted final (MARE best practice).
7. **Release (late Dec):** post v1.0 to arXiv; announce; decide on a follow-on journal version.

## Roles (to fill)

Each role, with how and when it's filled:

- **Lead editor(s)** — drive outline, integration, voice, submission. *Named by the organizing committee at/just after the OCEANS workshop, from the core group.*
- **Core drafting group** — consolidation, outline, cadence. *Self-selected from the organizers now, via the standing meetings.*
- **Section owners** — own and write sections. *Self-identify at each workshop's close (Milestone 2), confirmed during Consolidate (mid–late Oct).*
- **Broad reviewers** — add ideas, review. *Recruited from workshop participants and community sign-ups; set by the end of the workshops.*
- **Per-breakout moderators + scribes** — run and capture the sessions. *Assigned by the organizers as pre-work (Milestone 1), before each workshop.*
- **Bridge/coordinator** — keep OCEANS and AQUASIM aligned. *Mabel, now.*

## Decisions and working stances

These were the open questions; here is where we have landed (adaptable as things evolve):

1. **Paper count.** Aspiration is a single joint paper (avoids reinforcing "fragmentation"); reality may be one or two, and we will adapt.
2. **Audience & framing.** Written as a **community-facing** artifact — deliberately, so funders can pick it up and say "look what the community did." More powerful than addressing funders directly.
3. **Venue.** A journal is the stated goal (aspirational); realistically we will likely release on arXiv.
4. **Lead / governance.** Left intentionally ambiguous for now, to adapt as things evolve.
5. **Comms.** Email (core + broad threads); being set up separately.
6. **Meeting cadence.** Biweekly inter-workshop standing meeting (~4 before OCEANS) — confirmed. 
