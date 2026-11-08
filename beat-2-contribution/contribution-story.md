# Contribution: Mergebot still counts an approval after the reviewer is re-requested

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** osmar hernandez
**GitHub Username:** oherna25
**Issue:** https://github.com/pytorch/test-infra/issues/5543
**Pull Request:** https://github.com/pytorch/pytorch/pull/203945

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built the issue scout and used it to pick test-infra#5543**

I wrote a search strategy from my fit profile (Python, less AI, nothing too high-tech) and ran the scout over GitHub, then ranked candidates against the rubric. It ranked test-infra#5543 (Mergebot counts an approval after the reviewer is re-requested) as the best fit and passed on executorch#9500 and #10580. What fell short: the scout can't tell where the code behind an issue lives. Reading the code showed Mergebot's approval logic is in pytorch/pytorch `trymerge.py`, not test-infra, which the scout's own note had told me to confirm. I also found a second claimant on the issue, so I posted my claim with the proposed approach and a question about the target repo instead of coding first.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched GitHub with queries built from my fit profile: I know Python, I want to understand it better, I want to rely less on AI when looking for bugs, and I want to avoid anything too high-tech. The scout ranked the candidates by fit. test-infra#5543 came out on top: the task is stated plainly (make Mergebot ignore an approval once a new review has been requested from that reviewer), it is Python logic I can test, there is no assignee and no open PR, and the last claim was on 2026-07-13, more than 30 days ago. Its verdict was not a reject, so I did not choose against my tool. The other candidates lost: executorch#9500 is C++ and already has an open PR (#21875) from someone else, and executorch#10580 needs a Qualcomm Android device, which conflicts with avoiding high-tech work. What I hope to learn is how a real bot reads GitHub's review data and how to change it safely.

After claiming, I checked the code and found the logic lives in pytorch/pytorch, so my claim comment asks the maintainer to confirm the target repo. It also notes that another student (`vineetagarwal54`) asked for the issue earlier and got no reply, and offers to coordinate. My read of the tool: the ranking held up, but it grades the issue page and not the codebase, so it missed the wrong-repo problem until I read the code. I would add a rubric check that the code the issue describes exists in the repo the issue is filed in.

**Claim comment:** https://github.com/pytorch/test-infra/issues/5543#issuecomment-6714556478

**Toolkit**

- Tool: issue-scout, with my own search strategy (queries traced to my fit profile) and rubric. I ran the scan and read the ranked list against the issue threads.
- What it produced: a ranked list that put test-infra#5543 first, with executorch#9500 and #10580 passed over for stated reasons.
- Difficulties: it never checks where the described code lives, so it could not catch that the fix belongs in pytorch/pytorch. It also did not surface the second claimant until I read the thread.
- What changed: I posted a claim that asks about the target repo and offers to coordinate. I would add a "code lives in this repo" check to the rubric.

---

## Understanding the Issue

**Problem Description**

Mergebot (the bot that merges pytorch PRs) still counts a reviewer's approval after someone asks that reviewer to review again. GitHub does not dismiss the old approval on a re-request, so a PR can look approved when its reviewers have not actually signed off on the latest state.

**Expected Behavior**

Once a reviewer has a pending review request, Mergebot should stop counting their earlier approval until they approve again.

**Current Behavior**

`get_approved_by()` returns every reviewer whose latest non-COMMENTED review is APPROVED, including reviewers who are also in the PR's pending requested reviewers. On pytorch/pytorch#132216 it returned `['ezyang']` while ezyang was re-requested.

**Affected Components**

`PR.get_approved_by()` and `PR._get_reviews()` in `.github/scripts/trymerge.py` in pytorch/pytorch, and the tests in `.github/scripts/test_trymerge.py`. The issue is filed in pytorch/test-infra, which holds no Mergebot approval logic.

**Toolkit**

- Tool: Claude Code with `gh`, reading the issue thread and `trymerge.py`.
- What it produced: the finding that the approval logic is in pytorch/pytorch and that `_get_reviews()` never looks at pending requests.
- Difficulties: the issue gives no hint about which repo holds the code; I only found it by searching the code.
- What changed: I asked the maintainer in my claim comment to confirm the target repo instead of coding in test-infra.

---

## Reproduction Process

**Environment Setup**

Windows 11 Pro, Python 3.14.3, PyYAML 6.0.3 and requests 2.32.5, `gh` CLI logged in as oherna25. The code is `.github/scripts/trymerge.py` in pytorch/pytorch, at `main` commit `42ce6b4`. I forked pytorch/pytorch and made a sparse checkout of the fork (`git clone --filter=blob:none --no-checkout --depth 1`, then `git sparse-checkout set .github/scripts`), because the full repo is huge and only the scripts are needed.

