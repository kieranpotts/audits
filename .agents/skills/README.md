# Agent skills for managing architecture audit reports

The skills available to agents in this project are:

- **[scaffold-audit](./scaffold-audit/):** \
  Cuts an `audit/<slug>` branch from `main`, fills in some initial details,
  and opens a draft pull request.

- **[complete-audit](./complete-audit/):** \
  After the reviews have been completed, this skill can be used to land
  the audit report in the `main` trunk.

The **scaffold-audit** skill prepares a new, blank audit report. After this step,
the user will do the architecture audit and write up the report. When the report
is done, the **complete-audit** skill can be used to get an agent to check it
over and land the report in the `main` trunk.

```mermaid
flowchart LR
  scaffold["🤖<br/><b>scaffold-audit</b>"]:::agentic
  write["🧑<br/>write report"]:::anthropic
  complete["🤖<br/><b>complete-audit</b>"]:::agentic

  scaffold ==> write
  write ==> complete

  classDef agentic fill:#cce5ff,stroke:#004085,color:#004085,stroke-width:2px
  classDef scripted fill:#e2e3e5,stroke:#4b5157,color:#383d41,stroke-width:2px
  classDef anthropic fill:#fff3cd,stroke:#856404,color:#856404,stroke-width:2px,stroke-dasharray:2 3
```

For help with the actual architecture audit itself, or for help writing a report,
see the [**audit**](https://github.com/kieranpotts/skills/tree/latest/dev/skills/audit)
skill in my global skills collection.

## Compatibility

These skills are compatible with the [Agent Skills](https://agentskills.io/)
convention. Most agent harnesses support this convention natively, but
workarounds may be required for harnesses that do not.
