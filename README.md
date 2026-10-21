<div align="center">

# Rupali Bhatnagar

**Senior Software Engineer · AI-assisted engineering**<br>
India · open to relocation

[Résumé (PDF)](resume/Rupali_Bhatnagar_Resume.pdf) ·
[LinkedIn](https://www.linkedin.com/in/rupali-bhatnagar-b4864957/) ·
[g.dev/rupali59](https://g.dev/rupali59) ·
[Credly](https://www.credly.com/users/rupali-bhatnagar-59) ·
[Email](mailto:rupalibhatnagar0509@gmail.com)

</div>

---

Nine-plus years building high-scale backend and platform systems, six of them at **ServiceNow**
across Security Operations and Vulnerability Response, shipping engines that route
**1M+ vulnerable items a day** and dashboards used by **50+ enterprise security teams**.

Since June 2025 I've been an independent software consultant, working with AI agents in the loop:
Claude Code plugins, hooks and skills, MCP, schema-constrained LLM output and eval fixtures drawn
from real failures — built so that tools propose and explain, and a person decides.

| | |
|---|---|
| **Now** | Independent Software Consultant · platform and AI-tooling engineering |
| **Before** | ServiceNow · Security Operations & Vulnerability Response · 2019–2025 |
| **Focus** | Developer tooling · distributed systems · keeping large codebases honest |

---

## Selected work · 2025 – present

### [propagate](https://github.com/Rupali59/propagate) — Claude Code plugin & CLI

Open-source tool that keeps files which must agree across many repositories from silently drifting.

- **1,200+ declared file couplings**, with drift derived from file *content* on demand rather than
  from a stored baseline.
- **Pre-tool hooks** put the matching known hazard in front of an agent before it runs a risky command.
- **Never edits a downstream file** — it finds and explains, a person approves, and the decision
  lands in an append-only ledger.
- Every detector ships a `selftest` proving it can fire, because a check that cannot fail reports success.

<sub>**v0.15.41**, released continuously · **283 test files** · Node · ESM · Claude Code plugin API</sub>

### Manuscript — Claude-assisted editorial plugin for Obsidian

- Findings tracked in a **Postgres review ledger**; the author decides each one.
- The agent side ships as a **Claude Code plugin with a hook and a skill**, so every request
  carries a stable, versioned instruction set.

<sub>**1.0.0 released** (private) · **210 test files** · second contributor onboarding · TypeScript · Postgres</sub>

### Legacy desktop software revival

A discontinued astrology product whose vendor is unreachable, brought back and rebuilt.

- Replaced its dead **Flash** dependency with a stub control; built an installer verified end to
  end on clean Windows 11 ARM.
- Decoded its proprietary chart format (**350/350 round-trip**) and migrated its database to SQLite.
- Re-implemented the calculation engine in **C#**, validated against the original's output — now
  the spec for a **Flutter rebuild for iOS, Android, macOS and Windows**.

<sub>C# · Windows · SQLite · Flutter</sub>

### Motherboard — multi-tenant API gateway

- **21 Go modules**; client services register as plugins and publish their own routes.
- Tenant → authentication → RBAC path working end to end behind a **fail-closed entitlement gate**,
  with scoped per-request tokens.
- Notification hub live on Telegram.

<sub>Go 1.25 · Docker</sub>

### Workflow engine cutover

For a service-business CRM with a database-driven, runtime-editable RBAC/ACL engine.

- Six-phase cutover that deleted the legacy passes only after freezing their outcomes as a
  **golden test** — surfacing five defects that existed only because the new graph had never executed.
- Test suite cut from **104s to 28s**: one shared `mongod` instead of 89, then per-suite index scoping.

<sub>Express · BullMQ · Redis · MongoDB · Next.js</sub>

### LLM classification pipeline

- Gemini under enforced response schemas at `temperature: 0`; determinism rests on
  cache-on-first-write rather than on the model.
- Keyword-classifier fallback, so a provider outage degrades quality instead of stopping ingestion.
- Model-proposed sources are **existence-checked against the live API**; an inconclusive check is
  flagged, never guessed.

<sub>TypeScript · Gemini · MongoDB</sub>

### Trading research

Contributed the research layer — edge estimators and a hypothesis framework — and a design-drift
ratchet with canaries to a team's algorithmic trading system.

<sub>Python · Next.js</sub>

---

**Currently completing** — Manuscript's next release · the cross-platform Flutter suite (design
approved) · Motherboard platform v1 · a release gate for propagate.

**Also built** — four production portfolio sites (Next.js, Playwright, WCAG 2.2 AA gates; a video
codec ladder from 9.9 MB to 2.3 MB) · a Shopify storefront with an embedded Remix admin · a FastAPI
astronomical-calculation service (**965 tests**) · a classical-text ingestion pipeline publishing
[Sanskrit-texts](https://github.com/Rupali59/Sanskrit-texts) · a job-radar Claude Cowork skill ·
the public [rtistic](https://rtistic.vercel.app) site · recovery of **154 unreachable git commits**
from a live repository.

<sub>Client work is described by what was built rather than by client name. Those repositories are private.</sub>

### How I work with AI agents

- **Deterministic where it can be, model where it must be.** Schemas, caches and fallbacks carry
  the reliability; the model gets only the part that genuinely needs judgement.
- **Hallucinations treated as invisible absences.** A made-up source reads as coverage, so every
  model-proposed source is checked against the real API before it is accepted.
- **Checks that prove they can fail.** Detectors and guardrails ship a `selftest` against a
  known-positive, and negative cases they must not match.
- **Human-in-the-loop by construction.** Agents propose; a person disposes. "Found nothing" and
  "looked at nothing" are different outputs, because only one of them is a pass.

---

## Experience

### Independent — Software Consultant
`Jun 2025 – present` · Remote

Platform and AI-tooling engineering for small businesses; building open-source developer tools
alongside client work. See [Selected work](#selected-work--2025--present).

### ServiceNow — Senior Software Engineer
`Mar 2022 – May 2025` · Security Operations & Vulnerability Response · Remote

- **[Dynamic Approval Rule Engine](https://www.servicenow.com/docs/r/washingtondc/servicenow-platform/approvals/c_ApprovalEngines.html)** —
  multi-level approval workflow for vulnerability deferment and exception requests, built on
  Flow Designer to stay configurable across differing enterprise policies. **40% faster approvals.**
- **[Background Job Processing Framework](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vr-background-framework.html)** —
  multithreaded framework for long-running work that previously strained system resources,
  with job status tracking, cancellation and ETA visibility. **Up to 60% performance gain**,
  **1M+ tasks/month**.
- **[Penetration Testing Request Catalog & Workflow Automation](https://www.servicenow.com/docs/r/security-management/application-vulnerability-response/pen-test-config-v16-1.html)** —
  catalog and automated workflows for pen-test requests across **50+ subsystems**, cutting manual
  intervention by **30%**.
- **Real-Time Data Aggregation Engine** — near real-time multi-dimensional analytics, processing
  **100K+ records per 8-hour cycle** to power internal dashboards.

### ServiceNow — Software Engineer
`Apr 2019 – Mar 2022` · Security Operations & Vulnerability Response · Hybrid

- **[Assignment Rule Engine](https://www.servicenow.com/docs/r/security-management/configuration-compliance/cc-assignment-rules.html)** —
  cache-optimised engine prioritising infrastructure vulnerabilities and policy violations and
  routing them to the right remediation groups. Runs daily over **1M+ vulnerable items**.
- **[ML-Based Assignment Recommendations](https://www.servicenow.com/docs/r/security-management/vulnerability-response/ml_view_assignment_recommendations.html)** —
  classification-based recommendations with feature engineering and a user-facing review
  interface. **+20% task allocation accuracy.**
- **[CISO & Vulnerability Dashboards](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vulnerability-mgmnt-CISO-dashboard.html)** —
  led design and development of the executive CISO dashboard and its supporting dashboards,
  defining the metrics and the data pipeline behind them. Adopted by **50+ organisations**.
- **[Vulnerability Source Integrations](https://www.servicenow.com/docs/r/security-management/vulnerability-response/vulnerability-response-common-content-pack.html)** —
  Veracode, Qualys, Tenable and Microsoft TVM, standardising **500K+ vulnerability records/day**
  into a common model for downstream remediation.
- **POA&M generator** — auto-generated **Plans of Action & Milestones** (required under
  **NIST SP 800-53** and **FedRAMP**) from vulnerability findings. Built at an internal hackathon and
  **adopted by the Now on Now support team**, who ran it against ServiceNow's own instance.
- **Hackathon projects** — Diagnostic Framework (**40%** less debugging time) · Predictive
  Intelligence clustering and time-to-remediate regression · high-volume data generator
  (**100M+ records across 20–30 tables**, adopted by the performance team).

<details>
<summary><b>Earlier roles</b> — Darwinbox · NowFloats · Finomena · Babajob (2016–2019)</summary>

### Darwinbox — Software Developer
`Aug 2018 – Mar 2019` · Hyderabad

- Audit-trail microservice capturing every client data modification — PHP/Yii tailing MongoDB
  oplogs and publishing to AWS SQS for downstream processing.
- Oplog diff processor in Node.js resolving changes across strings, arrays and nested documents
  into human-readable audit entries.

### NowFloats — Software Engineer
`Jun 2017 – Jul 2018` · Hyderabad

- Boost merchant portal's **customer-relationship surface** — enquiries, call logs and call
  tracking — serving **50,000+ merchant websites** (C#, JavaScript, Knockout.js).
- **Appointment-scheduling system** across merchant sites — per-staff availability, slot modelling,
  booking — in Node.js and C#, generic across clinic, salon, restaurant and hotel verticals.
- **SPIDER** sales-prediction model — per-representative revenue forecasting at **84% accuracy**;
  won the internal hackathon.
- Facebook Graph API integration for merchant product sharing; order management dashboard
  (AngularJS, C#).

### Finomena — Software Developer
`Feb 2017 – May 2017` · Bengaluru · *company wound down 2017*

- Loan management, mandate and collections dashboards for a small-ticket lending platform in
  PHP/Laravel, at **8,000+ loan applications/month**.
- **Message categorisation service** turning SMS content into structured credit signal, for a
  lender scoring borrowers with no credit history.

### Babajob — Software Engineer
`May 2016 – Jan 2017` · Bengaluru · *acquired by Quikr, Jun 2017*

- **TelephonySystem** — the Go service behind the missed-call job channel: a first call created
  the jobseeker's profile and later calls enriched it. **10,000+ inbound calls and 20,000+ outbound
  SMS per day** on RabbitMQ, Redis and MongoDB.
- **Automated matching pipeline** — each call published the profile for matching against open
  roles through Elasticsearch, with the shortlist sent by SMS.
- Search subsystem in Java over Elasticsearch, with dynamic query generation via Mustache templates.

</details>

---

## Earlier projects

| Project | Stack |
|---|---|
| **[HIMK](https://github.com/Rupali59/himk-implementation)** — human activity recognition with an HMM-based Intermediate Matching Kernel. M.Tech thesis, re-implemented in 2026 as a containerised Python pipeline | Python · scikit-learn · hmmlearn · OpenCV · Docker |
| **[MIS](https://github.com/Rupali59/MIS)** — institute management platform for students, faculty and administration | Next.js · MongoDB |
| **[Parking Lot](https://github.com/Rupali59/parking_lot)** — system-design allocation problem | Go |
| **[WorkTracker](https://rupali59.github.io/WorkTracker/)** — personal work dashboard and digital garden | TypeScript |
| **Voice Transcriber** — dockerised real-time speech-to-text *(private)* | Python · Docker |

---

## Technical skills

| | |
|---|---|
| **AI & agent tooling** | Claude Code plugins, hooks and skills · MCP · schema-constrained LLM output · eval harnesses and fixture-based regression suites · graceful degradation · human-in-the-loop design |
| **Languages** | Go · TypeScript · JavaScript · Python · C# · Java · PHP · C++ |
| **Web** | Next.js · React · Node.js · Express · FastAPI · Remix · Laravel · Tailwind |
| **Data & messaging** | PostgreSQL · MongoDB · MySQL · Redis · Elasticsearch · RabbitMQ · BullMQ · AWS SQS |
| **Cloud & tooling** | AWS · Vercel · Fly.io · Docker · GitHub Actions · Linux |
| **ML** | scikit-learn · hmmlearn · OpenCV · ServiceNow Predictive Intelligence |
| **Platforms** | ServiceNow SecOps · Vulnerability Response · Flow Designer · Shopify |

---

## Education

| Degree | Institution | Grade | Years |
|---|---|---|---|
| **M.Tech**, Computer Science & Engineering — Pattern Recognition & Machine Learning | NIT Goa | 8.42 CGPA | 2014–2016 |
| **B.E.**, Computer Science & Engineering · Honours | LNCT Bhopal (RGPV) | 8.58 CGPA | 2010–2014 |

---

## Certifications & awards

**AI, 2026** — **Anthropic:** 5 certifications across Claude, Claude Code and Claude Cowork.
**Google:** Gemini Enterprise Agent Ready · Create Your First Gemini Enterprise Application ·
Google Cloud Innovator · Developer Program Premium Tier · AI Fundamentals.

- **Geektrust GOLD** — **95.8** on the Metro Card backend challenge; Readability and
  Maintainability assessed at **ADVANCED**.
- **Winner**, NowFloats hackathon — the SPIDER sales-prediction module · 2018
- **Chancellor's Scholarship** — top 10 students statewide, RGPV Bhopal · 2012 and 2013
- **Silver Medal**, Persistent Systems Programming Contest · 2013
- **Teaching Assistant** and **Vice President**, CSE Department — NIT Goa · 2014–2016

<details>
<summary>Earlier certifications</summary>

WhatsApp API Expert, Wati (2024) · Ultimate JavaScript: Fundamentals, Code With Mosh (2025) ·
Neural Networks & Deep Learning, Coursera (2020) · JavaScript Algorithms & Data Structures,
freeCodeCamp (2020) · Git Essential Training, LinkedIn Learning (2020)

</details>

---

<div align="center">

**Open to senior software engineering roles with an AI focus** — remote or on-site.<br>
[Email me](mailto:rupalibhatnagar0509@gmail.com) · [LinkedIn](https://www.linkedin.com/in/rupali-bhatnagar-b4864957/)

</div>