Challenges: pytest isn't installed, so I ran the tests with `python -m unittest`. The recorded-GraphQL tests hit a "Rate limit exceeded" error when run locally, so the full `test_trymerge.py` gave no usable baseline. I worked around it by feeding real review data from the REST API directly into `GitHubPR._reviews`.

**Steps to Reproduce**

1. Fetch the real data of pytorch/pytorch#132216, the PR from the issue thread: `gh api repos/pytorch/pytorch/pulls/132216/reviews` and `.../requested_reviewers`.
2. In `.github/scripts` on unmodified `main`, build `GitHubPR("pytorch", "pytorch", 132216)` and set `pr._reviews` from the REST reviews.
3. Call `pr.get_approved_by()`. Observed: it returns `['ezyang']`, even though `ezyang` is in the PR's pending requested reviewers (ezyang, jansel, gujinghui, EikanWang). The approval is counted for a re-requested reviewer.

**Reproduction Evidence**

- **Commit showing reproduction:** none. The reproduction was a throwaway script run against unmodified `main` (`42ce6b4`), so there is no commit for it. The fix commit is https://github.com/oherna25/pytorch/commit/b8a8425.
- **Screenshots/logs:** script output: `pending review requests: ['ezyang', 'jansel', 'gujinghui', 'EikanWang']`, `Mergebot get_approved_by(): ['ezyang']`, `ezyang approval counted although re-requested: True`.
- **My findings:** the bug reproduces. GitHub itself reports `reviewDecision: APPROVED` for that PR while the re-requests are pending, matching ZainRizvi's comment that GitHub keeps the old approval by design. I also found that the logic lives in pytorch/pytorch, not test-infra where the issue is filed.

**Toolkit**

- Tool: Claude Code with `gh` and Python, running the unmodified `trymerge.py` on real PR data.
- What it produced: A script showing `get_approved_by()` returning `['ezyang']` for pytorch/pytorch#132216 while ezyang had a pending re-request.
- Difficulties: Recorded GraphQL tests hit a local rate limit, so I fed REST review data into `GitHubPR._reviews` instead of running the full suite.
- What changed: I used the real data of the PR named in the issue as the reproduction, not a made-up case.

---

## Solution Approach

**Analysis**

`_get_reviews()` in `trymerge.py` keeps each login's latest non-COMMENTED review, and `get_approved_by()` returns every login whose latest review is APPROVED. Neither reads the PR's pending review requests, and GitHub keeps the old APPROVED review on a re-request, so a re-requested reviewer's approval is still counted.

**Proposed Solution**

Make `get_approved_by()` drop approvals from logins that have a pending review request, read from the REST `requested_reviewers` endpoint. If GitHub cannot be asked, return the old result so a transient failure does not block merges. Not changing: merge rules, `get_changes_requested_by()`, how reviews are fetched, and `GH_GET_PR_INFO_QUERY`.

**Implementation Plan**

1. Modify `.github/scripts/trymerge.py`: add `GitHubPR.get_requested_reviewers()` (cached, lowercased logins, empty on failure) and filter `get_approved_by()` with it.
2. Add `TestReRequestedReviewApproval` (5 tests) in `.github/scripts/test_trymerge.py`.
3. Open the PR from the fork branch against pytorch/pytorch.

Deviation: my claim comment proposed adding `reviewRequests` to `GH_GET_PR_INFO_QUERY`. I built it over REST instead, because the query's text is the cache key for the recorded GraphQL fixtures in `test_trymerge.py`, so changing it would invalidate all of them. The PR description says so.

**Toolkit**

- Tool: Claude Code, used to draft the patch and tests; I reviewed the diff.
- What it produced: the `get_requested_reviewers()` change and 5 unit tests (commit `b8a8425`).
- Difficulties: the first version of the tests errored because `GitHubPR(...)` calls GraphQL, which hit a rate limit; I added the same `gh_graphql` mock the other test classes use.
- What changed: the REST approach replaced the GraphQL one from my claim comment, and the tests were fixed to mock GraphQL.

---

## Testing Strategy

- Before the change: `python -m unittest test_trymerge.TestReRequestedReviewApproval` from `.github/scripts`. `test_approval_is_dropped_when_reviewer_is_re_requested` fails (1 failure of 5).
- After the change: the same command prints `Ran 5 tests ... OK`. Together with the existing `TestAuthorizedWithoutGreenlight` class: `Ran 18 tests ... OK`.
- Reproduction re-run: the 5 tests cover approve with no request (counted), approve then re-request (dropped, case-insensitive), request cleared (counted again), GitHub failure (old behavior), and no approvals (no request made).
- Not run: the full `test_trymerge.py` (local GraphQL rate limit) and lint (`spin fixlint`). The PR says so and relies on CI for both.

