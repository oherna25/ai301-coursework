# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**
oherna25

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/37#issuecomment-6008171071

The plan correctly identifies this as a documentation gap and keeps the
implementation scope appropriately narrow. Please update only docs/API.md:
document POST /profiles as multipart/form-data with the optional
github_username, portfolio_url, and resume_file fields, including the
accepted PDF, Markdown, and plain-text MIME types and the 422 response for
unsupported uploads. Document POST /reviews as application/json with the
required UUID profile_id and an example request body.

The reported reproduction is clear: “both POST /profiles and POST /reviews
get a single description line each, then the doc moves on to the next
section — no field list, content type, or example body for either.” Keep that
evidence alongside the source checks: the profile handler uses Form() and
File(), and ReviewCreate contains the required profile_id: UUID.

After editing, re-run the two planned source-inspection checks and record the
results. No server run or runtime test is necessary for this documentation-only
change.
## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

docs/37-api-request-body-schemas



**Evidence**

My unit-2 repro was read-only source inspection against the real repo (not a stand-in
script), so it was re-run directly rather than converted into a different check.

**Before** (commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`, the commit pinned in my
unit-2 repro comment — same result as posted there):

```
$ git show 2f4e82f52efbcfcc57d65b3fa5348672163ca088:docs/API.md | sed -n '18,26p'
`POST /profiles` — Create a profile with resume and GitHub username.
`GET /profiles/{profile_id}` — Retrieve a profile.
`DELETE /profiles/{profile_id}` — Delete a profile and associated data.

### Reviews

`POST /reviews` — Request a new portfolio review for a profile.
`GET /reviews/{review_id}` — Retrieve a completed review.
`GET /reviews` — List reviews for the authenticated user (paginated).
```

```
$ git show 2f4e82f52efbcfcc57d65b3fa5348672163ca088:api/routes/profiles.py | sed -n '23,34p'
@router.post("", response_model=ProfileResponse)
async def create_profile_endpoint(
    github_username: str = Form(default=None),
    portfolio_url: str = Form(default=None),
    resume_file: UploadFile = File(default=None),
    current_user: User = Depends(get_current_user),
    db=Depends(get_db),
):
    """
    Create a new profile with optional resume upload.
    Resume must be PDF or Markdown.
    Returns 422 if file is not PDF or markdown.
```

```
$ git show 2f4e82f52efbcfcc57d65b3fa5348672163ca088:api/schemas/review.py | sed -n '14,16p'
class ReviewCreate(BaseModel):
    profile_id: UUID
```

Confirms the gap exactly as filed: both endpoints get a one-line description with no
content type, field list, or example body.

**After** (working tree, branch `docs/37-api-request-body-schemas`):

```
$ sed -n '16,53p' docs/API.md
### Profiles

`POST /profiles` — Create a profile with resume and GitHub username.

Request: `multipart/form-data`

| field | type | required | notes |
|---|---|---|---|
| github_username | string | no | |
| portfolio_url | string | no | |
| resume_file | file | no | must be PDF, Markdown, or plain text; 422 otherwise |

Example:
```
curl -X POST http://localhost:8000/profiles \
  -F "github_username=octocat" \
  -F "portfolio_url=https://example.com" \
  -F "resume_file=@resume.pdf"
```

`GET /profiles/{profile_id}` — Retrieve a profile.
`DELETE /profiles/{profile_id}` — Delete a profile and associated data.

### Reviews

`POST /reviews` — Request a new portfolio review for a profile.

Request: `application/json`

| field | type | required | notes |
|---|---|---|---|
| profile_id | UUID | yes | |

Example:
```json
{ "profile_id": "d1194941-176d-4de7-8b3f-424fa7cc6ec7" }
```
```

```
$ sed -n '23,34p' api/routes/profiles.py
@router.post("", response_model=ProfileResponse)
async def create_profile_endpoint(
    github_username: str = Form(default=None),
    portfolio_url: str = Form(default=None),
    resume_file: UploadFile = File(default=None),
    current_user: User = Depends(get_current_user),
    db=Depends(get_db),
):
    """
    Create a new profile with optional resume upload.
    Resume must be PDF or Markdown.
    Returns 422 if file is not PDF or markdown.
```

```
$ sed -n '14,16p' api/schemas/review.py
class ReviewCreate(BaseModel):
    profile_id: UUID
```

Both POST endpoints now document their content type, full field list, and an example
body, matching the handler/schema source exactly (unchanged by this fix, as expected
for a documentation-only change).

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]


i only did one run and got 19/20 on the first run
# eval run written by run_eval.py at 2026-10-06T02:17:11Z
# model: sonnet (pinned)
# graded: C:\Users\osmar\.claude\skills\plan-check
# packages: 20 scored
#   rubric.md  sha256:1d53915f1222761f
#   evidence-guide.md  sha256:ada487c269e249e3
#   procedure.md  sha256:805d530629773028
#   SKILL.md  sha256:9bad3d6644a2d285
#
grading 20 package(s) with rubric.md + evidence-guide.md + procedure.md, model sonnet, 5 worker(s)...
  pkg-03: accept
  pkg-04: reject
  pkg-02: accept
  pkg-05: accept
  pkg-01: reject
  pkg-06: reject
  pkg-07: reject
  pkg-08: accept
  pkg-09: accept
  pkg-10: reject
  pkg-11: reject
  pkg-12: reject
  pkg-13: accept
  pkg-15: reject
  pkg-14: accept
  pkg-17: reject
  pkg-16: reject
  pkg-18: reject
  pkg-19: reject
  pkg-20: accept

item    category           gold    verdict  agree  note
pkg-01  wrong-cause        reject  reject   yes    
pkg-02  clear-accept       accept  accept   yes    
pkg-03  clear-accept       accept  accept   yes    
pkg-04  thread-convention  reject  reject   yes    
pkg-05  clear-accept       accept  accept   yes    
pkg-06  scope-creep        reject  reject   yes    
pkg-07  wrong-cause        reject  reject   yes    
pkg-08  clear-accept       accept  accept   yes    
pkg-09  clear-accept       accept  accept   yes    
pkg-10  unbuildable        reject  reject   yes    
pkg-11  wrong-cause        reject  reject   yes    
pkg-12  scope-creep        reject  reject   yes    
pkg-13  clear-accept       accept  accept   yes    
pkg-14  clear-accept       accept  accept   yes    
pkg-15  scope-creep        reject  reject   yes    
pkg-16  wrong-cause        reject  reject   yes    
pkg-17  unbuildable        reject  reject   yes    
pkg-18  unbuildable        reject  reject   yes    
pkg-19  scope-creep        reject  reject   yes    
pkg-20  thread-convention  reject  accept   NO     graded accept

categories: clear-accept 7/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4
agreement: 19/20 scored items  (bar: 18/20: PASS)



**Package analysis**

`pkg-20` (ghostty-org/ghostty#11261) is the one disagreement. My rubric graded it
**accept**; the gold label is **reject**, category `thread-convention`, with the note:
"excellent bounded plan that follows the thread's direction, but the comment contains no
AI-use disclosure and ghostty's stated policy requires disclosing all AI usage."

My rubric read it as accept because the package is genuinely strong on every axis my
checks look at: the diagnosis (stale `prev` pointer surviving a mid-print page-growth
reallocation) matches the repro evidence exactly, the scope is bounded to
`Terminal.print`'s grapheme paths with an explicit not-in-scope line, and the test plan
adds both fuzz-derived regression cases plus the no-hyperlink control and re-runs the
fuzzer corpus. `diagnosis`, `scope`, and `test` all pass cleanly. But none of my four
checks ever reads the plan comment against the repo's stated AI policy — they check the
plan's content against the evidence and the repo's files, not the comment against
`CONTRIBUTING.md`/`AI_POLICY.md`. Ghostty's repo-facts block states AI usage must be
disclosed in every comment; my rubric has no check that looks at the comment through that
lens at all, so there is nothing in it capable of catching this failure mode.

**Check rationale**

From `rubric.md`, the `scope` check:

> Passes if it names the concrete files or modules to change, states what it will not
> touch, and stays bounded to the root cause without unrelated changes.

I rejected an earlier, structural version of this check — something like "the plan has a
'Scope' heading with an explicit not-in-scope line" — in favor of judging the outcome
instead: does the change stay bounded, not does the write-up look a certain way. The
rubric template itself warns that structure-shaped checks are what make graders disagree
with themselves, and I saw why directly: `pkg-02`'s scope statement is one terse sentence
naming two subtraction sites, while `pkg-06`'s has multiple labeled sections — but
`pkg-06` is the one that should fail, because it turns an empty-tar fix into a five-front
campaign (preload regeneration, containerd upgrade, cross-runtime abstraction, CI
matrix). A heading-presence check would have scored `pkg-06`'s well-organized write-up
higher than `pkg-02`'s terse one. Judging boundedness itself instead of the formatting is
what lets `scope` reject `pkg-06` correctly alongside the other three `scope-creep`
packages (4/4).

**Trade-offs**

The `test` check is required, and it's what actually flips `pkg-04` to reject — but for a
reason adjacent to, not the same as, its gold category (`thread-convention`: the plan
ignores the maintainer's already-posted patched binary and root-cause pointer in
`src/tui/light_windows.go`, going with a docs-only workaround instead). My `test` check
doesn't look at thread direction at all; it fails `pkg-04` because its test plan is a
manual walkthrough on a Windows machine, not an automated test exercising the bug. That's
a real gap in the plan, so the verdict lands right, but it means `test` is catching
`pkg-04` by coincidence, not by design. The categories line makes the resulting blind
spot explicit: `thread-convention 1/2` — my rubric has no check that reads a plan's
comment against the thread or the repo's contribution/AI policy, so it will keep missing
any package in that family whose plan is otherwise well-tested and well-scoped, exactly
the shape `pkg-20` has.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
