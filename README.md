# 🔍 Architecture Audits

**A template for capturing audits of a system's architecture.**

This repository is the home of architecture audits for [Project Name]. It is a
permanent archive of standalone, point-in-time evaluations of the as-built
system's structural health.

Each audit report is a snapshot in time, and immutable once merged into the
`main` trunk.

An architectural audit is evaluation only. A finding may point toward a fix,
but it is not necessary for audit reports to suggest alternative designs.

An audit evaluates a system's architecture on its own terms, without
cross-referencing the _intended_ architecture captured in the
[design docs](https://github.com/kieranpotts/design), and so with
no prior knowledge of the trade-offs already considered. The purpose
is to surface genuinely fresh insights.

An audit report captures prioritized findings on structural health. It logs
code smells and anti-patterns such as shallow abstractions, tangled
dependencies, single-caller wrappers, leaky boundaries, and repeated patterns.
Security and privacy review is out of scope — that is the topic of the
[risk register](https://github.com/kieranpotts/risks).

## Ecosystem

This repository is one of six that form a coherent, version-controlled
documentation ecosystem:

- [**📋 Software Requirements Specification (SRS)**](https://github.com/kieranpotts/specs):
  Records _what_ the system does, in business terms.

- [**💬 Requests for Comments (RFC)**](https://github.com/kieranpotts/rfc):
  Records _how_ significant technical decisions were made, and _why_.

- [**📐 Design Docs**](https://github.com/kieranpotts/design):
  Describe _what the system looks like_, its as-is architecture.

- [**🗺️ Delivery Plans**](https://github.com/kieranpotts/plans):
  Capture _when, and in what order_, the work gets done.

- **🔍 Architecture Audits**:
  Evaluate the as-built system's architecture (this repository).

- [**⚠️ Risk Register**](https://github.com/kieranpotts/risks):
  Records the security and privacy risks the system carries.

In addition, the [**skills**](https://github.com/kieranpotts/skills) collection
provides an agentic workflow that operates across all six repositories.

This separation into dedicated repositories is intended for application
software that spans multiple code repositories, and potentially multiple teams,
where the requirements, decisions, designs, plans, audits, and risks are shared
concerns that sit above any single codebase. For a standalone code repository –
a small utility library, say – it may be preferable to fold these artifacts and
skills directly into that repository, rather than maintain them separately.

## Contents

- [**Audits**](./audits/):
  Every audit report, one directory per audit.

  - The [`INDEX`](./audits/INDEX.md) lists every audit merged
    into `main`, newest first.

  - The [`TEMPLATE`](./audits/TEMPLATE.md) is the starting
    point for a new audit.

- [**Contributing**](./CONTRIBUTING.md):
  Step-by-step instructions for running an audit and landing its report.

- [**Agents**](./AGENTS.md) and [**Skills**](./.agents/skills/):
  Instructions for agentic tools to run and land audits with a high
  degree of autonomy.

- [**Documentation**](./docs/):
  General guidance on how to get the most out of an audit – what to record,
  how to prioritize, and how it relates to the software design process.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
