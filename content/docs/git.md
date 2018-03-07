---
layout: single
title: Git
description: git notes
---

```
## Git Revert ##
Git checkout master    #then run a git log and get the id of the merge commit.  
git log                #then revert to that commit:
git revert -m 1 <merge-commit> # With ‘-m 1’ we tell git to revert to the first parent of the mergecommit on the master branch. -m 2 would specify to revert to the first parent on the develop branch where the merge came from initially.

Now commit the revert and push changes to the remote repo and you are done.
Getting back the reverted changes
This changes the data to look like before the merge, but not the history. So it’s not exactly like an undo. If we would merge develop into master again the changes we reverted in master wont be applied. So if we would like these changes back again we could revert our first revert(!).
git revert <commit-of-first-revert>
```

```
git log --follow -p <filename/path>      #view the log of a single file

# git rebase squash
git rebase -i <commit hash>; where the commit hash is the one before yours
the reword all of hte commits except for your latest one, the latest one you pick
then check the git log to make sure that you only have one commit
git push --force     # which will force your local into the branch you are working on and hopefully everything will get squashed 
```
