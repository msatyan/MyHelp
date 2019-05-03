

### git tag

```bash
#### Step1
# git checkout <branch>
# eg:
git checkout master

#### step2
git tag <tag name>
eg:
git tag  v1.0

# Annotated Tags
git tag -a v1.4
or
git tag -a v1.4 -m "my version 1.4"

# to list
git tag

## Tagging Old Commits: First get the old commit lists
# To gather a list of older commits
git log --pretty=oneline

#### Sharing: Pushing Tags to Remote
# Sharing tags is similar to pushing branches.
# By default, git push will not push tags.
# Tags have to be explicitly passed to git push.
git push origin v1.4

# Checking Out Tags
git checkout v1.4

# Deleting Tags
git tag -d v1.4
git push origin -d v1.4

# to get detail about the change
git show v1.4

# push remote
git push origin v1.4
or to push all tags
git push --tags

# For pulling
git fetch --tags to pull them all in
to pull a single one
git fetch tag

# There is no concept of checkout tag
# we can create a branch from a tag and it can be check out.
git checkout -b <branch name> <tag name>
git checkout -b MyTmpBranch1 v1.4

###
git checkout tags/v2.0.0-beta.1 -b napi
```

