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

### Rule: Be specific about cannot-reproduce

If I cannot reproduce the bug, I say that clearly and explain what I tried instead of implying the issue is solved or irrelevant.

- Wrong: "This seems fine on my machine, so it must not be a real issue."
- Right: "I could not reproduce this behavior using the reported setup and steps; the command completed without the described error, so I am treating this as unconfirmed rather than resolved."

### Rule: Write for the repo, not for my ego

I use the repo's language, ask useful questions, and keep my tone direct and professional instead of dramatic or defensive.

- Wrong: "I am 100% sure this is the repo's fault and the maintainers are wrong."
- Right: "I followed the reproduction path above and this output does not match the expected behavior; could you confirm whether this is the intended behavior or a regression in this version?"

## Things I never post

- "It is definitely broken." without the command, environment, or output that proves it.
- "This is fixed" or "This cannot be a bug" without direct evidence.
- A promise I cannot keep, such as "I will send the patch today" when I have not confirmed the root cause.
- A dramatic or blaming tone that hides the actual facts, like "This repo is garbage" or "The maintainers are clearly ignoring a serious issue."
- A vague report that says only "it fails" with no steps, artifact, or expected behavior.
- A claim about cause or blame without reproduction evidence, such as "This is definitely caused by X" when I have not isolated it.
