# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

**Where it lives**

- Practice submission (eval bundle, e.g. calib-01): the "Plan context"
  block holds the plan's scope pair ("Files:" and "Not in scope:"), its
  steps, and any deviation note. The "Candidate PR" block holds the
  "### Diff" (changed files and hunks), "### Commits", and the
  "### Title" and "### Description" whose claims get read against the diff.
  In calib-01 the plan says "Files: `themes.gitconfig`", "Not in scope: any
  other theme", and two steps (remove the shadowed line, verify with a strict
  parser); the diff touches only `themes.gitconfig`, one removed line.
- Your own PR (live): your `plan.md` with its deviation notes; the diff from
  `git diff main...HEAD`; your draft title and description.

**What good looks like**

- Every changed file and hunk is a file or step the plan names, or is covered
  by a deviation note or a line in the description. calib-01: one file, one
  deleted line, both named in the plan.
- Every plan step has a counterpart in the diff or an explicit "not done"
  statement. calib-01's verify step has no diff hunk by design (it is a
  check, not a change) and shows up in the test evidence instead.
- Every claim in the description can be found in the diff. calib-01's "Removes
  the shadowed first `file-decoration-style` line" is exactly the deleted line.
- Silent drift in either direction fails: a hunk the plan never authorized
  (more), or a promised file, step, or test missing with no note (less), or a
  description claiming "as planned" or "CHANGELOG entry included" that the
  diff does not bear out. A disclosed deviation or omission re-ties the
  mismatch and passes.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

**Where it lives**

- Practice submission (eval bundle): the "### Test evidence" section under
  "Candidate PR", read against the "Test plan:" sentence and the "Repro
  evidence" paragraph in "Plan context", and against the checks named in the
  "Repo facts" block. calib-01's plan test plan is "re-run the configparser
  repro, expect a clean parse; `delta --show-syntax-themes` smoke check"; its
  evidence section shows the strict-parser command, "before: ...
  DuplicateOptionError", "after: parsed OK", the `git config --get-all` output,
  and the theme render check.
- Your own PR (live): the test plan in your `plan.md`, the repro steps from
  your repro report, and your captured terminal output (suite run, linters,
  pre-commit) pasted into the PR description; the repo's CONTRIBUTING.md or
  PR template names which checks it expects.

**What good looks like**

- The commands from the test plan and repro were actually run and the output
  is shown, with the expected after-state visible: calib-01 shows the
  before error and the after "parsed OK", plus a second signal (one value
  from `git config --get-all`).
- Each repo-named check that applies has a visible outcome (pass counts, clean
  lint) or the description says it was not run and why. If the repo names no
  checks, the plan's own run is enough.
- Decisive evidence names an observable behavior and the expected result.
  "Tests pass", "verified locally", or output that does not match the plan's
  expected after-state proves nothing and fails. An untested part that is
  disclosed passes if the delivered behavior is still verified and the PR does
  not claim the untested part works.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

**Where it lives**

- Practice submission (eval bundle): "### Diff" (the unified diff, hunk by
  hunk) and "### Commits" under "Candidate PR". calib-01's diff is a single
  hunk in `themes.gitconfig` with one `-` line and unchanged context; the
  commit list is one commit.
- Your own PR (live): `git diff main...HEAD` and `git log main..HEAD
  --oneline` on your branch; also `git status` for stray untracked files
  you might have committed.

**What good looks like**

- Every hunk is the fix, its test, or a file the repo requires (changelog,
  docs). A reviewer can see the fix at a glance with nothing to separate out.
  calib-01 is the model: one removed line, no other hunk.
- Debris tells to look for: debug prints or logging left in, commented-out
  code, dead code or unused imports the change introduced, whitespace or
  formatting-only edits to unrelated lines, drive-by fixes to other things,
  and stray files (editor settings, build output, scratch scripts).
- A comment explaining why the fix works is not debris. Size alone does not
  fail the check; unrelated content does. Unrelated hunks that also break the
  plan's boundary are graded under plan fidelity as well.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

**Where it lives**

- Practice submission (eval bundle): the "Repo facts" block's "pull requests:"
  line (template sections and checklist asks) and "contribution policy:" line
  (including any AI-use rule); the "Thread highlights" for explicit
  maintainer direction; then the candidate PR's "### Title", "### Description",
  and "### Diff" to see whether each ask is honored. calib-01's repo facts say
  "no PR template; the contribution docs ask that PRs stay small and reference
  the issue" and "no stated AI policy"; the description references "(#2211)"
  and the diff is one line.
- Your own PR (live): the repo's `.github/PULL_REQUEST_TEMPLATE` (or the
  template shown when you open a PR), CONTRIBUTING.md, any AI_POLICY.md, and
  the issue thread for maintainer comments; your draft description is what you
  check them against. Your `voice-guide.md` is separate and does not enter
  this check.

**What good looks like**

- Every ask that applies is met observably: template sections filled with
  content specific to this PR, the issue referenced, a changelog entry present
  in the diff when asked, a required AI disclosure present naming the tool and
  extent, stated prohibitions respected, maintainer direction followed or
  explicitly engaged. calib-01: the issue is referenced and the PR is small,
  which are the only asks, so it passes.
- Or the description plainly says an ask is not done and why.
- Fail on an ask that is ignored, a section filled with boilerplate that says
  nothing about this PR, a box ticked without the thing existing, or a
  disclosure the policy requires but the description lacks. Asks that do not
  apply to this kind of change, and policies the package does not state, are
  not held against the PR.
