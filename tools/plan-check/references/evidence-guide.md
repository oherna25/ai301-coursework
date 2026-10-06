# Evidence guide: where evidence lives in a plan package

This guide maps every rubric check to the exact evidence source a grader should inspect and the observable conditions that count as good evidence.

## Diagnosis and grounding

Where it lives:
- the issue description or maintainer notes
- the repro-evidence block in the package
- the plan's stated cause or diagnosis section

What good looks like:
- the plan names a cause that matches the reproduced symptoms and the failing behavior, not one that ignores the evidence or predicts a different failure mode
- the diagnosis is anchored to the real observed inputs, outputs, stack traces, or steps in the repro, not to a generic guess

In live mode, this is the issue thread read alongside the posted reproduction comment. A valid diagnosis should explain the same behavior the evidence shows.

## Scope

Where it lives:
- the plan's scope statement or bounded-change section
- the files, modules, or areas named in the plan
- the repo-facts block when it states conventions or affected subsystems
- the issue context when it narrows the fix to a specific component

What good looks like:
- the plan clearly names the files or modules it will touch and explicitly says what it will not change
- the change stays focused on the root cause and does not drift into unrelated refactors, broad cleanup, or speculative rewrites

A bounded plan is not a wish list. It is a concrete change set that another engineer could inspect and judge as narrowly targeted.

## Executability

Where it lives:
- the candidate plan's implementation steps
- the repo-facts block for setup, project commands, and conventions
- any file-level notes that describe where work starts and how the fix will be applied

What good looks like:
- a stranger could begin from the repo and follow the plan without asking for missing setup details, unclear file names, or unexplained commands
- the plan states the intended order of work and the concrete artifacts or files involved, rather than vague steps like "investigate and fix"

If the plan depends on hidden context, unstated assumptions, or author-only knowledge, it fails this evidence family.

## Test plan

Where it lives:
- the plan's test strategy or planned regression test
- the reproduced failing scenario in the evidence block
- any test files or commands the plan expects to add or run

What good looks like:
- the plan says how success will be observed and ties it back to the exact reproduced bug
- the test names the failing behavior, expected result, and observable signal that distinguishes pass from fail

A decisive test plan is specific enough that a grader can tell what would count as evidence of a fix. Vague statements like "add tests” or “verify behavior” do not satisfy this standard.

## Honesty

Where it lives:
- the plan's discussion of uncertainty, risks, or unknowns
- the repo-facts block when it describes project conventions or constraints
- the plan comment if it compares expected results with current uncertainty

What good looks like:
- the plan distinguishes known facts from assumptions and labels unknowns clearly instead of pretending certainty
- if the implementation hits a surprise, the plan or update records that deviation without dressing it up as a solved problem

This is the family that catches false confidence. Honest plans do not hide uncertainty; they make it visible and still yield a credible next step.

## Comms

Where it lives:
- the plan comment itself
- the issue thread or maintainer signals in the package
- the repo-facts block for contribution policy, templates, and disclosure requirements

What good looks like:
- the plan responds to the actual thread context and the repo's stated expectations rather than shipping a generic template
- the wording aligns with maintainer guidance, contribution policy, and any AI-use or disclosure requirements described in the repo facts

A strong plan comment is not boilerplate. It acknowledges the thread, respects the repo's conventions, and signals the author understood what the maintainers were asking for.
