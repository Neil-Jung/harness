# HARNESS.md — Personal Multi-Agent Harness (v2)

> Binding constitution for agents. Stack-specific commands live in each project; this file defines invariants.  
> Contract index (tiers/roles/sensors): [`harness/`](harness/).  
> Copyable runtime artifacts: [`templates/`](templates/) · bootstrap cards: [`harness/templates/`](harness/templates/).

## 0. Purpose

Orchestrate AI productivity under human control:

- no implementation before sign-off  
- risk- and platform-scoped gates  
- file-backed state  
- vendor isolation  
- separated build vs review  
- clean remote history on R1  

### Agent invariants (MUST)

1. **No Y, No Code** — Until `SIGN-OFF.md` exists for the current scope, write no implementation code (spec/decision files only).
2. **Select risk** — `R0` (experiment) or `R1` (operating). Gates scale with risk, not stack.
3. **Select platform** — `Web` | `App` | `Other`. Enforce only that profile’s resource guards.
4. **Files are SoT** — If it is not in SPEC / DECISIONS / SIGN-OFF / DEBUG / HUMAN_GATES, it does not exist. Hand off via `@path`.
5. **Infrastructure abstraction** — Business/UI MUST NOT call vendor SDKs directly; adapters only.
6. **Build ≠ Review** — Implementers MUST NOT be the final gate for their own changes.
7. **R1 deployment** — Staging pass + squash-to-one remote push required (R0: recommended).

### Core loop

```
Idea
  → SPEC.md (detailed) + 3–4 human-facing decision prompts
  → SIGN-OFF.md (risk + platform + confirmed scope)
  → Data / infra guards
  → Platform resource guards (Web/App)
  → Implement (BE/FE or UI) + independent review suite
  → Staging (R1) → squash & push (R1) → DEBUG dual asset (human + agent)
```

Architecture-breaking mid-flight asks → DECISIONS impact note → isolate in new folder → promote after validation.

### Meta rule

If this harness fights a project, **change this file** (append §9 Retrospect). Do not contort the project.

### Activation gate (efficiency)

**Do not run the full harness loop on micro work.** Micro = bugfix / UI polish / copy / CSS / small tweak inside an already signed-off scope with no new data model, adapters, auth, storage, deploy, or irreversible side effects.

**Do activate the harness** when the ask needs SPEC / DECISIONS / SIGN-OFF, new or changed infrastructure, architecture forks, risk/platform re-selection, or irreversible external effects.

When harness-controlled: agents MUST open with an explicit **하네스 통제 작업** confirmation (why, R0/R1, platform, next gate). Cursor rule: `.cursor/rules/harness-activation.mdc`.

---

## 1. Philosophy

### 1.1 Hybrid planning (Waterfall + Agile)

- **Waterfall lock (macro):** directory topology, data architecture, and core plan are fixed before implementation. Do not casually mutate them without SPEC + DECISIONS updates and human sign-off when scope changes.
- **Agile loop (micro):** feature slices and bugfixes iterate under the locked plan: implement → review → fix.

### 1.2 Context-driven tradeoffs

No universally best algorithm/architecture. Agents MUST state the tradeoff among **readability · performance · resource cost · money cost** for current data scale and purpose.

Forbidden defaults: context-free spaghetti; prestige over-engineering without a stated need.

### 1.3 Infrastructure abstraction

DB/deploy vendor (Supabase, NCP, private NAS, on-prem, …) MUST be swappable without editing business logic or UI. Vendor APIs live only behind adapters (§5.A).

---

## 2. Risk (R0 / R1) · Platform profile

Both MUST be chosen at sign-off and written into `SIGN-OFF.md`.

### 2.1 Risk

| | **R0 experiment** | **R1 operating** |
|---|---|---|
| Criteria | No real users, no irreplaceable third-party data, no irreversible external side effects | Any of: real users, real/irreplaceable data, irreversible side effects (billing, send, public deploy, …) |
| Human gate | Summary confirm only | Summary confirm + non-empty `HUMAN_GATES.md` |
| Review suite | Efficiency + QA | Efficiency + QA + Resource + Security when public/sensitive |
| Staging | Recommended | **Required** |
| Squash & single remote push | Recommended | **Required** |

```
Real users now?
  yes → R1
  no → Irreplaceable third-party data?
         yes → R1
         no → Irreversible external side effects?
                yes → R1
                no → R0
```

Risk is independent of Web vs App vs codebase size.

### 2.2 Platform profile

Exactly one profile active. Enforce only that profile’s §5 resource section.

| Profile | Enables | Disables |
|---|---|---|
| **Web** | Browser RAM/CPU/paging; FE/BE split | Native lifecycle as requirements |
| **App** | Lifecycle, background/battery/permissions, chunked local data | Browser re-render / virtual-scroll mandates |
| **Other** | Shared invariants only | Web- and App-specific sections |

