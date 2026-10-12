# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]
https://github.com/oherna25/pathreview-ai301-fa26-s3/pull/1
**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]
docs/37-api-request-body-schemas
## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

18/20

**Package analysis**

pkg-05 (nushell/nushell#18848, the keybinding merge-by-name fix). The gold label was accept; my rubric said reject, failing it on "not tested".

My rubric read it that way because the plan's test plan lists three things: re-run the issue's script and expect both `atuin` rows, re-run with two same-name same-key bindings and expect one row plus a warning, and run `cargo test` on the config crate. The test evidence shows the first one with real before/after tables. For the second it only asserts "Same-key redefine prints the one-time warning", with no output shown. My "not tested" check fails "evidence is only an assertion" and requires the decisive repro or a named check to be "shown or disclosed". It treated the unshown warning output as a missing repro step. That is a miss, because the decisive repro (both rows survive after the fix) is shown, and the PR also has a unit test covering the warning (`same_name_same_key_replaces_with_warning`). The check was too strict about non-decisive plan steps.

**Check rationale**

The check as it reads in `rubric.md`:

> | not tested | The test-evidence section, read against the plan's test plan, the reproduction's own steps, and the checks the repo-facts block names (suite, linters, pre-commit) | A command or script from the test plan or repro was actually run and its output shows the behavior the plan expected (before and after, or an after-state matching the stated expectation), and the outcome of each repo-named check that applies is shown or its omission is stated. Fail if the evidence is only an assertion ("tests pass"), the output contradicts the expected after-state, or the decisive repro or a named check is neither shown nor disclosed. A disclosed untested part passes if the delivered behavior is still verified and the PR does not claim the untested part works. | required |

It reads that way because the check judges the outcome (is the claimed evidence observable?) and not the write-up's shape, so it asks for real command output matching the plan's expected after-state. Bare assertions like "tests pass" fail, since they are what let untested PRs through the four not-tested packages. The last sentence is the honest-outcome rule. A PR that discloses an untested part still passes if the delivered behavior is verified. Without it, the check would reject any PR that does less than everything.

**Trade-offs**

This check gives up pkg-05. Requiring observable output for the decisive repro and the named checks makes it hold PRs that pair a real before/after with an asserted secondary step (the warning in pkg-05). I accept that miss: it ran 4/4 on the not-tested category, and loosening it enough to pass pkg-05 would risk letting assertion-only evidence through. pkg-11 (also a clear-accept, rejected as silent drift) is a second false reject. Overall the run scored 18/20, which meets the bar.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
