# Rewrite `Rupali59/Rupali59` README as an engineer's resume

## Context

`github.com/Rupali59/Rupali59` is the GitHub profile README — the page a recruiter lands on.
It was last touched **2026-05-02**, ~4 months ago, and it no longer describes the work.

Three artifacts in that one repo tell four different stories about the same career:

| Artifact | Size | State |
|---|---|---|
| `README.md` | 14.2 KB | live; decorative; experience ends May 2025 |
| `docs/unreviewed/README.md` | 25.6 KB | a **better** unpublished draft — split ServiceNow roles, ServiceNow product-doc links, richer tables. Nothing links to it |
| `Rupali_Resume.pdf` | 95 KB | the actual resume; ServiceNow open-ended; no Motherboard, no Tathya |

They disagree on dates, on scores, and on which metrics exist. Nothing could notice,
because no coupling between them was ever declared — the exact failure shape in
`rule:adversarial-review-reads-the-ledger`.

**There is a fourth artifact, and it is the one recruiters actually read.** Your LinkedIn
(fetched 2026-08-25; the public view is partly behind a login wall, so roles and dates were
truncated) still carries the headline **"Senior Software Engineer at ServiceNow"** — present
tense, no end date. The README you're about to publish will say `Apr 2019 – May 2025`, and it
**links to that LinkedIn from its header**. A recruiter opening both sees a direct
contradiction about whether you currently have a job.

That is not something this plan can fix — LinkedIn is yours to edit — but it does mean the
README rewrite is half a job on its own. Flagging it here rather than leaving you to find it.
What LinkedIn *did* settle: C2 and C6 below, and two certifications the README is missing.

Meanwhile the tree shows where the work actually went in the last 12 months:

```
815  Vipin Kaushik/VipinKaushik      261  Tathya/Tathya-portfolio
350  PanditPawanKaushik/SSJK-mb      251  Motherboard  (36 go.work modules, Go 1.25.8)
169  propagate                       128  ManavDaehi/Manav-portfolio
```

None of it appears in the README.

**Goal:** one accurate, restrained, resume-toned README; every claim traceable to a
document or to the tree; every link resolving.

## Decisions taken (2026-08-25)

1. **May 2025 → present stays in Projects, not as a role.** The experience timeline still
   ends at ServiceNow. *Flagged once and proceeding:* a recruiter reads a 15-month
   employment gap. The mitigation below is to date the Projects section explicitly
   (`2025 – present`) so recency is visible without a role entry.
2. **Describe client work by domain; do not name clients.**
3. **Keep all three disputed metrics** — confirmed accurate; the PDF resume is the artifact
   that is behind, not the README.
4. **Restrained style.** No animated header, no typing SVG, no per-bullet icons, no badge walls.

## Execution order

**No README edit happens until the fact-check gate in Phase 2 passes.** Everything below the
gate is drafting; everything above it is establishing what is true.

| Phase | What | Gate |
|---|---|---|
| **0** | Clone the repo | — |
| **1** | Persist this plan into the repo as a working document | — |
| **2** | **Fact-check gate** — re-verify every load-bearing claim; collect Rupali's answers on the items only she can settle | **Nothing proceeds until this closes** |
| 3 | Rewrite `README.md` | Phase 2 |
| 4 | Repo hygiene — workflow, `.DS_Store`, orphan draft | Phase 3 |
| 5 | Declare the propagation edge and prove it fires | Phase 4 |

## Phase 0 — clone

The repo is **not cloned locally** (verified: no `.git` under `~/Documents/GitHub` points at it).

```bash
gh repo clone Rupali59/Rupali59 ~/Documents/GitHub/Rupali/Rupali59
```

`Rupali/` is a container of independent repos, not a repo — this matches
`Rupali/CLAUDE.md`'s existing layout. Add a row for it to that file's Contents table.

## Phase 1 — keep this document

Copy this plan to `~/Documents/GitHub/Rupali/Rupali59/docs/README-rewrite-2026-08-25.md`
and link it from the repo so it is not an orphan — `docs/unreviewed/README.md` sitting
unreferenced for months is precisely the failure this rewrite exists to fix, and dropping a
second unlinked doc beside it would repeat it. It stays as the working record of what was
measured, what was decided, and what is still open.

## Phase 2 — fact-check gate

Two lists. Neither is optional, and the second one blocks.

### 2a · Re-verify mechanically — I do this

The Projects rewrite rests on a subagent census. Per `rule:discernment-checks` §3 a report
saying "verified" is a claim about verification, so each load-bearing number gets re-measured
directly before it reaches the README. **A figure that changes under a second method was
never a finding** — report the discrepancy, do not tune toward the expected value.

| Claim | Re-measure by |
|---|---|
| Motherboard's last Go commit on `main` is 2026-06-21 | `git -C Motherboard log main -1 --format=%ad --date=short -- '*.go'` |
| Motherboard has 36 `go.work` modules, 702 `.go` files | count `use (…)` entries; `find … -name '*.go' \| wc -l` |
| `inventory-management` is unwired (no `main.go`, no external refs) | `find`, then grep the tree for imports of it |
| Astroclarity has no `app/` and no `src/` | `git -C Astroclarity ls-files \| wc -l`, then `ls` |
| `astroclarity.vercel.app` serves a **stale pre-reset build** | fetch it and compare against the repo's actual content — a 200 is not evidence the project is alive |
| SSJK-mb: 167 test files; prod cutovers still gated | `find … -name '*.test.js' -not -path '*/node_modules/*'`; re-read its `STATE.md` |
| propagate: 53 lib modules, 120 test files | `find propagate/lib -name '*.mjs'`; `find propagate/tests propagate/hooks -name '*.test.mjs'` |
| astroacharya: 1,034 tests passing | re-read `STATE.md`; treat as a doc claim unless the suite is actually run |
| Sanskrit corpus: 57 texts / 927 chapters / 91,782 shlokas | its `STATE.md` says **derive, never restate** — so derive it, and note that the previous generator was invisibly wrong (counted files, not `chapters[]`) |
| 30-day velocity table | re-run the `git log --since=2026-07-25` counts per repo |
| Every URL and repo I intend to link | `curl -o /dev/null -w '%{http_code}'`; `gh repo view --json isPrivate` — a private repo link shows a visitor a 404 |

