# Bug lifecycle

How a bug moves from report to closed, and what proof closes it. Generic: no product names, ids, or team members.

Date reflected: 12 November 2026.

## The stages

Intake, track, fix, validate, prove, close, then watch after the next cut.

| Stage | Done when |
|---|---|
| Intake | The bug is one tracked item with a symptom, a surface, and the build or commit where it was seen. |
| Track | The item has a type label, one owner, and a status that matches reality. |
| Fix | A failing repro exists on the build before the fix, and the fix is limited to what the repro needs. |
| Validate | The same repro is run after the fix, on the same build, and the result is recorded. |
| Prove | The proof record has the fixing commit, the before and after repro, and a walk outcome per row. |
| Close | The fix is merged and the proof record is attached. |
| Watch | Any recurrence after the next cut is logged against that cut. |

## Intake

1. Every bug becomes one tracked item before any work starts. Ideas and questions are not bugs.
2. The item carries the `type: bug` label, one owner label and an assignee (see [triage and tagging](triage-and-tagging.md)).
3. A bug found during a walk is logged against that walk and the cut it was found in.
4. A duplicate is linked to the original and closed as a duplicate. It is never fixed twice.

## Track

- Status is `in progress` while the fix is being made.
- An item closes only when its proof record is attached (see Close below). Merging a fix alone does not close the bug.
- Status is never ahead of the evidence. If the fix is merged but not validated, the item stays open and says so.

## Fix

- Before starting, write the standard in one line: the repro steps and the expected result.
- Show the repro failing on the current build. A fix with no failing repro is not a fix, it is a guess.
- Change only what the repro needs. Unrelated cleanup goes in its own item.
- Never skip, disable, or quarantine a test to get green.

## Validate

- Re-run the same repro after the fix, on the same build, and record the result.
- Report results in two lists, never mixed:
  - **Walked:** the repro was run and the result was seen. Pass or fail.
  - **Cannot be simmed:** the step needs a real device, a real account, a purchase, push, or the camera. Name the reason and the owner who can run it. Never report these as verified.
- Give the fix a walk tier, using the same tiers as the post-cut walk (see [walk tiers](case-studies/01-release-cut-policy.md#quality-before-and-after-a-release)): Tier 1 for a visible or shared-flow fix, Tier 2 for anything only a device can show, Tier 3 for copy, backend, flag-off, or docs fixes.
- The walk runs after merge and never holds it. Its result feeds the proof record in the next stage, and a Tier 1 or Tier 2 fix stays open until that walk is recorded.

## Prove

The proof record for a bug holds:

- the PR link and the commit SHA that landed on main;
- the failing repro before the fix, and the passing repro after it, on the same build;
- the walk outcome for each row, including silence-is-not-a-result rows marked as not run;
- the cut the fix shipped in, once it is cut.

A proof record with a missing row is incomplete. Say which row is missing and why.

## Close

An item closes when all of these are true:

1. The fix is merged to main.
2. The after-proof is recorded, with the commit SHA.
3. Any part that needs a device is in the "cannot be simmed" list with an owner, not counted as passed.

If one of these is false, the item stays open and the reason is written on it.

## Watch

- A bug found after a cut is logged against that cut.
- The measure is bugs found after each cut, reported from the record, not estimated (see [case study 1](case-studies/01-release-cut-policy.md)).

## Closeouts

Every closeout reports counts by state: closed, open, built but not wired, partially built, killed (with who decided), and fell off (named, never silent).
