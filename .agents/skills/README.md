# Agent skills

Skills available to agents in this repository are:

- **[Scaffold audit](./scaffold-audit/):**
  Cuts an `audit/<slug>` branch from `main`, fills in some initial details,
  and opens a draft pull request.

- **[Finalize audit](./finalize-audit/):**
  After the reviews have been completed, this skill can be used to land
  the audit report in the `main` trunk.

> [!NOTE]
> This scaffold skill merely prepares a new, blank audit report. After this
> step, the user will do the architecture audit and write up the report. For
> help with the actual architecture audit itself, see the
> [**audit**](https://github.com/kieranpotts/skills/tree/latest/dev/skills/audit)
> skill in my global skills collection.
