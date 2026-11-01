# Rissets Skills

Reusable agent skills for engineering and productivity, maintained by Rissets. Use them to clarify requirements, plan implementation, build with feedback, review changes, and carry context between sessions.

- **Documentation:** [hi.rissets.com](https://hi.rissets.com)
- **Source and updates:** [rissets/rissets-skills](https://github.com/rissets/rissets-skills)
- **Questions and bugs:** [GitHub Issues](https://github.com/rissets/rissets-skills/issues)

The promoted collection contains 27 skills: 20 for engineering and 7 for productivity. Skills are plain Markdown with supporting references and scripts where needed. Choose a single skill for a focused task, or combine them into a workflow while keeping human decisions explicit.

## Installation

Choose one installation route per runtime. Plugin installations use the Rissets marketplace; update settings depend on the runtime. The skills.sh route installs into your project by default and requires manual updates. Its two bucket-scoped commands select only promoted skills.

### 1. Get the skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugin marketplace add rissets/rissets-skills
claude plugin install rissets-skills@rissets
```

Enable auto-update for the `rissets` marketplace in `/plugin` → Marketplaces. Third-party marketplaces do not enable it by default.

</details>

<details>
<summary><strong>Codex</strong></summary>

```bash
codex plugin marketplace add rissets/rissets-skills
codex plugin add rissets-skills@rissets
```

Updates itself at startup.

</details>

<details>
<summary><strong>GitHub Copilot (CLI and VS Code)</strong></summary>

```bash
copilot plugin marketplace add rissets/rissets-skills
copilot plugin install rissets-skills@rissets
```

Then, once, add to `~/.copilot/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "rissets": { "source": { "source": "github", "repo": "rissets/rissets-skills" }, "autoUpdate": true }
  }
}
```

In VS Code, run **Chat: Install Plugin From Source** and enter `https://github.com/rissets/rissets-skills`. It updates daily.

</details>

<details>
<summary><strong>Gemini CLI (manual updates)</strong></summary>

```bash
gemini skills install https://github.com/rissets/rissets-skills.git --path skills/engineering
gemini skills install https://github.com/rissets/rissets-skills.git --path skills/productivity
```

Re-run both commands to update.

</details>

<details>
<summary><strong>Pi Agent (manual updates)</strong></summary>

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a pi --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a pi --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In Pi, run `/skill:setup-rissets-skills`, then `/skill:ask-rissets`. Use `/reload` after installation in an active session.

</details>

<details>
<summary><strong>Antigravity (manual updates)</strong></summary>

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a antigravity --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a antigravity --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In Antigravity, ask the agent to load `setup-rissets-skills`, then `ask-rissets`.

</details>

<details>
<summary><strong>OpenCode (manual updates)</strong></summary>

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a opencode --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a opencode --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In OpenCode, ask the agent to load `setup-rissets-skills` using its `skill` tool.

</details>

<details>
<summary><strong>Any other agent, or editable files (manual updates)</strong></summary>

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a <agent> --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a <agent> --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
Replace `<agent>` with your installer agent identifier, for example `cursor`, `devin`, `windsurf`, or `amp`.

</details>

[Runtime support and verification](./docs/agents/runtime-support.md).

### 2. Run `/setup-rissets-skills`

Run it once per repo. In Pi, type `/skill:setup-rissets-skills`. In Antigravity and OpenCode, ask the agent to load `setup-rissets-skills`. It will:

- Ask you which issue tracker you want to use (GitHub, GitLab, local files, or anything else you describe)
- Ask you what labels you apply to tickets when you triage them (`/triage` uses labels)
- Ask you where you want to save any docs we create

### 3. Choose your next skill

Start with [ask-rissets](./skills/engineering/ask-rissets/SKILL.md) when you want help choosing a skill or workflow. In Claude Code, type `/ask-rissets`; in Codex, use `$ask-rissets`; in Pi, use `/skill:ask-rissets`. In Antigravity and OpenCode, ask the agent to load `ask-rissets`.

Examples in this README use `/skill-name` as shorthand. Use your runtime's explicit skill invocation when its syntax differs.


## Working with Rissets Skills

| Situation | Start here | What you get |
| --- | --- | --- |
| An idea needs clearer requirements | [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md) | An interview that sharpens the plan and records domain language and decisions |
| The discussion is ready to become a plan | [to-spec](./skills/engineering/to-spec/SKILL.md) | A spec synthesized from the conversation |
| A plan needs executable slices | [to-tickets](./skills/engineering/to-tickets/SKILL.md) | Implementation issues with dependencies |
| A spec or set of issues is ready to build | [implement](./skills/engineering/implement/SKILL.md) | Implementation with test feedback and code review |
| A bug is difficult to reproduce or explain | [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md) | A reproduction loop, diagnosis, fix, and regression check |
| A branch needs review | [code-review](./skills/engineering/code-review/SKILL.md) | Findings against the spec and repository standards |
| A session exposed recurring friction | [retro](./skills/engineering/retro/SKILL.md) | Improvements to the agent's working environment |
| A plan needs discussion without a working directory | [grill-me](./skills/productivity/grill-me/SKILL.md) | An interview without writing local domain documents |

A typical engineering flow is:

```text
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

Use only the steps the task needs. For a small, well-defined behavior, reach directly for [tdd](./skills/engineering/tdd/SKILL.md). For work spanning more than one planning session, [wayfinder](./skills/engineering/wayfinder/SKILL.md) maintains a shared map of decisions. [ask-rissets](./skills/engineering/ask-rissets/SKILL.md) describes how the flows fit together.

## Repository layout

| Location | Purpose | Included in the plugin |
| --- | --- | --- |
| [`skills/engineering/`](./skills/engineering/README.md) | Promoted skills for code work | Yes |
| [`skills/productivity/`](./skills/productivity/README.md) | Promoted skills for general workflows | Yes |
| [`skills/in-progress/`](./skills/in-progress/README.md) | Public beta skills for feedback | No |
| [`skills/misc/`](./skills/misc/README.md) | Skills kept for occasional use | No |
| `skills/deprecated/` | Retired skills | No |
| [`docs/`](./docs/) | Human-facing documentation and runtime verification | Documentation only |

Published skill documentation targets `https://hi.rissets.com/skills-<skill-name>`. The files under `docs/engineering/` and `docs/productivity/` mirror the promoted skill folders. Repository updates do not deploy the website.

## Reference

These split on one axis: who can invoke them. **User-invoked** skills are reachable only when you type them (e.g. `/grill-me`); their job is to orchestrate. **Model-invoked** skills can be invoked by you _or_ reached for automatically by the agent when the task fits; they hold the reusable discipline. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one.

### Engineering

Skills for planning, building, debugging, and reviewing software.

**User-invoked**

- **[ask-rissets](./skills/engineering/ask-rissets/SKILL.md)**: Ask which skill or flow fits your situation. A router over the user-invoked skills in this repo.
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: Grilling session that also builds your project's domain model, sharpening terminology and updating `GLOSSARY.md` and ADRs inline.
- **[triage](./skills/engineering/triage/SKILL.md)**: Move issues through a state machine of triage roles.
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
- **[setup-rissets-skills](./skills/engineering/setup-rissets-skills/SKILL.md)**: Configure this repo for the engineering skills (issue tracker, triage labels, domain doc layout). Run once per repo before using the other engineering skills.
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: Turn the current conversation into a spec and publish it to the issue tracker. No interview, just synthesizes what you've already discussed.
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: Break any plan, spec, or conversation into a set of tracer-bullet tickets, each declaring its blocking edges, written as text in a local file, or as native blocking links on a real tracker.
- **[implement](./skills/engineering/implement/SKILL.md)**: Build the work described by a spec or set of tickets, driving `/tdd` at pre-agreed seams and closing out with `/code-review` before committing.
- **[implement-spec](./skills/engineering/implement-spec/SKILL.md)**: Implement a whole spec on one integration branch. Works the tickets as a task graph, running implementer subagents across the ready frontier for maximum concurrency, then closes out with `/code-review`.
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: Plan a huge chunk of work, more than one agent session can hold, as a shared map of decision tickets on the issue tracker, and resolve them one at a time until the way to the destination is clear.
- **[retro](./skills/engineering/retro/SKILL.md)**: Suggest improvements to the coding agent's environment (navigation, automated checks, coding standards, steering files, tooling) after a session, most severe first.

**Model-invoked**

- **[prototype](./skills/engineering/prototype/SKILL.md)**: Build a throwaway prototype to answer a design question, either a single shareable HTML file for state/logic questions, or several radically different UI variations toggleable from one route.
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: Disciplined diagnosis loop for hard bugs and performance regressions: build a feedback loop that goes red on this bug → minimise → hypothesise → instrument → fix → regression-test.
- **[research](./skills/engineering/research/SKILL.md)**: Investigate a question against high-trust primary sources and capture the findings as a cited Markdown file in the repo, run as a background agent.
- **[tdd](./skills/engineering/tdd/SKILL.md)**: Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**: Actively build and sharpen a project's domain model: challenge terms against the glossary, stress-test with edge-case scenarios, and update `GLOSSARY.md` and ADRs inline.
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: Shared discipline and vocabulary for designing deep modules: a lot of behaviour behind a small interface, placed at a clean seam, testable through that interface.
- **[code-review](./skills/engineering/code-review/SKILL.md)**: Two-axis review of the diff since a fixed point: **Standards** (does it follow the repo's coding standards, plus a Fowler smell baseline?) and **Spec** (does it faithfully implement the originating issue/spec?), run as parallel sub-agents so neither pollutes the other.
- **[pr](./skills/engineering/pr/SKILL.md)**: The shape a pull request body should take: a summary as the smallest visual that makes the change clear, before/after evidence that it works, and a merge-danger call (one-way or two-way door, plus blast radius).
- **[wizard](./skills/engineering/wizard/SKILL.md)**: Generate an interactive bash wizard that walks a human through steps only they can perform: provisioning infrastructure, setting up credentials or CI secrets, walking an unfamiliar third-party dashboard, or running a one-off migration or cutover.

### Productivity

General workflow tools, not code-specific.

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**: Get relentlessly interviewed about a plan or design until every branch of the design tree is resolved.
- **[handoff](./skills/productivity/handoff/SKILL.md)**: Compact the current conversation into a handoff document so another agent can continue the work.
- **[teach](./skills/productivity/teach/SKILL.md)**: Teach the user a new skill or concept over multiple sessions, using the current directory as a stateful teaching workspace.
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**: Turn a decision you can't answer alone into a Markdown questionnaire for the one person who can, filled in async, or together over a meeting. It grills you about the send (who it's for, what you need back), not the subject.
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**: Fire this the moment a message doesn't land. The agent re-pitches it with the context you're missing, in plain English, using your `GLOSSARY.md` vocabulary.

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)**: Interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved. The reusable interview primitive behind `grill-me`, `grill-with-docs`, `triage`, `wayfinder` and `improve-codebase-architecture`.
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**: Writing documents for agents: skills, AGENTS.md/CLAUDE.md, and any doc an agent reaches by a pointer.

## Migrating from the upstream collection

Rissets uses the repository `rissets/rissets-skills`, plugin `rissets-skills`, and marketplace `rissets`.

| Upstream skill | Rissets skill |
| --- | --- |
| `ask-matt` | [ask-rissets](./skills/engineering/ask-rissets/SKILL.md) |
| `setup-matt-pocock-skills` | [setup-rissets-skills](./skills/engineering/setup-rissets-skills/SKILL.md) |

The old skill names are not installed as aliases. Installing Rissets does not uninstall the upstream collection. Choose one distribution per runtime to avoid duplicate skills, and update any saved commands or workflow references to the new names.

Installation examples track the default `main` branch. Changes on a feature branch become available through those commands after they are merged. See [runtime support and verification](./docs/agents/runtime-support.md) for the tested installation paths and remaining verification limits.

## Contributing

Read [CONTRIBUTING.md](./CONTRIBUTING.md) and [SCOPE.md](./SCOPE.md) before opening an issue or proposing a skill. Report bugs and suggest improvements in [this repository's issues](https://github.com/rissets/rissets-skills/issues).

## License and attribution

Rissets Skills is adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills). The upstream copyright notice is preserved in [LICENSE](./LICENSE). The collection is distributed under the MIT license.
