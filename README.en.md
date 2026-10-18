# autoreview

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![AI Review](https://img.shields.io/badge/AI-code%20review-brightgreen.svg)](SKILL.md)

SynomosAI four-pillar system: **Identity · Traceability · Governance · Symbiosis**.

> This repo is part of the [SynomosAI](https://github.com/SynomosAI) skill ecosystem.

**Keywords**: automated code review · AI PR review · security scanning · structured review report

## Quick Start

This repo is an **Agent Skill** (SKILL.md spec).

```bash
git clone https://github.com/SynomosAI/autoreview.git
cd autoreview
cat SKILL.md
```

```bash
# PR mode:
gh pr view <PR-number> --json files,title,body
gh pr diff <PR-number>
# Local mode:
git diff main...HEAD
```

## What this skill covers

AI-powered automated code review generating a structured report across four dimensions:

1. 🔴 Security vulnerabilities: injection, XSS, auth bypass, sensitive data leakage
2. 🟡 Code standards: naming, complexity, duplication
3. 🟡 Performance: N+1 queries, unnecessary computation, memory leaks
4. 💭 Maintainability: comments, test coverage, error handling

Each issue includes file+line location, risk level (🔴/🟡/💭), and a fix suggestion.

## License

MIT License. © 2026 注册老炮@MedXpert.

## Disclaimer

This repo is a theoretical-positioning and tooling exploration; verify external standards independently before formal citation.
