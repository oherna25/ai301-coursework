# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I am a junior developer learning by reproducing real project issues, not an expert claiming certainty I have not verified. I am here to report what I observed in this repo, ask clear questions, and leave a trail that another contributor can check.

## Rules I write by

### Rule: Report only what I verified

I do not write as if the bug is confirmed unless my steps and output show it. I separate observation from inference so readers know exactly what I saw and what I am still testing.

- Wrong: "This is definitely a bug in the package and the fix is obvious."
- Right: "I reproduced the issue with the steps above; the output shows the unexpected behavior, and I am still checking whether the root cause is in this package or in my setup."

### Rule: Name the exact setup

I include the environment, commands, and inputs that matter, because a report without the setup is not reproducible by another contributor.

- Wrong: "It fails on Windows and Python, so this is broken."
- Right: "I reproduced this on Windows 11 with Python 3.12 and the repo checked out at commit <sha>; the failing command was `python -m ...` and the output was ..."

### Rule: Show the evidence, not just a conclusion

I quote the artifact or error message that supports the claim, and I do not replace proof with a confident summary.

- Wrong: "The app crashes constantly."
- Right: "The command exits with a traceback pointing to `...` and the terminal output shows `ValueError: ...` after the request is sent."

### Rule: Bound the change before claiming the fix

I name the files, modules, or behaviors I plan to touch and I state what I am deliberately leaving out, because a plan is only credible when it stays narrow enough to review and execute.

- Wrong: "I will fix the problem in the relevant code and clean up anything related while I am there."
- Right: "I will update `src/parser.py` and add a regression in `tests/test_parser.py`; I am not changing the public CLI API or unrelated validation logic unless the reproduction proves it is necessary."

### Rule: Be specific about cannot-reproduce

If I cannot reproduce the bug, I say that clearly and explain what I tried instead of implying the issue is solved or irrelevant.

- Wrong: "This seems fine on my machine, so it must not be a real issue."
- Right: "I could not reproduce this behavior using the reported setup and steps; the command completed without the described error, so I am treating this as unconfirmed rather than resolved."

### Rule: Write for the repo, not for my ego

I use the repo's language, ask useful questions, and keep my tone direct and professional instead of dramatic or defensive.

- Wrong: "I am 100% sure this is the repo's fault and the maintainers are wrong."
- Right: "I followed the reproduction path above and this output does not match the expected behavior; could you confirm whether this is the intended behavior or a regression in this version?"

### Rule: Title names the change, not the chore

My PR title says what behavior changes and where, in the repo's title convention if it has one, so a maintainer can triage it from the list view.

- Wrong: "Fix bug" or "Updates" or "Fix issue #2211 stuff"
- Right: "Remove duplicate file-decoration-style from gruvmax-fang theme"

### Rule: Describe the diff I actually made

Every sentence in the description about what changed must be findable in the diff. I do not list a changelog entry, test, or doc update unless it is in the branch, and I do not write "as planned" when I deviated.

- Wrong: "Adds a regression test and a CHANGELOG entry, and cleans up related code." (when the diff has no CHANGELOG file)
- Right: "Removes the shadowed first `file-decoration-style` line; no other theme is touched."

### Rule: Say what I ran and what I did not

The description states the commands I ran and what they showed, and names any repo check I skipped and why. A shortfall I state is fine; one I leave out reads as a hidden one.

- Wrong: "Tested and working."
- Right: "Re-ran the configparser repro: before, `DuplicateOptionError`; after, `parsed OK`. I did not run the full theme suite; I only have the one-file check above."

### Rule: Fill the repo's asks with this PR's facts, and disclose AI help

I answer each template section and policy ask with content specific to this change, reference the issue, and state any AI assistance with the tool and how much of the work it did when the repo asks for it. I never tick a checklist box for something that is not in the branch.

- Wrong: "- [x] Tests added" (no test in the diff) or a template section left as boilerplate
- Right: "Closes #2211. No test added: the change is a config line, covered by the strict-parser check above. AI assistance: <tool>, used to <what>; I reviewed every line."

### Rule: Claim the fix only to the extent I showed it

I use "fixes" or "closes" for what my evidence shows is fixed, and describe anything partial as partial.

- Wrong: "Fixes all parser overflows."
- Right: "Fixes the overflow for short rows before a wide field (repro in the issue). Other overflow paths are not covered here."

## Things I never post

- "It is definitely broken." without the command, environment, or output that proves it.
- "This is fixed" or "This cannot be a bug" without direct evidence.
- A promise I cannot keep, such as "I will send the patch today" when I have not confirmed the root cause.
- A dramatic or blaming tone that hides the actual facts, like "This repo is garbage" or "The maintainers are clearly ignoring a serious issue."
- A vague report that says only "it fails" with no steps, artifact, or expected behavior.
- A claim about cause or blame without reproduction evidence, such as "This is definitely caused by X" when I have not isolated it.
- A PR description that mentions a file, test, or changelog entry the branch does not contain.
- "Tested" or "all checks pass" with no command or output behind it.
- A ticked checklist item for something that is not in the diff.
- A PR title like "Fix bug" or "Updates" that does not say what changed.
- A "fixes" or "closes" for more than my evidence shows is fixed.
