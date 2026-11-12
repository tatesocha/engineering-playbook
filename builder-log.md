# Builder log: running engineering process as a founder with AI agents

Written by the author, who set this up while learning it. The systems here were new to me when I started. I understood them in theory first and learned them by running them. This log says what I built, what I got wrong, and what I changed. It does not claim years of practice.

Date reflected: 2 November 2026.

## Starting point

- I could manage a codebase in general: what to ship, in what order, and what a release should check.
- I had not set up written policy, risk-tiered merging, or agent-assisted work before this project.
- AI agents did a large share of the day-to-day work: drafting changes, running checks, keeping logs, and answering questions. I set the rules they follow, and I review what comes back.

## What I built

1. **A written release cadence and go/no-go checklist.** See [case study 1](case-studies/01-release-cut-policy.md).
2. **A proof gate for handoffs.** Agents tick a checklist before they return work. See [case study 2](case-studies/02-proof-gate.md).
3. **Risk-tiered merging.** Low-risk changes merge automatically after checks; high-risk ones wait for a person. See [case study 3](case-studies/03-risk-tiered-merge.md).
4. **A triage and tagging system.** Labels for stage, outcome, surface, owner, and risk. See [triage and tagging](triage-and-tagging.md).
5. **Supporting pieces:** a release log per sprint, an operating flow, and a roster that says who owns what, people and agents alike.

## What I got wrong at first

- **I wrote rules before I had evidence.** The first cadence was "once per sprint." I changed it the same day, after thinking through what a walk would cover.
- **Auto-merge widened the release surface.** Low-risk merges meant the release cut carried changes nobody had walked on a device. The fix was a rule about the cut, not a stricter merge rule.
- **Agents shared one tracker account,** so the assignee field stopped meaning anything. Ownership moved to a label.
- **Unassigned items slipped through anyway.** In November 2026 many items had no assignee, project or cycle, so every item is now assigned at creation as well as labelled. The label still says which agent owns it.
- **Checklists were too long at first,** which meant they got skipped. I cut them down to the lines that caught real rework.

## What I learned

- A gate is only as good as its evidence. A tick with no quoted check is an opinion.
- Write the rule, then find the first time it fails. The failure tells you what to change.
- Agents are useful for consistency and for checking many things quickly. They need a clear standard of "done" and someone to read their results.
- Keep decisions in one queue, with one recommended option. Otherwise they get lost in text.

## What I am still learning

- Whether the risk rule catches the changes that actually cause reverts. The measure I need is revert rate after low-risk merges. I have not collected it yet.
- How to measure outcomes honestly. The case studies have placeholders until I have verified counts.
- Live behaviour of the agent-answer tool and the model-routing rule. Both are built, and the live checks are still open.

## The role of AI agents

Agents did much of the drafting, checking, logging, and sweeping. A person set the policies, made the go and no-go calls, and reviewed the output. Where an agent's result was wrong or incomplete, the gate caught it and sent the work back.
