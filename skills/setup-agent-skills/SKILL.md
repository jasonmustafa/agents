---
name: setup-agent-skills
description:
  Configure this repo for engineering skills — GitHub or local-markdown ticket
  tracking, triage status vocabulary, and domain doc layout. Run once before
  first use of the other engineering skills.
disable-model-invocation: true
---

# Setup Agent Skills

Scaffold the per-repo configuration that the engineering skills assume:

- **Ticket tracker** — GitHub Issues or local markdown under `.scratch/`
- **Triage status vocabulary** — the strings used for the five canonical triage
  roles
- **Domain docs** — where `CONTEXT.md` and ADRs live, and the consumer rules for
  reading them

This is a prompt-driven skill, not a deterministic script. Explore, present what
you found, confirm with the user, then write.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists;
don't assume:

- `git remote -v` and `.git/config` — is this a GitHub repo? Which one?
- `AGENTS.md` and `CLAUDE.md` at the repo root — does either exist? Is there
  already an `## Agent skills` section in either?
- `CONTEXT.md` and `CONTEXT-MAP.md` at the repo root
- `docs/adr/` and any `src/*/docs/adr/` directories
- `docs/agents/` — does this skill's prior output already exist?
- `.scratch/` — sign that a local-markdown ticket tracker convention is already
  in use

### 2. Present findings and ask

Summarise what's present and what's missing. Then walk the user through the
decisions **one at a time** — present a section, get the user's answer, then
move to the next. Don't dump all sections at once.

Assume the user does not know what these terms mean. Each section starts with a
short explainer: what it is, why these skills need it, and what changes if they
pick differently.

**Section A — Ticket tracker.**

> Explainer: The ticket tracker is where ticket and specs live for this repo.
> Skills need to know whether to use the `gh` CLI or write markdown files under
> `.scratch/`.

If a git remote points at GitHub, recommend GitHub. Otherwise recommend local
markdown. Offer only:

- **GitHub** — issues live in this repo's GitHub Issues; use `gh`. Leave "PRs as
  a request surface" off unless the user explicitly requests otherwise.
- **Local markdown** — tickets live under `.scratch/<feature-slug>/`; ask
  whether to change the directory name (default `.scratch/`).

Record the choice in `docs/agents/ticket-tracker.md`.

**Section B — Triage status vocabulary.**

> Explainer: When work is triaged, each ticket moves through a small state
> machine: needs evaluation, waiting on reporter, ready for an AFK agent, ready
> for a human, or won't fix. GitHub records this with labels; local markdown
> uses a `Status:` line. The skill needs the exact strings to apply.

The five canonical roles:

- `needs-triage` — maintainer needs to evaluate
- `needs-info` — waiting on reporter
- `ready` — fully specified, ready for implementation
- `wontfix` — will not be actioned

Default: each role's status string equals its name. Ask the user if they want to
override any. If they don't care, use the defaults.

**Section C — Domain docs.**

> Explainer: Some skills read a `CONTEXT.md` file to learn the project's domain
> language, and `docs/adr/` for past architectural decisions. They need to know
> whether the repo has one global context or multiple contexts so they look in
> the right place.

Confirm the layout:

- **Single-context** — one `CONTEXT.md` + `docs/adr/` at the repo root. Most
  repos are this.
- **Multi-context** — `CONTEXT-MAP.md` at the root pointing to per-context
  `CONTEXT.md` files, typically for monorepos.

### 3. Confirm and edit

Show the user a draft of:

- The `## Agent skills` block to add to whichever of `CLAUDE.md` / `AGENTS.md`
  is being edited (see step 4 for selection rules)
- The contents of `docs/agents/ticket-tracker.md`,
  `docs/agents/triage-labels.md`, and `docs/agents/domain.md`

Let them edit before writing.

### 4. Write

**Pick the file to edit:**

- If `CLAUDE.md` exists, edit it.
- Else if `AGENTS.md` exists, edit it.
- If neither exists, ask the user which one to create — don't pick for them.

Never create `AGENTS.md` when `CLAUDE.md` already exists (or vice versa) —
always edit the one that's already there.

If an `## Agent skills` block already exists in the chosen file, update its
contents in-place rather than appending a duplicate. Don't overwrite user edits
to the surrounding sections.

The block:

```markdown
## Agent skills

### Ticket tracker

[one-line summary of where tickets are tracked]. See
`docs/agents/ticket-tracker.md`.

### Triage status

Tickets use the configured triage vocabulary. See
`docs/agents/triage-labels.md`.

### Domain docs

[one-line summary of layout — "single-context" or "multi-context"]. See
`docs/agents/domain.md`.
```

Then write the three docs files using the seed templates in this skill folder as
a starting point:

- [ticket-tracker-github.md](./issue-tracker-github.md) — GitHub issue tracker
- [ticket-tracker-local.md](./ticket-tracker-local.md) — local-markdown ticket
  tracker
- [triage-labels.md](./triage-labels.md) — status mapping
- [domain.md](./domain.md) — domain doc consumer rules + layout

### 5. Done

Tell the user the setup is complete and which engineering skills will now read
from these files. Mention they can edit `docs/agents/*.md` directly later —
re-running this skill is only necessary if they want to switch ticket trackers
or restart from scratch.
