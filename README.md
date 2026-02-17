# AI Content Agents

Multi-agent content automation for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Write, review, edit, and fact-check content — all from your terminal.

4 specialized AI agents and 7 slash commands that turn Claude Code into a full editorial team.

## Who is this for?

- **Technical writers** automating documentation workflows
- **DevRel engineers** producing blog posts, tutorials, and API docs
- **Content teams** that need consistent quality with built-in review cycles
- **Solo creators** who want an AI editor, reviewer, and fact-checker on every piece
- **Documentation teams** managing docs-as-code pipelines

## What it does

One command runs the entire content lifecycle:

```
/content-pipeline Blog post about API rate limiting for Node.js developers
```

```
Phase 1  Parse brief        → topic, type, audience, constraints
Phase 2  Research            → 5-8 credible sources via WebSearch
Phase 3  Draft               → structured content from template
Phase 4  Review              → 6-dimension scored review (30-point rubric)
Phase 5  Edit                → three-pass polish, 20% word reduction
Phase 6  Fact-check          → every claim verified with confidence levels
Phase 7  Final polish        → corrections applied, quality report generated
```

Output: publication-ready markdown + quality report with scores.

## Quick Start

```bash
# Clone
git clone https://github.com/PingPingE/ai-content-agents.git

# Copy into your project
cp -r ai-content-agents/.claude/ /path/to/your/project/

# Open Claude Code in your project
cd /path/to/your/project
claude
```

```
/content-pipeline Tutorial about setting up authentication with JWT
```

## Agents

| Agent | Model | Mode | Role |
|-------|-------|------|------|
| **content-writer** | sonnet | acceptEdits | Drafts blog posts, tutorials, API docs, landing pages. Has WebSearch for research. Orchestrates other agents via Task. |
| **content-reviewer** | sonnet | plan (read-only) | Scores content across 6 dimensions (accuracy, clarity, style, structure, completeness, audience). Cannot modify files — only evaluates. |
| **editor** | sonnet | acceptEdits | Three-pass editing: developmental, line, copy. Targets 20% word reduction while preserving author voice. |
| **fact-checker** | sonnet | plan (read-only) | Verifies statistics, quotes, technical claims, and links via WebSearch. Reports confidence: Verified / Likely / Unverified / Incorrect. |

### Separation of concerns

- **Writers write.** content-writer has `Edit`, `Write`, `WebSearch`, and `Task`.
- **Reviewers evaluate.** content-reviewer has read-only tools and `plan` mode — it scores but cannot change files.
- **Editors refine.** editor has `Edit` and `Write` but no `WebSearch` — it polishes prose, not facts.
- **Fact-checkers verify.** fact-checker has `WebSearch` but no `Edit` — it reports issues without modifying content.

## Skills (Slash Commands)

### Content creation

| Command | Agent | Description |
|---------|-------|-------------|
| `/content-pipeline <brief>` | content-writer | Full 7-phase automated pipeline: research, write, review, edit, fact-check |
| `/write-content <topic>` | content-writer | Draft content with automatic review loop (max 2 rounds) |

### Quality assurance

| Command | Agent | Description |
|---------|-------|-------------|
| `/review-content <file>` | content-reviewer | 6-dimension scored review with APPROVE / REVISE / REJECT verdict |
| `/edit-content <file>` | editor | Three-pass polish: structure, clarity, grammar |
| `/fact-check <file>` | fact-checker | Verify every claim, stat, quote, and link |

### Developer utilities

| Command | Agent | Description |
|---------|-------|-------------|
| `/ship` | content-writer | Pre-publish verification: build + lint + type check |
| `/auto-fix` | content-writer | Auto-fix build/lint/type errors (2-round loop) |

## Content Types

The pipeline supports four content types with built-in templates:

| Type | Word count | Template structure |
|------|------------|-------------------|
| **Blog post** | 800-1,500 | Hook, context, main points (3-5 sections), conclusion, CTA |
| **Tutorial** | 1,500-3,000 | Prerequisites, goal statement, step-by-step, verification, next steps |
| **API docs** | 500-1,000/endpoint | Endpoint, auth, parameters, request/response examples, error codes |
| **Landing page** | 300-600 | Headline, problem, solution, features, social proof, CTA |

## Review Scoring

The content-reviewer uses a 30-point rubric:

| Dimension | What it measures |
|-----------|-----------------|
| **Accuracy** (1-5) | Facts correct and cited, code examples work, no outdated info |
| **Clarity** (1-5) | Short sentences, jargon explained, active voice |
| **Style** (1-5) | Consistent tone, inclusive language, no filler |
| **Structure** (1-5) | Heading hierarchy, smooth transitions, scannable |
| **Completeness** (1-5) | CTAs present, all promises fulfilled, examples for every point |
| **Audience** (1-5) | Correct reading level, assumptions stated, relatable examples |

**Verdicts:** APPROVE (24-30) / REVISE (18-23) / REJECT (<18)

## Fact-Checking

The fact-checker catches:

- Outdated statistics presented as current
- Misattributed quotes
- Survivorship bias and cherry-picked data
- Correlation presented as causation
- Circular citations
- Broken links (404s)

**Source hierarchy:** Primary (official docs, research) > Secondary (news, reports) > Tertiary (Wikipedia) > Avoid (blogs, social media)

**Confidence levels:** Verified / Likely / Unverified / Incorrect

## Customization

### Add your style guide

Edit `.claude/agents/editor.md`:

```markdown
## Style Rules
- Use "workspace" not "project" (our product term)
- Oxford comma always
- Sentence case for headings
```

### Add your terminology

Edit `.claude/agents/content-writer.md`:

```markdown
## Terminology
- "team member" not "user"
- Always capitalize "API" and "SDK"
```

### Adjust models

Downgrade to haiku for simple editing tasks:

```yaml
model: haiku  # fast and cheap for basic edits
```

### Pair with developer workflows

This pipeline works alongside any Claude Code agent setup:

```
/implement Add new API endpoint for user profiles
/write-content API documentation for the /profiles endpoint
/fact-check docs/api/profiles.md
```

## File Structure

```
your-project/
├── .claude/
│   ├── agents/
│   │   ├── content-writer.md       # Drafting + research + orchestration
│   │   ├── content-reviewer.md     # 6-dimension quality scoring
│   │   ├── editor.md               # Three-pass editing
│   │   └── fact-checker.md         # Claim verification
│   └── skills/
│       ├── content-pipeline/       # Full automated pipeline
│       ├── write-content/          # Draft with auto-review
│       ├── review-content/         # Scored quality review
│       ├── edit-content/           # Style + clarity polish
│       ├── fact-check/             # Claim verification
│       ├── ship/                   # Pre-publish checks
│       └── auto-fix/               # Error auto-correction
└── ORCHESTRATION_HELPER.md         # Detailed usage guide
```

## Examples

### Full pipeline

```
/content-pipeline Blog post about WebSocket best practices for React developers, 1200 words, conversational tone
```

### Review existing content

```
/review-content docs/blog/websocket-guide.md
```

### Quick edit pass

```
/edit-content README.md
```

### Verify facts before publishing

```
/fact-check docs/tutorials/jwt-auth.md
```

## Related

- [claude-code-agent-template](https://github.com/PingPingE/claude-code-agent-template) — more multi-agent templates (starter, PR review, bug fix, code quality)
- [Claude Code docs](https://docs.anthropic.com/en/docs/claude-code)

## License

MIT
