

### VS 
* [Highlight all occurrences of selected word](https://marketplace.visualstudio.com/items?itemName=BenaiahJohn.Highlightalloccurrencesofselectedword)


### Dev tools
- [Git Extensions](https://gitextensions.github.io/)


### Visual Studio Code

##### upgrade
```bash
# https://code.visualstudio.com/docs/setup/linux

# RHEL/ CentOS
yum check-update
sudo yum install code

# Debian/Ubuntu based distributions
sudo apt-get update
sudo apt-get install code

# to remove
sudo apt-get remove code
sudo apt-get purge code

```

#### Disable telemetry reporting
```bash
# From File > Preferences > Settings
"telemetry.enableTelemetry": false
```

* [VS Marketplace](https://marketplace.visualstudio.com/search?term=devlabs&target=VS&sortBy=Relevance)
---

#### Git
* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
* [Git File History](https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-git-history)
* [Trailing spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
---

* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
* [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* [Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
* [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)
* [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)
* [HTML Snippets](https://marketplace.visualstudio.com/items?itemName=abusaidm.html-snippets)
* [open in browser](https://marketplace.visualstudio.com/items?itemName=techer.open-in-browser)
* [HTML Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)

---
* [Node.js Modules Intellisense](https://marketplace.visualstudio.com/items?itemName=leizongmin.node-module-intellisense)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)


* [Angular and TypeScript/HTML VS Code Snippets](https://marketplace.visualstudio.com/items?itemName=danwahlin.angular2-snippets)

* [Auto Import](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)
---
* [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
* [Auto-Open Markdown Preview](https://marketplace.visualstudio.com/items?itemName=hnw.vscode-auto-open-markdown-preview)

---
* [C/C++ for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

---
* [Python extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
* [VS Code Jupyter Notebook Previewer](https://marketplace.visualstudio.com/items?itemName=jithurjacob.nbpreviewer)
* [Jupyter: An extension with rich support for Jupyter](https://marketplace.visualstudio.com/items?itemName=donjayamanne.jupyter)


---
- [Red Hat: Language Support for Java(TM)](https://marketplace.visualstudio.com/items?itemName=redhat.java)
- [Microsoft: Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
- [Java Test Runner](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-test)
- [Maven for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven)
```bash
# To get Java debug support on VSCode
https://code.visualstudio.com/docs/languages/java

path=C:\Dev\jre18\bin;C:\Dev\maven354\bin
JAVA_HOME=C:\Dev\jdk18
JDK_HOME=C:\Dev\jdk18
JRK_HOME=C:\Dev\jre18

# Downloading Apache Maven
https://maven.apache.org/download.cgi

# Create myJavaApp1 Java Project
cd c:\work
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=myJavaApp1 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd c:\work\myJavaApp1
```


#### DB2 JCC setup
```bash
# DB2 JCC setup
SET CLASSPATH=.;C:\Dev\jdk18\lib\tools.jar;C:\SQLLIB\java\db2java.zip;C:\SQLLIB\java\db2jcc.jar;C:\SQLLIB\java\sqlj.zip;C:\SQLLIB\java\db2jcc_license_cu.jar;C:\SQLLIB\bin;C:\SQLLIB\java\common.jar;

# If not already exist, then copy the driver and license files at C:\SQLLIB\java\ Then run the folloing command 
mvn install:install-file -Dfile=C:\SQLLIB\java\db2jcc.jar -DgroupId=com.ibm.db2.jcc -DartifactId=db2jcc4 -Dversion=10.1 -Dpackaging=jar -DgeneratePom=true -DcreateChecksum=true

mvn install:install-file -Dfile=C:\SQLLIB\java\db2jcc_license_cu.jar -DgroupId=com.ibm.db2 -DartifactId=db2jcc_license_cu -Dversion=10.1 -Dpackaging=jar -DgeneratePom=true -DcreateChecksum=true

# Edit pom.xml of your project to include the following:
<dependency>
    <groupId>com.ibm.db2.jcc</groupId>
    <artifactId>db2jcc4</artifactId>
    <version>10.1</version>
</dependency>

<dependency>
    <groupId>com.ibm.db2</groupId>
    <artifactId>db2jcc_license_cu</artifactId>
    <version>10.1</version>
</dependency>

```


##### VSC git credentials pop-up
```bash
https://www.visualstudio.com/en-us/docs/git/set-up-credential-managers

Start
type: "credential manager"

Add a generic credential 
internet or network address : https://github.example.com
user name : user1@.example.com
Password: <git access token > 
          Eg: 23857694a1xxxxxxxx80e4281ae3a85b08f477dea


Then when opene a VS Code, you may get pop-up one more time
Give the same user name and password specified above 
```

##### VSC Linux Debug
```bash
VS Code : Configuring launch.json for C/C++ debugging
https://code.visualstudio.com/docs/languages/cpp
https://github.com/Microsoft/vscode-cpptools/blob/master/launch.md
https://blogs.msdn.microsoft.com/vcblog/2016/03/31/cc-extension-for-visual-studio-code/#debugging
https://marketplace.visualstudio.com/items?itemName=webfreak.debug
https://medium.com/@spe_/debugging-c-c-programs-remotely-using-visual-studio-code-and-gdbserver-559d3434fb78

https://github.com/Microsoft/vscode-cpptools/issues/78
```

#### GDB attach
```bash
    { 
        "name": "(gdb) Attach",
        "type": "cppdbg",
        "request": "attach",
        "program": "/work/dev/Python/python",
        "processId": "2170",
        "MIMode": "gdb",
        "miDebuggerPath": "/usr/bin/gdb",
        "additionalSOLibSearchPath" : "/work/ifxdb/try"
    },
```
