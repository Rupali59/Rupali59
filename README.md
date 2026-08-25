# Rupali Bhatnagar

**Senior Software Engineer** · India · open to relocation

[tathya.dev](https://tathya.dev) ·
[LinkedIn](https://www.linkedin.com/in/rupali-bhatnagar-b4864957/) ·
[g.dev/rupali59](https://g.dev/rupali59) ·
[Credly](https://www.credly.com/users/rupali-bhatnagar-59) ·
[rupalibhatnagar0509@gmail.com](mailto:rupalibhatnagar0509@gmail.com)

Nine years building high-scale backend and platform systems. Six of them at **ServiceNow**
across Security Operations and Vulnerability Response, where I shipped engines that route
**1M+ vulnerable items a day** and dashboards used by **50+ enterprise security teams**.

Since 2025 I've been building independently: a Go microservices platform, agent-facing developer
tooling shipped as a Claude Code plugin, and production web products. My interests are distributed systems,
developer tooling, and the unglamorous problem of keeping large codebases honest.

---

## Experience

### ServiceNow — Senior Software Engineer
`Mar 2022 – May 2025` · Security Operations & Vulnerability Response · Remote

- **[Dynamic Approval Rule Engine](https://www.servicenow.com/docs/r/washingtondc/servicenow-platform/approvals/c_ApprovalEngines.html)** —
  multi-level approval workflow for vulnerability deferment and exception requests, built on
  Flow Designer to stay configurable across differing enterprise policies. **40% faster approvals.**
- **[Penetration Testing Request Catalog & Workflow Automation](https://www.servicenow.com/docs/r/security-management/application-vulnerability-response/pen-test-config-v16-1.html)** —
  catalog and automated workflows for pen-test requests across **50+ subsystems**,
  cutting manual intervention by **30%**.
- **[Background Job Processing Framework](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vr-background-framework.html)** —
  multithreaded framework for long-running work that previously strained system resources,
  with job status tracking, cancellation and ETA visibility. **Up to 60% performance gain**,
  **1M+ tasks/month**.
- **Real-Time Data Aggregation Engine** — high-performance aggregation for near real-time
  multi-dimensional analytics, processing **100K+ records per 8-hour cycle** to power internal
  dashboards.

### ServiceNow — Software Engineer
`Apr 2019 – Mar 2022` · Security Operations & Vulnerability Response · Hybrid

- **[Assignment Rule Engine](https://www.servicenow.com/docs/r/security-management/configuration-compliance/cc-assignment-rules.html)** —
  cache-optimised engine prioritising infrastructure vulnerabilities and policy violations and
  routing them to the right remediation groups. Runs daily over **1M+ vulnerable items**.
- **[ML-Based Assignment Recommendations](https://www.servicenow.com/docs/r/security-management/vulnerability-response/ml_view_assignment_recommendations.html)** —
  classification-based recommendation system with feature engineering and a user-facing
  review interface. **+20% task allocation accuracy.**
- **[CISO & Vulnerability Dashboards](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vulnerability-mgmnt-CISO-dashboard.html)** —
  led design and development of the executive CISO dashboard and its supporting vulnerability
  dashboards, defining the key metrics and the data pipeline behind them. Adopted by
  **50+ organisations**.
- **[Vulnerability Source Integrations](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vulnerability-response-common-content-pack.html)** —
  integrations with Veracode, Qualys, Tenable and Microsoft TVM, standardising
  **500K+ vulnerability records/day** into a common model for downstream remediation.
- **Hackathon projects** — Diagnostic Framework (**40%** less debugging time) · ML vulnerability
  grouping and remediation-target estimation · PoA&M generator · High-volume data generator
  (**100M+ records across 20–30 tables**, adopted by the performance team).

<details>
<summary><b>Earlier roles</b> — Darwinbox · NowFloats · Finomena · Babajob (2016–2019)</summary>

### Darwinbox — Software Developer
`Aug 2018 – Mar 2019` · Hyderabad

- Audit-logging microservice capturing every client data modification — PHP/Yii listening to
  MongoDB oplogs and publishing to AWS SQS for downstream processing.
- Oplog diff processor resolving changes across strings, arrays and nested documents into
  human-readable audit entries.

### NowFloats / Boost360 — Software Engineer
`Jun 2017 – Aug 2018` · Hyderabad

- Responsive web platform features supporting **50,000+ daily active users**
  (C#, Bootstrap, JavaScript, jQuery, Knockout.js).
- **SPIDER** sales-prediction model — per-representative revenue forecasting at **84% accuracy**.
- Generic booking system on Node.js, configurable across hotels, clinics and restaurants.
- Facebook Graph API integration for merchant product sharing; order management dashboard
  (AngularJS, C#).

### Finomena — Software Developer
`Feb 2017 – May 2017` · Bengaluru

- Loan management, repayments and collections dashboards in PHP/Laravel, scaled to
  **8,000+ loans/month** on MySQL via Eloquent.

### Babajob — Software Engineer
`May 2016 – Jan 2017` · Bengaluru

- IVR and SMS system in **Go** with RabbitMQ — asynchronous, state-driven inbound call
  handling at **10K+ calls and 20K+ SMS per day**, with MongoDB-backed analytics.
- Search subsystem in Java over Elasticsearch, with dynamic query generation via Mustache
  templates.

</details>

---

## Projects

### Current · 2025 – present

My main line of work is a **documentation-integrity toolchain** — tooling that detects when
files which must agree have silently stopped agreeing — running across every workspace in the
tree and enforced by commit and session hooks.

| Project | What it is | Stack |
|---|---|---|
| **propagate** — a Claude Code plugin | Agent-facing developer tooling: 4 slash commands, a **SessionStart hook** that injects canonical engineering rules into every session, and a **PreToolUse guardrail that inspects the literal command an agent is about to run and surfaces the matching known hazard before it executes** — hazard docs are pull artifacts, and the failure mode is recognition rather than knowledge. Underneath: declares couplings between files that must change together and derives drift from file *content* on demand rather than storing state. **It never edits a downstream file — the tool finds and explains, a human approves, and the decision is recorded in an append-only ledger.** Every detector and every guardrail trigger ships with a `selftest` asserting it can actually fire, because a check that cannot fail reports success — that selftest has caught real bugs. Rearchitected across two generations to an immutable, ULID-keyed, content-pinned store; made portable after the suite passed locally and failed on every clean machine. 130 test files. | Node · ESM · Claude Code plugin API |
| **Multi-tenant CRM & workflow platform** | Express API plus two Next.js 16 apps (client and admin). A **DB-driven RBAC/ACL engine** — runtime-editable roles, generic field-level access control over CRUD, per-actor tier projection, table→field cascade, and a capability-matrix UI whose review-diff modal shows the consequences of a change before an atomic batch save, with fail-closed reconciliation and admin-floor guards. WebAuthn + OTP auth, BullMQ/Redis job queue, workflow engine, web-push. A phased task-model migration dark-shipped in five stages with a one-shot backfill of ~14,000 records. Test infrastructure cut from **78s to 28s** by running one shared `mongod` for the suite instead of 89. 228 test files. | Express · BullMQ · Redis · MongoDB · Next.js · React 19 |
| **Content & SEO platform** | Production site backed by the computation service below — the two are one system. Ten templated landing pages on a shared shell with `FAQPage` structured data and selective `noindex`, a server-side analytics pipeline, signed-cookie location handling with a durable resolved-location cache, and a migration of public pages to static generation. | Next.js · TypeScript · Radix · CASL |
| **Motherboard** | Go multi-module monorepo: an API gateway and multi-tenant plugin platform. **36 `go.work` modules, 702 Go files.** Plugin services authenticate, publish their routes to a client manager, and the gateway proxies to them behind a fail-closed entitlement gate and a plugin-key claim assertion. | Go 1.25 · Next.js |
| **Demand-intelligence platform** | Multi-source ingestion and opportunity scoring, with a **production LLM classification pipeline**: Gemini calls constrained by enforced response schemas, run at `temperature: 0` and batched, with determinism resting on cache-on-first-write rather than on the model — and a keyword-classifier fallback so a provider outage degrades quality instead of breaking ingestion. Model-proposed sources are **existence-checked against the live API before being accepted**, and an inconclusive check returns the candidate flagged rather than asserted either way. Ingestion also covers Search Console via **Workload Identity Federation** — adopted to remove service-account JSON-key fragility — plus Trends and YouTube. Entity ontology mapping demand against supply; scheduling moved off hosted cron onto a local agent. | Next.js · TypeScript · Mongoose · MongoDB · Gemini |
| **Ephemeris computation service** | FastAPI service over Swiss Ephemeris, a native library with process-global mutable state that is **not thread-safe**. Every call is serialised through a single-worker executor that releases the event loop during computation — the actual engineering problem behind the API. Adds an astronomical-timeline subsystem (boundary and instant finders, lunar-month tables, per-year caching with TTL) and typed per-calculation endpoints replacing one overloaded route. **1,000+ tests.** | Python 3.12 · FastAPI · MongoDB |
| **E-commerce storefront & embedded admin app** | Shopify Liquid theme plus an embedded Remix admin — metafield/metaobject schema installer, headless catalogue seeders, and certificate verification implemented natively in Liquid rather than through an app proxy. Accessibility pass to a 44×44 touch-target floor. | Shopify · Liquid · Remix · Polaris · Prisma |
| **Text digitisation & translation pipeline** | Ingestion for a structured-JSON corpus of classical texts: a TEI/SARIT parser handling prose and division-type detection, a scraper that splits on the source's own headings, a verse-marker grammar, per-work structural maps and validators. One structural fix took depth errors in a single work from **3,522 to 6**. Corpus: [Sanskrit-texts](https://github.com/Rupali59/Sanskrit-texts). | Python · JSON |
| **Filmmaker portfolio** | Production site with a Google Docs → works sync pipeline and multi-codec delivery (AV1/HEVC/H.264): a hero codec ladder took **10.4 MB to ~3 MB**, with delivery suppressed for non-watchers, and an H.264 Level 4.0 re-encode for iOS autoplay. | Next.js · React 19 · MongoDB |
| **Job-radar skill** | A Claude Cowork skill that categorises job postings, parses compensation and produces a match-score breakdown, with a local server and a health model. Tested against fixtures and a golden set. | Node · esbuild · vitest |
| **[tathya.dev](https://tathya.dev)** | My own practice — business sites and CRM. WebAuthn, CASL authorisation, d3-based assessment engine. | Next.js 16 · React 19 |

Also in this period: a Telegram bot service (grammY + webhook dispatch, inline-keyboard state
machine, adaptive heartbeat and briefing schedulers, en/hi i18n) and a ~30-page production site
rebuilt in Next.js against a live reference.

**A 154-commit recovery.** A worktree removal combined with dropped stashes left 154 commits
unreachable in a live repository. All 154 were located, recovered and permanently tagged, and
the restored work was reintegrated behind its tests.

### AI & agent tooling

Everything here I built; each is a repository of mine.

- **A production LLM pipeline, engineered for unreliability.** Enforced response schemas,
  `temperature: 0`, batching, a non-LLM fallback path so an outage degrades quality without
  stopping ingestion, and containment for the failure that matters most: a hallucinated source
  is an *invisible absence that reads as coverage*, so every model-proposed source is
  existence-checked before acceptance and an inconclusive check is flagged, never guessed.
- **A Claude Code plugin and a plugin marketplace.** `propagate` ships 4 slash commands, 3 hook
  scripts across 4 registrations on 2 events, 2 bundled skills, and a skill *lifecycle* CLI
  (create / promote / demote / reap); the marketplace serves **19 skills across 3 plugins**.
- **An agent guardrail.** A `PreToolUse` hook that pattern-matches the command an agent is about
  to execute against declared hazards and delivers the relevant one at the moment of risk —
  written after a documented hazard, sitting three files away, was hit anyway and cost 11 false
  verification records.
- **Evaluation harnesses, not vibes.** Detectors and guardrail triggers each carry a `selftest`
  asserting the check can fire against a known-positive input; the job-radar skill is tested
  against fixtures and a golden set. A check that cannot fail is worse than no check, because it
  reports success.
- **Human-in-the-loop by construction.** The tooling is designed so an agent proposes and a
  person disposes: no downstream file is ever edited automatically, and every approval is an
  append-only ledger event.

<sub>Client work is described by what was built rather than by client name. Those repositories
are private; the products are in production.</sub>

### Earlier

| Project | |
|---|---|
| **[HIMK](https://github.com/Rupali59/himk-implementation)** — human activity recognition using an HMM-based Intermediate Matching Kernel with SVM. M.Tech thesis, re-implemented in 2026 as a containerised Python pipeline with a Flask front end | Python · scikit-learn · hmmlearn · OpenCV · Docker |
| **[MIS](https://github.com/Rupali59/MIS)** — institute management platform for students, faculty and administration | Next.js · MongoDB |
| **[Parking Lot](https://github.com/Rupali59/parking_lot)** — system-design allocation problem | Go |
| **[WorkTracker](https://rupali59.github.io/WorkTracker/)** — personal work dashboard and digital garden | TypeScript |
| **Voice Transcriber** — dockerised real-time speech-to-text *(private)* | Python · Docker |

---

## Technical Skills

| | |
|---|---|
| **Languages** | Go · TypeScript · JavaScript · Python · Java · PHP · C# · C++ |
| **Web** | Next.js · React · Node.js · Remix · Astro · Laravel · .NET · Tailwind |
| **Data** | PostgreSQL · MongoDB · MySQL · Redis · Elasticsearch |
| **Messaging** | RabbitMQ · BullMQ · AWS SQS |
| **Commerce** | Shopify · Liquid · Polaris · Prisma |
| **Cloud & tooling** | AWS · Vercel · Docker · Fly.io · Git · Linux |
| **AI & agent tooling** | Claude Code plugins, hooks and skills · structured LLM output and schema-constrained generation · eval harnesses and golden sets · hallucination containment and graceful degradation · human-in-the-loop design |
| **ML** | scikit-learn · hmmlearn · OpenCV — pattern recognition and classification (thesis; ServiceNow assignment recommender) |
| **Platform** | ServiceNow SecOps · Vulnerability Response · GlidePlatform · Flow Designer |

---

## Education

| Degree | Institution | Grade | Years |
|---|---|---|---|
| **M.Tech**, Computer Science & Engineering — Pattern Recognition & Machine Learning | National Institute of Technology Goa | 8.42 | 2014–2016 |
| **B.E.**, Computer Science & Engineering | LNCT Bhopal (RGPV) | 8.58 CGPA | 2010–2014 |

---

## Certifications

**AI, 2026** — **Anthropic:** 5 certifications across Claude, Claude Code and Claude Cowork
(Jul–Aug 2026). **Google:** Gemini Enterprise Agent Ready · Create Your First Gemini Enterprise
Application · Google Cloud Innovator · Developer Program Premium Tier · AI Fundamentals
(Google Career Certificates).

**Earlier** — WhatsApp API Expert, Wati (2024) · Ultimate JavaScript: Fundamentals, Code With
Mosh (2025) · Neural Networks & Deep Learning, Coursera (2020) · JavaScript Algorithms & Data
Structures, freeCodeCamp (2020) · Git Essential Training, LinkedIn Learning (2020)

---

## Honors & Awards

- **Winner** — NowFloats internal hackathon, for the SPIDER sales-prediction module
- **Chancellor's Scholarship** — top 10 students statewide by theory marks,
  RGPV Bhopal · 2012 and 2013
- **Silver Medal** — Persistent Systems Programming Contest, inter-college · 2013
- **Teaching Assistant**, Computer Science Department — NIT Goa · 2014–2016
- **Vice President**, Computer Science Department — NIT Goa · 2014–2016

---

## Open to Opportunities

Senior and staff-level platform, backend and full-stack roles — remote or on-site. Also open to
open-source collaboration on developer tooling.
[Email me](mailto:rupalibhatnagar0509@gmail.com) or
[reach out on LinkedIn](https://www.linkedin.com/in/rupali-bhatnagar-b4864957/).
