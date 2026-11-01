# Publish the fork as Rissets Skills

The upstream collection uses Matt Pocock’s identity and official marketplace listing. This fork uses `rissets/rissets-skills`, plugin `rissets-skills`, marketplace `rissets`, and documentation at `https://hi.rissets.com/skills-<skill-name>`. The upstream MIT copyright and historical release evidence remain attributed. This supersedes ADR 0002’s upstream marketplace choice for this fork.

Rename `ask-matt` to `ask-rissets` and `setup-matt-pocock-skills` to `setup-rissets-skills`, without duplicate aliases. Existing users must use the new names; installing Rissets does not remove an upstream installation. Choose one distribution per runtime to avoid duplicate skills.

Claude Code uses the Rissets marketplace, with auto-update enabled explicitly. Codex retains its marketplace route. Pi Agent, Antigravity, and OpenCode receive explicit skills.sh instructions scoped to the two promoted buckets, avoiding native installers that recursively expose beta or retired skills. Pi uses `/skill:<name>`; runtime-specific invocation differs even though the skill content is shared.

The website URL is a publication target. Updating repository links does not deploy the website. Remote installation and runtime execution must be verified after publication; upstream test claims are not evidence that this fork was tested.
