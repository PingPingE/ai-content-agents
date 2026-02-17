# AI Content Agents

Multi-agent content automation for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).
4 AI agents + 7 slash commands — write, review, edit, and fact-check content from your terminal.

## Who is this for?

- **Technical writers** — documentation workflow automation
- **DevRel engineers** — blog posts, tutorials, API docs at scale
- **Content teams** — consistent quality with built-in review cycles
- **Documentation teams** — docs-as-code pipelines
- **Solo creators** — AI editor, reviewer, and fact-checker on every piece

## When to use

| Situation | Command |
|-----------|---------|
| New content from scratch | `/content-pipeline <brief>` |
| Polish a rough draft | `/edit-content <file>` |
| Quality-check before publishing | `/review-content <file>` |
| Verify facts in existing content | `/fact-check <file>` |
| Pre-publish build checks | `/ship` |

## Quick Start

```bash
git clone https://github.com/PingPingE/ai-content-agents.git
cp -r ai-content-agents/.claude/ /path/to/your/project/
cd /path/to/your/project && claude
```

```
/content-pipeline Blog post about API rate limiting for Node.js developers
```

This single command runs the full pipeline:

```
Research → Draft → Review (30-point rubric) → Edit → Fact-check → Final polish
```

Output: publication-ready markdown + quality report.

## Agents

| Agent | Role |
|-------|------|
| **content-writer** | Drafts content, researches via WebSearch, orchestrates other agents |
| **content-reviewer** | Scores on 6 dimensions (accuracy, clarity, style, structure, completeness, audience). Read-only. |
| **editor** | Three-pass polish (structure → clarity → grammar). Targets 20% word reduction. |
| **fact-checker** | Verifies every claim, stat, and quote via WebSearch. Read-only. |

## Commands

| Command | What it does |
|---------|-------------|
| `/content-pipeline <brief>` | Full automated pipeline — research through fact-check |
| `/write-content <topic>` | Draft with auto-review loop |
| `/review-content <file>` | 6-dimension scored review (APPROVE / REVISE / REJECT) |
| `/edit-content <file>` | Style and clarity polish |
| `/fact-check <file>` | Claim verification with confidence levels |
| `/ship` | Pre-publish check (build + lint + types) |
| `/auto-fix` | Auto-fix build/lint/type errors |

## Supports

Blog posts, tutorials, API docs, and landing pages — each with built-in templates and word count guidelines.

See [ORCHESTRATION_HELPER.md](./ORCHESTRATION_HELPER.md) for detailed usage, customization, and workflow examples.

## Related

- [claudetemplate.com](https://claudetemplate.com) — production-grade Claude Code agent templates
- [claude-code-agent-template](https://github.com/PingPingE/claude-code-agent-template) — more open-source templates (starter, PR review, bug fix, code quality)

## License

MIT
