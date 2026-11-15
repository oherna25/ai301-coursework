# Opening a fix for Mergebot's stale approvals, and the scout and voice guard I used to get there

## Overview

Mergebot, the bot that merges PyTorch pull requests, still counts a reviewer's approval after someone asks that same reviewer to review again, because GitHub keeps the old approval on a re-request. I picked this issue (pytorch/test-infra#5543) with an issue scout I built, found that the code actually lives in pytorch/pytorch, reproduced the bug on real PR data, and opened a fix with five tests: https://github.com/pytorch/pytorch/pull/203945. As of 2026-11-14 the PR is open and unmerged, with no human review yet. The part of the toolkit I wrote myself is the scout's search strategy and grading rubric, plus the voice guide that a hook (the "voice guard") checks my GitHub comments against.

## What happened

**Picking the issue.** I wrote a search strategy from my fit profile (Python, less reliance on AI, nothing too high-tech) and ran the scout. It ranked test-infra#5543 first and passed over executorch#9500 (C++, someone else already has a PR) and executorch#10580 (needs a Qualcomm Android device). The scout graded the issue page, not the code. When I searched for the function the issue was about, `get_approved_by()` was not in test-infra at all. It is in pytorch/pytorch's `.github/scripts/trymerge.py`. So I added a required rubric check to the scout, "Code lives in this repo". The scan note I wrote for it says that under the new check #5543 "would have been `fail` (symbol found only in pytorch/pytorch)". That is the change to my own tool. I also posted a claim on the issue that asks the maintainer to confirm the target repo.

**Reproducing it.** The full test suite hit a local GraphQL rate limit, so I fed real review data from GitHub's REST API into the unmodified `trymerge.py` at commit `42ce6b4`, using the PR named in the issue (pytorch/pytorch#132216). The output:

```
pending review requests: ['ezyang', 'jansel', 'gujinghui', 'EikanWang']
Mergebot get_approved_by(): ['ezyang']
ezyang approval counted although re-requested: True
```

That is the bug on real data, not a made-up case.

**Changing my plan.** My claim comment proposed adding `reviewRequests` to the GraphQL query `GH_GET_PR_INFO_QUERY`. While building, I saw that the query's text is the cache key for the recorded GraphQL fixtures in `test_trymerge.py`, so editing it would invalidate all of them. I rebuilt the fix over REST instead: a cached `get_requested_reviewers()` that `get_approved_by()` uses to drop approvals from re-requested reviewers, and falls back to the old behavior if GitHub can't be reached, so a network error doesn't block merges. The PR description says I deviated from my own claim and why. My first test run also errored because `GitHubPR(...)` calls GraphQL, so I added the same class-level `gh_graphql` mock the other test classes use. The key test, from commit `b8a8425`:

```python
@mock.patch("trymerge.gh_fetch_json_dict", return_value={"users": [{"login": "Malfet"}]})
def test_approval_is_dropped_when_reviewer_is_re_requested(self, mock_fetch, *args):
    pr = self._pr([("malfet", "APPROVED"), ("seemethere", "APPROVED")])
    self.assertEqual(pr.get_approved_by(), ["seemethere"])
```

Before the change, running `python -m unittest test_trymerge.TestReRequestedReviewApproval` gave 1 failure out of 5, and it was this test. After the change it prints `Ran 5 tests ... OK`, and `Ran 18 tests ... OK` together with the existing `TestAuthorizedWithoutGreenlight` class.

**The voice guard stopped my claim draft.** My voice guide has a rule for claims: "A claim says I want the issue, what I have already done (read the thread, reproduced it), my concrete first step, and a timeframe I can keep. I do not promise a patch before I have isolated the cause." The guard's log shows it working:

```
2026-11-11 20:47 [hook] stop: rule broken: "A claim says I want the issue, ..." | target: gh issue comment .../issues/5543 --body-file
2026-11-11 20:48 [hook] pass | target: gh issue comment .../issues/5543 --body-file
```

I revised the draft and it passed a minute later. The revised claim, which includes "I expect to report back here within a week of your answer", is the comment posted 2026-11-12. One honest note: that comment repeats the claim I had already posted on 2026-11-07, before the guard existed, so the issue thread now holds two near-identical comments from me.

**Where it landed.** The result I can point to is small. The PR is open, and the EasyCLA bot first said "CLA not signed" and now shows it signed. Dr. CI posted a status on the PR and the triage bot labeled it. The label that matters is `missing actionable issue`, with this comment: "Such PRs are a low priority for maintainers to review and might not get a response given the very high volume of PRs we receive." The five CI workflows were also still waiting for a maintainer to approve them. No maintainer has replied on the PR or on the issue. The other claimant on the issue, vineetagarwal54, has not replied to my offer to coordinate either. So nothing has merged, and I can't say a maintainer has confirmed my reproduction.

## Limitations and what's next

The fix is not yet shown to work in the real merge flow. I ran only the new tests and the existing `TestAuthorizedWithoutGreenlight` class, not the full `test_trymerge.py` or lint, and the PR says so. It also adds one REST call per approval check, which maintainers may or may not want. The bigger limit is process. pytorch/pytorch deprioritizes PRs without an `actionable` issue or a named maintainer, and #5543 is labeled only `good first issue` and sits in a different repo. I did not read the PR template and contribution rules before I wrote the code, and that is why the PR carries the `missing actionable issue` label.

The tools have limits too. The scout now checks which repo holds the code, but it still can't see who else has claimed an issue until I read the thread. The voice guard only checks commands it can parse, so a post through the browser or a raw `gh api` call walks around it. It did not stop me from posting the claim twice.

What I'd do next: ask in the issue thread for a maintainer to label #5543 `actionable`, since adding that label requests re-triage of open PRs automatically. I'd add a "read the target repo's contribution rules and PR template" check to the scout, so that problem shows up before I write code. And I'd make the guard also compare a new comment against what I have already posted on the thread.
