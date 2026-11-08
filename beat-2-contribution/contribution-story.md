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
**Pull Request:** [GitHub PR link, once opened

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

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
