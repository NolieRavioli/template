# EVE Data Framework 3 Agent Playbook

Updated on 2025-10-29

## Overview
This playbook explains how the multi-agent charter supports **EVE Data Framework 3**, a self-hosted operations hub that bootstraps the runtime from `main.py`, pulls data from ESI and the Static Data Export (SDE), stores information in coordinated SQLite databases, and presents dashboards plus manual refresh tools through the Flask UI under `webUI/`.

Use this document with [`AGENTS.md`](AGENTS.md) to align autonomous contributors with the project’s modules:
- Runtime bootstrap (`main.py`, `util/utils.py`, `config.yaml`)
- Data ingestion (`esi/`, `util/esi_rate_limiter.py`, `util/sde.py`)
- Storage (`db/database.py`, `db/models.py`, `_publicData/`, `_privateData/`)
- Analytics (`analysis/`)
- Web experience (`webUI/` templates, blueprints, console streaming)
- Authentication (`util/auth.py`)
- Documentation (`docs/`, this README)

## Quickstart for Agents
1. **Study the Runtime Flow**: Read `main.py` and `util/utils.py` to understand how configuration, auto-install, logging, and Flask startup are sequenced.
2. **Inspect Data Pipelines**:
   - Review `esi/personal_*` and `esi/public/*` modules to see how tokens are requested, ESI calls are coalesced, and responses merged into SQLite.
   - Explore `util/esi_rate_limiter.py` for caching/rate limiting rules and `util/sde.py` for SDE processing.
3. **Examine Storage Layout**:
   - Public data resides in `_publicData/public.db` via `db/models.py`’s `PublicBase`.
   - Private owner databases live under `_privateData/<owner_id>/<owner_id>.db` driven by `PrivateBase` models.
4. **Walk Through the UI**:
   - `webUI/__init__.py` constructs the Flask app and registers blueprints from `dashboard.py`, `personal_routes.py`, and `public_routes.py`.
   - `webUI/templates/console_output.html` mirrors log streams for long-running tasks before redirecting back to the dashboard.
5. **Understand Authentication**: `util/auth.py` stores Fernet-encrypted tokens, while `util/utils.get_token` refreshes credentials lazily for each owner.
6. **Map Analytics to UI**: Modules in `analysis/` (e.g., `analysis/job_slots.py`, `analysis/structures.py`) compute metrics surfaced on the dashboard.
7. **Coordinate via OpsMetaAgent**: Before coding, request a plan from the MetaAgent so it can sequence RuntimeBootstrapEngineer, WebUIDashboardMaestro, ESIIngestionSpecialist, AnalysisInsightsAgent, DatabaseCartographer, AuthSecuritySentinel, and OperationsChronicler as required.

## Agent Roster
| Agent | Focus | Key Deliverables |
| --- | --- | --- |
| OpsMetaAgent | Multi-subsystem orchestration | Delegation plans, conflict checks, mandate verification |
| RuntimeBootstrapEngineer | Startup flow & runtime settings | `main.py`, `util/utils.py`, `config.yaml`, dependency manifests |
| WebUIDashboardMaestro | Flask dashboards & console UX | Blueprint wiring, template updates, session safety reviews |
| ESIIngestionSpecialist | ESI/SDE pipelines & rate limiting | Fetcher modules, retry logic, log instrumentation |
| AnalysisInsightsAgent | Derived metrics for dashboards | `analysis/*.py`, reporting hooks, UI integration notes |
| DatabaseCartographer | Public/private SQLite stewardship | Model updates, initialization routines, migration guidance |
| AuthSecuritySentinel | OAuth token handling & RBAC | `util/auth.py`, secure config defaults, audit logs |
| OperationsChronicler | Documentation & onboarding | README updates, FAQs, architecture diagrams |

## Collaboration Workflow
1. **Plan**: Invoke the OpsMetaAgent when a request spans multiple domains (e.g., adding a new refresh job that touches `esi/`, `analysis/`, and `webUI/`).
2. **Implement**: Specialists execute within their domains, referencing the mandates in `AGENTS.md` to ensure hooks, schemas, and UI routes remain consistent.
3. **Document**: OperationsChronicler updates this README or supporting docs with new runtime flags, refresh paths, or troubleshooting steps.
4. **Verify**: Run targeted checks—`python -m compileall`, integration scripts, or UI walkthroughs—to confirm the operations hub still boots cleanly and routes produce expected console output.
5. **Release**: Summarize changes, update the changelog, and align deployment instructions (container definitions, `.env.example`) when relevant.

## Best Practices
- Keep `RuntimeSettings` in sync with `config.yaml`; document every new flag.
- Funnel all outbound ESI requests through `util/esi_rate_limiter.py` to benefit from caching and TTL enforcement.
- Preserve the dual-database boundary—never persist private character data to the public database or expose it via public routes.
- Emit structured logs so console streaming and future log aggregation stay machine readable.
- When extending analysis modules, provide UI fallbacks (e.g., “N/A”) if source data is stale or unavailable.
- Support headless operation by exposing CLI entry points that mirror dashboard actions whenever feasible.

## Troubleshooting Cheat Sheet
| Symptom | Likely Cause | Where to Look |
| --- | --- | --- |
| Auto-install loop during startup | Missing `Runtime.auto_install` guard or dependency pin mismatch | `main.py`, `util/utils.py`, `requirements.txt` |
| Console page never redirects | Log tee buffer not flushed or countdown missing | `webUI/templates/console_output.html`, `webUI/personal_routes.py` |
| Duplicate market rows | Upsert logic not idempotent or cache TTL ignored | `esi/public/markets.py`, `db/models.py` |
| Token refresh failures | Fernet key mismatch or expired refresh token | `util/auth.py`, `_privateData/<owner>.db` |
| Stale dashboard metrics | Analysis module not invoked or missing fallback | `analysis/*.py`, `webUI/dashboard.py` |

## Contribution Guidelines
1. Update both `AGENTS.md` and this README whenever agent roles, mandates, or cross-team workflows change.
2. Provide sample console output snippets or dashboard screenshots when altering long-running jobs or UI layouts.
3. Run linting (`ruff`), typing (`mypy`), and targeted smoke tests (`python -m compileall Python/Eve-Data-Framework`) before submitting work.
4. Add changelog entries describing operational impact, including schema migrations or new refresh capabilities.

## Changelog
- **2025-10-29** — Rebuilt the agent charter and documentation to mirror the EVE Data Framework 3 runtime, ingestion, storage, UI, analysis, and security architecture.
- **2025-10-29** — Initial Eve Data Framework agent suite published.
