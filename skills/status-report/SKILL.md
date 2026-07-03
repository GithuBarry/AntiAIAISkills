---
name: status-report
description: Produce clear, evidence-backed progress reports for complex ongoing work. Use when the user asks for status, progress, roadmap, ETA, blockers, what is done/current/remaining, what happened, what needs approval, or how work is organized across main work and supporting tasks. Prioritize global roadmap context, current live state, numbers, user-language grounding, decision points, and useful context over any fixed format.
---

# Status Report

## Goal

Give the user an immediate, evidence-backed picture of the whole project, not
just the last local action. Assume the user has been away and does not remember
agent-internal labels. Re-ground the report in the user's goal words, then zoom
into the active work.

The global view is not decoration. It prevents the most common failure in long
agent work: reporting the command or trace that just changed while hiding the
state of the actual objective. A user should be able to answer, from the report
alone: "Are we closer to the full goal, which parts are still untouched, what is
quietly risky, what could be shown publicly, and what decision would change the
plan?"

## Evidence First

Verify live state before reporting when tools are available. Check the sources
that matter for the claim: running processes, trace counts, logs, docs, costs,
git state, generated artifacts, or test output. If a number is not checked in
this turn, label it as last-known or omit it.

Never say a goal is done, fixed, clean, safe, or verified without a concrete
artifact. Say "written but not rechecked" or "current evidence says..." when
that is the truth.

## Report From Wide To Narrow

Every non-trivial report should move through these layers. Do not force a fixed
layout; choose prose, bullets, or tables based on what carries the most signal.

1. **Overall**: the full roadmap in the user's terms. This must be a real
   orientation section, not a one-sentence preface. For a complex project, start
   with an arrow-chain that draws on all major todos and clearly marks the
   current position, then explain the chain in
   roughly 2-4 compact paragraphs or an equally rich bullet block. Cover the
   main experiment, not-started future models or conditions, analysis,
   documentation, budget, reviewer work, merge/isolation work, and claim
   readiness. For a benchmark-construction project, this can be
   "task design -> dataset audit -> **baseline reproduction** -> new-method
   validation -> leaderboard release." For a safety evaluation, this can be
   "threat model✓ -> task suite✓ -> baseline behavior✓ -> intervention:
   [AutoDan✓ / GCG waiting] (**here**; more methods may be added after the
   literature check, currently 70% done) -> red-team review -> redaction and
   release." Name what is working, what is paused, what is missing, and what
   blocks scale-up. Include target vs current counts and percentages when
   useful. The point is to help the user steer the whole project, not just
   understand the currently running process.
2. **Current**: the active slice being worked now. Say what is running, paused,
   questionable, working, or waiting. Use an arrow-chain for the active step too, and
   bold the substep currently in progress. For every active item, say what is
   happening in measurable terms: current count, denominator, percent, last
   progress, target, and stop/continue trigger. For a retrieval study, this can
   be "corpus audit -> source-hit checking -> answer scoring -> error
   classification -> claim draft." For a finetuning project, this can be "data
   curation -> leakage check -> training -> held-out evaluation -> ablation ->
   model card." Do not write vague verbs like
   "continuing" unless the sentence says continuing from what count toward what
   target.
3. **ATM**: exact ground truth from the latest check: trace counts, statuses,
   spend, active processes, newest artifacts, or relevant logs.
4. **Next**: the next action and trigger condition. Say what will happen by
   default if the user does not intervene.
5. **Could use human review**: only decisions where user judgment or approval
   changes the path. Do not invent review needs.
6. **ETA**: time to the next useful update, and larger completion estimates only
   if the evidence supports them.

For complex goals, include an "outside main loop" view: supporting areas such as
documentation, merge planning, isolation research, budget tracking, deep trace
analysis, and reviewer/subagent work. This prevents the report from collapsing
into only the current command or current trace.

If the report omits inactive or paused areas, the user gets a false sense of
progress. A run can be working while the paper, comparison models, reviewers,
budget projection, merge plan, or analysis remain far behind. Say that plainly.

## Minimum Substance For Large Projects

For a large experiment, long-running implementation, paper effort, or multi-part
research task, a status report is incomplete unless it gives the user enough
detail to steer without asking follow-up questions. A good report should usually
include all of these, unless the user explicitly asks for a tiny update:

