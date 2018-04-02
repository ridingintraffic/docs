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
# git rebase squash
git rebase -i <commit hash>; where the commit hash is the one before yours
the reword all of hte commits except for your latest one, the latest one you pick
then check the git log to make sure that you only have one commit
git push --force     # which will force your local into the branch you are working on and hopefully everything will get squashed 
```
 
## Branches
```
$ git branch <branchname>             # creating a branch
$ git branch -d <branchname>          # deleting a branch
$ git branch -av                      # displaying branch info
$ git branch --merged                 # to look at the merged branches
$ git branch --no-merged              # unmerged branches
```

## Git Log
```
$ git log --stat --pretty=oneline master...your-branch                      # look at the changed between branches
$ git log --left-right --graph --cherry-pick --oneline master...your_branch # look at the changed between branches with more colors
$ git log --follow -p <filename/path>                                       #view the log of a single file
```

## Git Resets
```
$ git log
....
commit 766f988169
commit 82f5ea34
git reset --hard 766;              # will reset directly to that old version throwing away everything in between

```

## Git Diff
```
$ git diff                               # Find out what changes you’ve made since the last commit with:
$ git diff "@{yesterday}"                # Or since yesterday:
$ git diff 1b6d "master~2"               # Or between a particular version and 2 versions ago:
$ git whatchanged --since="2 weeks ago"

```

## I did something terribly wrong, please tell me git has a magic time machine!?!
```
git reflog
# you will see a list of every thing you've done in git, across all branches!
# each one has an index HEAD@{index}
# find the one before you broke everything
git reset HEAD@{index}
# magic time machine
```
You can use this to get back stuff you accidentally deleted, or just to remove some stuff you tried that broke the repo, or to recover after a bad merge, or just to go back to a time when things actually worked. I use reflog A LOT. Mega hat tip to the many many many many many people who suggested adding it!

## I committed and immediately realized I need to make one small change!
```
# make your change
git add . # or add individual files
git commit --amend
# follow prompts to change or keep the commit message
# now your last commit contains that change!
```
This usually happens to me if I commit, then run tests/linters... and FML, I didn't put a space after the equals sign. You could also make the change as a new commit and then do rebase -i in order to squash them both together, but this is about a million times faster.
Oh shit, I need to change the message on my last commit!
```
git commit --amend
# follow prompts to change the commit message

Stupid commit message formatting requirements.
```

## I accidentally committed something to master that should have been on a brand new branch!
```
# create a new branch from the current state of master
git branch some-new-branch-name
# remove the commit from the master branch
git reset HEAD~ --hard
git checkout some-new-branch-name
# your commit lives in this branch now :)
```
Note: this doesn't work if you've already pushed to origin, and if you tried other things first, you might need to git reset HEAD@{number} instead of HEAD~. Infinite sadness. Also, many many many people suggested an awesome way to make this shorter that I didn't know myself. Thank you all!

## I accidentally committed to the wrong branch!
```
# undo the last commit, but leave the changes available
git reset HEAD~ --soft
git stash
# move to the correct branch
git checkout name-of-the-correct-branch
git stash pop
git add . # or add individual files
git commit -m "your message here"
# now your changes are on the correct branch
```
A lot of people have suggested using cherry-pick for this situation too, so take your pick on whatever one makes the most sense to you!
```
git checkout name-of-the-correct-branch
# grab the last commit to master
git cherry-pick master
# delete it from master
git checkout master
git reset HEAD~ --hard
```

## I tried to run a diff but nothing happened?!
```
git diff --staged
```
Git won't do a diff of files that have been add-ed to your staging area without this flag. File under ¯\_(ツ)_/¯ (yes, this is a feature, not a bug, but it's baffling and non-obvious the first time it happens to you!)

## Fuck this noise, I give up.
```
cd ..
sudo rm -r fucking-git-repo-dir
git clone https://some.github.url/fucking-git-repo-dir.git
cd fucking-git-repo-dir
```
