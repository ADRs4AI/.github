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

ADRs4AI is an **epistemic-continuity protocol**: A git-native,
model-agnostic methodology, toolset, and culture for making that thinking
**durable, findable, and parseable** — by future humans, future AI
instances, and the tools between them. It does not make an AI persistent,
and it does not make anyone remember. **It makes the work resumable — and the thinking compound.**

It was built the honest way: By a professor with Severely Deficient
Autobiographical Memory—which is not an absence of memory but a
*different* one: Semantic, deliberate, salience-driven; he does not
experience a moment and remember it afterward, he decides in the moment
what deserves encoding, and folds the rest into invariants he can trust—
collaborating daily with AI models that retain nothing between sessions.
Neither side of the workflow could rely on episodic continuity, so nothing
was allowed to depend on it. And once memory ceased to be an implicit
dependency, the collaboration became more robust for everyone:
**Memory-independent by design.**

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

**Every question ships with ORRCF — Options, Recommendation, Rationale,
Confidence, Falsifier** (spelled out on purpose; the acronym is house
shorthand). An AI that asks a question must lay out the option space (the
diversity that resists anchoring), state its attributed lean, and give the
rationale — not a justification after the fact, but the actual thinking
trace that connects the options to the lean. Then two closers: A
confidence, stated at the end *with its reasons*, because a number without
reasons is performative confidence, and performative confidence is
corrosive to epistemic continuity; and a falsifier—*what would prove this
wrong*—so every recommendation carries the conditions of its own
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

## What you actually get

- **The template** — a repository starter: The ADR/seed templates, the
  directives, the inbox protocol, the crew registry, the task-runner
  recipes. Versioned releases; adopt whole or by feature.
- **The companion skill** — teaches any Claude (or compatible agent) the
  syntax and the culture, so your models write parseable artifacts from
  their first session.
- **The VS Code extension** — tree views of ADRs and open questions,
  diagnostics that catch malformed questions *at author time* (with
  fix-its), deep links, and an MCP server so agents can query the record.
- **The iOS client** — the record in your pocket: Dossiers of open
  questions, recommendations you can *Accept or Override* from wherever
  you are — a sibling of the extension on the client side of the split.
- **The ADR format itself** — a small, versioned document grammar with
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

And its engineering corollary, learned twice and engraved: **Implicit
grammar + generative models = silent invisibility.** Either parse
liberally, or lint loudly, or state the grammar where the models read —
per field, pick at least one. We pick all three.

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
purpose paragraph in his voice, house typography) 2026-08-21, Pharos 5*
