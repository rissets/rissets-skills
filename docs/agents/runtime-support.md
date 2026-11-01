# Rissets runtime support

Documentation target: [hi.rissets.com](https://hi.rissets.com). This repository change does not publish the website or release the fork.

| Runtime | Installation route | Invocation |
| --- | --- | --- |
| Claude Code | Rissets marketplace | `/setup-rissets-skills`, `/ask-rissets` |
| Codex | Rissets marketplace | Explicitly select the skill, or use `$setup-rissets-skills` and `$ask-rissets` |
| Pi Agent | skills.sh, both promoted buckets | `/skill:setup-rissets-skills`, `/skill:ask-rissets` |
| Antigravity | skills.sh, both promoted buckets | Ask the agent to load the named skill |
| OpenCode | skills.sh, both promoted buckets | Ask the agent to load the named skill with its `skill` tool |

Copy install commands from [the canonical install block](../../.agents/install-block.md). Only engineering and productivity are shipped. Keep a single distribution per runtime; installing Rissets does not uninstall the upstream distribution.

## Verification, 2026-11-01

- skills CLI 1.7.4 installed 20 engineering and 7 productivity skills from the local working tree into an isolated project for Pi, Antigravity, and OpenCode. The resulting set exactly matches the promoted plugin set. This proves file installation and selection, not an interactive agent session.
- The installed Codex CLI accepts the documented plugin and marketplace command forms. No remote fork install or Codex skill execution was performed.
- Plugin paths, top-level and bucket README links, docs pages, renamed frontmatter, and invocation policies match all 27 promoted skills. README install sections match the canonical blocks.
- The linker was exercised with temporary destinations. Global skill directories were left unchanged because the existing linker replaces ordinary directories; they contain existing installations.
- Plugin version consistency and `git diff --check` pass.
- `claude plugin validate .` passes with warnings. The required strict run fails because root `CLAUDE.md` is not plugin context; the validator also reports a missing icon. Both conditions already exist in the upstream layout.
- The bundled skill-creator validator rejects the existing `disable-model-invocation` field. That field is required by this repository and was retained; name, description, directory names, and explicit invocation policies were checked separately.

Remote install commands target the repository after these changes are published. Interactive runtime behavior, remote marketplace resolution, automatic updates, and website availability remain unverified for this release.

## Sources

- [skills CLI commands](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)
- [skills agent registry](https://github.com/vercel-labs/skills/blob/main/src/agents.ts)
- [Pi skills](https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md)
- [OpenCode skills](https://docs.opencode.ai/docs/skills/)
- [Antigravity skills](https://antigravity.google/docs/skills)
