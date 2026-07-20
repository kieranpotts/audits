# Overview

An architecture audit is a point-in-time evaluation of a system's design.

An architecture audit is scoped to the structural design of a system. The
process involves static review of code and data structures. The auditors look
for code smells and anti-patterns, things like shallow abstractions, tangled
dependencies, single-caller wrappers, leaky boundaries, and repeated patterns.

An architecture audit report is distinct from the system's
[design docs](https://github.com/kieranpotts/design). Design docs are a living
description of what the architecture is _intended_ to be. By comparison, an
audit report is a snapshot evaluation of the _actual_ architecture, as it exists
in production at a point in time.

Once complete, an audit report becomes a permanent, immutable record within a
chronologically-ordered stack of historical audit reports. By comparison,
design docs are living documentation, evolving in lock-step with the production
system.

Of course, findings from an architecture audit may influence the evolutionary
design of the system. Architecture audits may feed downstream refactoring work,
with the resulting changes ultimately being reflected in the design docs.
