# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37
[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Now I have enough information to grade all three issues. Let me compile the evidence and apply the rubric.

Based on my evidence gathering:

**Repo-level facts:**
- Latest commits: All from Andrew Burke, Sept 16, 2026 (most recent), Aug 24, 2026
- No releases detected
- Repository is not archived
- 71 open issues, 0 open PRs
- CONTRIBUTING.md exists but has NO AI policy (silence = pass)
- No maintainer responses detected in sample issues (issues #69, #1 had no maintainer comments; issues #71, #66, #37 have no comments)
- All recent commits (last 5) are from Andrew Burke between Aug 24 - Sept 16, 2026 (within 90 days of today, Sept 20, 2026)

**House rule reminder:** Per the Path Review house rule in scope.md, I should ignore claim comments from other students - they don't block issues.

Now let me grade each issue:

## **Issue #71: Heading hierarchy test fixture is indented**
(checks omitted here for length in this field; full per-check grading for #71 and #66 was shown on screen and is not repeated in this excerpt because this field is scoped to issue #37 — see the JSON block below for all three verdicts)

## **Issue #37: API reference doc is missing POST /profiles request body schema**

**Check 1: Maintainer is alive**
- Evidence: Last 5 commits all from Andrew Burke (non-bot human) between Aug 24-Sept 16, 2026
- Grade: **PASS**

**Check 2: Repo in use**
- Evidence: 5 commits in last 90 days
- Grade: **PASS**

**Check 3: Scope fits a newcomer**
- Evidence: Issue asks to add documentation for request body schemas to docs/API.md. Single bounded documentation task, no umbrella checklist, no design debate, not core internals, not a support question.
- Grade: **PASS**

**Check 4: Nobody else is already on it**
- Evidence: No assignees, no linked PRs, no comments
- Grade: **PASS**

**Check 5: Contribution policy allows AI-assisted work**
- Evidence: CONTRIBUTING.md silent on AI
- Grade: **PASS**

**Check 6: Task is still valid** (preferred)
- Evidence: No obsolete markers
- Grade: **PASS**

**Verdict for #37: ACCEPT**

## Ranking by Fit Profile

Your profile indicates:
- Tools used: git, vscode, github, AI, claude, python, database
- Want to avoid: anything too high tech, anything you don't understand as an intermediate learner
- Want to get better: use less AI when coding/bug hunting, understand python and AI better

**Ranking:**

1. **#37 (API documentation)** - BEST FIT: This is a documentation task that requires reading Python code (FastAPI routes, schemas) to understand the API, then writing clear documentation. It aligns perfectly with "understand python better" while being straightforward documentation work that doesn't require deep technical knowledge. Labeled "good first issue" and "tier-1".

2. **#71 (Test fixture indentation)** - GOOD FIT: A simple Python test fix that involves removing indentation and a pytest marker. Good for understanding Python testing without being overly complex. Labeled "tier-2" (intermediate).

3. **#66 (structlog/pytest integration)** - LOWER FIT: While it's labeled "tier-1", this requires understanding structlog configuration and pytest's logging capture system, which is more "high tech" logging infrastructure knowledge. Still acceptable but requires more specialized knowledge.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "5 commits from Andrew Burke (non-bot) between Aug 24-Sept 16, 2026 (within 90 days)"},
      {"name": "Repo in use", "grade": "pass", "evidence": "5 default-branch commits in last 90 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded documentation task, no umbrella/debate/core-internals/support-question"},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "No assignees, no linked PRs, no comments claiming work"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "CONTRIBUTING.md silent on AI usage (silence passes)"},
      {"name": "Task is still valid", "grade": "pass", "evidence": "No maintainer comments marking obsolete or fixed"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/71",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "5 commits from Andrew Burke (non-bot) between Aug 24-Sept 16, 2026 (within 90 days)"},
      {"name": "Repo in use", "grade": "pass", "evidence": "5 default-branch commits in last 90 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded task: remove test indentation and pytest marker, no umbrella/debate/internals"},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "No assignees, no linked PRs, no comments"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "CONTRIBUTING.md silent on AI usage (silence passes)"},
      {"name": "Task is still valid", "grade": "pass", "evidence": "No obsolete markers"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/66",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "5 commits from Andrew Burke (non-bot) between Aug 24-Sept 16, 2026 (within 90 days)"},
      {"name": "Repo in use", "grade": "pass", "evidence": "5 default-branch commits in last 90 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded task: configure structlog in conftest.py, no umbrella/debate/internals"},
      {"name": "Nobody else is already on it", "grade": "pass", "evidence": "No assignees, no linked PRs, no comments"},
      {"name": "Contribution policy allows AI-assisted work", "grade": "pass", "evidence": "CONTRIBUTING.md silent on AI usage (silence passes)"},
      {"name": "Task is still valid", "grade": "pass", "evidence": "No obsolete markers"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

first run: 
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-04: accept
  issue-01: accept
  issue-03: reject
  issue-02: reject
  issue-05: reject
  issue-06: accept
  issue-08: reject
  issue-09: accept
  issue-11: accept
  issue-07: reject
  issue-10: reject
  issue-13: reject
  issue-12: accept
  issue-16: accept
  issue-17: reject
  issue-15: accept
  issue-19: accept
  issue-14: accept
  issue-18: reject
  issue-20: accept

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  accept   NO     graded accept
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  accept   NO     graded accept
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  accept   yes    
issue-20  reject  accept   NO     graded accept

categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 0/1  scope 2/4
agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in policy)

second run: 
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-04: accept
  issue-03: reject
  issue-01: accept
  issue-02: reject
  issue-05: reject
  issue-06: accept
  issue-07: reject
  issue-09: accept
  issue-08: reject
  issue-11: accept
  issue-10: reject
  issue-13: reject
  issue-14: accept
  issue-12: reject
  issue-15: accept
  issue-16: accept
  issue-19: reject
  issue-18: reject
  issue-17: reject
  issue-20: reject

item      gold    verdict  agree  note
issue-01  accept  accept   yes    
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  accept   NO     graded accept
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  reject   NO     failed: Scope fits a newcomer
issue-20  reject  reject   yes    

categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 3/4
agreement: 18/20 scored items  (bar: 18/20: PASS)

third run (the confirming run committed as eval-run.txt, after adding a fifth
scope condition for closed/abandoned-PR history):
grading 20 bundle(s) with rubric.md, model sonnet, 5 worker(s)...
  issue-02: reject
  issue-04: accept
  issue-03: reject
  issue-01: reject
  issue-05: reject
  issue-06: accept
  issue-07: reject
  issue-09: accept
  issue-08: reject
  issue-11: accept
  issue-10: reject
  issue-12: reject
  issue-13: reject
  issue-14: accept
  issue-16: accept
  issue-15: accept
  issue-17: reject
  issue-18: reject
  issue-19: reject
  issue-20: reject

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: Scope fits a newcomer
issue-02  reject  reject   yes    
issue-03  reject  reject   yes    
issue-04  accept  accept   yes    
issue-05  reject  reject   yes    
issue-06  accept  accept   yes    
issue-07  reject  reject   yes    
issue-08  reject  reject   yes    
issue-09  accept  accept   yes    
issue-10  reject  reject   yes    
issue-11  accept  accept   yes    
issue-12  reject  reject   yes    
issue-13  reject  reject   yes    
issue-14  accept  accept   yes    
issue-15  reject  accept   NO     graded accept
issue-16  accept  accept   yes    
issue-17  reject  reject   yes    
issue-18  reject  reject   yes    
issue-19  accept  reject   NO     failed: Scope fits a newcomer
issue-20  reject  reject   yes    

categories: claimed 4/4  clear-accept 6/8  dead-repo 3/3  policy 1/1  scope 3/4
agreement: 17/20 scored items  (bar: 18/20: below the bar)

This third run is the one saved to eval-run.txt and is a regression from the
second run: reworking the scope check's wording to catch issue-15's closed-PR
history made it over-fire on issue-01 and issue-19 (both gold accept), which
it had graded correctly in the second run. The scope check still needs
another revision pass before a future confirming run; I did not re-run the
harness again to fix this, so this 17/20 run is the one of record.

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]
issue-15  reject  accept   NO     graded accept

my rubric didnt check for closed PR history for that issue so it passed each test as instructed by the rubric since it was a criteria that was missed by my rubric.
**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

| Scope fits a newcomer | Issue body and full comment thread (references/evidence-guide.md, family 3). | Pass only if the issue is one bounded, mergeable unit of work: (a) it is not itself explicitly framed as a tracking/umbrella issue whose own body says its listed sub-items should become separate issues (a boilerplate bug-report checklist like "I searched for duplicates" is not this, and a reporter's own numbered list of possible causes or fix ideas for one bug is not this either); (b) the thread shows an actual disagreement between two or more commenters about which approach to take, with no maintainer comment settling it — a single reporter listing options with nobody else weighing in is not a disagreement; (c) no maintainer comment states the fix requires changes to core internals/architecture; (d) it is not a pure usage/support question ("how do I get this to work?") with no implied code change; (e) the issue does not carry a history of two or more closed/unmerged linked PRs that already attempted this exact fix, or a pattern of contributors repeatedly claiming it and going quiet (auto-unassigned for inactivity) — that history means real difficulty behind a friendly label, regardless of how bounded the write-up reads. Any one of (a)-(e) failing fails the check. Terse write-ups with no reproduction steps still pass on their own; grade the size of the work, not the polish of the writeup. | required |

if a newcomer such as myself or a college student looks at the issue they should be able to not have to mess with internal structure and should not involve making the app/project run. it should be running already be running and the issue should be accessible.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]
 i expanded the definition of what a is within scope of a newcomer which caused issue 19 to be accepted the first time but not the second time.




---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

the issue is a tier 1 issue that is open and unclaimed ( for now). issue-select stated : best fit: documentation task that requires reading Python/FastAPI code but stays low-complexity. i weigh it on what it touches on and what tools it requires/needs and how much is required to test if the issue is fixed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