**Always on:** R0/R1, file SoT, No Y No Code, adapter lock when external I/O exists, Build ≠ Review, deployment gates per risk table.

---

## 3. Artifacts (file SoT)

Conversation is not durable state. Missing file ⇒ missing fact.

Templates: [`templates/`](templates/) · card/sprint/evaluator: [`harness/templates/`](harness/templates/)

| Artifact | When | Contents |
|---|---|---|
| `SPEC.md` | Before sign-off | Data, deps, directories, adapter map, bottleneck algorithms |
| `DECISIONS.md` | Each fork | Options, choice, rationale, rejected, impact |
| `SIGN-OFF.md` | Human confirm | Scope, **R0/R1**, **Web/App/Other**, date, pointers |
| `HUMAN_GATES.md` | **Required on R1** | Irreversible / non-automatable approvals; MUST NOT be empty on R1 |
| `debug/DEBUG.md` + `DEBUG.human.md` + `DEBUG.agent.md` (or project-root equivalents) | End of loop / after notable fix | **Dual SoT** in a project `debug/` folder when present: index + human narrative + agent prevention log (always write both companions) |

**Agent rules:** do not cite “chat decisions”—open the file; SPEC/DECISIONS changes precede code; reinject **`debug/DEBUG.agent.md`** (or root `DEBUG.agent.md`) on related work (humans read **`DEBUG.human.md`**); when appending debug, update **both** companions in one turn; Korean body OK in human file; keep ASCII filenames; prefer project `debug/` folder, names stable.

---

## 4. Stages · Exception protocol

**Model grades (no product names):** assign by capability, not vendor.

| Role | Grade | Why |
|---|---|---|
| Planner | **Strongest** reasoning | Stage 1 + architecture impact; early mistakes cascade |
| Implementer | Mid-tier OK | Plan is locked; execution is more mechanical |
| Reviewer | **Strongest** reasoning | Separate pass; hard judgment; no self-final-gate |

### Stage 1 — Macro plan (Waterfall)

1. Full detail → `SPEC.md` (**not** a task checklist alone — see Planner depth below).
2. Human sees only: confirmed core capabilities + 3–4 decision forks.
3. Lock risk + platform in `SIGN-OFF.md`.
4. **No Y, No Code** until SIGN-OFF exists (allowed: SPEC/DECISIONS/SIGN-OFF/HUMAN_GATES drafts).
5. Domain directory map + module interface boundaries in SPEC.

#### Planner depth (MUST) — handoff to mid-tier Implementer

Planner exists because Implementer may be mid-tier. A plan that only lists process steps (“1 make API 2 wire UI 3 test”) is **insufficient** and MUST be rejected/rewritten.

`SPEC.md` MUST include what a weaker model is unlikely to infer unaided:

| Slot | Required content |
|---|---|
| **Non-obvious coding skills** | Patterns, invariants, anti-patterns, API/contract pitfalls, concurrency/ordering, idempotency, authz boundaries, adapter usage — anything the Implementer would otherwise “invent” wrongly |
| **Edge cases** | Empty/null/partial data, race/double-submit, offline/retry, permission denial, large lists, timezone/locale, upgrade/migration, failure modes + expected behavior |
| **Acceptance probes** | How to know each edge is handled (test idea, manual check, or assert) — not “works on happy path” |
| **Explicit non-goals** | What not to build / not to over-engineer |

Forbidden SPEC smell: only numbered workflow with no skills, edges, or probes.  
Allowed human surface stays thin (3–4 forks); depth lives in the file for the Implementer.


### Stage 2 — Data & infra

Enforce §5.A–B.

### Stage 3 — Resources (profile-scoped)

Enforce §5.C (Web) or §5.D (App) or §5.E (Other).

### Stage 4 — Implement & review (Agile)

| Production | Responsibility |
|---|---|
| Backend | Schema/API/business logic/skeleton via adapter interfaces |
| Frontend / UI | UI + design system for active profile; own the slice end-to-end |

| Review | Checks | Activation |
|---|---|---|
| Efficiency | Complexity, readability, duplication, over-engineering | Always |
| QA | Exceptions, edges, runtime failures | Always |
| Resource | Leaks, churn, unnecessary load | R1 and/or platform resource rules |
| Security | Authz, injection, exposure, rate limits, … | **Dynamic:** ON only if public surface and/or sensitive data |

### Stage 5 — Staging & VCS

1. Local commits unrestricted.  
2. Staging validation (**required R1**).  
3. Squash + single remote push (**required R1**).  
4. Append **both** `DEBUG.human.md` + `DEBUG.agent.md` under project `debug/` (root `DEBUG.md` may point there); reinject agent file later.

### Exception — architecture-breaking mid-flight

