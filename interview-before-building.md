# Interview before building

A workflow where the agent asks you questions before it writes anything, so the plan comes from your answers rather than from its guess.

Date reflected: 11 November 2026.

## The idea

Most wasted agent work starts with a plausible guess. The agent reads a short request, fills the gaps with its own assumptions, and builds something coherent that is not what you wanted. The fix is cheap: the agent asks first.

The interview is not a form. It is a short conversation whose output is a written standard: what "done" looks like, what is in scope, what is out, and which choices you made.

## When to use it

- The request names an outcome but not the steps.
- The work is visible to a user, changes data, or costs money.
- Two reasonable readings of the request would produce different products.
- The work is new to the team, so there is no earlier standard to copy.

Skip it for a one-line fix with a failing test that already states the expected result.

## The steps

1. **State the goal in one sentence.** You say what should be true when the work is finished. The agent may restate it, and you correct the restatement.
2. **The agent asks questions in small batches.** Three to seven at a time. Each question offers the default the agent would take, so "yes" to the defaults is a valid answer.
3. **Ask only what changes the outcome.** If the agent can look something up in the code or the docs, it looks it up and does not ask. Questions are for choices only you can make: who it is for, what must not change, what you would be embarrassed to ship.
4. **Write the answers down as the standard.** One short list: the done definition, the scope in, the scope out, the decisions made and their reasons. Record it where the team will see it, in the work item or the pull request, not only in the chat.
5. **Play the plan back in five lines or fewer.** You approve it, or you correct one line. Only then does the build start.
6. **Build against the standard.** When the agent reports, it reports against the list from step 4, one line per item, marked with the stage it reached.
7. **Keep the answers.** A question answered once is not asked again. Anything the answers settled that will apply to later work goes into the [instruction file](agent-instructions.md).

## Rules for the agent

- Do not ask a question you could answer by reading the code.
- Offer a default with every question. A question with no default is a chore.
- If an answer conflicts with an earlier one, stop and ask which one holds. Do not pick silently.
- If you cannot name the most likely reading, ask. If you can, state the reading you chose and proceed, then say so in the report.
- Ask once. If a question was answered, record the answer and move on.

## Example questions

These are shapes, not a script:

- "Who uses this screen first: a new user or someone who has used it for a month? I will design for the first visit and check the second." (Default: the first visit.)
- "Should this change touch the database? If yes, I will prepare the change and wait for approval before anything runs against production." (Default: no database change.)
- "Is there a frame or a spec this must match? If none, I will not build the screen yet." (Default: wait for one.)
- "Which of these are required for the first release, and which can follow?" (Default: the smallest set that completes one user task.)

## What a good interview produces

A standard short enough to read in one minute, that answers:

- What is done, in one sentence a user would recognise.
- What is in scope, and what is explicitly not.
- Which decisions were made, by whom, and why.
- What will be checked, and by whom, before the work is called built.

## Common failures

- **Too many questions at once.** The reader stops answering. Keep batches small.
- **Questions with no default.** Every answer becomes a decision the reader has to invent.
- **Asking what the code already says.** It wastes the reader's time and suggests the agent did not look.
- **Treating the interview as approval.** A yes to the plan approves the plan. It does not approve a production write, a new dependency, or a new user-facing word. Those still need their own yes.
- **Skipping the write-down.** An interview that lives only in a chat is lost at the next session.

## Related

- The standard it produces is the "write the standard before starting" principle in the [README](README.md).
- The instruction file that keeps the answers is covered in [instruction files for AI agents](agent-instructions.md).
- The stage a piece of work reaches is checked against the [bug lifecycle](bug-lifecycle.md) and the proof gate in [case study 2](case-studies/02-proof-gate.md).