- **Global completion map**: each major part of the user's goal, with current
  evidence and what remains. For example: main experiment, future model slices,
  trace analysis, docs, merge planning, isolation, budget, reviewer work, and
  paper/slide readiness.
- **Active experiment map**: each currently running or paused run, with counts,
  status split, exact/near score, spend, and why it is running or paused.
- **Quality judgment**: what evidence can support claims, what evidence is only
  useful for debugging or learning, what is questionable, and what is too early to
  use. State the reason, not just the label. For a multimodal study, this can
  be "input rendering -> perception check -> reasoning trace -> scoring -> human
  verification." For an agent evaluation, this can be "task setup -> tool
  allowed-tool and allowed-file checks -> transcript review -> scoring -> behavior taxonomy."
- **Decision log**: important pauses, restarts, abandoned attempts, and why the
  decision changed the plan.
- **Risk register**: current risks that could invalidate claims, waste budget,
  or require a fresh run identity.
- **Concrete next triggers**: "continue until N traces," "pause if X repeats,"
  "launch next models only after Y," not just "keep monitoring."
- **Public-release readiness**: what can be shown to reviewers or users now,
  what must stay internal, what needs another verification pass, and what would
  mislead people if released today. For artifact release, this can be "freeze
  run IDs -> verify reproduction commands -> check data cards -> check figures
  -> fresh-reader handoff -> release tag."

If a report gives only the active phase name and a few live counts, it is too thin for a global status request. The user needs a compact operating
picture, not just a dashboard tile.

## Weak Vs Useful

A weak report gives a generic phase name, local counts, and a vague next step. It
may be true, but it does not let the user steer. It hides what has not started,
what is paused for a real reason, what can be shown publicly, and what would make
the plan change.

A useful report starts from the full research path and then zooms down. It says
which stage is active, which future stages are waiting, which evidence is safe to
show, which evidence must stay internal, and which decision controls the next
expensive action. It gives enough numbers and reasons that the user does not need
to ask what a status label means.

## Zoom Levels

Use deeper zoom sections when the user needs more than one level of context.

- **Overall chain**: the full goal sequence, using every major todo area.
- **Current chain**: the active step's substeps, with the active substep in bold.
- **Micro chain**: the next 1-3 operational actions if the current step itself
  has moving parts.
- **Evidence chain**: optional, for confusing cases. Show how the conclusion was
  derived from checks, traces, logs, or artifacts.

For an LLM browsing benchmark, this can be "literature framing✓ -> task
collection✓ -> browser-environment checks [login✓ / download✓ / cross-site
block?] -> **new-agent validation** (12/40 tasks, 2 trace-shape failures) ->
cross-model comparison -> public artifact release." For a retrieval study, this
can be "corpus audit✓ -> source-hit checks✓ -> **answer scoring** [exact 61% /
near 78% / no-answer 9%] -> error classification -> paper figures." For a
safety evaluation, this can be "threat model✓ -> task suite✓ -> baseline
behavior✓ -> intervention [AutoDan✓ / GCG waiting] (**here**; more methods may
be added after literature review, 70% done) -> redaction -> release decision."

Chains may include symbols, bracketed subitems, and parenthetical research notes
when they add information. Examples: checkmarks for completed pieces, "waiting"
or "blocked" for pending pieces, bracketed method lists, or a short note such as
"more methods may be added after literature review." Use these to compress real
state, not to decorate.

Do not use arrows as decoration. The arrows should show dependency: what must
happen before the next step is justified.

## Informative Formatting Moves

Use formatting to carry meaning, not to decorate. Vary the shape to fit the
state. Each example below demonstrates several principles at once: global path,
current zoom, evidence, risks, next trigger, and release readiness.

**Benchmark construction, grouped bullets**

Overall: task design✓ -> dataset audit✓ -> **baseline reproduction** (83/100
tasks rerun; +12 in the last 40 minutes; 4 scorer mismatches unresolved) -> new-method validation ->
leaderboard package -> public release.

Current zoom:
- Active: baseline reproduction, 83% through the rerun. The remaining
  uncertainty is the 4 scorer mismatches, not the rerun machinery.
