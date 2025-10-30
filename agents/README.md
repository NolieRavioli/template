# Advanced Multi-Agent Playbooks

This repository houses curated **AGENTS.md** playbooks that describe how specialized AI collaborators should operate within different language or framework ecosystems. Use these documents to bootstrap consistent multi-agent workflows, enforce coding standards, and clarify responsibilities across your team.

## Getting Started

1. Choose the technology stack you are working on (Python basics, Flask web apps, or C++ basics).
2. Open the corresponding `AGENTS.md` to understand which meta agent coordinates the work and which specialist agents are available.
3. Follow the README in that directory for quickstart setup, tooling expectations, and contribution guidelines.

## Quick Links

- [Python — Basic Toolkit](Python/Basic/README.md)
- [Python — Flask-Based Services](Python/Flask-Based/README.md)
- [Python — Eve Data Framework](Python/Eve-Data-Framework/README.md)
- [C++ — Basic Toolkit](C++/Basic/README.md)

## Charter Overview

| Subtree | AGENTS Charter | Key Capabilities |
| --- | --- | --- |
| `Python/Basic/` | [Advanced Multi-Agent Guide for Python Projects](Python/Basic/AGENTS.md) | Meta-driven orchestration for core Python utilities with code, documentation, testing, infra, security, packaging, data, auth, and utility specialists.
| `Python/Flask-Based/` | [Flask-Oriented Multi-Agent Guide](Python/Flask-Based/AGENTS.md) | Web-focused delegation covering backend APIs, templating, front-end assets, authentication, deployment, QA, and observability agents coordinated by a meta agent.
| `Python/Eve-Data-Framework/` | [Eve Data Framework Agent Charter](Python/Eve-Data-Framework/AGENTS.md) | Schema-driven REST services on Eve with agents for resource design, hooks, security, deployment, and documentation.
| `C++/Basic/` | [Advanced Multi-Agent Guide for C++ Projects](C++/Basic/AGENTS.md) | Structured support for C++ source, build, documentation, testing, packaging, performance, safety, and cross-language integration led by a meta coordinator.

## Usage Tips

- Each directory’s README provides stack-specific setup steps, tooling conventions, and quality gates.
- The `MetaAgent` in every charter interprets requests, activates the right specialists, and explains delegation decisions—consult it when planning complex tasks.
- Extend or adapt these charters by adding new agents or adjusting scopes to match your organization’s practices.

## License

Distributed under the terms of the [MIT License](LICENSE).
