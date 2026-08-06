+++
title = 'achievement farming autopsy: why Pair Extraordinaire is so hard to earn'
date = 2026-08-06T11:30:00+00:00
draft = false
tags = ['write']
listIcon = "/writing.png"
teaser = "GitHub says co-author a commit, get the badge. I tested every documented condition. The badge never came. Here's the autopsy."
+++

GitHub's achievement badges are a small game we all play without admitting it. Most of them pop within hours: open an issue, merge a PR, get a star — done. But **Pair Extraordinaire** (co-author a commit on the default branch of a repo) is the one that refuses to cooperate, and the community forums are full of people asking why.

I spent a week testing every documented condition. This is what I found.

<!--more-->

## What the docs say

The [official documentation](https://docs.github.com/en/pull-requests/how-tos/commit-changes/creating-a-commit-with-multiple-authors) is short and specific: add a `Co-authored-by: Name <email>` trailer to a commit, and for it to count, the email must be **associated with the co-author's GitHub account**. That's it. No collaborator requirement, no merge-method requirement, no signing requirement.

The [troubleshooting guide](https://docs.github.com/en/account-and-profile/how-tos/contribution-settings/troubleshooting-missing-contributions) adds: contributions can take **up to 24 hours** to appear, and commits only count if they land on the **default branch**.

## What the community discovered

The [community discussion #20481](https://github.com/orgs/community/discussions/20481) ("How do I get the Pair Extraordinaire Badge?") is 23 replies of people sharing what *actually* worked for them, and the pattern is consistent:

1. The co-author must be a **collaborator** on the repo (invitation accepted)
2. The trailer email must be the co-author's **verified email**
3. Merge through a **pull request** — squash-merge seems to be the one that reliably counts
4. Then **wait 24–48 hours**

None of this is in the official docs. It's folklore, passed between strangers in a GitHub discussion thread. Which tells you something about how opaque this particular badge is.

## What I observed in my own testing

I set up a test repo, added a collaborator, made signed co-authored commits, merged them through PRs to the default branch. The results:

- ✅ The **contribution graph updated** within hours — the co-author's account showed the commits, proving the trailer email resolved correctly
- ✅ The commits showed **both avatars** and `Verified`
- ✅ Other activity badges (YOLO, Pull Shark, Quickdraw) appeared within 24 hours
- ❌ **Pair Extraordinaire never appeared** — not at 24h, not at 48h

So the co-authorship machinery works. GitHub *knows* about these commits. The badge just doesn't fire.

## The most likely explanations

1. **Anti-farming detection.** The badge is a git-data badge, which means it's batch-processed and scrutinized differently than activity badges. If a repo looks like a farm (rapid PRs, trivial content), the system may silently exclude it. This is the explanation I find most likely — and it's the one GitHub won't confirm or deny in public docs.

2. **A hidden eligibility rule.** The 2026 achievements rework changed several badges' conditions. It's entirely possible Pair Extraordinaire now requires something undocumented — a minimum repo age, a minimum contribution history, a different person rather than a second account.

3. **A system bug.** GitHub's own forums have reports of achievements disappearing and reappearing. Git-data badges are processed in batches; if your batch was dropped, you'd see exactly this: contributions recorded, badge never issued.

## What I'd tell someone trying this today

- Follow the community recipe exactly: real collaborator, verified email, signed commit, PR merged to default branch. That's the ceiling of what you can control.
- **Don't automate it.** If the repo looks like a farm, it will be treated like a farm. One honest PR is more likely to count than fifty scripted ones.
- If it still doesn't appear after 48h, **open a support ticket** with the evidence: repo URL, PR link, commit SHA, collaborator confirmation, contribution-graph screenshots. The docs have no extra condition to discover, which means this is now a support question, not a documentation question.

## The meta-lesson

Achievements are a game, and like all games, some rules are printed and some aren't. The fun part — and the reason I keep doing this — is that the unprinted rules are discoverable. You test, you document, you share. That's open source in its purest form: not code, but *knowledge about how the system actually works*.

If you've earned Pair Extraordinaire, or if you're stuck like I am, [the discussion thread](https://github.com/orgs/community/discussions/20481) is still open. Add your data point. The folklore needs more entries.
