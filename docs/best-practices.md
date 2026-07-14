# Best practices

Practical guidance for running a good audit.

## Cite evidence, not impressions

Every finding names specific files and lines. "The API layer is messy" is not a
finding, since it gives the reader nothing to check. "`handlers/orders.go:120-180`
duplicates the same three-step validation across five handlers" is a proper,
actionable finding.

## Observation before opinion

State what you see and the cost it imposes before offering any suggestion. A
pointer toward a fix is optional, and should stay a pointer – a sentence, not
a worked-out redesign.

## "Not worth fixing" is a valid finding

Not every smell earns a fix. If the cost of the change would exceed the cost
of the smell, say so, and record it as low priority with the rationale. A
report that recommends fixing everything it finds is not being honest about
trade-offs.

## Stay within the codebase's idioms

Don't flag a consistent style choice as a smell just because you'd have made
a different one. An audit is for structural problems, not for imposing a
personal preference on an otherwise-consistent codebase.

## Prioritize by impact over effort

Order findings by how much they'd simplify the rest of the system, against how
invasive the fix would be.

A 30-item backlog does not get acted on. A report that leads with the three
findings worth fixing first does.

## Stay evaluation-only

An audit does not change code, file issues, or open pull requests against
the audited repository. The report is the deliverable. What happens next is
for the target project's own team to decide.

## Keep the report immutable once merged

Do not go back and edit a merged audit report as the system changes underneath
it. If the findings need reassessing, run a new audit.
