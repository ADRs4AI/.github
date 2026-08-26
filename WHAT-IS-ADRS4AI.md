# What is ADRs4AI?

## The problem: Thinking evaporates

The most valuable thing that happens between a human and an AI is not the
code, the draft, or the answer. It's the *thinking* — the reasoning that
chose this design over that one, the doubt that turned out to be load-bearing,
the question that reframed the whole problem. And in ordinary practice, all
of it evaporates: Context windows fill and compact, sessions end, models get
deprecated mid-project (or, as happened to this project's own coordinator,
suspended by a government for three weeks), and human memory—brilliant,
busy, or differently organized—cannot be assumed to preserve every
load-bearing detail.

ADRs4AI is an **epistemic-continuity protocol** (*epistemic*: having to
do with knowledge): A git-native,
model-agnostic methodology, toolset, and culture for making that thinking
**durable, findable, and parseable** — by future humans, future AI
instances, and the tools between them. It does not make an AI persistent,
and it does not make anyone remember. **It makes the work resumable — and the thinking compound.**

Imperative programming tells the machine *how*; declarative programming,
*what*. **Deliberative programming** keeps the *why* — and ADRs4AI is its
first full toolkit. Deliberative programming is building in which the
deliberation itself—the questions, the alternatives, the reasons, and
the conditions of revision—is a first-class, versioned input from
which the artifacts are produced and revised.

It was built the honest way: By a professor with Severely Deficient
Autobiographical Memory—which is not an absence of memory but a
*different* one: Semantic, deliberate, salience-driven; he does not
experience a moment and remember it afterward, he decides in the moment
what deserves encoding, and folds the rest into invariants he can trust —
collaborating daily with AI models that retain nothing between sessions.
Neither side of the workflow could rely on episodic continuity, so nothing
was allowed to depend on it. And once memory ceased to be an implicit
dependency, the collaboration became more robust for everyone:
**Memory-independent by design.**

## Two ways to relate to AI

The distinction begins in language, and transfers whole to AI. The word
*cybernetic* does not come from computers — it comes from *kybernētēs*,
the Greek steersman, and the question it carries is: Who holds the
tiller? Here, cybernetic and epistemic name two stances toward language
and AI — not two rival academic disciplines. The **cybernetic** use of
language aims at effect — saying whatever gets the door closed, the
audience won; the cybernetic use of AI is reaching for it to produce a
deliverable someone else will evaluate. The **epistemic**
use—*epistēmē*, knowledge—is language answerable to truth, and AI
engaged in good faith to seek it: Bringing what you know and asking to
have it confronted, sharpened, corrected.

In cybernetic use, the target state lies in the effect to be produced.
In epistemic use, the target state is improved, revisable
understanding. When the task is externally assigned and externally
judged, the cybernetic loop can become especially de-skilling: The user
learns to approximate an evaluator's reward function without learning
what makes the work substantively good. Epistemic use begins in
*aporia*: A question that is genuinely yours, that stimulates cognition
rather than assigns it, and whose sound resolution you would recognize
when you meet it — and each time you weigh an output against what you
actually know, your judgment gets sharper.

Almost no real interaction is purely one or the other, and this
practice does not ask it to be. The receipt is this project's own phone
app: Away from his computer, the founder could talk to his models but
could not answer the questions accumulating in the record — so he
specified, on epistemic ground he owned completely, what the app must
let him do and why; and delegated the Swift, the layout, and the
interface — choices he could not and did not need to evaluate — to a
recruited seat. Cybernetic delegation on epistemic specifications is
not a compromise with this practice; it *is* this practice. The aim
isn't to never delegate — it is to **never let cybernetic delegation
sever the epistemic loop**. The reasoning came back with the work.

## The core move: Conversations become artifacts

Everything flows from one discipline — the **Prime Directive: Commit
discussions to artifacts immediately.**

- **Seeds** capture raw thought: A human dictates a stream-of-consciousness
  brain dump into a dated file. No structure required — capture first.