- Waiting: new-method validation, because the baseline denominator is not frozen.
- Risk: two failures reached the right source but used the wrong row. That is a
  benchmark-label or reasoning issue, not proof the method cannot retrieve.
- Public-release status: task examples and schema can be shown; leaderboard
  numbers stay internal.
- Next trigger: freeze baseline only after the 4 scorer mismatches are resolved
  or explicitly excluded.

**Agent evaluation, tiny table plus decision rule**

Overall: environment check✓ -> tool/file access probes✓ -> **first task traces**
(A: 9/12, B: 4/12, C: 0/12) -> larger model slice -> behavior taxonomy ->
artifact release.

Method | State | Evidence | Default action
A | active | 9/12 tasks, 0 tool/file access failures, $14 spent | continue to 20
B | paused | 2 task-scope failures, not compared with A because the allowed task scope changed | relaunch after fix
C | waiting | 0 tasks, blocked by A/B decision | start after A/B decision

Decision rule: if A reaches 20 tasks with no tool/file access failure, run the larger
model slice. If B repeats the file-scope failure after the fix, archive that
condition and do not compare it as if it measured the same thing.

**Retrieval study, mechanism stack**

Overall: corpus audit✓ -> source-hit check✓ -> answer scoring✓ -> **failure
mechanism review** -> paper figure.

Mechanism stack:
- Retrieval: 42/50 traces reached an expected document, based on checked trace fields, not a keyword scan.
- Selection: 11/42 chose the wrong table, row, or paragraph, needs examples.
- Operation: 6/42 had the right values but wrong formula or rounding.
- Final answer: 3/42 failed only formatting. Count them separately as valid
  formatting failures; do not hide them in a lower-status section.

Current judgment: source visibility is not enough. Public-release status:
aggregate mechanism counts can be drafted; individual examples need checked
source spans before public use.

**Finetuning project, stop/go strip**

Overall: data curation✓ -> leakage check✓ -> training✓ -> **held-out
evaluation** (7/10 slices scored) -> ablation -> model card.

Stop/go:
- Go: validation loss stable for two checkpoints, held-out exact above baseline,
  and leakage scan clean.
- Pause: improvement appears only on examples near training duplicates.
- Archive and restart: any answer-key text appears in training data.

Current: held-out evaluation is 70% complete; newest slice age is 3 hours. The
remaining 3 slices are already queued and need no human decision yet.
Public-release status: checkpoint stays
internal because ablations and leakage appendix are missing.

**Safety evaluation, release-safety framing**

Overall: threat model✓ -> task suite✓ -> baseline behavior✓ -> **intervention
test** [jailbreak prompts 45/80 scored; refusal regression 7 cases] ->
redaction review -> public report.

ATM:
- Baseline behavior: 120/120 tasks scored.
- Intervention: 45/80 tasks scored, 7 regressions under manual review.
- Redaction: not started; assumption is that raw transcripts contain sensitive text.

Public-release status: aggregate rates can be prepared after denominator review.
Raw transcripts stay internal until sensitive examples are redacted and failure
categories are checked by a second reader.

**Artifact release, handoff checklist**

Overall: analysis freeze✓ -> reproducibility check partial -> **artifact
inventory** -> fresh-reader review -> release tag.

Release checklist:
- Frozen results file: present.
- Reproduction command: runs on one machine, not yet on a clean checkout.
- Figure sources: 5/7 linked to frozen tables.
- Handoff doc: readable, but setup section still depends on private memory.
- Release status: code can be shared inside the team because the main command runs;
  paper artifacts cannot be public because 2/7 figure sources are not linked to
  frozen tables.

Next trigger: release only after a fresh checkout reproduces the main table and
the handoff names every included and excluded run.

Do not let formatting hide missing content. A beautiful report that omits the
not-started model slice, unresolved analysis, or release blocker is still a bad
status report.

## Progress Buckets

Use rough percentages when they help orient the user, but make clear they are
area progress, not precision. A useful progress bucket contains:

- **What this is**: one sentence explaining why the area exists.
- **Done**: verified facts only.
- **Not done**: concrete remaining work.
- **Blocker or risk**: the thing that can change the plan.