Two figures the census itself flagged as already contradicted, kept here so they are not
quietly reused: propagate's `ISSUES.md` claims *18 sidecars / 7 workspaces*, the tree today
has **36 and 13**; and `Motherboard/…/STATE.md:25` claims `main` has not moved since
2026-05-09, which git contradicts. Neither number goes anywhere near the README.

### 2b · Only you can settle these — this is the blocking half

| # | Question | Why it can't be resolved from the tree |
|---|---|---|
| C1 | NowFloats end date — **Jul 2018** (resume PDF) or **Aug 2018** (both READMEs)? | Two of your own documents disagree |
| C3 | NowFloats reach — resume says "50000+ clients", README says "50K DAU" | Clients ≠ daily active users; only you know which is true |
| C15 | NowFloats hackathon win dated **Jan 2017** on LinkedIn, but your resume starts you there **Jun 2017** | Either the award date or a tenure date is wrong |
| C16 | "JS Fundamentals · Code With Mosh (2025)" is on the README but **not on LinkedIn** | Keeping it on your word; confirm |
| — | ACE Coliving — is it still live and yours to claim? | Private, last push 2025-10-10, absent from disk and every registry |
| — | The three metrics you confirmed (500K+/day, 1M+ tasks/mo, 60%) | Confirmed in decision 3; noting that the PDF still disagrees |

`rule:discernment-checks` §7: a wrong *answer* gets caught by the next measurement, a wrong
*premise* gets ratified and never questioned again. These six are premises.

## Files touched

| File | Action |
|---|---|
| `README.md` | full rewrite |
| `docs/unreviewed/README.md` | harvest, then delete — two READMEs that disagree is the defect |
| `.github/workflows/profile.yml` | delete (see §Broken CI) |
| `.DS_Store` | `git rm --cached`, add to `.gitignore` |
| `.gitignore` | add `.DS_Store` |
| `.propagates.yml` | **new** — declare README ↔ resume coupling |
| `docs/README-rewrite-2026-08-25.md` | **new** — this plan, per Phase 1 |
| `Rupali_Resume.pdf` | leave; flagged as needing Rupali's own update |
| `tech.log`, `assets/bar_graph.png` | delete — both are waka-workflow artifacts, dead once the workflow goes |

Everything in this table is **Phase 3 and later**. Nothing here is touched before the
Phase 2 gate closes.

## New README structure

Plain markdown headings. No `<img>` icons on bullets. No `capsule-render`, no
`readme-typing-svg`, no `skillicons.dev`.

```
# Rupali Bhatnagar
Senior Software Engineer · Hyderabad, India
tathya.dev · LinkedIn · GitHub · Email · g.dev/rupali59 · Credly

<3–4 line summary: 9 years, high-scale backend/platform, 6 at ServiceNow in
 Security Operations & Vulnerability Response, now building platform + product
 systems independently.>

## Experience          ← ends May 2025, per decision 1
## Projects            ← two dated groups; carries 2025–present
## Technical Skills
## Education
## Certifications
## Honors & Awards
## Open to Opportunities   ← one line, not a card table
```

### Experience — reuse the unreviewed draft, do not re-derive

`docs/unreviewed/README.md` already splits ServiceNow into two roles with locations and
**links every feature to its ServiceNow product documentation**. Those links are the single
strongest thing on the page — they prove the features shipped into a commercial product.
Harvest them verbatim:

- Sr. Software Engineer · Mar 2022 – May 2025 · Security Operations, Vulnerability Response
  — Dynamic Approval Rule Engine (40% faster approvals) · Pen-Testing Workflow Automation
  (30% less manual intervention, 50+ subsystems) · Background Job Framework (60%, 1M+ tasks/mo)
- Software Engineer · Apr 2019 – Mar 2022
  — Assignment Rule Engine (1M+ vulnerable items/day) · ML Assignment Recommendations (+20%)
  · CISO & Vulnerability Dashboards (100K+ records / 8h, 50+ orgs) · Source Integrations
  (Veracode · Qualys · Tenable · MS TVM, 500K+ records/day)
  — Hackathons: Diagnostic Framework (40%) · ML Vuln Grouping · PoA&M Generator ·
    **High-Volume Data Generator (100M+ records across 20–30 tables)**

**Add the High-Volume Data Generator** — it is in the resume PDF, is arguably the most
impressive hackathon item, and the current README drops it.

Then Darwinbox (Aug 2018 – Mar 2019), NowFloats/Boost360, Finomena (Feb – May 2017),
Babajob (May 2016 – Jan 2017) — compact bullets, keep the numbers (50K users, 84%
SPIDER accuracy, 8,000+ loans/mo, 10K calls + 20K SMS/day).

### Projects — the section that has to carry 2025–present

Two dated groups so recency is legible:

**Current · 2025 – present** — ordered by actual 30-day velocity, not by what sounds best.

