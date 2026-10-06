# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

Read the issue first, then the repro evidence, then the candidate plan, and finally the relevant comments or repo facts. This order matters because the grader must establish the observed bug and the expected behavior before judging whether the plan matches it. The issue tells you what the package is trying to fix; the repro evidence shows what is actually broken; the plan then becomes the thing to compare against that baseline.

Record for each part:
- the stated bug or request
- the reproduced behavior and any exact failure signals
- the proposed fix scope and the files it names
- any missing or contradictory details

## Evidence gathering

For each rubric check, pull the fact from the exact part of the package that owns it:

- diagnosis: read the issue and the repro evidence together, then note the claimed root cause and the observed failure mode
- scope: read the candidate plan's scope statement and any file list, then record what it will change and what it explicitly leaves alone
- test: read the plan's test strategy or test code, then record the reproduced scenario and what it asserts
- execution: read the plan steps and repository facts together, then note whether a stranger could start implementing without guessing missing setup

If a required fact is missing, record it as absent rather than inferring it.

## Check execution

Grade each check as P, F, or ? in this order:

1. diagnosis
2. scope
3. test
4. execution

Use the following rules:
- P: the evidence clearly satisfies the pass condition
- F: the evidence clearly fails the pass condition or is contradicted by the package
- ?: the evidence is incomplete, ambiguous, or missing, so the grader cannot tell

A check may be graded without rereading the whole package only when the relevant evidence has already been recorded and no new contradiction appears. If the evidence is incomplete, do not invent missing details; mark the check as ? and carry that through the final verdict.

## Verdict assembly

Apply the rubric's verdict rule exactly: ready only if every required check passes. Preferred checks never change the verdict. If any required check is unclear or fails, the package is held. In the output, quote the decisive evidence for the failing or unclear required check so the reason for the verdict is explicit and reviewable.
