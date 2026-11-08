# Scan notes


## 2026-11-08: added "Code lives in this repo" check

What changed: rubric.md now has a required check, "Code lives in this repo". It reads the files, functions or error text the issue names, searches the issue's own repo for them, and fails if they are only found in a sibling repo of the same owner.
Why: the scout ranked pytorch/test-infra#5543 first, but Mergebot's approval logic (`get_approved_by()` in `trymerge.py`) lives in pytorch/pytorch. The scout graded the issue page and never looked at the code, so I only found out after forking test-infra. Under the new check #5543 would have been `fail` (symbol found only in pytorch/pytorch), and the scout would have sent me to ask the maintainer before forking.
