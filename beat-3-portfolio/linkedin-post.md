I opened a fix for a bug in the automated system that merges code into PyTorch, one of the most widely used AI projects. The bug: when a reviewer is asked to look at a change a second time, the system still counts their earlier approval, so a change can look signed off when it isn't.

This was my first contribution to a large open source project. I started with a small tool I built to rank beginner-friendly issues, and it picked this one. While reading the code, I found that the problem lived in a different repository than the one where it was reported. I told the maintainers that up front and changed my tool so it checks for that next time.

I then reproduced the bug on a real change from the issue thread and wrote a fix with five automated tests. One of them failed before my fix and passes after it. Partway through, I dropped my first approach because it would have broken the project's existing tests, and I explained that change in my pull request.

Where it stands today: the pull request is open and no maintainer has reviewed it yet. The project's own bot flagged that changes without a maintainer-approved issue get a low priority, so my next step is to ask for that approval.

What I learned: check a project's contribution rules before writing code, not after.

Pull request: https://github.com/pytorch/pytorch/pull/203945

#OpenSource #Python #SoftwareTesting
