

### Binary in Linux

```bash
/bin (and /sbin) 
# were intended for programs that needed to be on a small / partition before the larger /usr, etc.
# These must be available before file systems are mounted. Things like mount, and fsck
# similarly installations on small embedded devices.

/sbin 
# Similar to /bin, but for system management programs (not normally used by ordinary users) needed before /usr is mounted.

/usr/bin
# is for distribution-managed normal user programs.

/usr/sbin
# is for distribution-managed normal system programs.

/usr/local/bin
# is for normal user programs not managed by the distribution package manager, 
# Eg locally compiled packages.
# FYI: You should not install them into /usr/bin because future distribution upgrades may modify or delete them without warning.

/usr/local/sbin
#  Locally installed programs for system administration (Similar to /usr/local/bin)

/opt
# which is for monolithic non-distribution packages
```

### Paths
In general PATH is used primarily by the shell, while LD_LIBRARY_PATH is used by the dynamic loader.

```bash
PATH: 
# executables (e.g. /home/username/bin:/usr/local/bin:/usr/bin:/bin).

MANPATH: 
manual pages (e.g. /usr/local/man:/usr/man).

LD_LIBRARY_PATH:
# LD_LIBRARY_PATH is used for run time resolution of native code libraries.
# The name LD comes from dynamic loader, the system component that loads libraries into dynamically linked executables.

LD_RUN_PATH:
# LD_RUN_PATH is used for the link time resolution of libraries  
# FYI: Linker will not search LD_LIBRARY_PATH

PERL5LIB:
# Perl libraries (e.g. /usr/local/lib/site-perl:/usr/lib/site-perl:/usr/lib/perl:/usr/share/perl).

PYTHONPATH: 
# Python libraries (e.g. /usr/local/lib/python:/usr/lib/python:/usr/lib/python2.6).

TCLLIBPATH: 
# TCL libraries (e.g. /usr/local/lib/tcltk:/usr/lib/tcltk).

CLASSPATH:
# The CLASSPATH environment variable tells the Java virtual machine where to find the class libraries, such as the jdmktk.jar file
```


### Package Management
####  Debian and Ubuntu Package Management
Linux-based operating systems install software in pre-compiled packages, package management tools keep track of updates and upgrades of it. The Debian and Ubuntu Package Management are based on a tool called dpkg. The apt-get and apt-cache etc are merely frontend programs that provide a more usable interface and connections to repositories for the underlying package management tools called **dpkg** and **debconf**.  

Advanced Packaging Tool (APT) was introduced in  Ubuntu 16.04 to simplify the package manager and to merge multiple commands into one single command. The functions from **apt-get** have been taken and have been created to function in similar ways in Apt. In general **apt** is mostly a subset of **apt-get** and **apt-cache** commands providing necessary commands for package management
- apt-get
- apt

##### /etc/apt/sources.list
The file /etc/apt/sources.list controls repositories from which **APT** constructs its database

#### New Apt basic commands
```bash
list – list packages based on package names
search – search in package descriptions
show – show package details
update – update list of available packages
install – install packages
remove – remove packages
upgrade – upgrade the system by installing/upgrading packages
full-upgrade – upgrade the system by removing/installing/upgrading packages
edit-sources – edit the source information file
```



apt command	the command it replaces	function of the command

| apt command | the command it replaces | function of the command |
|-------------|-------------------------|-------------------------|
apt install	| apt-get install	| Installs a package
apt remove	| apt-get remove	Removes a package
apt purge	| apt-get purge	| Removes package with configuration
apt update	| apt-get update | Refreshes repository index
apt upgrade	| apt-get upgrade | Upgrades all upgradable packages
apt autoremove | apt-get autoremove	| Removes unwanted packages
apt full-upgrade | apt-get dist-upgrade	| Upgrades packages with auto-handling of dependencies
apt search | apt-cache search | Searches for the program
apt show | apt-cache show | Shows package details


FYI: apt has a few commands of its own as well.

| new apt command | function of the command
|-----------------|-------------------------|
apt list | Lists packages with criteria (installed, upgradable etc)
apt edit-sources | Edits sources list



### Package Management for Fedora RHEL and CentOS 

**YUM** and **DNF** are simply front-ends to a lower-level tool called **RPM**, (similar to apt-get’s relationship with dpkg).  Starting with version 22, Fedora uses the **dnf** package manager instead of YUM, then now it is. 
- **yum** : Red Hat, CentOS
- **dnf** Fedora