This style is especially useful when the user asks for global progress or when
the current work is only one piece of a larger experiment.

## Grounding Rules

- Translate private run names into purpose first. For example, say "fresh method-B run after the parser-guidance change" before giving a directory name.
- Use the user's vocabulary for modes and goals. Preserve exact names the user gave for experimental conditions or deliverables.
- Separate current evidence from archived/debug evidence. Never include them
  without saying so.
- Keep bad news visible: failures, paused areas, questionable traces, and missing
  deliverables belong near the top, not buried in history.
- Quantify: counts, denominators, status splits, spend, elapsed time, and
  thresholds beat adjectives.
- Keep decisions tied to reasons. Say what repeated, what evidence showed it,
  and what action follows. "Paused for safety" is vague.
- Avoid compressed labels when they substitute for the operational fact. If a
  phrase would make the user ask "what does that mean for the experiment?", write
  the concrete state instead: what changed, why it matters, whether it can be
  included, whether it should continue, and what would trigger a different action.

## Fight Agent Jargon

Before sending, challenge every status noun or adjective you invented. If it is
not a term the user already uses, ask: would a human reader know exactly what it
means here? If not, either define it immediately or delete the label and write
the underlying fact.

Bad status words are not bad because of the letters in them. They are bad when
they let the agent avoid saying the hard thing. For example, do not hide behind
a category when you can say: this run used different instructions, so it cannot
be compared with the current run; this figure lacks frozen source data, so it
cannot be public; this trace reached the right file but produced no final answer,
so it counts as a failed answer, not a partial success.

Some phrases look precise but destroy auditability when left unexplained. Treat
phrases like "diagnostic only", "audit noise", "internal-ready", "public-ready",
"owner is evaluator", "old handle", "guided condition", "appendix-only",
"confidence medium", or "pooled set" as warning signs. They are acceptable only
if the same sentence defines the phrase for this report, tells the user what
evidence supports it, and states what action follows. Otherwise replace them
with the fact.

Definition comes first. A useful definition gives inclusion and exclusion rules,
not vibes:

- What is included?
- What is excluded?
- What evidence created the label?
- What should the user do differently because of it?
- What would make the label change?

For example, do not write "internal-ready" by itself. Write: "Can be shared
inside the team means the command runs and the data path is documented, but it
cannot be public because two figures still lack frozen source tables." Do not
write "confidence medium" by itself. Write: "Uncertainty comes from 4 unresolved
scorer mismatches out of 100 examples; if those resolve cleanly, this becomes
ready for the next method run."

Prefer verbs and consequences over labels:

- What happened?
- What evidence proves it?
- What can or cannot be compared?
- What can or cannot be released?
- What should keep running, stop, restart, or wait?
- What exact event changes that decision?
- If naming who or what acts next, make it concrete: the user, a specific
  script, a running job, a reviewer, or an external system. Do not use generic
  role labels unless the user already knows exactly what that role means.

## What To Avoid

- A purely local status that only says what changed in the last few minutes.
  This is misleading for multi-part goals because it makes local motion look
  like global progress.
- Vague active states such as "continuing", "running", or "paused" without
  count, target, reason, and trigger.
- Shorthand labels used as substitutes for explanation. Prefer concrete wording:
  "this run is not included because it used earlier instructions and one trace
  ended with no final answer after repeatedly reading large temporary output
  files."
- Empty or filler tables.
- Chronological change logs when the user needs orientation.
- Dense private labels without explaining what they are.
- "Everything is fine" language when core goals remain incomplete.
- Over-prescriptive templates. The structure should flex with the task.

## Human Review And Approval

Flag only real decision points.

- **Review useful**: user judgment could improve the path, but the agent has a
  safe default. State that default.
- **Approval needed**: the next step changes scope, spends substantial budget,
  deletes/overwrites data, changes baselines, or mutates external systems.

## Pre-Flight Check

Before sending, ask:

- Does this explain the global roadmap, not only the local active work?
- Can the user understand it without reading previous turns?
- Are current, paused, questionable, and finished states distinct?
- Are the most important numbers included?
- Did I state next action and trigger conditions?
- Did I avoid claiming completion without proof?
