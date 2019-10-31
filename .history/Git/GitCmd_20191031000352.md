

### Git Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email abcdef@somemail.com

# Caching your GitHub password in Git
# git config --global credential.helper wincred
```

### Frequently used Git commands
```
git status
git add -A
git commit -m "Checkin Comment"
git push -u origin master
```


### [A New Branch for your work](https://www.atlassian.com/git/tutorials/using-branches)
```bash
# Let us say, you are creating a new branch for your dev work
# let us create a branch dev1 then.
git clone https://github.com/msatyan/MyHelp.git
cd MyHelp
git branch dev1
git checkout dev1


# do some work and check-in your changes to dev1 branch
git status
git add -A
git commit -m "dev1 changes"
git push origin dev1

# Dev work completed, then switch branch to master
# pull the dev1 branch changes to master
git checkout master
git pull https://github.com/msatyan/MyHelp.git dev1

# now you have dev1 changes, push it to remote
git push origin master

# Delete the branch and push
git push origin --delete dev1
git push origin :dev1
```


### [Merge changes from a repository](https://www.atlassian.com/git/tutorials/git-merge)
```bash
# pull changes from some other repository
git pull https://github.com/msatyan/SomeOtherRepository.git <branch on that repo>
git pull https://github.com/msatyan/SomeOtherRepository.git SomeOtherTask
git pull https://github.com/msatyan/SomeOtherRepository.git master

# Resolve conflicts if any (complete the mergetool setup first)
git mergetool

# DO: Test and then checkin
git status
git add -A
git commit -m 'New Help Info'
git push origin dev1
```

### [Syncing](https://www.atlassian.com/git/tutorials/syncing)
```bash
# See help on
git remote
git fetch
git pull
git push
```
### [Resetting, Checking Out, and Reverting](https://www.atlassian.com/git/tutorials/advanced-overview)
```
git reset
git checkout
git revert
```


### [git-diff](https://git-scm.com/docs/git-diff)
```
git diff [options] [<commit>] [--] [<path>…​]
git diff [options] --cached [<commit>] [--] [<path>…​]
git diff [options] <commit> <commit> [--] [<path>…​]
git diff [options] <blob> <blob>
git diff [options] [--no-index] [--] <path> <path>
```


### [git log](https://www.atlassian.com/git/tutorials/git-log)
```
git log --oneline --decorate --graph --all
```

### [git Remote](https://git-scm.com/docs/git-remote)
```bash
# to get remote URL, or referential integrity has been broken:
git config --get remote.origin.url

# to get full output or referential integrity is intact:
git remote show origin

# It will print all your remotes' fetch/push URLs.
git remote -v
```

### Ignore to untrack a file
```bash
# To untrack a single file that has already been added/initialized to your repository
git rm --cached filename

git add .
git commit -m "untrack the file"
```

### Delete Commit History in Git Repository
```diff
- Warning: This will remove your old commit history completely, You can’t recover it again.
```

- Create Orphan Branch – Create a new orphan branch in git repository. The newly created branch will not show in ‘git branch’ command.
```
git checkout --orphan temp_branch
```

- Add Files to Branch – Now add all files to newly created branch and commit them using following commands.
```
git add -A
git commit -am "the first commit"
```

- Delete master Branch – Now you can delete the master branch from your git repository.
```
git branch -D master

```

- Rename Current Branch – After deleting the master branch, let’s rename newly created branch name to master.
```
git branch -m master

```
- Push Changes – You have completed the changes to your local git repository. Finally, push your changes to remote (Github) repository forcefully.
```
git push -f origin master
```


### FYI:
* [Making a Pull Request](https://www.atlassian.com/git/tutorials/making-a-pull-request)
* [Become a Git pro in just one blog](https://itnext.io/become-a-git-pro-in-just-one-blog-a-thorough-guide-to-git-architecture-and-command-line-interface-93fbe9bdb395)