1. Impact assessment → `DECISIONS.md`.  
2. Isolate in dedicated folder (e.g. `src/features/<name>/`); do not touch existing paths.  
3. After validation, promote shared logic and rewrite directory map in one controlled refactor.

---

## 5. Guards (data · infra · resources)

### 5.A Infrastructure abstraction [LOCK]

**MUST NOT:** vendor APIs inside business/UI (e.g. scattered `.from().select()`).

**MUST:** (1) I/O contracts in an interface module; (2) concrete adapters in an isolated directory (`supabase`, `naverCloud`, `privateNas`, …); (3) vendor migration edits **adapter files only**.

Paths declared in project `SPEC.md` (Web example: `src/common/database/interface.ts` + adapter files).

### 5.B Data shape

- **Flat First:** bulk data → 1D table-like structures + FK mappings; nested 2D/3D arrays exceptional.
- **Node–link:** sparse complex M:N → nodes + links, not nested multi-dim loops. Name bottleneck algorithms in SPEC (e.g. BFS hop-distance).

### 5.C Web profile

| Concern | Rule |
|---|---|
| RAM | Subscriptions/timers/listeners MUST cleanup on teardown |
| CPU | Memoize hot paths; debounce/throttle high-freq input; re-render changed subtrees only |
| Network/memory | Bulk fetch via paging (~20–50) and/or virtualized lists |

Inactive if profile ≠ Web.

### 5.D App profile

| Concern | Rule |
|---|---|
| Leak | Unsubscribe on screen/app teardown |
| Battery/background | Background work & permissions declared in SPEC; no silent abuse |
| Local bulk | Chunk/page loads; no full hydrate by default |

Inactive if profile ≠ App.

### 5.E Other profile

§5.C–D OFF. If external I/O exists, §5.A–B still apply. Extra constraints only via SPEC.

---

## 9. Retrospect

Friction ⇒ fix this harness; append below.

**When:** ignored rules, expensive misfire, model/tool upgrade obsolete scaffolding.

```
### YYYY-MM-DD · title
- **trigger**:
- **remove**:
- **add**:
- **outcome**:
```

### 2026-08-14 · Planner depth: skills + edges mandatory

- **trigger**: Plans that only list process steps leave mid-tier Implementers to invent coding skill and edge handling.
- **remove**: Implicit “SPEC = task list is enough”.
- **add**: §4 Planner depth (non-obvious skills, edge cases, acceptance probes, non-goals); SPEC template slots; `harness/20-roles.md` Planner depth MUST.
- **outcome**: Thin human prompts stay; deep handoff lives in SPEC.

### 2026-08-14 · Model assignment by grade only

- **trigger**: Product names (e.g. Fable) in Planner line pinned the harness to vendors.
- **remove**: Named-model examples in stage protocol.
- **add**: Role × grade table (Planner/Reviewer = strongest; Implementer = mid-tier OK); no vendor product names.
- **outcome**: §4 model grades only.

### 2026-07-18 · Re-hydrate harness/ contract index (plan)

- **trigger**: Plan “개인 하네스 엔지니어링 구조” — `harness/` missing while v2 constitution remained.
- **remove**: Nothing from v2 single-file norms.
- **add**: `harness/00–90` stack-neutral contract index + `harness/templates/*` (project-card, sprint, handoff, evaluator, bootstrap); adoption notes in `harness/90-retrospect.md`.
- **outcome**: Plan layout restored as index; normative text stays in this file.

### 2026-07-14 · Activation gate + dual DEBUG + confirm banner

- **trigger**: Full harness on micro UI/bugfix is inefficient; owner wants harness only when controlled elements apply, with an explicit confirmation message; dual human/agent DEBUG under `debug/`.
- **remove**: Implicit “always treat every chat as harness stage-1”.
- **add**: Activation gate (Micro vs Harness-controlled); required **하네스 통제 작업** banner when active; `.cursor/rules/harness-activation.mdc`; project `debug/DEBUG.{md,human,agent}.md`.
- **outcome**: Agents skip full loop on micro work; announce harness control when gates matter.

### 2026-07-13 · Adopt harness v2 (owner-controlled)

- **trigger**: Prior AI-recommended harness (tiers/sensors/PGE) was not owner-operated; need vendor isolation, platform branching, file SoT, Waterfall+Agile multi-agent pipeline.
- **remove**: Legacy split harness docs/templates.
- **add**: Single `HARNESS.md` + `templates/*`; R0/R1; Web/App/Other; adapter lock; No Y No Code; split review; staging+squash; isolate→promote.
- **outcome**: Consolidated constitution; templates at `templates/`.

### 2026-07-13 · Consolidate to one constitution file

- **trigger**: Split topic files added lookup cost without benefit at this size.
- **remove**: `harness/00–90*.md` multi-file layout.
- **add**: All normative rules in this file; keep `templates/` only.
- **outcome**: This file.