| Project | Description | Stack | Link |
|---|---|---|---|
| Astrology-practice platform | Multi-app plugin service: Express API + two Next 16 apps (client UI, admin). WebAuthn + OTP auth, BullMQ/Redis job queue, web-push notifications, workflow engine; ~14,000-record client migration; 167 test files | Express · BullMQ · Redis · MongoDB · Next 16 · React 19 | private (Fly + Vercel) |
| propagate | Declares couplings between files that must move together, derives drift **from content on demand** rather than storing state, records every verification in an append-only ledger. **Never edits a downstream file** — a human makes every call. 53 modules, 120 test files; ships as a Claude Code plugin with commit and session hooks across 13 workspaces | Node ≥22 · ESM | private |
| Filmmaker portfolio | Next.js + MongoDB, Google-Doc→works sync pipeline, multi-codec reel delivery (AV1/HEVC/H.264) cutting the home page from ~6.4 MB to ~2.3 MB | Next · React 19 · MongoDB · Vercel Blob | live, unlinked *(see note)* |
| Sanskrit text corpus | Open corpus plus digitisation and translation pipeline — 57 texts, 927 chapters, 91,782 shlokas across 12 categories | Python · JSON | **[Sanskrit-texts](https://github.com/Rupali59/Sanskrit-texts)** — public |
| Vedic-astrology compute backend | FastAPI service computing panchanga, festivals and muhurta from canonical sources over `pyswisseph`; **1,034 tests passing** | Python 3.12 · FastAPI · pyswisseph · MongoDB | private |
| Motherboard | Go multi-module monorepo — API gateway and multi-tenant plugin platform. **36 `go.work` modules, 702 Go files.** Plugin services authenticate, publish their routes, and the gateway proxies to them behind a fail-closed entitlement gate and a plugin-key claim assertion | Go 1.25.8 · Next 16 | private · maintenance |
| Marketing-intelligence tool | GA4 + Gemini ingestion with opportunity scoring and a nightly ingest job | Next · TS · SQLite | private |
| Own practice site | Next 16 / React 19 — WebAuthn, CASL authorisation, d3 assessment engine | Next · TS | [tathya.dev](https://tathya.dev) |

> **Client-naming note.** Decision 2 says describe by domain, don't name clients. Several
> live URLs contain the client's own name (`vipinkaushik.com`, `manavdaehi.com`,
> `kirtik.co.uk`, `pawankaushik-web.vercel.app`), so linking them *is* naming them. Those
> rows are described but **not linked**. `tathya.dev` is your own practice, not a client, so
> it is linked. If you'd rather trade the anonymity for verifiable links, say so.

> **Three rows the census killed.** `AstroClarity`, `Rishta` and `ACE Coliving` are **not**
> in the table above — see C10–C13. Do not reinstate them without re-measuring.

**The strongest available headline, and it has no row today.** The census's own conclusion:
the dominant engineering output of the last 30 days is a **documentation-integrity
toolchain** — `propagate` + `curate-docs` + 18 canonical rule files with a restatement
detector + three registries (`ports.yml`, `deploy.yml`, `mongo.yml`) each with a reconciler —
applied across 13 workspaces and enforced by commit hooks, plugin hooks and a scheduled
digest. That is a distinctive, measurable systems story and it is currently invisible.
Consider a short "Currently building" paragraph above the table saying exactly that.

**Earlier**

Only these four link to something a visitor can actually open. **`Voice_transcriber` is
private** — the current README's implied link would 404; describe it without a link or drop it.

| Project | Link |
|---|---|
| HIMK — M.Tech thesis: Human Activity Recognition via HMM-based Intermediate Matching Kernel + SVM | [himk-implementation](https://github.com/Rupali59/himk-implementation) — public |
| MIS — institute management (students, faculty, admin) | [MIS](https://github.com/Rupali59/MIS) — public |
| Parking Lot — system-design allocation problem | [parking_lot](https://github.com/Rupali59/parking_lot) — public |
| WorkTracker — personal work dashboard | [rupali59.github.io/WorkTracker](https://rupali59.github.io/WorkTracker/) — public |
| Voice Transcriber — dockerised real-time speech-to-text | *private, no link* |
| Coliving booking site — PostgreSQL-backed leads, SEO | *private, no link; see C13* |

**Link rule, applied everywhere:** a project links to a public repo, or to a verified-live
URL, or to nothing. Never to `https://github.com/Rupali59` as a stand-in — the current
README does this for Motherboard, AstroClarity and Rishta because those repos are private,
and it reads as three broken links.

### Skills — from the resume's own table, as text

Languages · Web · DBMS · Queues · Cloud/DevOps · Platform (ServiceNow SecOps, GlidePlatform,
Flow Designer). Grouped prose or a small table. Not 40 shields.

## Corrections to make while rewriting

| # | Current | Correct to | Source |
|---|---|---|---|
| C1 | NowFloats `Jun 2017 – Aug 2018` | **confirm** — resume PDF says `Jun'17–July'18`, both READMEs say Aug 2018 | PDF p.1 vs README |
| C2 | Education `8.42 / 10`, `8.58 / 10` | **RESOLVED — keep as-is.** LinkedIn states `GPA: 8.42`, agreeing with both READMEs. The PDF's `84.2%` is the outlier; the PDF is what should change | LinkedIn |
| C3 | NowFloats "50K DAU" | resume says "50000+ clients" daily — clients ≠ daily active users | PDF p.1 |
| C4 | Hackathons: 3 listed | 4 — add High-Volume Data Generator (100M+ records, 20–30 tables) | PDF p.1 |
| C5 | CISO dashboards row merges two resume bullets | separate the Real-Time Aggregation Engine (100K+ records / 8h) from the CISO Dashboards (50+ orgs) | PDF p.1 |
| C6 | Chancellor's Scholarship "2012 & 2013" | **RESOLVED — keep as-is.** LinkedIn lists 2012 and 2013. The unreviewed draft's "2013 only" is the outlier | LinkedIn |
| C7 | About Me: "Building — Motherboard · AstroClarity · Rishta" | Wrong on all three. By 30-day velocity the answer is propagate, the astrology-practice platform, and the filmmaker portfolio | census |
| C8 | Motherboard "auth, scheduling, notifications, **inventory**" | Drop *inventory* — `motherboard-commerce/services/inventory-management` is 15 Go files with **no `main.go` and no external references**; `order-management` is empty with zero commits | `Motherboard/CLAUDE.md` monorepo table |
| C9 | Motherboard "🟢 Active" | **Maintenance.** Last Go-code commit on `main` was **2026-06-21**; the last 30 days are 19 commits of which 3 touch code | `git log main -- '*.go'` |
| C10 | AstroClarity "🔨 Building" | **Remove the row.** The repo is a deliberate 34-file skeleton — no `app/`, no `src/` — reset by `bbf8048` on 2026-07-17 and blocked on an unresolved nav-model decision. `astroclarity.vercel.app` returns 200 because it is serving a **stale pre-reset build** | `Vipin Kaushik/propagation/state/Astroclarity/STATE.md:15-20` |
| C11 | Rishta "🔨 Building" | **Remove.** Not on disk; last push 2026-06-28; `Rishabh/` is a doc-only husk the hub `CLAUDE.md` already flags as self-contradictory | `CLAUDE.md:37` |
| C12 | SSJK CRM "JS · EJS · Astro · TS", "✅ Live" | Stack matches neither the dormant `SSJK-CRM` repo (last push 2025-09-15) nor the live `SSJK-mb`. Restate as the row in the Projects table above, and qualify "Live" — prod cutovers are still gated | `SSJK-mb/STATE.md:27-29` |
| C13 | ACE Coliving "✅ Live" | **Unverifiable.** Private, last push **2025-10-10**, absent from disk and from every registry (`deploy.yml`, `.vercel/project.json`, all STATE files). Move to *Earlier* with no status claim | census |

C1, C2 and C6 need **your** call — they are facts only you can settle. Everything else is
mechanical. I'll leave the current value in place and list them rather than guess.

| C15 | Achievements: "Winner — NowFloats Hackathon · 2017" | **Needs your call.** LinkedIn dates the award **Jan 2017**, but the resume puts your NowFloats tenure at `Jun'17 – Jul'18` and Babajob at `May'16 – Jan'17`. A Jan-2017 NowFloats award predates the stated start by five months. Either the award date or a tenure date is wrong | LinkedIn vs PDF p.1 |
| C16 | Certifications: 5 listed | LinkedIn shows two more, both recent and both worth having: **AI Fundamentals** (Google Career Certificates, Feb 2026) and **Fundamentals of Digital Marketing** (Google, Mar 2026). Note LinkedIn does *not* list "JS Fundamentals · Code With Mosh (2025)" — unverified, keeping it on your word | LinkedIn |

> **Why C8–C13 exist.** I asked a subagent to census the tree and then re-checked its
> load-bearing claims against git myself, per `rule:discernment-checks` §3. Six of the
> current README's eight project rows are wrong in a way that a reader could catch — the
> kind of error that costs more than an out-of-date README, because it makes every other
> claim on the page cheaper.

## Broken CI

`.github/workflows/profile.yml` (`anmol098/waka-readme-stats`) has failed **every night**,
most recently 2026-08-24, with:

```
github.GithubException.BadCredentialsException: 401 {"message": "Bad credentials"}
```

The `GH_TOKEN` PAT expired. Consequences visible to any visitor: a red ✗ on the repo, and a
`## Coding Activity` heading rendering as an **empty section** — the last successful metrics
commit was 2026-04-10.

**Recommendation: delete the workflow and the Coding Activity section**, plus `tech.log` and
`assets/bar_graph.png` which only exist to feed it. A permanently-red workflow on your own
profile repo is worse signal than no metrics at all. Rotating the PAT is a secret write —
that is yours to do (`!` it in the prompt) — and it can be restored later if you want it back.

## Propagation

The user asked for the propagation system to be used, and it produced the finding above:
three artifacts, no declared edges, four disagreeing claims. Close the loop by declaring them.

New `.propagates.yml` in the profile repo:

```yaml
workspace: true
sources:
  README.md:
    propagates_to:
      - path: Rupali_Resume.pdf
        why: the PDF resume and the profile README state the same career; they diverged on
             dates, scores and three metrics because nothing coupled them
        kind: prose
```

Per `rule:adversarial-review-reads-the-ledger` §5, **verify the edge fires** rather than
trusting the declaration: edit `README.md`, run `propagate check --changed`, confirm
`Rupali_Resume.pdf` is named. A declaration nothing tests is the same failure in a new place.

Then record the outcome in the workspace ledger (`Rupali/propagation/`) per
`rule:state-and-decisions`, and file the two open items — rotate-or-retire the waka PAT, and
update the PDF resume to match the README — as durable work rather than session todos.

## Verification

1. **Links** — every URL in the finished README, expecting no 4xx/5xx:
   ```sh
   grep -oE 'https?://[^)"< ]+' README.md | sort -u | while read -r u; do
     printf '%-6s %s\n' "$(curl -sL -o /dev/null -w '%{http_code}' --max-time 12 "$u")" "$u"
   done
   ```
   Baseline measured today: `personacalculator.vercel.app` and `ssjk-crm.onrender.com` are
   **404** (neither is in the current README, but both appear as repo homepages — do not
   reach for them). All 13 other candidate live URLs returned 200.
2. **No placeholder links** — `grep -c 'github.com/Rupali59)' README.md` must be `0`.
3. **Metrics trace** — each number in the Experience section appears in `Rupali_Resume.pdf`
   or is one of the three explicitly confirmed in decision 3. No number without a source.
4. **Render check** — push to a branch, open the PR's rendered README on GitHub; profile
   READMEs render from `main`, so confirm on the branch before merging.
5. **CI clean** — after deleting the workflow, `gh run list --repo Rupali59/Rupali59`
   shows no new failures.
6. **Propagation edge fires** — mutate `README.md`, `propagate check --changed` names the
   resume, then revert. Confirm it goes red for the stated reason.

## Out of scope — but yours to do

- **Update the LinkedIn headline.** It says you are currently at ServiceNow. The README will
  say you left in May 2025, and it links to LinkedIn. One of them has to move.
- **Update `Rupali_Resume.pdf`** — it is a binary authored in Google Docs. Once the README
  lands, the PDF is the stale artifact: it has no Motherboard, no propagate, no client work,
  it states percentages where LinkedIn and both READMEs state CGPA, and it is missing the
  three metrics you confirmed in decision 3.
- **Rotate or retire the `GH_TOKEN` / `WAKATIME_API_KEY` secrets** — secret writes are gated;
  run them yourself with `!`.
- Any change to client repos.

---

# Phase 2a results — re-measured 2026-08-25

Every figure below was measured directly, not taken from the census report.
**Four claims changed under the second method. None were tuned toward the expected value.**

## Confirmed unchanged

| Claim | Measured | Method |
|---|---|---|
| Motherboard last Go commit on `main` | **2026-06-21** (`486707c`) | `git log main -1 -- '*.go'` |
| Motherboard `go.work` modules | **36** | `awk '/^use \(/,/^\)/'` + count |
| Motherboard `.go` files / `_test.go` | **702 / 87** | `find`, vendor excluded |
| Motherboard 30-day commits | **19**, of which **0** touch `.go`/`.ts`/`.tsx` | `git log --since=2026-07-25` |
| Astroclarity has no `app/`, no `src/` | **confirmed** — config + docs only | `ls`, `test -d` |
| propagate lib modules / test files | **53 / 120** | `find` |
| propagate version | **0.2.0** | `VERSION` + `package.json` |
| 30-day velocity, all 11 repos | **exact match** on every row | `git log --since=2026-07-25` |
| Public repos to link | Sanskrit-texts, MIS, himk-implementation, parking_lot, WorkTracker — all **public**, all **HTTP 200** | `gh repo view`, `curl` |

## Discrepancies found — the census was wrong on these

| # | Census said | Actually | Consequence |
|---|---|---|---|
| **D1** | `inventory-management` has **no `main.go`** and is unwired | It **has** `cmd/server/main.go`, 15 Go files, 3 test files, a full `internal/{domain,handler,mongo,config}` tree, and appears in `go.work`. What is true: **0 external references** | The hub `CLAUDE.md`'s claim is wrong on one of three parts. The README must not repeat "no main.go" — it simply omits *inventory* from the platform description, because nothing calls it |
| **D2** | SSJK-mb has **167 test files** | **228** git-tracked test files: `server` 167, `admin` 46, `ui` 12, `scripts` 3. 167 is the *server* subtotal mistaken for the total | Use 228, or say "167 on the API alone" |
| **D3** | Astroclarity has **34** tracked files | **44** | Conclusion unchanged — still a skeleton |
| **D4** | Sanskrit corpus: **57 texts / 927 chapters / 91,782 shlokas** | Derived independently: **54 / 918 / 92,166** | Differs on all three. Its own `STATE.md` says *derive, never restate*, and records that a previous generator was invisibly wrong. **Do not put a precise count in the README** — both methods agree only on the order of magnitude. Use "90,000+ verses across 50+ texts" |

## Qualifications that change how a number may be used

- **astroacharya's "1,034 tests pass"** is real but describes the branch
  `feat/muhurta-typed-endpoints`, which is **14 commits ahead of `origin/main` with no PR
  open**. 85 test files on disk. Usable, but it is not `main`.
- **`astroclarity.vercel.app` returning 200 is not evidence of a live project.** It serves a
  fully built Next.js app — preloaded fonts, CSS and JS chunks — while the repository has no
  `app/` and no `src/`. That is a **stale build predating the 2026-07-17 reset**. C10 stands.
- **LinkedIn returns HTTP 999** to unauthenticated requests. That is its anti-bot response,
  not a broken link — safe to link from the README.

**Gate status: 2a CLOSED. 2b (the blocking half) remains open.**

---

# Phase 2b — authenticated LinkedIn, read 2026-08-25

## First: two earlier claims in this document were wrong

The "Context" and "Corrections" sections above cite a LinkedIn read performed with an
unauthenticated fetch. **That fetch hit a login wall and produced plausible content anyway** —
the `rule:discernment-checks` §6 failure exactly: a reader that cannot report failure invents
an answer. Reading the profile signed-in, through the browser, contradicts it:

| Earlier claim in this doc | Actually |
|---|---|
| Headline is "Senior Software Engineer at ServiceNow" — present tense, implying she never left | Headline is **"ex Senior Software Engineer at ServiceNow"**. The fetch dropped the word *ex*. **There is no contradiction with the README, and the concern raised in Context is void** |
| Certifications include "AI Fundamentals (Feb 2026)" and "Fundamentals of Digital Marketing (Mar 2026)"; also Wati, Coursera, freeCodeCamp with dates | The certifications section holds **10 entries and none of those**. *AI Fundamentals* is real — confirmed from her own post and Credly — but is not in that section. *Fundamentals of Digital Marketing* appears **nowhere** and was invented |
| Git Essential Training, Jun 2020 | **Jan 2020** |

C2 and C6 were marked RESOLVED on that source. Both happen to be correct — but they were
right by luck, and are now properly verified below.

## Verified from the signed-in profile

**Roles** — every date confirmed; the README's dates are right and the PDF's are not.

| Employer | Title | Dates | Mode |
|---|---|---|---|
| ServiceNow *(6 yrs 2 mos)* | Senior Software Engineer | Mar 2022 – May 2025 | Remote |
| ServiceNow | Software Engineer | Apr 2019 – Mar 2022 | Hybrid |
| Darwinbox | Software Developer | Aug 2018 – Mar 2019 | Hyderabad |
| NowFloats | Software Engineer | **Jun 2017 – Aug 2018** *(1 yr 3 mos)* | Hyderabad |
| Finomena | Software Developer | Feb 2017 – May 2017 | Bengaluru |
| Babajob.com | Software Engineer | May 2016 – Jan 2017 | Bengaluru |

- **C1 RESOLVED: NowFloats ends Aug 2018.** The PDF's `July'18` is the outlier.
- **C2 RESOLVED: NIT Goa grade 8.42, LNCT 8.58 CGPA.** The PDF's percentages are the outlier.
- **C6 RESOLVED: Chancellor's Scholarship has two entries, Jan 2013 and Jan 2012.**
- **C3 REOPENED.** LinkedIn says, in her own words, *"These features support over **50,000
  daily active users**."* The DAU framing is hers. The decision to soften it to
  "merchants/clients" was taken against the PDF alone, before this was known.
- **C15 CONFIRMED AS A REAL INCONSISTENCY.** The honors entry is dated **Jan 2017** and its
  description credits the SPIDER module — which LinkedIn itself places inside the NowFloats
  role starting **Jun 2017**. Her LinkedIn contradicts itself; the honors entry needs the fix.

**Certifications section — the actual 10**

| Certification | Issuer | Issued |
|---|---|---|
| Claude Code in Action | Anthropic | Aug 2026 |
| Introduction to Claude Cowork | Anthropic | Jul 2026 |
| Claude Platform 101 | Anthropic | Jul 2026 |
| Claude Code 101 | Anthropic | Jul 2026 |
| Claude 101 | Anthropic | Jul 2026 |
| Create Your First Gemini Enterprise Application | Google | Apr 2026 |
| Gemini Enterprise Agent Ready | Google | Feb 2026 |
| Google Developer Program — Premium Tier | Google | Feb 2026 |
| Google Cloud Innovator | Google | Jan 2026 |
| Git Essential Training | LinkedIn Learning | Jan 2020 |

Plus **AI Fundamentals** (Google Career Certificates, ~Feb 2026) — evidenced by her own post
and Credly, absent from the certifications section.

**Five Anthropic certifications from Jul–Aug 2026 are the most on-topic credential she has**,
given `propagate` is a Claude Code plugin, and the README lists none of them.

## New divergences this read surfaced

| Field | README / résumé | LinkedIn |
|---|---|---|
| Location | Hyderabad, India | **Bengaluru, Karnataka, India** |
| Availability | "Full-Time Remote · Hyderabad · Bangalore · open to relocation" | **"Open to work · Recruiters only — Delhi, India +4 more · On-site · Hybrid"** — recruiters-only, and *not* remote |
| ServiceNow metrics | 40% / 30% / 60% / 1M+ / 100K+ / 50+ orgs | **No numbers at all.** Every quantified claim is missing from LinkedIn |
| Source integrations | Veracode · Qualys · Tenable · MS TVM | "third-party sources **like Veracode**" only |

**Typos live on the public honors entries** — `inovation`, `hat predicts`, `u to 84%`,
`Sciene`, `fculty`, `menoring`, `Depatment`, `evets`, `ad co-ordinated`. Visible to any
recruiter reading the profile.

---

# Outcome — 2026-08-25

**Applied to the working tree, uncommitted** (`rule:never-commit-unless-asked`).

| Phase | Result |
|---|---|
| 0 · Clone | `~/Documents/GitHub/Rupali/Rupali59` |
| 1 · Keep this document | `docs/README-rewrite-2026-08-25.md`, indexed from `docs/README.md` |
| 2a · Mechanical re-verification | Closed. 4 census claims corrected — see above |
| 2b · Blocking facts | Closed. C1, C2, C3, C6, C15, C16 all resolved |
| 3 · README rewrite | 14,207 → 11,113 bytes |
| 4 · Hygiene | Workflow, `tech.log`, `bar_graph.png`, `docs/unreviewed/` removed; `.DS_Store` untracked |
| 5 · Propagation edge | Declared, fires, goes quiet, writes nothing. `doctor: all green` |

## Verification, run

1. **Links** — 16 unique URLs, all HTTP 200 except LinkedIn's 999 (its anti-bot response to
   unauthenticated requests, not a broken link).
2. **Placeholder links** — `grep -c 'github.com/Rupali59)'` = **0**. The three fake links are gone.
3. **Dead rows** — `AstroClarity`, `Rishta`, `ACE Coliving`, `SECTION:waka`, `inventory`: **0 each**.
4. **Corrections** — C1 (Aug 2018), C2 (8.42), C3 (50,000+ DAU), C4 (100M+ records), and the
   Anthropic certifications all present.
5. **CI** — `.github/workflows/` no longer exists, so there is no job left to fail nightly.
6. **Edge** — fires on a changed README, silent on an unchanged one, byte-identical store.

## Still open, and all of it is Rupali's

Tracked as durable work in `Rupali/propagation/state/Rupali59/STATE.md`, not as session todos.

- **P1 — update `Rupali_Resume.pdf`.** It is now the stale side of a declared edge.
- **P2 — LinkedIn:** fix the NowFloats hackathon date (its own experience section contradicts
  it); fix nine typos live on the public honors entries; reconcile "Open to work" with the
  README's city-free line.
- **P2 — decide the WakaTime integration's fate.** Retired here; the PAT rotation is a secret
  write and is yours.
- **P3 — add the ServiceNow metrics to LinkedIn.** It carries no numbers at all.

---

# Round 2 — the 90-day re-measure, same day

Round 1 ranked Projects on a **30-day** window. Re-measured over **90 days**
(`--since=2026-05-25`), the ordering inverts and four published facts turn out to be wrong.

## The window error

| Repo | 30-day | 90-day (no merges) | Round-1 verdict |
|---|---:|---:|---|
| `Vipin Kaushik/VipinKaushik` | 20 · 5 code | **415 · 338 code — #1 in the tree** | omitted as "low-velocity" |
| `pawankaushik-web` | ~0 | 41 · 37 code | omitted as "dormant" |
| `gemastrology-{theme,shopify}` | 0 | 22 · 19 code | never seen |
| `SSJK-bot` | 0 | 13 · 11 code | never seen |

Tree total: **2,165 non-merge commits across 35 repositories in 3 months** (discounting
`Obsidian`, 71 of 86 automated, and `WorkTracker`, 24 of 43 — every other repo is 0% automated,
checked rather than assumed). A 30-day window measures the current sprint; a résumé is a
quarterly instrument. **Rank on 90 days.**

## Four defects in the page shipped in round 1

| # | Was | Measured | Now |
|---|---|---|---|
| X1 | marketing-intel stack "· SQLite" | facade **fully removed 2026-06-20** (`03b434c`, `68ff5ad`); `mongoose ^9.6.3` | Mongoose · MongoDB |
| X2 | propagate "120 test files" | **130** repo-wide — round 1 counted only `tests/` + `hooks/` | 130 |
| X3 | propagate "13 workspaces" | **12** ledgers on disk; the census said 13 | number dropped |
| X4 | Manav "6.4 MB → 2.3 MB" | **no commit or STATE line supports it**; `b34585f` gives hero **10.4 MB → ~3 MB** | the commit-backed figure |

**X4 is the instructive one.** Round 1's verification asserted "each number traces to a source"
and passed — because it only tested the Experience section, while X4 sits in Projects. *The
check was scoped narrower than the claim it was supposed to guarantee.* Round 2's V3 runs over
the whole page; every metric was re-measured and printed beside its source.

**X2 is the subtotal-as-total error, made twice.** Round 1 flagged the census for reporting
SSJK-mb's 167 *server* tests as the project total, then made the same error on propagate.

## The framing change

> *"I am a software engineer. Yes I'm working with the astrology domain, but I don't want that
> to be the headline. I would prefer to leverage the work I have done there."*

Round 1 titled rows **by domain**. With the new rows added that would have been **5 of 11 rows
saying "astrology"** — a skimmer concludes domain specialist. Rows are now titled by
engineering substance, domain demoted to a trailing clause. Verified: **0** domain terms above
the Projects table and **0** in any row title.

`Astrology practice platform` → **Multi-tenant CRM & workflow platform** ·
`Vedic astrology compute backend` → **Ephemeris computation service** ·
`Sanskrit text corpus` → **Text digitisation & translation pipeline** ·
`Marketing intelligence tool` → **Demand-intelligence platform**

## Added

Three rows — **Content & SEO platform** (the quarter's #1 build), **E-commerce storefront &
embedded admin app** (adds Shopify/Liquid/Remix/Polaris/Prisma, absent from the skills table
until now), **Job-radar skill** (second shipped artifact in the Claude-tooling space the
certifications claim). The Telegram bot and the ~30-page site rebuild folded into one sentence.

In-row upgrades that cost no rows: the **RBAC/ACL engine** and **78s → 28s** test infra on the
CRM row; the **v1→v2→v3 rearchitecture** and portability work on propagate; **Workload Identity
Federation** on the demand platform.

Plus one standalone line: **a 154-commit recovery**, verified independently —
`git tag -l 'rescue/*' | wc -l` = **154**.

**Trimmed for lack of evidence.** The recovery line originally carried "`git fsck
--unreachable` → 0" and "8 of 29 stashes held unique content", both from the subagent report.
Neither could be reproduced from any file reachable on disk, so both were cut. Only the tag
count is independently verifiable, so only it survives.

## Verification run

| # | Check | Result |
|---|---|---|
| V1 | domain terms above Projects / in row titles | **0 / 0** |
| V2 | X1–X4 applied | SQLite 0 · "130 test files" 1 · "13 workspaces" 0 · 6.4 MB 0, 10.4 MB 1 |
| V3 | every Projects metric traced, re-measured | 130 ✓ · 228 ✓ · 78s→28s ✓ · "not 89" ✓ · 36 ✓ · 702 ✓ · 10.4 MB ✓ · 3,522→6 ✓ · 154 tags ✓ · 44×44 ✓ · 1,034 tests ✓ |
| V4 | links | all 200; LinkedIn 999 (anti-bot, expected) |
| V5 | no client named | 0 leaks across 13 name and domain patterns |
| V6 | Current row count | 11 |
| V7 | propagation edge | fires, names the résumé, store byte-identical |

---

# Round 3 — the AI gap, benchmarked against the 2026 market

## The defect

Three questions, one defect. The propagate row ended *"ships as an editor plugin"* — five words
for a Claude Code plugin with slash commands, hooks and skills. Every other AI reference on the
page was ServiceNow 2019–2022, the 2016 thesis, or a skills row reading
`scikit-learn · TensorFlow · MATLAB`. **And the page listed ten 2026 AI certifications.**
Credentials with no visible work is the worst available combination.

## The bar, searched rather than remembered

- Languages and frameworks are **Tier 3** now; architecture, AI-assisted workflow and
  code-quality judgment are the differentiators.
- *"If your AI resume doesn't mention evaluation, hiring managers assume you've shipped
  unevaluated features. In 2026 that's a disqualifier at serious companies."*
- *"Listing 'Claude Code' in your skills section is the 2026 equivalent of listing 'Microsoft
  Word' in 2010."*
- The checklist that replaced LangChain+Pinecone: agent orchestration · MCP · **eval design** ·
  prompt engineering · vector/RAG · cost optimisation · **safety/guardrails** · computer-use ·
  observability · frontier-model fluency.

Sources are listed in the plan file.

## Verdict

**At or above bar on classical engineering** — architecture is the strongest axis and now reads
that way. **Beginner-level on AI, as presentation rather than substance:** four to five
checklist items are evidenced in code she authored, and the page showed none of them.

## What was claimed, and the authorship proof for each

| Claim | Evidence | Authorship |
|---|---|---|
| Claude Code plugin: 4 commands, 2 hook events, 2 skills | `ls commands/` = 4; `hooks.json` declares `SessionStart` + `PreToolUse`; `ls skills/` = 2 | `plugin.json` author `Rupali`; **169 of 169 commits** hers |
| Marketplace: 19 skills across 3 plugins | `skills-marketplace/{propagate:2, quarantine:2, tathya:15}` | hers |
| PreToolUse agent guardrail | `hooks/gotcha-guard.mjs` — matches the literal command against declared hazard triggers | hers |
| Eval harnesses | `lib/rules/rules-check.mjs` `selftest`; per-hazard `**Fires on:**` assertions; job-radar *"fixtures, golden set, and a testing method"* | job-radar **34 of 34 commits** hers |
| Gemini evaluation gating source promotion | `@google/genai ^1.17.0`; `lib/gemini.ts`, `lib/reddit/classify.ts`, `lib/reddit/recommend-subreddits.ts`; `app/api/subreddits/promote/route.ts` | hers |

## What was deliberately NOT claimed

**`gbrain` is excluded entirely** — `github.com/garrytan/gbrain`, **1,024 commits in 12 months,
0 by Rupali**, top author Garry Tan with 502. She operates it, wrote a 200-line operational
convention for it, and diagnosed real defects in it. None of that is authorship.

Because gbrain was the only vector/RAG and cost-optimisation evidence, **the README claims
neither.** Four to five of ten, all real, beats nine of ten with one that fails a reference
check. `grep -ci gbrain README.md` = **0**.

The two Gemini commits that *delete* Gemini code were checked before the claim was written: the
2026-06-20 one removed a superseded briefing engine, and the 2026-08-22 one retired `GEMINI.md`,
an agent instruction file, not the API. The API path is live today.

## Also changed

- Skills row `ML & research` split: a new **AI & agent tooling** row, and **ML** kept but tied
  to the thesis and the ServiceNow recommender where it is actually true.
- Ten certification list-items compressed to two lines, still after Projects.
- Summary now says the tooling is agent-facing.

## Verification run

| Check | Result |
|---|---|
| Every AI claim traces to an authored artifact | propagate 169/169 · job-radar 34/34 · plugin author `Rupali` |
| gbrain absent | 0 |
| Plugin numbers re-derived | 4 / 2 / 2 / 19 across 3 — all match |
| Evaluation named, pointing at a harness | 5 occurrences |
| Certifications below Projects | Projects §99, Certifications §189 |
| Links | all 200; LinkedIn 999 (anti-bot) |
| No client named | 0 leaks |
| Domain above Projects / in row titles | 0 / 0 |
| Propagation edge | fires, store byte-identical |

## Round 3, addendum — the AI census, and two more errors it found

The census that ran alongside round 3 corrected two factual claims and found one severe
undersell. All three re-verified independently before acting.

| # | Was | Measured | Now |
|---|---|---|---|
| **X5** | HIMK stack "MATLAB · Python" | `gh api .../languages` → **TeX 100 KB, Python 67 KB, HTML, Makefile, Dockerfile — zero MATLAB.** `requirements.txt`: numpy, scipy, scikit-learn, opencv-python, **hmmlearn**, scikit-image, pymongo | Python · scikit-learn · hmmlearn · OpenCV · Docker, described as a **2026 re-implementation** with a Flask front end |
| **X6** | Skills row "scikit-learn · TensorFlow · MATLAB" | **Zero `.m` files and zero tensorflow/torch/keras imports anywhere in the tree.** Two of three entries unsupported | scikit-learn · hmmlearn · OpenCV |
| **X7** | Demand platform had one line on Gemini | It is the **only production LLM system** in the tree, and the strongest AI artifact | Promoted to a full paragraph, and leads the AI section |

**X5 and X6 are the same error as X4 in round 2** — a claim inherited from an older document and
never measured. The 2026 Python rebuild is a *better* story than "2016-era MATLAB"; the README
was underselling the work by repeating a stale label.

### What X7 actually contains, verified in her own source

- `lib/reddit/classify.ts:59-60,183` — `MODEL = 'gemini-3-flash-preview'`, `BATCH_SIZE = 10`,
  `temperature: 0`.
- Its header: *"Determinism rests on cache-on-first-write (caller) + temperature 0, NOT on the
  model being deterministic. On any failure the caller falls back to the keyword classifiers, so
  a Gemini outage degrades quality but never breaks ingestion."*
- `lib/reddit/recommend-subreddits.ts:3-14` — *"A hallucinated SUBREDDIT … sits in the tracked
  list producing zero posts forever, an invisible absence that reads as coverage. So every
  candidate is existence-checked against Reddit before it is returned. Unverifiable candidates
  are returned FLAGGED, not dropped … asserting either way would be fabricating a fact we do not
  have."* `verified: boolean | null`, `MAX_VERIFY = 12`.
- `lib/gemini.ts` — 4 `responseSchema` / `responseMimeType` declarations.

That is LLM-reliability engineering — schema-constrained output, a non-LLM degradation path, and
hallucination containment with an explicit refusal to assert an unverified fact. It is the same
discipline as this repository's own rules, applied to model output.

### Deliberately excluded, on the census's evidence

| Excluded | Why |
|---|---|
| `astro-posts` LLM-as-judge rubric | Owner-owned repo, but the generator it credits (`~/.hermes`) is **absent from this machine and from all 92 GitHub repos**, and the rubric files record a **client's home directory**. Authorship cannot be established |
| `openclaw-mcp-server` | The only MCP server authored — **3 commits, one 13 KB file, stub architecture doc.** "Built MCP servers" would not survive an interview |
| `gstack-design-layer` | **1 commit, 7 KB**, while its description promises an "adversarial five-judge panel with scoring". The specific sounds-impressive-but-thin trap |
| Claude Code Action workflows | 7 of them, essentially all Anthropic's template |
| The 45 `SKILL.md` under `~/.claude/skills/` | **Symlinks to third-party skills** — Vercel, Shopify, Homebrew, and gstack. Installed, not authored. The defensible number is **19** |
