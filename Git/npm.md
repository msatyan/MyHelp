


## One time System Setup
------------------------

#### git config 
```bash
git config --global user.name "User1"
git config --global user.email user1@gmail.com
```

```bash
cd C:\try\npm-tmp-pkg2
C:\try\npm-tmp-pkg2>ls 
index2.js     package.json
```

#### npm adduser 
```bash
npm adduser
#Username: user1
#Password:
#Email: (this IS public) user1@gmail.com

# to list user info
npm config ls
```


## Create NPM Package
---------------------
* create package.json (npm init)
* Create entry poing script to this module
* npm publish
* Test the new package.
- npm install <package name>


#### npm init (Create package.json)
The **npm init** is to create a package.json, it is an interactive module. at the end it will create a package.json

```bash
md npm-tmp-pkg
cd npm-tmp-pkg

npm init
```

#### Create entry poing script (index.js) for the package
```JavaScript
//cat index.js
exports.PrintMsg = function( )
{
	console.log( "Hello World!" );
}
```


#### npm publish
```bash
npm publish
```

#### Test the new package
```bash
cd /tmp
npm install npm-tmp-pkg
```


## Create NPM Package and put source on Github
----------------------------------------------

#### npm init
```bash
C:\try\
md npm-tmp-pkg2
cd npm-tmp-pkg2

npm init
```

#### Create entry poing script (index2.js) for the package
```JavaScript
// cat index2.js

exports.PrintMsg = function( )
{
	console.log( "Hello World!"  );
}
```


#### Create a git repository
```bash
git init
git add .
git commit -m 'First commit'

git remote add origin https://github.com/user1/test2.git
git remote -v

git push origin master
```

#### npm publish
```bash
npm publish
```


#### Test the new package
```bash
npm install npm-tmp-pkg2
```


## Increment NPM Version
------------------------
##### FYI:
* npm version patch   (no breaking change and no new functionality)
* npm version minor   (new functionality added, but no breaking)
* npm version major   (breaking change)

### Version Patch
```bash
npm version patch
```

#### Push all changes to git
```bash
git status
git add -A

git commit -m "Win64 build"
git push -u origin master
```

### publish
```bash
npm publish
```

