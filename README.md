# 🔍 Architecture Audits

**A template for capturing audits of a system's architecture.**

This repository is the home of architecture audits for [Project Name]. It is a
permanent archive of standalone, point-in-time evaluations of the as-built
system's structural health.

An audit evaluates a system's architecture on its own terms, without
cross-referencing the _intended_ architecture captured in the
[design docs](https://github.com/kieranpotts/design). Auditors may have
no prior knowledge of the trade-offs already considered. The purpose is to
surface genuinely fresh insights.

An audit report captures prioritized findings on structural health. It logs
code smells and anti-patterns discovered in the code, such as shallow
abstractions, tangled dependencies, single-caller wrappers, leaky boundaries,
and repeated patterns.

Each audit report is a snapshot in time, and immutable once merged into the
`main` trunk.

An architectural audit is evaluation only. It is not the role of audit reports
to suggest fixes or alternative designs. And security and privacy review is
out-of-scope — that is the subject of the
[risk register](https://github.com/kieranpotts/risks).

> [!NOTE]
> See **[TS-3: Design Docs](https://github.com/kieranpotts/standards/tree/latest/dev/src/003)**.
> for more guidance on preparing and maintaining architecture audit reports,
> as well as other forms of design doc.

## Ecosystem

This repository is one of six that form a coherent, version-controlled
documentation ecosystem. Each answers a different question about a software
system.

- [**📋 Software Requirements Specification (SRS)**](https://github.com/kieranpotts/specs) \
  Captures what the system does, in business terms.

- [**💬 Requests for Comments (RFC)**](https://github.com/kieranpotts/rfc) \
  Records how significant technical decisions were made, and why.

- [**📐 Design Docs**](https://github.com/kieranpotts/design) \
  Documents what the system looks like in production.

- [**🔍 Architecture Audits**](https://github.com/kieranpotts/audits) (this repository) \
  Logs historical evaluations of the as-built system's structural integrity.

- [**🗺️ Delivery Plans**](https://github.com/kieranpotts/plans) \
  Tracks when, and in what order, the work gets done.

- [**⚠️ Risk Register**](https://github.com/kieranpotts/risks) \
  Records the inherent security and privacy risks the system carries.

In addition, the [**✨ Agent SKills**](https://github.com/kieranpotts/skills)
collection offers composabe agentic workflows that operate across all six
repositories.

This separation into dedicated repositories is intended for application software
that spans multiple code repositories, and potentially multiple teams, where the
requirements, decisions, designs, plans, audits, and risks are shared concerns
that sit above any single codebase.

For a standalone code repository – a small utility library, say – it may be
better to fold all documentation into the same repository.

## Contents

- [**Audits**](./audits/) \
  Every audit report, one directory per audit.

  - The [`INDEX`](./audits/INDEX.md) lists every audit merged
    into `main`, newest first.

  - The [`TEMPLATE`](./audits/TEMPLATE.md) is the starting
    point for a new audit.

- [**Contributing**](./CONTRIBUTING.md) \
  Step-by-step instructions for running an audit and landing its report.

- [**Agents**](./AGENTS.md) and [**Skills**](./.agents/skills/) \
  Instructions for agents to run and land audits with a high degree of autonomy.

- [**Documentation**](./docs/) \
  General guidance on how to get the most out of an architecture audit – what
  to record, how to prioritize, and how audits fit into the wider software
  design process.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
