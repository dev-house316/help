## Git

Change the **global** username for commits made by default on all repos:

```
git config --global user.name "Darren Jensen"
git config --global user.email "darren.jensen@gmail.com"
git config credential.username 'jensendarren'
```

Change the **local** username for commits made in a _specific_ repo:

```
git config user.name "Darren Jensen Contractor"
git config user.email "darren.jensen@acontractor.com"
```

Get the diff between two commits

```
# Between 4ac0a673 and 5688b75
git diff 5688b75..4ac0a673

# Between working copy and 5688b75
git diff 5688b75
```

Show a specific file at a particular commit

```
git show 000a7a9a:path/to/the/file.txt
```

Replace that version of the file in your wd

```
git checkout 000a7a9a path/to/the/file.txt
```

### Pushing to multiple git repos

Taken from [this gist](https://gist.github.com/rvl/c3f156e117e22a25f242)

Start by cloning the test repo!!

`git clone git@bitbucket.org:darren_jensen/hurdey-gurdey.git`

Setup remotes (the **origin** remote probably points to one of these URLs):

```
# Just set one additional remote since we can assume the remote origin is already set to git@bitbucket.org:darren_jensen/hurdey-gurdey.git since that is where we cloned from
git remote add rotati git@github.com:rotati/hurdey-gurdey.git
```

Setup remote push URLs

```
git remote set-url --add --push origin git@bitbucket.org:darren_jensen/hurdey-gurdey.git
git remote set-url --add --push origin git@github.com:rotati/hurdey-gurdey.git
```

Set the default checkout default remote to origin:

```
git config --add checkout.defaultRemote origin
```

Check the config

```
git remote show origin
cat .git/config
```

So now all pushes will push to both remote repositories (no changes to the workflow here):

```
git push origin master
```

For pulling in work is slightly different in order to fetch changes from both remote repos. In order to do that:

```
git fetch --all
git merge --squash github/next_release bb/next_release
```

Process is:

```
git checkout develop
git pull origin develop
git checkout -b some_new_branch
git fetch --all
git branch -a
git checkout rotati/167337886_blah <-- now in detached HEAD
git merge some_new_branch <-- effectivly merging in develop HEAD
git checkout some_new_branch
git merge --squash rotati/167337886_blah
# Do work then commit....
```

### Deleting a local and remote commit

```
# Find the commit SHA you wish to remove from the current branch logs
git log --pretty=oneline --abbrev-commit

# Open the rebase tool to show the last N commits (here 2)
git rebase -i HEAD~2

# In the text editor that opens, remove the commit line from the file
# In my case the file opens in nano so I just remove the like using CTRL+K and then exit from nano

# Check the log again and you should see the commit is gone!
git log --pretty=oneline --abbrev-commit

# Finally, you must to a forced push to update the changes to the remote branch (note the + before the branch name means to force the changes)
git push origin +branch_name
```

### Deleting local and remote branches

```
# To delete a local branch
git branch -d branch_name

# To delete a remote branch
git push <remote_name> --delete <branch_name>
```