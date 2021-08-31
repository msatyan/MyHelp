

### [Merge changes from a repository](https://www.atlassian.com/git/tutorials/git-merge)
```
-- pull changes from some other repository
git pull https://github.com/msatyan/SomeOtherRepository.git <branch on that repo>
git pull https://github.com/msatyan/SomeOtherRepository.git SomeOtherTask
git pull https://github.com/msatyan/SomeOtherRepository.git master

-- Resolve conflicts if any (complete the mergetool setup first)
git mergetool

-- DO: Test and then checkin
git status
git add -A
git commit -m 'New Help Info'
git push origin MyNewBranch
```




### FYI
```bash
# error: You have not concluded your merge (MERGE_HEAD exists).
Then you may undo the merge and pull again
or if you are sure that you have resolved all merge conflicts then

m -rf .git/MERGE*
```


#### Undo the merge and pull again.
```
To undo a merge:

git merge --abort [Since git version 1.7.4]

git reset --merge [prior git versions]

Resolve the conflict.

Don't forget to add and commit the merge.

git pull now should work fine.
```