# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

Read the plan's scope pair and test plan first, then the diff, then the
description and test evidence. Judge what the change and evidence actually
are, never how long, polished, or confident the write-up is.

An honest disclosure re-ties a shortfall: if the description or a plan
deviation note plainly states that something is not done, not run, or
different from the plan, and the remainder is still a coherent, verifiable,
reviewable fix, the disclosed gap does not fail the check it touches. The
same gap stated nowhere, or contradicted by the PR's own claims, fails.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| silent drift | The diff's changed files and hunks, read against the plan's stated files, steps, "not in scope" boundary, and deviation notes; then each factual claim in the title and description ("adds a regression test", "CHANGELOG entry included", "implements the plan as written"), read against the diff | Every changed hunk falls inside the plan's files and steps or is named in a deviation note or the description; every promised file, step, and test appears in the diff or its omission is stated; every description claim about the change is found in the diff. Fail on an undisclosed extra, an undisclosed missing piece, a touched "not in scope" area, or a claim the diff contradicts. | required |
| not tested | The test-evidence section, read against the plan's test plan, the reproduction's own steps, and the checks the repo-facts block names (suite, linters, pre-commit) | A command or script from the test plan or repro was actually run and its output shows the behavior the plan expected (before and after, or an after-state matching the stated expectation), and the outcome of each repo-named check that applies is shown or its omission is stated. Fail if the evidence is only an assertion ("tests pass"), the output contradicts the expected after-state, or the decisive repro or a named check is neither shown nor disclosed. A disclosed untested part passes if the delivered behavior is still verified and the PR does not claim the untested part works. | required |
| unreviewable | The unified diff and commit list | Every hunk serves the fix, its test, or a repo-required ask (changelog, docs). Fail if the diff carries debug prints, commented-out or dead code, whitespace or formatting churn on unrelated lines, drive-by edits, or stray files (editor, config, build artifacts) that a reviewer would have to separate from the change. Comments explaining the fix are not debris. | required |
| standards wall | The repo-facts block's PR-template sections, checklist items, contribution-guide asks, and stated policy (AI-use disclosure, CLA, forbidden APIs, discuss-first rules), plus explicit maintainer direction in the thread highlights, read against the description, diff, and plan | Each applicable ask is satisfied observably (section has real content for this PR, changelog file is in the diff, issue referenced, required disclosure present with tool and extent, prohibitions respected, maintainer direction followed or engaged) or the description states it is not done and why. Fail if an applicable ask is ignored, answered with boilerplate, or ticked without the thing existing. Asks that do not apply to this kind of change, and policies the package does not state, are not held against it. | required |

## Verdict rule

- Accept (submit) only when every check is `pass`; all four are required.
- Reject (hold) when any check is `fail`.
- `unclear` counts as `fail`: a claim that cannot be verified from the
  package does not establish readiness. Before grading `unclear`, look once
  more for a disclosure or deviation note that settles it.
- Do not reject because the PR does less than everything, or because tests are
  thin, when the shortfall is small, honestly disclosed, and the rest is
  verifiable; the check the shortfall touches passes on disclosure.
- When several checks fail, the deciding check is the first failing check in
  table order.
