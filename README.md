# bstack

Benjamin's personal collection of AI agent skills and workflows.

Inspired by [tstack](https://github.com/t3dotgg/tstack), bstack is an independently
maintained collection that will be extensively customized for my own setup.
It targets Pi, OpenCode, Codex, Claude Code, and optionally Hermes.

The initial skills come from tstack. Their behavior will evolve here; compatibility
still needs verification in each harness, especially for multi-model delegation.

## Skills

| Skill | Say | What it does |
|---|---|---|
| `full-send` | "full send" | Takes a change to a merged PR with nobody watching: proves it, reviews it, files it, babysits it, merges it. |
| `full-stop` | "full stop" | Same as `full-send`, but stops when the PR is ready for you to merge. |
| `council` | "council" | Gets review from three models from different providers, and loops until they agree. |
| `sol-loop` | "sol loop" | Reviews a change with GPT Sol in a loop until both agents agree. |
| `file-pr` | "file a PR" | Files a short PR that leads with the problem, not an inventory of changes. |
| `takeover` | "take over" | Finishes someone else's PR, branch, or agent thread, and keeps their credit. |
| `babysit-pr` | "babysit" | Watches a PR through CI and review bots, and fixes the real findings. |
| `modernize` | "modernize" | Rebases an old PR and decides if it should still exist. |
| `leaving-pr-comments` | (automatic) | Formats comments that an agent posts on your behalf. |
| `grill-me` | "grill me" | Starts an interview to sharpen a plan or design, using `grilling`. |
| `grilling` | "grill my plan" | Interviews you through the decisions and dependencies in a plan. |
| `interface-review` | "interface-review" | Reviews interface regressions introduced by a branch, PR, or uncommitted change. |
| `better-interface` | "review this interface" | Combines accessibility, layout, writing, typography, color, and UI reviews. |
| `better-accessibility` | "check accessibility" | Reviews keyboard access, focus, ARIA, forms, motion, and zoom. |
| `better-layout` | "improve the layout" | Improves grouping, alignment, responsive structure, and reading order. |
| `better-writing` | "improve interface copy" | Improves labels, errors, empty states, and confirmations. |
| `better-typography` | "improve typography" | Reviews type scale, spacing, font features, wrapping, and punctuation. |
| `better-colors` | "improve colors" | Builds palettes and semantic tokens, converts colors, and checks contrast. |
| `better-ui` | "polish the UI" | Polishes surfaces, icons, alignment, shadows, and motion. |
| `make-interfaces-feel-better` | "make interfaces feel better" | Improves the small visual and interaction details of an interface. |
| `openspec-explore` | "openspec explore" | Explores ideas, investigates problems, and clarifies requirements. |
| `openspec-propose` | "openspec propose" | Creates a change proposal with design, specs, and implementation tasks. |
| `openspec-new-change` | "openspec new change" | Starts a new change with an empty planning scaffold. |
| `openspec-continue-change` | "openspec continue" | Creates the next planning artifact for a change. |
| `openspec-ff-change` | "openspec ff" | Creates all artifacts needed for implementation in one pass. |
| `openspec-apply-change` | "openspec apply" | Implements the tasks in an OpenSpec change. |
| `openspec-update-change` | "openspec update change" | Revises an existing change’s planning artifacts. |
| `openspec-verify-change` | "openspec verify" | Checks implementation against the change’s specs, design, and tasks. |
| `openspec-sync-specs` | "openspec sync" | Merges a change’s delta specs into the main specs. |
| `openspec-archive-change` | "openspec archive" | Archives a completed change. |
| `openspec-bulk-archive-change` | "openspec bulk-archive" | Archives multiple completed changes. |
| `openspec-onboard` | "openspec onboard" | Guides you through a complete OpenSpec workflow. |

Some skills call others. The full install below includes their dependencies:
`full-send` uses `sol-loop`, `file-pr`, and `babysit-pr`; `full-stop` uses
`full-send`; `takeover` uses `modernize`, `file-pr`, `babysit-pr`, and
`leaving-pr-comments`. PR workflows use `leaving-pr-comments`. `grill-me` uses
`grilling`; `interface-review` uses `better-interface` and the six domain skills.

Imported skills include their references, agent metadata where provided, and
licenses. Source revisions and attribution are in [THIRD_PARTY.md](THIRD_PARTY.md).
Some instructions name harness-specific tools; invocation and tool support still
need verification in each agent.

## Install with Bun

Install from GitHub:

```bash
bunx skills add MrM0bi/bstack --global --skill '*' --agent pi opencode codex claude-code --yes
```

Add `hermes-agent` to the agent list if wanted. These commands install skill files;
they do not configure providers, MCP servers, extensions, or delegation tools.

Use `bunx skills check` and `bunx skills update <skill-names> --global --yes`
for tracked remote updates. A Git push alone does not update other machines.
To try local edits before publishing, run the install command from this checkout
with `.` in place of `MrM0bi/bstack`.

## Agent skill directories

Use the Skills CLI installation command above to install for Pi, OpenCode, Codex,
and Claude Code. It manages the skill locations and links for the selected agents;
no manual directory-wide symlinks are needed. Add `hermes-agent` to the agent list
to include Hermes.

Manage this collection in bstack and rerun the install command after local edits,
rather than editing the installed files in each agent's directory.

## Upstream inspiration

The `upstream` Git remote points to tstack for reference. bstack evolves independently;
upstream changes can be reviewed and cherry-picked when useful, rather than
synchronized automatically. bstack uses a fresh Git history; original license attribution is retained.

## Requirements

- An authenticated [GitHub CLI](https://cli.github.com) (`gh`).
- `python3` for `babysit-pr`'s `pr-wait` script.
- `council` and `sol-loop` need subagents on other providers' models. T3 Code
  does this with `delegate_task`. Otherwise you need a harness that can run
  those models.

OpenSpec skills also require the `openspec` CLI and an initialized target project.
Installing skills from bstack does not initialize your projects:

```bash
bun add --global @fission-ai/openspec
cd /path/to/your/project
openspec init
```

## Customization

Skills, helper scripts, and references are maintained in this repository. Keep
machine-specific settings and model preferences in `CLAUDE.md` or `AGENTS.md`
so the shared workflows remain portable across my agents and machines.

## License

[MIT](LICENSE). Original tstack copyright notices are retained; bstack modifications
are copyright Benjamin.
