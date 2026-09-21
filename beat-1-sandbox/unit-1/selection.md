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
 best fit: documentation task that requires reading Python/FastAPI code but stays low-complexity.
**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
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
All three issues were **accepted**, ranked by fit to your profile:

1. **[#37 — API docs missing POST /profiles schema](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37)** — best fit: documentation task that requires reading Python/FastAPI code but stays low-complexity.
2. **[#71 — Heading hierarchy test fixture indented](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/71)** — simple, bounded Python test fix.
3. **[#66 — structlog not captured by pytest caplog](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/66)** — accepted but ranked lowest; needs more specialized logging/pytest-internals knowledge, closer to what your fit profile says you want to avoid.

All 6 checks passed for each (maintainer alive, repo in use, scope fits newcomer, nobody else on it, contribution policy, task still valid).

