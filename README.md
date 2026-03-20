# kosh

A Claude Code plugin for testing WordPress sites. Run automated functional, performance, and accessibility audits against any live URL using real browser automation via Playwright MCP.

## What it does

Kosh tests a site across three dimensions:

- **Functional & design:** User journeys, layout consistency, link validation, OpenGraph metadata, content quality
- **Performance:** Load times, console errors, network failures, mixed content
- **Accessibility:** WCAG 2.2 Level AA compliance: heading hierarchy, alt text, color contrast, keyboard navigation, form labels, ARIA

Each test visits 4–6+ pages, simulates real user behavior, and outputs a structured JSON report. An optional script converts any report to a formatted Markdown document, and a merge script combines all three into one comprehensive report.

## Prerequisites

- [Claude Code](https://claude.ai/code) 1.0.33 or later
- Node.js (for report generation scripts)
- Playwright MCP — installed automatically on first run via `npx @playwright/mcp@latest`

## Setup

Clone the repo:

```bash
git clone https://github.com/katodea/kosh.git
cd kosh
```

Load the plugin when starting Claude Code:

```bash
claude --plugin-dir .
```

The `reports/data/` directory is created automatically when a session starts.

## Usage

All three commands accept a URL as the argument.

**Functional & design test**
```
/kosh:functional-design https://example.com
```

**Performance test**
```
/kosh:performance https://example.com
```

**Accessibility test**
```
/kosh:a11y https://example.com
```

Each command navigates to the URL, walks through multiple pages, and saves a JSON report and a formatted Markdown report to `reports/`. JSON reports are overwritten on each run — save or rename them before testing a new site if you need to keep them.

## Combining reports

After running all three tests, merge them into one comprehensive report:

```
/kosh:merge
```

## Project structure

```
commands/        Slash commands (/kosh:a11y, /kosh:functional-design, /kosh:performance)
skills/          Full testing procedures for each command
schemas/         JSON schemas for report validation
scripts/         Report generation and merge scripts
hooks/           Session hook that creates reports/data/ on startup
.mcp.json        Playwright MCP server configuration
.claude/         Project settings and Playwright tool permissions
```

## Report structure

All reports follow the same shape:

```json
{
  "url": "https://example.com",
  "websiteName": "Example",
  "timestamp": "2026-03-20T10:00:00.000Z",
  "visitedPages": ["https://example.com", "..."],
  "mobile": { ... },
  "desktop": { ... },
  "issues": {
    "critical": [],
    "high": [],
    "medium": [],
    "low": []
  }
}
```

Schema definitions are in `schemas/`.
