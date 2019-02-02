
### Useful Tools
* [git-scm](https://git-scm.com/)
* [kdiff3](http://kdiff3.sourceforge.net/)
* [Git Extensions](https://github.com/gitextensions/gitextensions)
* [Atlassian SourceTree](https://www.sourcetreeapp.com/)
* [WinMerge](http://winmerge.org/?lang=en)



### Git Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email abcdef@somemail.com

```


### List config
```bash
git config --list
# or for shorter
git config -l

# To get system config with specifics
git config --list --global
git config --list --local
git config --list --system


or .gitconfig file on your home dire, say
# if you are UNIX/Linux
cat ~/.gitconfig
# Windows
type %USERPROFILE%\.gitconfig
```

### Caching your GitHub password in Git
```bash
# Windows
git config --global credential.helper wincred

# Linux
git config --global credential.helper store

# tell git to cache your password for a specific duration, say 8 hours, then.
git config --global credential.helper 'cache --timeout 28800'
```


### Flush any stored password from cache
```bash
# Say you want to switch to another user or forget the password for wathever reason
git credential-cache exit
```


### Frequently used Git commands
```
git status
git add -A
git commit -m "Checkin Comment"
git push -u origin master
```


### Useful Tools
* [git-scm](https://git-scm.com/)
* [kdiff3](http://kdiff3.sourceforge.net/)
* [Git Extensions](https://github.com/gitextensions/gitextensions)
* [Atlassian SourceTree](https://www.sourcetreeapp.com/)
* [WinMerge](http://winmerge.org/?lang=en)


### mergetool & difftool
```bash
https://git-scm.com/docs/git-mergetool
https://git-scm.com/docs/git-difftool#git-difftool---no-trust-exit-code

git config --global --add merge.tool kdiff3
git config --global --add mergetool.kdiff3.path "C:/Dev/KDiff3/kdiff3.exe"
git config --global --add mergetool.kdiff3.trustExitCode false

git config --global --add diff.guitool kdiff3
git config --global --add difftool.kdiff3.path "C:/Dev/KDiff3/kdiff3.exe"
git config --global --add difftool.kdiff3.trustExitCode false

#The use of the trustExitCode option depends on what you want to do when diff tool returns.
https://git-scm.com/docs/git-difftool#git-difftool---no-trust-exit-code
```

### Setting up kdiff3 as the Default Merge Tool for git on Windows
```bash
git config --global merge.tool kdiff3
git config --global mergetool.kdiff3.cmd '"C:\\Dev\\KDiff3\\kdiff3" $BASE $LOCAL $REMOTE -o $MERGED'
# FYI: Alternatively you may modify the .gitconfig directly

# Now you can issue the following command to resolve the difference.
git mergetool
```


### Visual Studio Code git credentials pop-up
```bash
https://www.visualstudio.com/en-us/docs/git/set-up-credential-managers

Windows Start
type: "credential manager"

# Add a generic credential
internet or network address : https://github.mygit.com
user name : user1@SomMail.com
Password: <git access token >
          Eg: 23857d694a1f39423897130138982392f2a7aa80e

# Then when opene a VS Code, you may get pop-up one more time
# Give the same user name and passrod specified above
```

