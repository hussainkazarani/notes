## Push to Github (Basics)
`git add file1 file2` &rarr; add files to staging area

`git commit -m "msg1" -m "body"`  &rarr; make a commit to the tree
 
`git push origin main` &rarr; push local branch to the branch(main) which is at server(origin)

> Both `origin` and `main` are names that are conventions

## Add Remotes
`git remote -v` &rarr; check current remotes

`git remote add origin git@github.com:hussainkazarani/testing.git` &rarr; add this server as my origin

## Pull and Push
`git push` &rarr; only executable after setting upstream

`git pull` &rarr; only executable after setting upstream

`git push origin main` &rarr; save on the server `origin` on branch `main`

`git pull origin main` &rarr; get from the server `origin` on branch `main`

`git branch -vv` &rarr; check if upstream is set

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

```diff
repo
├─ main
│  └─ main_folder/
│
├─ branch1 (from main)
│  ├─ main_folder/
│  └─ branch1_folder/
│
└─ branch2 (from branch1)
   ├─ main_folder/
   ├─ branch1_folder/
   └─ branch2_folder/

# above all branches are from created from `main`. we always check the difference in files

# PR: branch1 to main
git diff main..branch1
+ branch1_folder/

# PR: branch2 to branch1
git diff branch1..branch2
+ branch2_folder/

# PR: branch2 to main
git diff main..branch2
+ branch1_folder/
+ branch2_folder/
```

`git branch` &rarr; shows all branches

`git branch newbranch` &rarr; creates a new branch

`git checkout "branch"` &rarr; move to that branch

`git checkout -b "newbranch"` &rarr; creates and moves to the new branch

`git push origin newbranch` &rarr; creates new branch on server

`git branch -D branch2` &rarr; delete a branch locally

`git push origin -u branch2` &rarr; create a branch on remote/server

`git push origin --delete branch2` &rarr; delete a branch on remote/server

`git reflog` &rarr; check all local operations done

## Git Reset
`git reset <optional sha>` &rarr; only unstages the staged files. no commits undone. if `sha` is given, the files stay but not staged

`git reset --soft <sha>` &rarr; the commit is undone and those files go to staging. always to `git reset` after. can also use `git reset --soft HEAD~1` to go back 1 commit before head

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
> 1\. your current changes<br>
> 2\. the changes made by another party (incoming)<br>
> 3\. the base before any of the other 2 changes

`> main` `git merge <branch2>` &rarr; merges `branch2`(incoming) into `main`(current)

`git merge --abort` &rarr; abort the merge if there are other problems

`git add <conflict file>` &rarr; after resolving merge conflict add the file to staging as it is removed from it automatically

`git commit -m "msg"` &rarr; final commit

`git log -1 --pretty=%P <mergeCommitID>` &rarr; give merge parents

## Merge vs Rebase
\- Merge combines all commits in a branch into a single commit and adds that \***single**\* commit to the top of current branch

\- Rebase puts all the commits in a branch at the top of current branch sequentially. \***No commits are lost**\*

## Fake Commits
```js
// need to change author date and committer date
GIT_AUTHOR_DATE="2026-01-24 12:00:00 +0530" \
GIT_COMMITTER_DATE="2026-01-24 12:00:00 +0530" \
git commit -m "your message"

// complete version
GIT_AUTHOR_NAME="Alice" \
GIT_COMMITTER_NAME="Alice" \
GIT_AUTHOR_EMAIL="alice@example.com" \
GIT_COMMITTER_EMAIL="alice@example.com" \
GIT_AUTHOR_DATE="2026-01-24 12:00:00 +0530" \
GIT_COMMITTER_DATE="2026-01-24 12:00:00 +0530" \
git commit -m "your message"

// amend commits
git commit --amend -m "msg" // only for latest commit
```

## Other
`git cherry-pick <hash>` &rarr; copy a commits from other branches

`git log <branch> --oneline` &rarr; show the logs of that branch

`git status` &rarr; check status of git

`git -v` &rarr; check version of git

`git revert <SHA>` &rarr; does the opposite of what was done in the commit. this means it adds if it was removed, and it removes if it was added.

`git clone URL` &rarr; clone a repo

`.gitignore` file &rarr; ignores files from pushing (including itself). always checked

## Configs
`git config --global --list` &rarr; shows all the global configs

`git config username "kazarani"` &rarr; set some cnfig value locally (always use string quotes)

`git config --local user.name` &rarr; view local configs

## Git Subtree
> used when we need to add another git repo as a folder inside of a repo

```js
// here we will add bootcamp into misc
// /projects/misc
// /projects/bootcamp

// 1. get pwd of bootcamp
cd bootcamp/
pwd // /projects/bootcamp

// 2. add this repo as remote
cd misc
git remote add bootcamp-repo /projects/bootcamp 

// 3. execute remaining commands
git fetch
git subtree add --prefix=bootcamp bootcamp-repo main -m "Import bootcamp repo into misc under /bootcamp"

// 4. change commit name
git push origin main --force
```

## Change Old Commit Name
```js
// understand HEAD. its the latest commit and where we currently are.
HEAD     = E
HEAD~1   = D
HEAD~2   = C
HEAD~3   = B
HEAD~4   = A

// rebase
// i go 4 steps behind head. it is taken as fixed base and any commit above it can be changed
git rebase -i HEAD~4 
```

```js
// example commits
/* 
a1 fix typo        - HEAD
b2 BAD MESSAGE     - HEAD~1
c3 add feature     - HEAD~2
d4 init            - HEAD~3
z9 older commit    - HEAD~4
*/

// go 4 commits before HEAD (z9)
// i can change any messages from above HEAD~4(z9)
// i can change commit messages of d4, c3, b2, a1
git rebase -i HEAD~4 

/*
change the commit from 'pick' to 'reword'
Editor opens:
pick d4 init
pick c3 add feature
pick b2 BAD MESSAGE
pick a1 fix typo

Change:
pick d4 init
pick c3 add feature
reword b2 BAD MESSAGE
pick a1 fix typo

Save + exit.
*/

// git asks for new message. type and save

// then force push
git push --force-with-lease // safer version of push --force
```

```js
// delete single commit branches easier
git update-ref -d HEAD // removes pointer to head
git update-ref -d refs/heads/hello // removes branch pointer and branch (optional if i dont wanna see the fucked up commit)
git gc --prune=now
```