**Toolkit**

- Tool: Claude Code writing `unittest` tests, run with `python -m unittest`.
- What it produced: 5 tests; before the change 1 fails, after it all 5 pass, and with `TestAuthorizedWithoutGreenlight` 18 pass.
- Difficulties: pytest and lint tools are not installed locally and the full `test_trymerge.py` could not be run, so I could not show a full-suite or lint result.
- What changed: The PR states what was not run and relies on CI for it.

---

## Implementation Notes

**2026-11-07**

Ran the scout and picked test-infra#5543. Read the thread: GitHub keeps an old approval on a re-request, so the fix has to be built in the bot. Forked and cloned test-infra, then found the approval logic isn't there; it is `get_approved_by()` in pytorch/pytorch `trymerge.py`. Posted my claim comment with the plan and two questions (target repo, fixture churn).

**2026-11-07**

Reproduced the bug by running the unmodified `trymerge.py` on the real data of pytorch/pytorch#132216: `get_approved_by()` returned `['ezyang']` while ezyang was re-requested. Wrote a first fix, then reverted it when told to only reproduce. Re-applied it later, changing the plan from GraphQL to REST so the recorded fixtures stay valid. Wrong turn: the first test run errored until I added the GraphQL mock.

**2026-11-07**

Committed `b8a8425` and pushed it to my fork. The PR was opened as #203945 and I rewrote its body with the testing evidence and AI disclosure. Wrote down the risk that it is auto-closed without an `actionable` issue or a backing maintainer.

**Toolkit**

- Tool: Claude Code and git, working in a sparse checkout of my fork.
- What it produced: Branch `fix/trymerge-ignore-approval-on-re-request`, commit `b8a8425`.
- Difficulties: The first test run errored because the tests needed the same GraphQL mock as other classes; the sandbox also denied the first fork command.
- What changed: Added the class-level mock; I forked the repo myself.

---

## Pull Request

**PR Link:** https://github.com/pytorch/pytorch/pull/203945

**PR Description:** Links the issue (`Fixes https://github.com/pytorch/test-infra/issues/5543`) and my claim comment, and says there is no maintainer "Supported by" handle yet. It states BC-breaking: No, lists the 5 tests with the before/after output, states what I did not run (full suite, lint) and what is not changed, and discloses the AI assistance (Claude Code). The Summary section is left for me to write, since the template says human written only.

**Maintainer Feedback:**

- 2026-11-07: none yet. The issue thread has no maintainer reply to my claim comment.

**Status:** Awaiting review. Risk: pytorch/pytorch auto-closes PRs without an `actionable` issue or a backing maintainer, and neither exists yet.

**Toolkit**

- Tool: `gh` and the GitHub PR template; Claude Code drafted the body from my reproduction and test evidence.
- What it produced: PR #203945 with a filled template and real before/after test output.
- Difficulties: The PR was opened with the template still unfilled and not as a draft; pytorch/pytorch auto-closes PRs without an `actionable` issue or a backing maintainer, and neither exists yet.
- What changed: I rewrote the body with `gh pr edit`. I still need to write the Summary myself, because the template says human written only.

---

## Learnings and Reflections

**Technical Skills Gained**

Reading a real bot's review logic (`_get_reviews()` keeps the latest non-COMMENTED review per login) and how GitHub's GraphQL `reviewDecision` differs from its REST reviews; using a sparse checkout to work in a huge repo; mocking network calls in `unittest`; and that a recorded-fixture test suite is tied to the exact text of its GraphQL query.

**Challenges Overcome**

The code lived in a different repo than the issue, which I only found by searching the code; the test environment had no pytest and rate-limited GraphQL, so I mocked the network and ran `unittest`; and the PR template's rules (an `actionable` issue or backing maintainer, a human-written summary) mean the PR may be closed regardless of the code.

**What I'd Do Differently Next Time**

Check the target repo, the PR template and the AI policy before writing code, not after. I would read the contribution rules first and ask the maintainer to confirm the repo and approach, then build, so the PR opens ready for triage instead of unfilled.

---

## Resources Used

- The issue thread, where ZainRizvi explained GitHub's by-design behavior: https://github.com/pytorch/test-infra/issues/5543
- pytorch/pytorch CONTRIBUTING.md (PR lifecycle and pre-conditions) and the PR template, which set the bar for the description
- pytorch/pytorch#132216, the real PR whose data reproduced the bug
