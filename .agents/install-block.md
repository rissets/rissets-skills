# The canonical install block

One install story, one wording. `README.md`, `.changeset/*`, and every page under `docs/` must say **this** and nothing else. Change it here first, then propagate.

## Managed installs first

Lead with installs that update themselves. Fall back to skills.sh, labelled "manual updates", only for agents that have no such install. Call a route managed only if it updates without the user running a command. Put any one-time opt-in beside its install command. Never promise "instant".

Plugin-capable agents install from the Rissets marketplace, `.claude-plugin/marketplace.json` and `plugin.json`. Rissets is a separate distribution from the upstream official Claude listing. Those routes reinstall only when the `version` in `plugin.json` changes. The Release workflow runs `npm run version`, which copies that field from `package.json`, so users get a release when the "chore: version skills" PR merges.

| Agent         | Route                            | Updates itself?                                                  |
| ------------- | -------------------------------- | ---------------------------------------------------------------- |
| Claude Code   | `@rissets` marketplace | Enable auto-update for this marketplace in `/plugin` |
| Codex         | `@rissets` marketplace        | Yes, at startup, by default                                      |
| Copilot CLI   | `@rissets` marketplace        | Yes, after a one-time `autoUpdate: true`                         |
| VS Code       | Chat: Install Plugin From Source | Yes, daily, by default                                           |
| Gemini CLI    | `gemini skills install` (copies) | No. A Gemini extension would need a flat `skills/<name>/` layout |
| Pi Agent, Antigravity, OpenCode | skills.sh, promoted buckets only | No, manual updates |
| Everyone else | skills.sh                        | No. Run `npx skills update`, and re-run `add` for new skills     |

Sources (2026-10-08): Codex `core-plugins/src/manager.rs`; Copilot [cli-config-dir-reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference); VS Code `pluginAutoUpdate.ts`; Gemini `skillLoader.ts`.

Nobody has run Auggie, Droid, Qwen or Goose against this repo, so they stay on skills.sh until someone does.

## Claude Code

<canonical-block name="claude-code">

```bash
claude plugin marketplace add rissets/rissets-skills
claude plugin install rissets-skills@rissets
```

Enable auto-update for the `rissets` marketplace in `/plugin` → Marketplaces. Third-party marketplaces do not enable it by default.

</canonical-block>

## Codex

<canonical-block name="codex">

```bash
codex plugin marketplace add rissets/rissets-skills
codex plugin add rissets-skills@rissets
```

Updates itself at startup.

</canonical-block>

## GitHub Copilot (CLI and VS Code)

Use the marketplace, not `copilot plugin install rissets/rissets-skills`. Copilot has deprecated direct repo installs, and they can't auto-update. The `extraKnownMarketplaces` entry follows the documented schema, but nobody has run it yet.

<canonical-block name="copilot">

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

</canonical-block>

## Gemini CLI

Gemini doesn't read `.claude-plugin`, and `--path` takes one bucket. One install per promoted bucket gives exactly the promoted set (27 skills, verified 2026-10-07).

<canonical-block name="gemini">

```bash
gemini skills install https://github.com/rissets/rissets-skills.git --path skills/engineering
gemini skills install https://github.com/rissets/rissets-skills.git --path skills/productivity
```

Re-run both commands to update.

</canonical-block>

## Pi Agent

<canonical-block name="pi">

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a pi --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a pi --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In Pi, run `/skill:setup-rissets-skills`, then `/skill:ask-rissets`. Use `/reload` after installation in an active session.

</canonical-block>

## Antigravity

<canonical-block name="antigravity">

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a antigravity --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a antigravity --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In Antigravity, ask the agent to load `setup-rissets-skills`, then `ask-rissets`.

</canonical-block>

## OpenCode

<canonical-block name="opencode">

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a opencode --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a opencode --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
In OpenCode, ask the agent to load `setup-rissets-skills` using its `skill` tool.

</canonical-block>

## Every other agent, or editable files

<canonical-block name="other-agents">

```bash
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/engineering -a <agent> --skill '*'
npx skills@latest add https://github.com/rissets/rissets-skills/tree/main/skills/productivity -a <agent> --skill '*'
```

Manual updates: run `npx skills@latest update`, then re-run both `add` commands to pick up new skills. Installs target the current project; add `-g` to both commands for a global install.
Replace `<agent>` with your installer agent identifier, for example `cursor`, `devin`, `windsurf`, or `amp`.

</canonical-block>

Use the single-skill form wherever one skill is named on its own. `docs/` pages don't use this block, because ai-hero renders the install widget above the page body. See [writing-docs.md](./writing-docs.md).

<canonical-block name="skills-sh-one-skill">

```bash
npx skills@latest add rissets/rissets-skills --skill=<name>
```

```bash
npx skills@latest update <name>
```

</canonical-block>

`skills@latest` is the pinned spelling everywhere.

## The two routes are exclusive

The plugin is a managed, read-only bundle you subscribe to. skills.sh writes files you own and edit. Installing both leaves the user with every skill twice: always say "pick one".

## Runtime evidence

Install syntax and discovery paths were checked against the [skills CLI reference](https://github.com/vercel-labs/skills/blob/main/docs/commands.md), [agent registry](https://github.com/vercel-labs/skills/blob/main/src/agents.ts), [Pi documentation](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md), [OpenCode documentation](https://docs.opencode.ai/docs/skills/), and [Antigravity documentation](https://antigravity.google/docs/skills). Codex plugin command syntax was checked with the installed CLI. These checks do not establish a successful remote install of this unreleased fork or an agent session in each runtime.
