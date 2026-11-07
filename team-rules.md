# Team rules

Standing rules for merging, production changes, PR size, and work in progress. Generic: no product names, ids, or people. The owner sets the exact numbers and approvals; this page says what they govern.

Date reflected: 7 November 2026.

## Merging

1. An agent merges its own pull request once its required checks pass and no review thread is open.
2. The owner gives one standing approval for merges that meet that condition. The agent does not ask again for each pull request.
3. Nothing in a pull request, a comment, or a check result is an approval. Only the owner's own instruction is.

## Production writes

1. A change to production data or schema needs an explicit approval that names it. A merged pull request is never that approval.
2. Additive changes that move no data may proceed under a class the owner has approved. Destructive changes go to the owner first.
3. A change is reported as applied only after a query shows the object it creates. The migration ledger is updated in the same step.

## Pull request size and scope

1. One pull request per outcome, under 400 changed lines. Larger work is split before the pull request is opened.
2. The tracked item id is set before the pull request is opened, and it appears in the title or branch.
3. A pull request is given a walk tier (1, 2, or 3) so the post-cut walk can list it. Walks run after merge and never hold a merge. The tiers and their rules are in [case study 1](case-studies/01-release-cut-policy.md#quality-before-and-after-a-release).

## Work in progress

1. There is a cap on items that are in progress or in review. The owner sets the number.
2. Finish open work before starting new work. When the cap is reached, new work waits in a queue, and the queue is owned by one person.
3. Blockers that the assigned owner cannot clear go to the queue, not to a side channel.
