# What is being built

Concept-level. Companion to [`REPO-CATALOG.md`](REPO-CATALOG.md), which **measures** the same
work — files, commits, authorship share, test counts. This file deliberately carries none of
that. It says what each thing is *for*, what its parts are, and which decisions were interesting.
If you want the vitals, that is the other file.

---

## Multi-tenant plugin platform

A Go API gateway where client applications are **plugins rather than tenants**: a plugin service
authenticates against the platform, publishes its own route table, and the gateway proxies
matching requests through to it. Routing is read from the database at request time rather than
compiled in, so bringing a new client service online adds rows, not a deploy.

Parts: identity (authentication, OAuth 2.0, client management), coordination (scheduling, config,
health), commerce (plans, subscriptions, invoicing), communications, infrastructure (storage,
cloud adapters), analytics.

- Gates are ordered and **fail closed where it matters**: a plugin with no declared entitlement is
  refused rather than treated as open, and a token minted for one plugin cannot be replayed
  against another.
- The gateway mints a fresh, scoped token per proxied request carrying the caller's resolved
  capabilities downstream — the plugin service never sees the user's own credential.
- Policy-driven RBAC over a database policy store; circuit breakers on the proxy pool.
- **Not wired:** the billing domain is complete — plans, invoices, PDF generation, webhook parsing
  — on top of no payment processor, and several messaging channels register a send route that does
  not send. Said plainly because a complete domain model over a missing dependency reads as
  finished and is not.

## Client applications as plugins

The repeating unit of client work: a public site, plus a plugin service that registers with the
platform. Two SDKs, one Go and one Node, carry the boring half — fetching and refreshing the
plugin token, publishing the route table idempotently, install and uninstall lifecycle hooks, and
the middleware that verifies a request genuinely arrived through the gateway.

The SDK arrived *after* several plugin services already existed, so adoption is partial — the
older services still authenticate with a hand-rolled shared-secret header. Worth knowing because
the presence of a plugin manifest file is not evidence of registration: the same filename holds
two unrelated formats, an endpoint map in the older services and a real manifest in the newer ones.

## Documentation-integrity toolchain

The main line of work, and the most reusable thing here. The problem: across many repositories,
files that must agree — a rule and the code enforcing it, a registry and its reconciler, a résumé
and the repository it describes — stop agreeing **silently**, because nothing declares them coupled.

The tool lets a coupling be declared, then derives drift from file *content* on demand rather than
storing a baseline. Deriving beats remembering: a stored baseline can miss a change that happened
while nothing was watching, and can invent drift when the baseline itself goes bad.

Parts: a CLI; a Claude Code plugin registering session and pre-tool hooks; a set of canonical rule
files with a detector that hunts *restatements* of a rule rather than the rule itself; and three
registries — ports, deployments, databases — each with a reconciler checking the registry against
what is actually on disk.

- **It never edits a downstream file.** It finds and explains, a person approves, and the decision
  is appended to an immutable ledger.
- Hazard documents are pull artifacts — nobody reads one at the moment of risk. So a pre-tool hook
  inspects the literal command about to run and surfaces the matching known hazard before it
  executes. The failure mode being fixed is recognition, not knowledge.
- Every detector and every hazard trigger ships a **selftest asserting it can actually fire**. A
  check that cannot fail reports success forever; the selftest has caught exactly that, including
  on its own first run.

## Vertical CRM and workflow engine

A service business's operations as software: client records, task queues, appointments,
notifications, and a workflow engine whose graphs are edited at runtime, compiled, published by
hash, and executed against timers and tokens.

- Access control is **data, not code** — roles and capabilities live in the database and are
  editable at runtime, with a capability-matrix UI that shows the consequences of a change before
  an atomic save.
- Field-level projection is deny-by-default: a field with no declared tier is never returned by any
  query, so adding a column cannot accidentally expose it.
- The engine cutover deleted two legacy passes only after freezing their outcomes as a golden test
  and proving the new engine equalled them — which surfaced defects that existed *only* because the
  compiled graph had never actually executed.
- **Not throughput:** the background-job registry is real and validated at load, but registers no
  production jobs. Scaffolding.

## Business assessment product

A diagnostic funnel: a business answers a question bank and is scored against a benchmark table, so
the output is a comparison against similar businesses rather than an absolute number.

Two scoring generations run simultaneously behind type guards during migration, because older
scores must stay readable. Fully bilingual, including a renderer that keeps English glossary terms
intact inside translated sentences — matched longest-first with letter-boundary lookarounds so a
term appearing inside a longer word is not mangled. Accessibility is **asserted in the build** —
contrast solved statically from the design tokens, automated WCAG checks per theme and per language
in end-to-end tests — rather than reviewed by eye.

## Demand intelligence

Multi-source ingestion — search console, trends, video, social, first-party bookings — feeding an
LLM classification pipeline and an opportunity score that maps demand against what a practice
actually offers.

