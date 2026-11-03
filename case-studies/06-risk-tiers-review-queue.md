# Case study 6: Cut the review queue without auto-merging risk

**Date reflected:** 3 November 2026
**Format:** Axios-style summary. A visual version is linked below.
**Visual version:** https://claude.ai/artifact/FmWAMGy4SDXLoNCvanR71n (private link, owner can share)

## The business problem

**Review queues slow a small team, and removing them is risky.** Every pull request waited for a person, including trivial ones. Auto-merging everything would let a risky change land unseen.

- Most businesses have this shape: the process that protects quality also caps throughput.
- Removing the queue without a rule is a gamble. Keeping it without a rule is a tax.

**Why it matters:** the fix is a rule that sorts work by consequence, not by who wrote it.

## What we did

A workflow reads each change and labels it by risk. The author cannot set the label, so a risky change cannot be talked down.

- **Low risk:** merges on its own once every required check passes.
- **High risk:** waits for a person. Triggers include database migrations, access rules, deploy and CI config, secrets, payments, server functions, dependency lock files, and any change over 300 lines or 10 files.

## Rules that come with it

- Checks are never skipped or disabled to get green.
- High-risk changes never merge automatically.
- A change that touches a screen opens as a draft until someone has used it on a device.

## Trade-offs

- Low-risk changes reach main with no human look, so the release review has to cover them.
- Size thresholds are blunt. A large generated change can be high risk on size alone. That is intended.
- A path rule can miss a risk. The list is reviewed whenever something slips through.

## Where this transfers

Any team with a review bottleneck and a real cost of failure has this shape: payments operations, claims handling, content approvals, data pipelines.

- **Decision:** sort by consequence, automate the bottom tier, and make the top tier impossible to self-certify.
- **Owner:** the product lead sets the tiers. The workflow applies them.

## Result

<!-- Fill only with verified counts from the workflow runs. Do not estimate. -->
