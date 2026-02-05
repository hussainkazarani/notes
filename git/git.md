## Push to Github (Basics)
`git add file1 file2` &rarr; add files to staging area

`git commit -m "msg1" -m "body"`  &rarr; make a commit to the tree
 
`git push origin main` &rarr; push local branch to the branch(main) which is at server(origin)

> Both `origin` and `main` are names that are conventions

## Add Remotes
`git remote -v` &rarr; check current remotes

`git remote add origin git@github.com:hussainkazarani/testing.git` &rarr; add this server as my origin

## Pull and Push
`git push` - only executable after setting upstream

`git pull` - only executable after setting upstream

`git push origin main` - save on the server `origin` on branch `main`

`git pull origin main` - get from the server `origin` on branch `main`

`git remote -vv` &rarr; check if upstream is set

```bash
# upstream helps set the server and branch as default for that particular branch
# sets the `git push` for the current branch (main) to origin/main
git push -u origin main
git push --set-upstream origin main
```

> \***Important to remember**\*<br>
> branch `main` with `upstream set` - `git pull` gets from correct source<br>
> branch `main` with `w/o upstream set` - `git pull` wont work

## Branches
> one thing to not about branches is that unstaged/committed changed transfer to new branches cus they are technically not in any branch

`git branch` &rarr; shows all branches

`git branch newbranch` &rarr; creates a new branch

`git checkout "branch"` &rarr; move to that branch

`git checkout -b "newbranch"` &rarr; creates and moves to the new branch

`git push origin newbranch` &rarr; creates new branch on server

`git branch -D branch2` &rarr; delete a branch locally

`git push origin --delete branch2` &rarr; delete a branch on remote/server

## Git Reset
`git reset <optional sha>` &rarr; only unstages the staged files. no commits undone. if `sha` is given, the files stay but not staged

`git reset --soft <sha>` &rarr; the commit is undone and those files go to staging

`git reset --hard <sha>` &rarr; the commit is undone and files dont stay

`git push --force origin main` - overwrite the server `origin` with my local one

## Stashing
`git stash list` &rarr; lists all the stashes i have

`git stash apply` &rarr; creates a stash on current uncommited changes

`git stash drop` &rarr; delete most recent stash

`git stash clear` &rarr; delete all stashes

`git stash pop <name>` &rarr; delete specific stash

## Merge
> there are 2 main thing to remember with merge. <br>
> first is that \***merge happens into the branch you are in**\*. <br>
> second is that there are 3 ways of conflicts in merge:<br>
> 1 &rarr; your current changes<br>
> 2 &rarr; the changes made by another party (incoming)<br>
> 3 &rarr; the base before any of the other 2 changes

`> main` `git merge <branch2>` &rarr; merges `branch2`(incoming) into `main`(current)

`git merge --abort` &rarr; abort the merge if there are other problems

`git add <conflict file>` &rarr; after resolving merge conflict add the file to staging as it is removed from it automatically

`git commit -m "msg"` &rarr; final commit

## Fake Commits
```python
# need to change author date and committer date
GIT_AUTHOR_DATE="2026-01-24 12:00:00 +0530" \
GIT_COMMITTER_DATE="2026-01-24 12:00:00 +0530" \
git commit -m "your message"
```

## Other
`git cherry-pick <hash>` &rarr; copy a commits from other branches

`git log <branch> --oneline` &rarr; show the logs of that branch

