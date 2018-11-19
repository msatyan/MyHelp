
### Silent Install
```bash
# Client
https://www.ibm.com/support/knowledgecenter/en/SSGU8G_12.1.0/com.ibm.cpi.doc/ids_cpi_018.htm

installclientsdk.exe -i silent -DLICENSE_ACCEPTED=TRUE -DUSER_INSTALL_DIR=c:\informix

# Server
https://www.ibm.com/support/knowledgecenter/en/SSGU8G_12.1.0/com.ibm.inst.doc/ids_inst_016.htm

ids_install.exe -i silent -DLICENSE_ACCEPTED=TRUE -DUSER_INSTALL_DIR=C:\InformixS
```


### Manual Install

```bash
# let us say we want to install IDS at /opt/informix/12.10.FC12
sudo mkdir /opt/informix

cd /work/t
tar -xvf iif.12.10.FC12.linux-x86_64.tar
export INFORMIXDIR=/opt/informix/12.10.FC12
sudo ./ids_install

# When it ask for install folder you may give 
# /opt/informix/12.10.FC12
```


### Basic step
```bash
# to make it easy access
sudo ln -s /opt/informix/12.10.FC12 /work/informix

# if user informix don't have a home dir yet, then
# sudo usermod -d /path/to/new/home -m username
cd /home
sudo mkdir informix
sudo chown informix:informix informix
sudo usermod -d /home/informix informix
```

### Copy Onconfig
```bash
sudo  cp /work/dev/srv/etc/onconfig.ids0 /work/informix/etc/onconfig.ids0
sudo chown informix:informix /work/informix/etc/onconfig.ids0
```

### sqlhost
```bash
# if you are using loop back connection then
# ids0     onsoctcp   127.0.0.1  5550
# ids0_dr  drsoctcp   127.0.0.1  5560
# if you are using static IP then you may give the IP
ids0     onsoctcp   192.168.56.5  5550
ids0_dr  drsoctcp   192.168.56.5  5560
```



#### srv_clean.bsh 
```
# su informix
# or
# sudo -u informix bash

onmode    -kuy 

rm -rf    /work/dev/srv/ids0/tmp
mkdir     /work/dev/srv/ids0/tmp
chmod 775 /work/dev/srv/ids0/tmp

rm        /work/dev/srv/ids0/dbsp
touch     /work/dev/srv/ids0/dbsp
chmod 660 /work/dev/srv/ids0/dbsp

rm        /work/dev/srv/ids0/log
touch     /work/dev/srv/ids0/log
chmod 666 /work/dev/srv/ids0/log
```

### ls -l /work/dev/srv/ids0
```
# output
-rw-rw---- 1 informix informix   dbsp
-rw-rw-rw- 1 informix informix   log
-rw-r--r-- 1 informix informix   sqlhosts
drwxrwxr-x 2 informix informix   tmp
```



### Env
```bash
#export SQLIDEBUG=2:/work/dev/srv/ids0/tmp/sqli/sqt
#sqliprint -o 0.txt sqt_5798
#export PS1="[\u@\h:\w]$ "

alias ls='ls --color=none'

#################################################
# export ODBCINI=/work/dev/odbc/envs/odbc.ini
# sudo ln -s /opt/informix/12.10.FC12 /work/informix
export INFORMIXDIR=/work/informix
#################################################

export INFORMIXSERVER=ids0
export INFORMIXSQLHOSTS=/work/dev/srv/ids0/sqlhosts
export ONCONFIG=onconfig.ids0

export LD_LIBRARY_PATH=${INFORMIXDIR}/lib:${INFORMIXDIR}/lib/esql:${INFORMIXDIR}/lib/cli
export PATH=$INFORMIXDIR/bin:$PATH

export CLIENT_LOCALE=en_us.8859-1
export DB_LOCALE=en_us.8859-1
```



#### Configuring installation path permissions during installation
```bash
https://www.ibm.com/support/knowledgecenter/en/SSGU8G_12.1.0/com.ibm.sec.doc/ids_us_012.htm

onsecurity 
/etc/informix/trusted.insecure.directories
```


```bash
sudo mkdir /etc/informix
sudo chown informix:informix /etc/informix

sudo touch /etc/informix/trusted.insecure.directories
sudo chown informix:informix /etc/informix/trusted.insecure.directories
```

### sudo vi /etc/informix/trusted.insecure.directories
```bash
# Remove public write permissions
# Removes public write access to directories in the installation path.
# Add the directory to the list of trusted but nonsecure directories
# Adds any directories with public write access to the /etc/informix/trusted.insecure.directories file.
#g:

/work
```

