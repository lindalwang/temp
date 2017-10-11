### One time actions

1. Fork master repo (on github.com)
   - This is done by clicking on the `Fork` button on https://github.com/pensando/sw

2. Clone your fork
```
$ git clone https://github.com/jainvipin/sw
```

3. Add upstream link
```
$ git add remote upstream https://github.com/pensando/sw

# now git remote -v should show it appropriately, confirm by doing
$ git remote -v
origin     https://github.com/jainvipin/sw (fetch)
origin     https://github.com/jainvipin/sw (push)
upstream   https://github.com/pensando/sw (fetch)
upstream   https://github.com/pensando/sw (push)
```

### One time for every feature

1. Create a branch to work on feature e.g. feature-foo
```
$ git checkout -b feature-foo
```

### For every change in a feature

1. Make sure you are in the correct branch (if branch is not created, create one using above)
```
$ git checkout feature-foo
```

2. Make changes, edit files, etc.
```
$ emacs foo.c
```

3. When you are ready, push the changes
```
$ git push

# if git push is done first time when a branch is set, you might need to set upstream
$ git push -f --set-upstream origin feature-foo

# this would trigger the sanity run, and let you know if there was a failure
```

4. Say sanity failed, and you need to make more changes
```
$ git checkout feature-foo
$ emacs foo.c
$ git add foo.c
$ git commit -m "fixed sanity failure" --amend
$ git push -f
# this would trigger the sanity run, and let you know if there was a failure
```

### How to rebase with master and resubmit

1. Fetch master and Rebase
```
# from any branch (note that each branch is independent of each other and also your master)
$ git fetch upstream master
$ git rebase upstream/master
<may have conflicts, resolve them as follows>
   $ git add .
   $ git rebase --continue
```

2. Push rebased changes
```
# force push is needed because your branch has diverged
$ git push -f
    
# this would trigger the sanity run and confirm if sanity passes
```

### Working on multiple branches
Each Branch is independent with respect to the following:
  - You can do make another change in a different branch
  - Rebase with master independent of other branches
  - Push the changes independently
  - Run sanities independently
  - Commit/Merge independently

Note: when you switch between branches the changes must be committed to the local clone, but this is like stashing your changes.

### Keeping your master up to date with upstream master
```
$ git fetch upstream master
$ git rebase upstream/master
```
Keeping master up to date with master ensures that when a new branch is created it has the latest copy of upstream master.

### Deleting a branch
After a series of commit has gone into a branch, and feature development/testing is complete, a branch can be easily deleted using
```
$ git branch -d feature-foo
```

