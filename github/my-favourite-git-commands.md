# My favourite Git commands

```bash
# create a new branch
git checkout -b /feature/postcode

# checkout remote branch
git checkout --track origin/feature/postcode


# clone with a directory name
git clone <git address> <directory name>

# pull the latest commits and merge them into the current branch
git pull

# fetch the latest commits
git fetch

# delete the local branch forcefully
git branch -D feature/tools 

# delete the remote branch
git push origin --delete feature/lambda

# sometimes you get this error
error: unable to push to unqualified destination: remoteBranchName The destination refspec neither matches an existing ref

# then sync your branch list
git fetch -p

# delete files from commit
git rm --cached ./lock.json

```

