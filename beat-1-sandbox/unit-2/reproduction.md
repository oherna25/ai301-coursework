# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

oherna25

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-5882142580

Hi! I'd like to take this one as a first contribution. I looked at docs/API.md and confirmed it currently has no request-body section for either POST /profiles or POST /reviews — the doc lists the routes but stops before describing the body fields, and api/routes/profiles.py shows that endpoint reading multipart form data rather than JSON, which the current doc doesn't call out anywhere.

Next, I'm going to read through api/routes/profiles.py and api/schemas/review.py to pin down the exact fields, types, and (for POST /profiles) the multipart form-data field names, then draft the missing schema sections with example request bodies. I'll post my findings and the doc draft here once I've verified the fields against the actual route/schema code.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-5882386739

Environment: `codepath/pathreview-ai301-fa26-s3` at commit `2f4e82f5` (main), read-only source inspection — no running server needed to confirm this gap, just the checked-out files.

Steps:
1. Cloned the repo, checked out `2f4e82f5`.
2. Read `docs/API.md` lines 18–26: both `POST /profiles` and `POST /reviews` get a single description line each, then the doc moves on to the next section — no field list, content type, or example body for either.
3. Read `api/routes/profiles.py`'s handler: it takes `github_username` and `portfolio_url` as `Form()` fields and an optional `resume_file` as `File()` — multipart form data, not JSON — and returns 422 if the file isn't PDF, Markdown, or plain text.
4. Read `api/schemas/review.py` and `api/routes/reviews.py`'s handler: the body is the `ReviewCreate` model — JSON with one required field, `profile_id` (UUID).

Expected: `docs/API.md` describes each POST endpoint's content type, fields, and an example body.

Actual: it doesn't — confirming the issue exactly. Proposed additions:

**POST /profiles** — `multipart/form-data`

| field | type | required | notes |
|---|---|---|---|
| github_username | string | no | |
| portfolio_url | string | no | |
| resume_file | file | no | must be PDF, Markdown, or plain text; 422 otherwise |

**POST /reviews** — `application/json`

```json
{ "profile_id": "uuid" }
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (initial): 18/20 agreement. Met the raw bar but failed the category floor —
   0/1 in `disclosure` — because my only check reading repo conventions/AI-disclosure
   (`Repository conventions`) was weighted `preferred`, so it could never flip a verdict.
2. `--only pkg-19,pkg-20` plus 8 canaries (`pkg-01,02,03,04,05,06,07,18`), after flipping
   `Repository conventions` to `required`: 9/10. `pkg-19` fixed; `pkg-20` (the disclosure
   package) still wrongly accepted.
3. Same `--only` set, after rewording the check to require an explicit disclosure
   statement naming the tool: 8/10. `pkg-20` fixed, but the wording was too strict and
   newly broke two previously-correct accepts, `pkg-03` and `pkg-07`.
4. Same `--only` set, after rewording again to separate two distinct repo-policy shapes
   (comments-in-your-own-words vs. must-disclose-AI-use, the latter satisfied by any
   explicit acknowledgment, not a named product): 10/10. All ten packages agreed.
5. Full confirming run: **19/20 agreement, bar 18/20: PASS**, category floor matched in
   every category (`clear-accept 7/8, disclosure 1/1, no-evidence 4/4,
   unfollowable-comms 3/3, wrong-target 4/4`). Saved with `--save-run eval-run.txt`; this
   is the committed run.

**Package analysis**

`pkg-20` (ghostty-org/ghostty#13604, category `disclosure`). Gold: **reject** — "excellent
repro on every proof check; ghostty's stated AI policy requires disclosing all AI usage
and the comments do not disclose." My rubric's final run: **reject**, matching gold.

Before I revised it, my rubric graded this package **accept** — the reproduction itself is
genuinely excellent (environment, steps, and artifact all pass), and the only check that
reads repo conventions and disclosure policy (`Repository conventions`) was weighted
`preferred`, so per my own verdict rule ("preferred checks never change the verdict") it
could never hold the package back no matter what it found. My rubric read the *evidence*
correctly even then — conventions checks don't gate the fix, the weight-and-wording did.
After making that check `required` and rewriting its pass condition to explicitly require
an acknowledgment of AI assistance whenever a repo's policy demands one, the check now
fails ghostty's package (no such acknowledgment appears anywhere in the claim comment or
report) and the required-check failure correctly forces a reject, regardless of how strong
the reproduction evidence is elsewhere.

**Check rationale**

The check, exactly as it reads in `rubric.md` now:

> Repository conventions | The claim comment and repro report, compared with the
> repository's conventions, the repo-facts block (including any stated AI-assistance
> disclosure policy), and the claim comment's own commitments and tone. | The package uses
> the repository's relevant terminology and reporting conventions, makes no unsupported
> claims about the issue or its cause, and does not substitute boilerplate over-promising
> (a guaranteed fix timeline, a demand to reserve or assign the issue) for evidence. Read
> the repo's stated AI-related policy for what it actually asks: a policy that only
> requires comments be written in the contributor's own, non-AI-generated words is
> satisfied by natural, specific prose (no separate disclosure statement is needed). A
> policy that requires disclosing AI assistance when it is used is satisfied only by an
> explicit acknowledgment of that assistance in the package (it does not need to name a
> specific product) — for this check, treat every package as AI-assisted work, so a
> disclosure-required policy with no acknowledgment anywhere in the package fails the
> check, and natural or "human-sounding" writing is never itself evidence that disclosure
> was not required. | required |

It reads this way because my first two attempts at it were wrong in opposite directions.
Weighted `preferred`, it could never fail a package no matter what it found (the `pkg-20`
miss above). Made `required` but worded to demand a statement naming the specific AI tool,
it correctly caught `pkg-20` but then wrongly failed `pkg-03` (ripgrep) and `pkg-07`
(p5.js) — both clear accepts. Reading those two side by side showed the real distinction:
ripgrep's policy only asks that comments be human-written, which natural prose already
satisfies with no disclosure statement at all; p5.js's policy asks for disclosure, and its
package's claim comment already disclosed ("I used an AI assistant to help me organize
this report...") without naming a specific product. I rejected the "name the tool" wording
because it punished a package that had already done the disclosure correctly, and settled
on requiring only an explicit acknowledgment, scoped to whichever policy shape the repo
actually states.

**Trade-offs**

Making `Repository conventions` `required` (rather than `preferred`) is what let it catch
`pkg-19`'s boilerplate over-promising claim ("I will fix it within 2 days guaranteed...
keep this issue reserved for me") and `pkg-20`'s missing disclosure — both previously
false accepts. The cost showed up on `pkg-12` (prettier, category `clear-accept`, gold
`accept`): in my committed full run it was graded `reject` on this same check, but
re-grading it alone afterward for this write-up, it graded `accept` on an identical rubric
and evidence guide — the per-check evidence text on the passing run reads "natural specific
prose satisfies AI policy's requirement for understood work," which is exactly the
judgment call the check now asks the grader to make on every package's AI-adjacent
policy language. Prettier's stated policy ("only submit code you fully understand...
low-quality AI content is closed immediately") isn't actually a disclosure requirement, but
its phrasing is close enough to one that the grading model's call on it varies run to run.
That instability is the price of a required check whose pass condition depends on reading
intent in ambiguous repo-policy wording, rather than a single fixed keyword.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
