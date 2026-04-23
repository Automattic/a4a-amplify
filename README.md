# Amplify by Automattic for Agencies

A Claude Code plugin that audits agency websites across conversion, trust, SEO, and AI readiness criteria. It returns a scored, actionable report.

Initially built for Automattic for Agencies Partner Managers as a sales tool: run an audit on an agency's site before or during a call, surface specific findings, and use them to drive meaningful conversations about what Automattic for Agencies products can improve. Amplify will expand into a self-serve benefit available to agencies directly through the [Automattic for Agencies](https://automattic.com/for-agencies/) tiering system.

> **Internal use only.** Amplify is not yet available to agencies. Do not share reports or tooling externally without approval.

## Built on Kosh

Amplify is built on the foundation of [Kosh](https://github.com/a8cteam51/kosh), the Claude Code plugin for WordPress site testing developed by the great minds on Team 51. Kosh's command, skill, and schema architecture is the backbone Amplify runs on, and several of its Playwright-based checks are reused directly.

### Kosh vs. Amplify: what they are and when to use each

| | Kosh | Amplify |
|---|---|---|
| **Purpose** | QA testing. Does the site work correctly? | Conversion audit. Will the site win clients? |
| **Question it answers** | Are there bugs, broken links, or accessibility failures? | Does this site build trust, convert leads, and surface well to AI tools? |
| **Pages tested** | 4 to 6 pages per audit, full site traversal | Homepage only |
| **Output** | Issues list categorized by severity | Weighted scores (Human Mode + AI Mode) with actionable prompts |
| **Audience** | Developers and QA engineers | Partner Managers and agency teams |
| **Use when** | You need to validate a site works before launch or after a build | You need to assess an agency's web presence for a sales conversation or improvement plan |

They are complementary, not competing. A site can pass every Kosh check and still score poorly on Amplify, and vice versa. Use both for a complete picture.

## What it does

Amplify evaluates an agency's homepage through two lenses:

- **Human Mode:** how a potential client perceives the site. Trust signals, contact and conversion, SEO, mobile experience, content quality, design and experience, accessibility, and audience resonance. 100-point score.
- **AI Mode:** how AI tools perceive the site. Technical health, structured data, AEO readiness, E-E-A-T signals, content freshness, entity clarity, content specificity, and llms.txt. 100-point score.

Each audit visits the homepage only, runs programmatic DOM checks via Playwright, captures screenshots for visual AI analysis, extracts copy for content analysis, scores every signal against a defined rubric, and outputs a structured report with copy-paste Claude prompts agencies can use to act on findings immediately.

## Quick start

```bash
git clone https://github.com/Automattic/a4a-amplify.git
cd a4a-amplify
claude --plugin-dir .
```

On first run, Claude Code will ask you to trust this project's settings. Accept the prompt. This pre-approves the Playwright browser tools so you are not prompted for each one during an audit.

Then run an audit:

```
/amplify https://agencysite.com
```

For detailed setup instructions, see the [Getting Started guide](docs/getting-started.md).

## Score thresholds

Both Human Mode and AI Mode are scored independently on a 100-point scale.

| Score | Status |
|---|---|
| 80 – 100 | Strong |
| 50 – 79 | Needs work |
| 0 – 49 | At risk |

## Project structure

```
commands/        Slash command (/amplify)
skills/          Full audit procedure (skills/amplify/SKILL.md)
schemas/         JSON schema for report output validation
scripts/         Report generation and formatting scripts
hooks/           Session hook that creates reports/data/ on startup
.mcp.json        Playwright MCP server configuration
.claude/         Project settings and Playwright tool permissions
```

### How commands, skills, and schemas relate

| Component | File | Purpose |
|---|---|---|
| Command | `commands/amplify.md` | Parses the URL and delegates to the skill |
| Skill | `skills/amplify/SKILL.md` | Full five-phase audit procedure |
| Schema | `schemas/amplify-report-schema.json` | Defines and validates the JSON report output |

## Report structure

```json
{
  "url": "https://agencysite.com",
  "agencyName": "Agency Name",
  "timestamp": "2026-04-23T10:00:00.000Z",
  "humanMode": {
    "score": 74,
    "threshold": "amber",
    "criteria": {}
  },
  "aiMode": {
    "score": 52,
    "threshold": "amber",
    "criteria": {}
  },
  "issues": {
    "critical": [],
    "high": [],
    "medium": [],
    "low": []
  },
  "actionablePrompts": []
}
```

Full schema definition is in `schemas/amplify-report-schema.json`.

## Roadmap

**Phase 1: Claude Code plugin (current)**
Partner Managers run `/amplify` from Claude Desktop, enter an agency URL, and receive a scored report. Goal: validate the scoring model with real agencies before a full product build.

**Phase 2: Agency self-serve**
Amplify is distributed directly to agencies as a Claude plugin. Agencies run audits themselves, on demand, without a PM facilitating.

**Phase 3: Platform integration**
Amplify is integrated natively into the Automattic for Agencies dashboard. Agencies audit connected sites directly from their account, no manual URL entry required.

**Phase 4: Client site audits**
Agencies audit prospective client sites as a prospecting and sales tool. Walk into a pitch with a scored report already in hand.

## Contributing

### Adding or editing the skill

The skill file (`skills/amplify/SKILL.md`) is a structured prompt, not code. It tells Claude exactly what to check, in what order, and how to score and report it. When editing:

- Keep instructions explicit and mandatory. Claude follows these literally, so vague language produces inconsistent results.
- Maintain the five-phase structure: programmatic audit, visual analysis, content analysis, scoring, report generation.
- Test changes by running `/amplify` against a real agency site and reviewing the JSON output.

### Adding or editing the schema

If you change what the skill collects, update `schemas/amplify-report-schema.json` to match. The report generation scripts depend on this structure.

## Git workflow

- **Main branch:** `trunk`
- **Branch prefixes:** `feature/`, `fix/`, `update/`, `add/`, `remove/`
- **Commit style:** conventional commits. `feat:`, `fix:`, `docs:`, `chore:`
- **Merge strategy:** squash merge preferred for feature branches