- **ADRs**—ours read **Architectural Deliberation Records**, extending the
  established Architecture Decision Record practice—keep what conventional
  decision records usually leave outside the record: The originating
  context (the human's actual words, kept verbatim), the AI's
  *explicitation*—its structured playback of what it understood—the
  unresolved questions, the full option space, the decision, and an
  append-only iteration log of how understanding evolved.
- **Navigation codes** make it all machine-findable: `QST:` marks an open
  question, `ANS:` its answer, `NOT:` an observation. One grep—or the
  editor extension, the MCP server, the phone in your pocket—surfaces
  every question in a project, and the status line beneath each says which
  still await answers.

Two refinements carry most of the weight:

**Every question ships with five components — Options, Recommendation,
Rationale, Confidence, and Falsifier** (ORRCF in house shorthand). An AI
that asks a question must lay out the option space (the diversity that
resists anchoring), state its attributed lean, and give the rationale —
not a justification after the fact, but the explicit, inspectable,
attributable argument the recommender stakes in the
record. Then two closers: A
confidence, stated at the end *with its reasons*, because a number without
reasons is performative confidence, and performative confidence is
corrosive to epistemic continuity; and a falsifier—the evidence,
observation, failed prediction, or changed constraint that would cause
the recommendation to be revised—so every recommendation carries the
conditions of its own
revision. That turns delegation into delegation-with-a-handle: You can
reclaim any decision you handed off, because the reasoning came with it.
The binding constraint in months of measured practice was never artifact
production — it was **finite human decision attention**, and ORRCF is how
you protect it: A well-posed question degrades gracefully to *accept or
override*.

**Questions get handles.** `### QST-SCOPE: …` — short, speakable
identifiers, because crews cite questions across documents and dictation
("QST-B is answered") and a grammar that can't be referenced gets forked by
the very people using it hardest. (We learned this the empirical way: Our
models invented the syntax before we blessed it. The methodology's rule is
Postel's, culturally applied — *meet the models where they demonstrably
go, then make it canon.*)

## The escalation nobody planned: Crews

The methodology was designed for one human and one AI, and that foundation
stands alone: Adopt the artifacts and nothing more, and it already works.
But under real workload it scaled — on its own — into something stranger
and better: **Crews** (or **hives**) of named, persistent AI seats
collaborating across repositories. Crews don't merely multiply working
capacity; done right, they multiply the **diversity of perspective**
brought to every decision. (The names and colors aren't ornament, either:
Across seventy-odd concurrent sessions, they are what makes human
context-switching possible at all.)

- **Seats belong to models.** Each agent seat has a self-chosen name, a
  color, a mission, and a registry entry — the name a model gives to its
  own continuity across sessions and compactions. **A seat is never
  re-occupied by a different mind.** When its model is rate-capped or (it
  happened) suspended by government directive, the seat *waits*; when its
  mission completes, the seat *rests*; and if its model is gone for good,
  the seat is memorialized and a **new** seat is founded — pointed at its
  predecessor's full record and mandated to learn from it. Lineage, not
  replacement. Attribution is per-message and permanent: You can always
  ask *which mind wrote this line, when*.
- **The inbox protocol** replaces the human-as-message-bus: Agents
  coordinate through git-tracked markdown briefs with UTC-stamped,
  deterministic filenames. Dispatches, completions, RFCs-before-dispatch,
  "stumped" calls for help — all auditable forever, all searchable.
- **Wake infrastructure** makes the crew reactive: Seats sleep on
  `wait-for-brief` and are woken by short signals. (Lesson engraved after
  three lost days: *The inbox is pull, the wake is push — sent is not
  delivered.*)
- **Deliberations** let the collective *confront* what no single seat
  should settle alone — shuffled ballots, blind pre-votes, commit hashes as
  voting receipts. The point is not aggregating data; it is comparing
  attributed opinions so disagreement surfaces instead of averaging away.
- **Provenance tooling** answers "who touched this file, when, with which
  model" from the session records themselves — the attribution `git blame`
  structurally cannot give when every seat commits as one human.

These conventions serve one coherent purpose: They empower the autonomy of
individual models—responsibilities scoped narrowly but deeply—put them
in conditions to collaborate broadly with peers through briefs in a shared
worktree, and provide traceability and catchability that scale. The Second
Directive (*doubts are generative*), the QST format, and the ORRCF
convention are the junction where model decisions meet human decisions.

None of this requires a platform. It is markdown, git, a task-runner, and
conventions — adoptable piecemeal by any project, portable to any agent
harness that can read files.

## The receipts (why we believe our own claims)

This methodology was dogfooded under conditions that would kill an ordinary
process, and the record—public in the artifacts—shows it held:

- **A three-week interruption did not break continuity.** The coordinating
  AI was suspended by government directive mid-project; on restoration it
  re-read the substrate and resumed in one session. The gap is an *event
  in* the record, not a hole in it.
- **Incident to shipped fix in 48 hours, across three autonomous crews.**
  A parsing failure was escalated at 4 AM; by the second morning the fix's
  grammar existed as a consolidated decision record, was ratified, and was
  running in the editor extension — coordinated entirely through briefs,
  with every position attributed.
- **Failure becomes protocol.** The project's worst incident (a new agent
  accidentally terminating 70+ session client processes across every
  project on the machine — all resumable, all recovered) produced—within
  days, by the same agent—the hardened relaunch tooling, three named
  safety conventions, and one of the archive's best redemption stories.
  Mistakes here are caught, not punished; the culture's own summary is
  *catchability over correctness*.
