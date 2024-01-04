# Peer Review

## Smaller Git Diff

We should look into making a change-set guideline so that changes like this could only show 2 lines change. rather than 4 lines due to order differences.
Your software architect or senior software engineers in your team can pitch in for a better way to standardize these commit policies.

Less change-set or git diff the better readability for the reviewer -> Which in turn would help us review concise and faster peer reviews. Is what I think, let me know what you guys think.   

## Code Review

[Good article about how to approach code reviews](https://mtlynch.io/human-code-reviews-1/)

## Restrictions

Restrictions for open Pull Request (PR) / Merge Request (MR) Rules.

### Protected branch

You can enable bunch of guard rails in order for branches to be not directly merged in new changes.
Such branches could be termed as `protected branches`
`develop`, `main`, `master`, `release` comes to my mind which could be protected to include at least 1 approval from a reviewer to be merged in.

### Enable conversation resolution

Require conversation resolution before merging
When enabled, all conversations on code must be resolved before a pull request can be merged into a branch that matches this rule. 
[Github docs link](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-conversation-resolution-before-merging)

### [Do not allow bypassing the above settings](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#do-not-allow-bypassing-the-above-settings)

### Restrict force push

You can completely disable this or only enable for certain users to force push. This is helpful when you have smaller teams and code review is not possible at the last moment. Sometimes rewriting git history is necessary for rebasing or removing rogue commit in order to deliver a package to other cross teams.

### Allow deletion

This should be unchecked since this could sometimes lead to some issues when the remote branch is being deleted. By default I believe protected branch are exempted from this rule. But always good to keep that in handy to know about this rule.