Model calls are constrained by enforced response schemas at temperature 0 and cached on first
write, so **determinism rests on the cache rather than on the model**. A keyword classifier stands
behind it, so a provider outage degrades quality instead of stopping ingestion. Model-proposed
sources are existence-checked against the live API before being accepted, and an inconclusive check
returns the candidate flagged rather than asserted either way. Cloud access uses workload identity
federation, adopted to remove service-account key files.

**Weakest layer, named:** scheduling. The pipeline runs; what triggers it has moved between hosted
cron, CI schedules and a local agent, and is the least settled part of the system.

## Deterministic ephemeris service

Astronomical computation where the same inputs must return the same answer *forever*, because
results are persisted and later compared against each other.

Computed bundles are content-addressed by their inputs **and the version of the underlying C
ephemeris library**, and that version is verified at startup with a hard failure in production —
determinism treated as a product property with an enforcement mechanism, rather than an assumption.
Every call into that library is serialised through a single worker, because it carries
process-global mutable state. Caches are invalidated by a fingerprint of the rules that produced
them rather than by a clock. Fully local: the service makes no external calls.

## Trading research infrastructure

A contribution to someone else's trading system; the part built here is the research layer, whose
job is to make a strategy claim falsifiable before capital touches it.

Edges are denominated in basis points so they compare directly against round-trip cost. Hypotheses
are machine-checkable artifacts rather than prose. Datasets carry content checksums. Walk-forward
splits are pure index arithmetic with a mandatory embargo gap. The number of trials is stamped on
every report so multiple-testing correction cannot be skipped. Sweeps report the *size of the
plateau* rather than the peak. And the verdict is a pure function with thresholds passed in, never
derived from the report being judged.

Also built there: a design-drift gate with a ratcheted baseline held at zero, a selftest feeding
every rule an input that must trip it, and canaries so a rule going blind to a renamed token is
caught rather than reported clean.

## Publishing and content pipelines

Sites backed by sync pipelines, where the interesting artifact is the written **field-ownership
contract**: which fields the sync overwrites on every run, which are seeded once and then belong to
an editor, and which key is immutable. Upserts key on the source system's numeric id rather than a
slug, because slugs change.

An AI language classifier was replaced by a Unicode script-share majority test with an explicit
"mixed" outcome and a human queue for the genuinely ambiguous pair — cheaper, deterministic, and
honest about what it cannot decide. Media runs through a three-codec ladder, content-hashed for
immutable caching, with codec strings parsed out of the container's own boxes rather than
hand-written. A document-to-database diff/apply path guards destructive operations with an explicit
allowlist, a percentage-of-collection cap, and an echoed content hash that rejects a stale apply.

## Agent tooling

A habit more than a project: when an agent is in the loop, put the deterministic part in code and
leave the model only what genuinely needs judgement.

The shape is consistent — a small CLI behind a name-to-handler map, an append-only ledger with a
state machine that refuses illegal transitions, and evaluation fixtures captured from real observed
failures rather than invented. **Empty results are attributable:** several distinct causes are
reported separately instead of collapsing into one "nothing found", because an absence that cannot
say why gets acted on as though it were a result. Golden sets are blind-labelled before scoring and
compared by band rather than by exact number.

## Text digitisation

A pipeline turning scanned and heterogeneous sources into a structured, addressable corpus —
normalising several unrelated JSON shapes that share no identifier, and taking chapter numbers from
filenames rather than from array position.

Stated honestly: the corpus is large and translation coverage is still under a fifth of it, and the
pipeline and the corpus live in different repositories. A single "translation pipeline" claim
overstates both.

---

## Recurring positions

Three things that show up in every project above, stated once here instead of eleven times.

**Correctness gates as build steps, not review comments.** Contrast solved statically from tokens;
design-token drift ratcheted against a baseline that only moves down; content sources enforced by
import; a publish command whose *refusal* is the thing CI asserts. The pattern is that the gate
ships with proof it can fail.

**Declared is not built.** Dependencies present in a manifest with zero import sites. A job registry
with no registered jobs. A complete billing domain over no payment processor. Shared libraries
tagged and released with no importers. Found independently in several codebases, so it is recorded
as a class rather than a bug: a manifest, a registry or a version tag is a *claim* about code, and
reading the call sites is the only thing that settles it.

**Human-in-the-loop by construction.** The tools propose, explain and record; a person decides.
Where a tool could act autonomously, it is deliberately built not to.

---

## Corrections this view implies

Recorded, not applied — this pass changed no claim-carrying file.

- The HTML résumé claims WebAuthn passkeys, an OTP fallback and JWT sessions for a codebase where
  all four packages are declared and never imported. The real build is a constant-time password
  check issuing an opaque random token in a TTL collection.
- Three corrections that landed in the HTML résumé never reached the profile README, despite a
  declared edge between them.
- Three different test counts for the ephemeris service across three files in this repository.
- `REPO-CATALOG.md` names clients throughout, and this is a public repository. The résumé was
  de-identified deliberately; the catalog was not.

## Standing rule for this file

**Concept before mechanism, mechanism before number.** If a sentence here opens with a count, it
belongs in `REPO-CATALOG.md` instead. This file should survive a month of commits without becoming
wrong — that is the entire reason it carries no vitals.
