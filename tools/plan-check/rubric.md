# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | The plan's stated cause, read against the reproduced evidence and the bug description. | Passes if the plan identifies a plausible root cause that matches the evidence and does not contradict it. | required |
| scope | The plan's scope statement and the files it says it will change, read against the repo facts and the issue. | Passes if it names the concrete files or modules to change, states what it will not touch, and stays bounded to the root cause without unrelated changes. | required |
| test | The test plan or added regression test, read against the reproduction and expected behavior. | Passes if the plan includes an automated test that exercises the bug and makes the expected outcome observable. | required |
| execution | The plan's setup and implementation steps, read as if for a stranger starting from the repo. | Passes if someone else could follow the steps without missing setup, commands, or required context to begin the fix. | preferred |

## Verdict rule

Ready if every required check passes. Preferred checks never change the verdict. If any required check is unclear or fails, the package is held. Unclear counts as fail.