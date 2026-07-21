# Agent skills

Skills available to agents in this repository are:

- **[Scaffold audit](./scaffold-audit/):**
  Cuts an `audit/<slug>` branch from `main`, fills in some initial details,
  and opens a draft pull request.

- **[Complete audit](./complete-audit/):**
  After the reviews have been completed, this skill can be used to land
  the audit report in the `main` trunk.

> [!NOTE]
> This scaffold skill merely prepares a new, blank audit report. After this
> step, the user will do the architecture audit and write up the report. For
> help with the actual architecture audit itself, see the
> [**audit**](https://github.com/kieranpotts/skills/tree/latest/dev/skills/audit)
> skill in my global skills collection.

## Compatibility

Agent harnesses are converging on the `./.agents/skills/` path for dynamic
retrieval of project-specific skills. This is compatible with the Agent Skills
convention — see https://agentskills.io/.

As of May 2026, OpenAI Codex, GitHub Copilot, Gemini CLI, Google Antigravity,
OpenCode, and Pi will auto-discover these skills, but Claude Code and Cursor
will not.

You will require workarounds for incompatible harnesses. For Claude Code, you
can simply symlink this directory from `.claude/skills/`. Cursor requires more
effort to transpile these skills into its native "rules" format.
