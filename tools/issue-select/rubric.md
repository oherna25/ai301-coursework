# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer is alive | Repo-facts block: the "maintainer first-response sample" (reply latency from accounts with Owner/Member/Collaborator badges) and commit author list. | Pass if the maintainer first-response sample shows at least one Owner/Member/Collaborator reply within 30 days of an issue being opened, OR at least one default-branch commit authored by a non-bot human account in the last 90 days. Fails only when both are absent: no maintainer reply in the sample and no human-authored commit in 90 days. | required |
| Repo in use | Repo-facts block: default-branch commit dates, latest release date if present, open/closed issue and PR counts, star/fork counts only as context not as the test. | At least 3 default-branch commits in the last 90 days, or a release in the last 180 days and at least 1 default-branch commit in the last 180 days. Zero commits in 180 days fails. | required |
| Scope fits a newcomer | Issue body and full comment thread (references/evidence-guide.md, family 3). | Pass only if the issue is one bounded, mergeable unit of work: (a) it is not itself explicitly framed as a tracking/umbrella issue whose own body says its listed sub-items should become separate issues (a boilerplate bug-report checklist like "I searched for duplicates" is not this, and a reporter's own numbered list of possible causes or fix ideas for one bug is not this either); (b) the thread shows an actual disagreement between two or more commenters about which approach to take, with no maintainer comment settling it — a single reporter listing options with nobody else weighing in is not a disagreement; (c) no maintainer comment states the fix requires changes to core internals/architecture; (d) it is not a pure usage/support question ("how do I get this to work?") with no implied code change; (e) the issue does not carry a history of two or more closed/unmerged linked PRs that already attempted this exact fix, or a pattern of contributors repeatedly claiming it and going quiet (auto-unassigned for inactivity) — that history means real difficulty behind a friendly label, regardless of how bounded the write-up reads. Any one of (a)-(e) failing fails the check. Terse write-ups with no reproduction steps still pass on their own; grade the size of the work, not the polish of the writeup. | required |
| Nobody else is already on it | Issue assignees, linked PRs, and the last 20 comments in the thread. Look for "I'm working on this," draft/open PRs referencing the issue number, and assignment fields as listed in references/evidence-guide.md. | The issue has no assignee, no open PR that mentions the issue, and no comment in the last 30 days claiming the work unless that commenter later said they dropped it. An assignee, open linked PR, or un-retracted claim fails. | required |
| Contribution policy allows AI-assisted work | Repo-facts block: the "contribution policy" line (or CONTRIBUTING.md / AI_POLICY.md / AGENTS.md / PR templates in live mode, per references/evidence-guide.md, family 5). | Pass unless the policy states an outright ban on AI-generated or AI-assisted contributions. Conditions (disclosure, required human review, required testing) pass. Silence (no stated policy) passes. | required |
| Task is still valid | Issue body vs current default-branch state described in repo-facts (recent commits touching the named files; comments that say "already fixed" / "wontfix"). | No maintainer comment marks it obsolete, and if the issue names files, those files still exist on the default branch. A "fixed in #N" / closed-as-duplicate note fails. | preferred |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
Accept only if every required check is pass. Any required fail or unclear is reject (unclear counts as fail). preferred checks never change accept/reject; they are used only to rank issues that already accepted. If two required checks conflict (for example a recent maintainer comment saying the issue is still wanted, but an open PR already implements it), the “nobody else is already on it” check wins and the verdict is reject.

