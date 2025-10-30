# Flask-Based Services

Curated blueprints, templates, and infrastructure patterns for building production-grade Flask applications with coordinated AI agents.

## Quickstart
1. Review `Python/Flask-Based/AGENTS.md` to understand the available agents and mandates.
2. Use `FlaskChefAgent` to scaffold backend services and `TemplateWeaverAgent` for frontend assets.
3. Run tests via `SmokeTestAgent` to validate routes, workers, and integrations.

## Components
- `app/` — application factory, blueprints, templates, and static assets.
- `services/` — domain-specific logic and integrations.
- `tests/` — pytest-based smoke and integration suites.

## Deployment Notes
- Provide `.env.example` files documenting required environment variables.
- Prefer containerized deployments with Gunicorn or uWSGI behind a reverse proxy.
- Track observability hooks (logging, metrics) in the "Monitoring & Observability" README section.
