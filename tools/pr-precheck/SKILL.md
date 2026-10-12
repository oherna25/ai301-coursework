---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

this tool answers the question of whether a PR package is ready to submit. A PR package contains the plan it claims to implement, the issue that plan belongs to, the branch's diff, the draft PR title and description, and any test evidence. The tool reads these artifacts against the rubric and procedure to determine readiness. 

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

In live mode, the tool reads the plan.md file (with its deviation notes), the branch's diff, the draft PR title and description, the test evidence, and the issue. The branch's diff is everything the branch changes relative to the repo's default branch: `git diff main...HEAD` (three dots), run from the working copy. In eval mode, the bundle is the whole world; nothing is fetched, and every check runs with the full verdict rule.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, the tool reads scope.md to determine the boundaries of its evaluation. It follows the rules specified in scope.md, refusing to evaluate anything outside those boundaries. If the scope's repo line is an unfilled placeholder, the tool refuses to proceed until it is filled. In eval mode, the tool ignores scope.md entirely and evaluates everything within the bundle according to the full verdict rule.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->
In live mode, the tool reads voice-guide.md to determine the style and tone it should use for the PR title and description. It gates the outgoing text according to the rules in voice-guide.md, reporting any broken rules. It never changes the verdict on its own. In eval mode, the tool ignores voice-guide.md entirely and evaluates everything within the bundle according to the full verdict rule.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->
In live mode, the tool reads rubric.md to determine the checks and the verdict rule, references/evidence-guide.md to map where each evidence family lives, and procedure.md to follow the step-by-step instructions. If the procedure is silent on a step, the tool reports the gap and never improvises around it. If rubric.md or procedure.md has no content, the tool refuses to proceed according to the refusal rule. In eval mode, the tool ignores these files and evaluates everything within the bundle according to the full verdict rule.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->
In live mode, the tool grades according to the standing rules: it prioritizes evidence, grades the substance rather than the polish, follows the rubric for decisions, uses the procedure to determine how to apply the rubric, and treats unclear grades as specified by the rubric's verdict rule. In eval mode, the tool ignores these rules and evaluates everything within the bundle according to the full verdict rule.
