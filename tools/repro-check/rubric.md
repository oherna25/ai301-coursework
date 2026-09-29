# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment | The repro report's environment record, including the operating system, runtime or container details, repository or GitHub process, and versions relevant to the issue. | The recorded environment is specific enough to explain where the reproduction ran and to let another person repeat it; missing details do not prevent reproduction only when they are demonstrably irrelevant to the issue. | required |
| Reproduction steps | The claim comment and the repro report's commands, code, inputs, and setup steps. | The steps and inputs are complete and followable from a clean starting point, and they lead to the reported behavior or to a clearly evidenced cannot-reproduce result. | required |
| Target behavior | The output excerpt or other artifact produced by the reproduction, read against the behavior and error described in the issue. | The artifact demonstrates the issue's reported behavior, or demonstrates that the issue cannot be reproduced; an adjacent or different failure does not pass. | required |
| Expected and actual outcome | The claim comment's expected-versus-actual explanation and the output artifact read against the issue description. | The expected behavior and observed behavior are both stated accurately, and the explanation matches the evidence rather than overstating or mislabeling the result. | required |
| Repository conventions | The claim comment and repro report, compared with the repository's conventions, the repo-facts block (including any stated AI-assistance disclosure policy), and the claim comment's own commitments and tone. | The package uses the repository's relevant terminology and reporting conventions, makes no unsupported claims about the issue or its cause, and does not substitute boilerplate over-promising (a guaranteed fix timeline, a demand to reserve or assign the issue) for evidence. Read the repo's stated AI-related policy for what it actually asks: a policy that only requires comments be written in the contributor's own, non-AI-generated words is satisfied by natural, specific prose (no separate disclosure statement is needed). A policy that requires disclosing AI assistance when it is used is satisfied only by an explicit acknowledgment of that assistance in the package (it does not need to name a specific product) — for this check, treat every package as AI-assisted work, so a disclosure-required policy with no acknowledgment anywhere in the package fails the check, and natural or "human-sounding" writing is never itself evidence that disclosure was not required. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept (ready) only when every required check passes. Reject (hold) when any
required check fails or is unclear. Preferred checks never change the verdict;
an unclear preferred check is recorded as unclear but does not prevent
acceptance.
