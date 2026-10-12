# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

Read in this order, and finish each step's notes before moving on:

1. The plan context (repro evidence, then the plan). Note: the files the plan
   names, its steps, its "not in scope" boundary, any deviation notes, and the
   test plan's commands and expected after-state. The plan comes before the
   diff because the diff is judged against it; reading the diff first lets the
   change define what "in scope" means.
2. The repo-facts block and the issue thread highlights. Note: each PR-template
   section and checklist ask, each contribution-guide ask, any stated policy
   (AI disclosure, CLA, prohibitions, discuss-first), and any explicit
   maintainer direction.
3. The diff and commit list. Note: every changed file, what each hunk does, and
   any hunk that is not the fix, its test, or a repo-required file.
4. The test evidence. Note: each command shown, its output, and which repo-named
   checks have a visible outcome.
5. The title and description last. Note: every factual claim about what changed,
   what was run, and what was left out, plus any disclosure or template content.
   The description is read last because its claims are judged against everything
   above.

## Evidence gathering

Gather the facts for each check from the part named below, using
references/evidence-guide.md for where each lives. If a needed fact is
missing, record it as absent; never infer it.

- silent drift: list the plan's files and steps beside the diff's changed
  files and hunks. Mark each hunk as inside the plan, covered by a deviation
  note or the description, or unauthorized. Mark each plan item as present in
  the diff, disclosed as omitted, or missing. Then take each claim in the
  title and description about what changed and find it in the diff; record any
  you cannot find.
- not tested: set the plan's test-plan commands and the repro steps beside the
  evidence section. Record whether each was run, what output was shown, and
  whether the output matches the plan's expected after-state. List the checks
  named in repo-facts (suite, linter, pre-commit) and record each one's visible
  outcome or stated omission.
- unreviewable: walk the diff hunk by hunk. Record any debug print,
  commented-out or dead code, formatting-only change on unrelated lines,
  drive-by edit, or stray file.
- standards wall: for each ask and policy recorded in step 2 of the read order,
  find where the description or diff honors it, or where the description says
  it is not done. Record asks that are ignored, boilerplate, or ticked without
  the thing existing. Record asks that do not apply to this kind of change.

## Check execution

Grade the checks in rubric order: silent drift, not tested, unreviewable,
standards wall. For each, apply the rubric's pass condition to the facts
gathered and write one line of evidence: the fact or quote that decided it.

- pass: the gathered facts satisfy the pass condition, including by an honest
  disclosure the rubric accepts.
- fail: the facts contradict the pass condition (an undisclosed extra or
  missing piece, a false claim, an assertion with no output, debris, an ignored
  ask).
- unclear: a needed fact is absent or ambiguous. Look once more for a
  disclosure or deviation note that settles it; if none, keep unclear.

A check may be graded from its recorded notes without rereading the package
only if no later read contradicted those notes. If the rubric or this procedure
is silent on a step you need, report the gap in the summary; do not invent a
step. Do not let a check's grade depend on the write-up's length or polish.

## Verdict assembly

Apply the rubric's verdict rule exactly: accept only if all four checks pass;
any fail rejects; unclear counts as fail. The deciding check is the first
failing (or unclear) check in rubric order; quote its evidence line in the
summary as the reason for the verdict. When every check passes, say so and
quote the strongest single piece of evidence. Write a short per-check summary,
then end the reply with the JSON block from SKILL.md, valid and last.
