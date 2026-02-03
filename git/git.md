git add file1 file2
git commit -m "msg1" -m "body"
git push origin main
git checkout -b "newbranch"
git checkout "branch"
git branch newbranch
git push
git pull origin main
git reset --hard <sha>
git reset --soft <sha>
git push --force origin main

git stash list
git stash apply
<!-- delete most recent stash -->
git stash drop
<!-- delete all stashes -->
git stash clear
<!-- delete specific stash -->
git stash pop <name>

<!-- branch2 is merged into one -->
base, incoming, and current
<in branch1> git merge <branch2> 
git merge --abort
git add <conflict file>
git commit -m "msg"

git branch -D branch2
git log branch --oneline
<!-- copy a single commit from another branch -->
git cherry-pick <hash>

<!-- change date -->
GIT_AUTHOR_DATE="2026-01-24 12:00:00 +0530" \
GIT_COMMITTER_DATE="2026-01-24 12:00:00 +0530" \
git commit -m "your message"