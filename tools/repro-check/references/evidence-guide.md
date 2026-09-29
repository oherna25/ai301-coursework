# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: In the repro report's environment record, usually the section that lists the OS, runtime, package manager, repository revision or GitHub process, and the exact versions relevant to the issue. In an eval bundle, it is the environment block inside the repro report; in live mode, it is the student's reported environment in the draft comment and any repo or tool version details mentioned in the issue or project docs.

What good looks like: The report names the environment it actually ran in and includes the version details that could affect the bug or the fix, such as OS, Python/Node version, dependency versions, and repo commit or release. A missing detail is okay only when the issue is clearly not sensitive to it, and the report says so rather than silently omitting it; the version information should match the issue's stated target or clearly explain the difference.

## Steps

Where it lives: In the repro report's commands, code snippets, setup steps, inputs, and any preconditions needed to trigger the behavior. In a full package, the claim comment can also provide the short summary that ties the reproduction to the issue, while the detailed steps live in the repro report; in live mode, the steps are what the student posts in the issue thread and any linked script or command block.

What good looks like: The steps start from a clean or explicit starting state, list the exact commands or code to run, and are followable by a stranger without guesswork. They lead to the same behavior the issue describes, or they clearly state a cannot-reproduce result with the same exact setup and inputs; a vague “run the app” description does not count as a valid reproduction.

## Behavior shown

Where it lives: In the artifact section of the repro report: terminal output, stack traces, screenshots, logs, or other evidence captured from the run. In an eval bundle, this is the output excerpt or screenshot description read against the bug described in the issue; in live mode, it is the actual result pasted into the issue thread or attached to the draft comment.

What good looks like: The artifact directly shows the issue's reported behavior or the absence of it, with the relevant error text, output, or screenshot matching the issue description. A good report quotes the specific failing line or mismatch and explains why it is the same bug rather than a neighboring error; an adjacent failure or an unrelated warning does not pass.

## Honesty

Where it lives: At the overlap between the claim comment and its evidence in the repro report. The expected-versus-actual explanation belongs in the claim comment, while the backing facts live in the reproduced output or the clear statement that reproduction did not occur. In live mode, it is also visible in how the student describes the issue in the issue thread relative to the actual evidence they posted.

What good looks like: The report states exactly what it observed: expected behavior, actual behavior, and the evidence that supports each claim, or it honestly says it could not reproduce the bug. A strong report does not overstate cause, scope, or fix status; it matches the evidence rather than inferring a broader issue from a nearby symptom or from a different environment.

## Comms

Where it lives: In the claim comment as it speaks to the issue, and in the repro report as it aligns with the repository's documented contribution norms and issue templates. In live mode, this includes the project's docs, issue template, or contribution policy, plus any AI-use disclosure requirements; in eval mode, the repo-facts block and issue context provide the repository-specific standard to compare against.

What good looks like: The wording is specific, honest, and aligned with the repo's conventions: it names the right project terms, matches the template's expectations, and does not hide missing evidence behind boilerplate. The report says what happened and what it did not prove, and it follows any required disclosure rules rather than treating boilerplate as a substitute for a real reproduction. Read what the repo's stated AI-related policy (repo-facts block, or CONTRIBUTING/AI-policy docs in live mode) actually asks, since these are two different rules: a policy that only requires comments be written in the contributor's own, non-AI-generated words is satisfied by natural, specific prose — no separate disclosure statement is expected, and the check should not demand one. A policy that requires disclosing AI assistance when it is used is satisfied only by an explicit acknowledgment of that assistance somewhere in the package (it does not need to name a specific product, just say assistance was used and that the contributor verified the work); treat the package as AI-assisted work for this purpose, so silence under a disclosure-required policy is a fail, never excused by the writing sounding natural or human-authored.
