# Theme Preview Roadmap — Technical Operational Dispatcher

**Framework Author**: William Fitzpatrick (*Writer Science*)  
**Source Lecture**: [The Most Powerful Writing Frameworks to Write CLEARLY](https://www.youtube.com/watch?v=cayUBPHB1HQ)  
**Parent Collection**: [Master Collection](../../kirby-fitzpatrick-writers-collection/SKILL.md) | [Global Help](../../../kirby-help/SKILL.md)  

---

## 1. Cognitive Foundation: The Previewed Sequence and the Slot-Allocation Contract

Fitzpatrick's fourth framework, stated plainly: **preview a list, then take it in order.**

It has two halves, and neither survives alone. The preview is a *declaration of cardinality and membership*; the in-order delivery is the *redemption* of that declaration. A writer who previews and then wanders has issued a broken contract; a writer who delivers a clean sequence with no preview has issued no contract at all — and the reader spends working memory reverse-engineering the document's topology instead of absorbing its content.

The cognitive mechanism is **slot allocation**. A reader cannot hold unlabeled novelty. When the fourth paragraph of a migration runbook arrives as a bare fact, the reader must answer three questions before parsing it: *Is this new or a continuation? Where does it sit in the whole? How much is left?* Those questions cost the same attention whether the paragraph is easy or hard. A preview sentence answers all three **once**, up front, and the reader then reads forward with a fixed frame: N slots, one currently open, a known number closed behind.

```text
ANTI-PATTERN — Unannounced Sequence ("Topology Discovery Tax")
────────────────────────────────────────────────────────────────────────
¶1  TOPIC:    The v3 billing migration
    COMMENT:  ... breaks the nightly reconciliation job.
    ✗ no roadmap. Zero slots allocated. Reader holds 1 problem, 0 shape.

¶2  "The schema change adds a nullable tenant_id."      ← novelty, unlabeled
¶3  "A dual-write window covers the transition week."   ← novelty, unlabeled
¶4  "A drain-and-cutover script finishes the move."     ← novelty, unlabeled

Reader model:  3 orphan arrivals. Each one re-opens "how much is left?"
Working memory: spent modeling DOCUMENT SHAPE, not the migration.
Symptoms:       forward skimming, re-reads, "did they cover rollback?"
Review thread:  "Also — what about cutover?" (answered in ¶4, four screens down)
```

```text
PATTERN — Theme Preview Roadmap ("Three Slots, Filled In Order")
────────────────────────────────────────────────────────────────────────
¶1  TOPIC:    The v3 billing migration
    COMMENT:  ... breaks the nightly reconciliation job.
    ROADMAP:  "This migration runs in three stages: the schema change,
               the dual-write window, then the drain-and-cutover."
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
               STRESS POSITION of the intro ¶ → allocates 3 slots

        ┌─────────────────┬──────────────────────┬──────────────────┐
        │ SLOT 1          │ SLOT 2               │ SLOT 3           │
        │ schema change   │ dual-write window    │ drain-and-cutover│
        └────────┬────────┴──────────┬───────────┴────────┬─────────┘
                 ▼                   ▼                    ▼
¶2  "Stage 1 — the schema change adds ..."      → SLOT 1 ✓ CLOSED
¶3  "Stage 2 — the dual-write window ..."       → SLOT 2 ✓ CLOSED
¶4  "Stage 3 — the drain-and-cutover ..."       → SLOT 3 ✓ CLOSED

Reader model:  3 known slots, filled left-to-right. Shape discovery = 0.
Review thread: "Stage 2's window is too long" — a CONTENT objection, not a
               coverage question.
```

The invariant, as an equation:

```text
Preview(A, B, C) ∧ Deliver(A, B, C in order)
   ≡  reader always knows exactly three things:
        (1) what is closed    → A
        (2) what is current   → B
        (3) what remains      → C, one item, bounded
```

Three engineering consequences follow directly:

1. **Bounded suspense.** The reader's "how much is left?" channel is answered at time zero and stays answered. Unbounded prose forces that channel to re-poll at every paragraph boundary.
2. **Interrupts become appointments.** A reviewer's *"what about rollback?"* is a genuine interruption in un-previewed prose. With a roadmap, the answer is *"that's item C, below"* — the question is scheduled, not raised.
3. **Stop-and-resume is cheap.** A reader who abandons an RFC after Stage 1 still holds a correct model of the whole. A reader who abandons un-previewed prose holds a fragment of unknown size.

The failure mode in engineering writing is not a *missing* preview so much as a **misplaced** one: the roadmap appears at the *start* of the intro (delaying the locomotive — see [Locomotive Syntax Engine](../../kirby-fitzpatrick-locomotive-syntax/SKILL.md)), in a *separate* "Overview" section nobody reads, or as a synonym-drifted table of contents whose tokens do not match the headings they point at.

---

## 2. Core Transformation Protocols

### Protocol 1 — The Two-Part Contract (Preview ⇒ In-Order Delivery)
The roadmap is a promise plus its redemption. Ship them as a unit or not at all. A preview that is not delivered in order is **worse than no preview**: the reader has paid the attention cost of slot allocation and then been denied the payoff, so they re-scan the document hunting for the missing slot — the exact tax the preview was meant to remove.

### Protocol 2 — Terminal Roadmap Position (Final Clause of the Intro ¶)
The roadmap lands as the **last sentence of the introductory paragraph**, in the stress position, *after* the topic is established and the destabilizing fact is on the table. Never in the first clause (it delays the subject-verb nexus), never in a detached "Overview" section (readers skip meta-blocks), never at the document end (a summary is not a roadmap).

| Misplaced roadmap | Repaired position |
|---|---|
| `This document has three parts. The migration breaks reconciliation, so...` | `The migration breaks nightly reconciliation. It runs in three stages: schema, dual-write, then cutover.` |
| `## Overview\nThe following sections cover...` | Roadmap clause as the intro paragraph's final sentence; the sections then echo its tokens. |

### Protocol 3 — Cardinal Enumeration with an Exact Count
Name the number and the members in the same breath: *"in three stages: A, B, then C."* Never `several`, `a few`, `various considerations`, `the following topics`. An unquantified preview allocates no slots and provides no closure test — the reader cannot tell whether the document is finished when it stops.

### Protocol 4 — Token Echo (Preview Tokens ⇒ Downstream Labels)
Every previewed member must reappear **verbatim** as a downstream heading, bullet label, PR commit subject, or ticket title. This is the lexical weld that lets a skimming reader (or an LLM agent chunking the document) map roadmap to body without inference.

| Drifted (preview ≠ delivery) | Welded (preview ≡ delivery) |
|---|---|
| Preview: `...the dual-write window...` → Heading: `## Phase 2: Shadow Traffic Migration` | Preview: `...the dual-write window...` → Heading: `## Stage 2 — Dual-write window` |
| Preview: `...three risks...` → Bullets: `[a] contention, [b] lock duration, [c] disk` (count ✓, names ✗) | Preview: `...three risks: lock contention, lock duration, then disk headroom...` → Bullets repeat those three nouns. |

### Protocol 5 — Parallel Form (Countable Grammar)
All members share one syntactic shape — a noun phrase or a gerund, never a mix. Mixed forms break the automatic count: the reader has to *parse* to discover that the third "member" was a clause.

| Un-countable list | Countable roadmap |
|---|---|
| `...three things: the schema change, we also need a dual-write window, and then obviously the cutover has to be drained.` | `...three stages: the schema change, the dual-write window, then the drain-and-cutover.` |

### Protocol 6 — Chunk Ceiling (3 ± 1; Nest Prose Beyond Five)
A roadmap carries **three to five** members. Beyond five, preview the *groups*, deliver the groups, and preview each group's members on entry (two-level roadmap). A twelve-item preview is a table of contents wearing a roadmap's clothes — it allocates slots the reader cannot hold, which is indistinguishable from allocating none.

```text
Two-level roadmap (9 workstreams, 3 phases)
¶1 roadmap:  "The refactor runs in three phases: isolate, migrate, then delete."
¶"Isolate"  : "Isolation covers three modules: auth, billing, then search."
                ^^^^^^^^^^^^ inner roadmap, same contract, smaller scope
```

### Protocol 7 — Ordered-Only Enumeration
Engineering roadmaps carry **sequence semantics**, not bare membership. Use order markers (`first … then … finally`, or explicit stage numbering) rather than a comma-and-`and` list, unless delivery order truly does not matter — in which case say so (`these three are independent; read them in any order`). Silence on ordering forces the reader to infer it, which is the disorientation the roadmap exists to prevent.

### Protocol 8 — Mid-Document Amendment Protocol
Scope changes during review: never silently insert item D between B and C. **Amend the preview in place** and state the amendment — mark the roadmap (and its delivery) as revised, name what was added or dropped, and say why. The roadmap is the document's contract with its reader; a contract amended in one place must stay consistent everywhere it is quoted.

### Protocol 9 — Per-Item Closure Marker
Close each delivered item by naming it again in its final sentence — *"That completes Stage 2"*, *"that is the second risk"*. Without an explicit close, the reader cannot tell whether the next paragraph is a new slot or a continuation of the current one, and the slot bookkeeping collapses back into topology discovery.

### Protocol 10 — Preview Inflation Ban (Promise Only What Ships)
Never preview to signal thoroughness. A roadmap is a **budget**, not a boast: if a member cannot be delivered with real content, cut it from the preview. The professional failure mode of senior engineers is a five-item preview where items 4 and 5 are one-liners — the reader's slot for item 4 was allocated at equal weight and is repaid with a sentence, which reads as padding and devalues items 1–3 retroactively.

### Roadmap Ledger (drafting scaffold)
Draft the roadmap as a ledger before writing prose. Column 3 must be filled with the literal downstream label; column 4 must not be filled until the section exists.

| # | Preview token (as written in ¶1) | Downstream label (verbatim) | Order | Closed by |
|---|---|---|---|---|
| 1 | the schema change | `## Stage 1 — Schema change` | 1st | "Stage 1 ships independently of the window." |
| 2 | the dual-write window | `## Stage 2 — Dual-write window` | 2nd | "Stage 2 ends when the counters match for 24 h." |
| 3 | the drain-and-cutover | `## Stage 3 — Drain and cutover` | 3rd | "Stage 3 reverts with one flag flip." |

**Cold-read test:** read column 2 top-to-bottom. If it does not read as a plausible table of contents for the document you actually wrote, the roadmap is lying.

---

## 3. Engineering Application Scenarios

### 3.1 Code Reviews (multi-issue review threads)
A review comment that lists findings without cardinality and order hands the author a pile: the author must guess priority, guess whether the reviewer is done, and guess which findings depend on which. Preview the count and the review order in the **first** comment, then label every subsequent comment against it.

**Before (unannounced sequence):**
> The inner loop calls `findUser` for every row — that's an N+1. The HTTP client has no timeout. Also the migration is missing an index on `invoices.customer_id`. Should probably add validation on the response object too.

**After (Theme Preview Roadmap):**
> Requesting changes: **four findings, in the order I'd fix them** — first the N+1 in `list_invoices`, then the missing client timeout it exposes, next the missing index on `invoices.customer_id`, and last the unvalidated response object.
>
> **(1/4) N+1 in `list_invoices`.** … **(2/4) Client timeout.** … **(3/4) Missing index.** … **(4/4) Response validation.**

The author now knows the size of the change set, the priority order, and — critically — that the review is *complete* at 4/4. Follow-on discussion ("did you check the other call sites?") lands as a fifth finding appended to a bounded list, not as a suspicion that the reviewer is still reading.

### 3.2 PR Descriptions
The PR body's opening paragraph should end on a roadmap that maps 1:1 onto the commit sequence, so the reviewer can review in the same order the author wrote.

```markdown
Retried webhooks were charging customers twice. This PR fixes that in three
commits: first the idempotency key on charge requests, then the `charge_attempts`
backfill, and finally the removal of the legacy dedupe job.

Review order: 1 → 2 → 3 (each commit is independently revertible).
Rollback order: 3 → 2 → 1.

### 1/3 — Add idempotency keys to charge requests
### 2/3 — Backfill `charge_attempts` from webhook logs
### 3/3 — Delete the legacy dedupe job
```

**Before:** `This PR cleans up billing and adds idempotency. There's a new table, a backfill script, and some index changes. Should be safe.`
**After:** the roadmap above — three commits announced, three commits delivered in the announced order, headers echoing the preview tokens verbatim. Note the *second* roadmap in the same paragraph: rollback order, announced in reverse. Reviewers approve faster when the revert sequence is previewed, because the blast-radius question is answered before it is asked.

### 3.3 Architecture RFCs / ADRs
An RFC's `Context` section is the intro paragraph: it ends on the roadmap. `Decision` and `Consequences` are the slots, delivered in the announced order, with headers echoing the preview tokens. Rejected alternatives get their own preview, so a reader can stop early and still know what was considered.

**Before:**
> **Context.** We store every session in one Redis instance. Failover stalls traffic, and we have EU residency obligations.
> **Decision.** We will shard sessions by region.
> **Alternatives.** We looked at a few options.

**After:**
> **Context.** A single Redis instance holds every session, so a failover stalls all authenticated traffic for 40–90 s, and the keyset cannot be region-scoped against our EU residency obligation. **This decision turns on three constraints, in order of weight: first residency, then keyset size, and finally the failover budget.**
> **Decision.** Because that unshardable, cross-region keyset is the root cause, **sessions are sharded by region** — residency is satisfied by construction, the 12 GB keyset splits into three EU/US-resident partitions, and the failover budget is met because a single region's promotion no longer blocks the others. *(That closes all three constraints announced in Context.)*
> **Alternatives.** **Three were rejected, in order of how close they came:** application-level encryption (residency ✓, latency ✗), a hot/cold keyset split (size ✓, residency ✗), and a session-affinity proxy (budget ✓, size ✗).

A reader who stops after `Context` knows residency, keyset size, and failover budget are the axes of the decision — a correct (if incomplete) model of the RFC. The same reviewer, reading an un-previewed RFC, stops after `Context` knowing only that Redis failover hurts.

---

## 4. Verification Checklist

- [ ] **Preview present and positioned**: does the introductory paragraph *end* on a roadmap clause — after the topic and the destabilizing fact, in the stress position — rather than opening with it, burying it mid-paragraph, or delegating it to a detached "Overview" section?
- [ ] **Cardinality integrity**: is the announced count exact (`three`, not `several`), and does the document deliver exactly that many items — no silent insertions, no dropped members, no eleventh-hour fourth item?
- [ ] **Token echo test**: does every preview token reappear verbatim as a downstream heading, bullet label, or commit subject? Any synonym drift between roadmap and body is a broken link — weld it by renaming one to match the other.
- [ ] **Order and closure**: is delivery strictly in the announced sequence, with each item closed by name at its end (*"that completes Stage 2"*) so the reader's slot bookkeeping never has to guess where one item stopped and the next began?
- [ ] **Chunk ceiling and promise honesty**: does each roadmap carry 3–5 members (nested two-level roadmaps beyond that), is the grammar parallel enough to count at a glance, and does every previewed member ship with real content — no preview inflation, no table-of-contents masquerade?