# Instruction files for AI agents

What a standing instruction file is, why an AI agent needs one, and how to write one that gets followed.

Date reflected: 11 November 2026.

## The short version

An AI agent starts every session with no memory of your last one. It does not know your rules, your tools, or what you already decided. An instruction file is a plain text file that the agent reads at the start of each session, so the rules are there every time, without you repeating them.

In Claude Code the file is usually called `CLAUDE.md` and sits at the top of the repository. Other tools use other names for the same idea. The name matters less than the habit: one short file, written down, that the agent reads first.

## Why an agent needs one

Without a file, you pay for the same explanation again and again:

- Every session starts from a blank slate. The agent guesses how you merge, how you release, and what "done" means.
- Guesses differ between sessions. Two agents given the same task can produce two different answers, and neither is wrong by any rule you wrote, because you wrote none.
- Rules that exist only in a chat get lost when the chat ends.
- A rule that is written down can be checked. A rule in someone's head cannot.

The file is the cheapest place to put a decision once, so that it holds for every later session.

## What goes in it

Keep only what an agent would otherwise get wrong. Good candidates:

1. **How to check the work.** The exact commands that must pass before a change is handed back, for example the type check and the test run.
2. **Standing rules.** What the agent may do alone (merge a low-risk change once checks pass) and what it must ask about (a production write, a new dependency, a new word a user will see).
3. **What "done" means.** The stages a piece of work moves through, and which stage the agent is allowed to claim.
4. **Things that have bitten you before.** Each one with the reason. A rule without a reason gets argued with; a rule with a reason gets applied to cases you did not foresee.
5. **Shorthand.** The team's names for things, so the agent does not guess what a label or an abbreviation means.
6. **What not to touch.** Files, folders, or settings that look editable but are owned by someone else or generated.

## What stays out of it

- **Secrets and credentials.** Never. Not in the file, not in a comment, not in an example. Point to where they are kept instead.
- **Things the code already says.** The agent can read the code. Repeating a function's behaviour in the file creates a second copy that drifts.
- **History.** Who decided what in March belongs in a decision record, not in the file. The file says what is true now.
- **Long essays.** A long file gets skimmed and then skipped. If a rule needs three paragraphs, put the rule in one line in the file and link the explanation.

## How to write one that gets followed

- **Write each rule as an instruction the agent can check.** "Run the type check before every commit" can be verified. "Be careful with the database" cannot.
- **Put the reason on the same line.** "Never edit a migration once it is on main, because the database has already run it."
- **Keep it short.** Start with the ten lines that would have saved the last three sessions. Add a line when a session gets something wrong, not before.
- **Date it, or date the rules that change.** A rule that was true in November may be false in December. A date tells the next reader how far to trust it.
- **Read it back after editing.** Ask the agent to restate the rules in its own words. A gap shows up in the restatement.
- **One file per repository.** Add a second file in a subfolder only when one part of the repository has rules that would confuse the rest.

## A small example

```markdown
# Instructions for this repository

## Before handing back any change
- Run the type check and the test suite. Quote the result.
- Never skip or disable a test to get green. Say which test is failing and why.

## Merging
- Low-risk changes merge once required checks pass. Do not ask again for each one.
- Anything that touches the database schema waits for the owner's typed approval.

## Done means
- Built: the code is written and the checks pass.
- Verified: the walk on a device has been run and passed.
- Shipped: merged and deployed.
- Accepted: the owner has seen it working.
- Claim only the stage you have reached.

## Why
- We do not claim "verified" from a passing check alone. A check can pass on code that does not do the thing.
```

## Where this sits in the playbook

- The rules a file carries are the team's standing rules. The [team rules](team-rules.md) page is the human version of the same decisions.
- Writing the file is itself a planning step. The questions you answer while writing it are covered in [interview before building](interview-before-building.md).