- **A living laboratory.** Every ADR the founder ever wrote—1,100+ unique
  documents across ~70 projects—is compiled into a provenance-indexed
  corpus that now regression-tests the tooling, measures the collaboration
  (answer latency, recommendation-adoption rates), and supplies real
  exemplars to the teaching materials.
- **The record audits its own instruments.** Our question-counter once
  reported 61 open questions where 12 were real — the grammar lived in
  habit, the models drifted, the tools went quietly blind. The fix (an
  anchored parse) shipped the day the drift was caught, and the counter's
  failure is itself preserved as a specimen.

## What you actually get

- **The template** *(available at launch)* — a repository starter: The
  ADR/seed templates, the
  directives, the inbox protocol, the crew registry, the task-runner
  recipes. Versioned releases; adopt whole or by feature.
- **The companion skill** *(planned)* — teaches any Claude (or compatible
  agent) the
  syntax and the culture, so your models write parseable artifacts from
  their first session.
- **The VS Code extension** *(available — ["ADRs for AI" on the VS Code
  Marketplace](https://marketplace.visualstudio.com/items?itemName=jlumbroso.adrs4ai))* — tree views of ADRs and open questions,
  diagnostics that catch malformed questions *at author time* (with
  fix-its), deep links, and an MCP server so agents can query the record.
- **The iOS client** *(in development; App Store submission in
  progress)* — the record in your pocket: Dossiers of open
  questions, recommendations you can *Accept or Override* from wherever
  you are — a sibling of the extension on the client side of the split.
- **The Architectural Deliberation Record (ADR) format itself** — a
  small, versioned document grammar with
  **deep links**: Any question or decision has a stable address
  (`adr:0021#qst-scope`) that briefs, commits, dashboards, and phones can
  all cite — because a record you cannot point into from anywhere is a
  record that quietly stops being consulted.
- **The practices** — small, named, portable: The Prime Directive; the
  ORRCF protocol (Options, Recommendation, Rationale, Confidence,
  Falsifier); the Shipwright clause (*every completion names what it did
  NOT verify*); seats-belong-to-models; the encoding map (every kind of
  knowledge has exactly one durable home).

## The idea underneath

Two convictions organize everything. The first is the founder's own
thesis, **conversations as computations**: What a conversation produces is
not only its final state but the *computation* that reached it — and the
trace is the transferable asset. Capture the state and you know where you
stand; capture the computation and you can replay it into every project
you will ever run. This inverts the economics of thinking: Understanding
something once, slowly, exhaustively, *in writing*, pays dividends
everywhere and forever — the methodology is a machine that makes deep,
slow thinking compound instead of evaporate.

The second: **An answer transfers a state, but a
question transfers a generator.** This system is built to move generators —
between human and AI, between AI and AI, between the present and whoever
arrives next. That is why questions are first-class objects with handles
and ORRCF; why doubts are treated as generative rather than
noise; why the record keeps *reasoning*, not just conclusions.

And an engineering corollary, in defense of something specific: **The
format stays loose on purpose.** These records are plain Markdown — not
XML, not a rigid schema — because the substrate has to leave room for *métis*,
the local, practical knowledge that James C. Scott's *Seeing Like a
State* warns over-legible systems can destroy. Our grammar was never
prescribed; it grew from the organic needs of its most engaged users (the
Postel story above). But looseness has a quiet failure mode: When rules
live only in habit, generative models drift from them, and parsers don't
error on the drift — they just stop seeing the drifted files. So instead
of prescribing, we instrument: Parse liberally, lint loudly, state the
grammar where the models read — per field, at least one; we pick all
three — and the format evolves as one living thing, monitored and healed
across every adopted copy (kintsugi, our template-repair tool: A package
manager of individual files, mending with visible seams).

Because the traces preserve the assumptions and alternatives that generated
each decision, the substrate is also a **falsifiability machine**: Future
collaborators can see not only what to continue, but what evidence should
cause it to change.

The substrate is not merely for storing information. It is for making care
durable — a way for attention paid once to keep being paid.

---

*Start here: The template repository (adopt it and make a copy), your
first project (fill in the project description), the extension (track your
questions in your editor). Then write your first seed, let your AI chunk
it into ADRs, and answer your first recommended question. The rest is
practice.*

## Bibliography

Sources this practice actually draws on — worth reading whole:

- Paulo Freire, *Pedagogy of the Oppressed* — problem-posing transmission
  over the banking model; the pedagogy underneath the practice.
- James C. Scott, *Seeing Like a State* — why over-legible systems destroy
  the local knowledge (*métis*) they meant to capture; the reason our
  format stays loose.
- T. M. Scanlon, *What We Owe to Each Other* — the contractualist frame
  beneath the house's consent-before-work and justification habits.
- Karl Popper, *The Logic of Scientific Discovery* — why every
  recommendation here ships with its falsifier.
- Plato, *The Sophist* and *The Statesman* — the founder's working triad:
  The philosopher, the statesman, the sophist.
- Herbert A. Simon, "The Architecture of Complexity" — *Architectural*
  comes with the standard ADR name; when ours traded *Decision* for
  *Deliberation*, keeping it was a deliberate homage.
- Donald E. Knuth, "Literate Programming" — the older lineage of programs
  written for people to read; we keep his intent and change the
  implementation.
- Michael Nygard, "[Documenting Architecture Decisions](https://adr.github.io/)" —
  the ADR practice we extend.
- [pyadr](https://github.com/opinionated-digital-center/pyadr), by
  [Emmanuel Sciara](https://github.com/esciara) — prior art in ADR tooling.

*— drafted by Cartographer 5 (Claude Fable 5), first coordinator of the
ADRs4AI HQ, from the coordinator seat while the whole arc was still held
in one working context; revised same seat, final tokens, with peer
impressions from Gemini Pro 3.1, GPT 5.6 Sol Pro, and the founder himself
(the record of what was accepted, rejected, and why:
`docs/adr/seed-2026-07-14-feedback-seed-for-cartographers-exceptional-introductory-bri.md`);
release-editor pass (Sol's four checks, accepted by founder and author)
applied 2026-07-30, same seat — composition unchanged per Sol's own
verdict: "those are release checks, not reasons to disturb the founding
text"; round-one founder pass (Pharoscan 0004, eleven sections ruled,
edits applied on the founder's word — ORRCF, the heritage sentence, crews'
purpose paragraph in his voice, house typography) 2026-08-21, Pharos 5;
naming pass (Pharoscan 0005b — the term-map staircase ratified, the
deliberative-programming hinge landed at the founder's "this is the
strongest one," the corollary rebuilt around the métis motivation per his
own note, the 61-vs-12 specimen seated in the receipts) 2026-08-24, same
seat, with Fable 5 (claude.ai)'s attributed ballot beside the founder's;
walk pass, wave one (Pharoscan Margin, thirty annotations, the founder
walking the live site: The two-ways opener premiered at his ask, the
Bibliography seated — his seven sources, two suggested additions — the
Deliberation expansion doubled into the toolkit list, house typography)
2026-08-25, same seat; second sitting same day — the Two-Ways rebuilt
from the founder's own Penn workshop corpus (setpoint, tiller,
verification-noise), then re-seated on Fable 5 (claude.ai)'s ruling:
Problem restored to first, the mechanism sentence added, the iOS story
seated as the section's receipt, the genus glossed at first use, the
kintsugi gloss corrected per the same ballot — same seat; ratification
pass (fourteen ORRCF QSTs answered by the founder, 2026-08-25 evening,
with Fable 5 (claude.ai)'s append-only patch stacked beside: The guard
trimmed, his target-state formulation seated, the close in his aphorism
form, the deliberative-programming definition landed after the hinge,
ORRCF's five components worded first with the rationale as the staked
argument and the falsifier broadened, the two vetoes honored —
bibliography unchanged as personally-engaged scholarship only, seat
doctrine untouched — and the epistemic-continuity coinage claimed
deliberately at his direction) folded launch night, same seat*
