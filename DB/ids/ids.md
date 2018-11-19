
#### Configuring installation path permissions during installation
```
https://www.ibm.com/support/knowledgecenter/en/SSGU8G_12.1.0/com.ibm.sec.doc/ids_us_012.htm

onsecurity 
/etc/informix/trusted.insecure.directories
```

#### env.bsh
```
#export SQLIDEBUG=2:/work/dev/srv/ids0/tmp/sqli/sqt
#sqliprint -o 0.txt sqt_5798
#export PS1="[\u@\h:\w]$ "

alias ls='ls --color=none'

#################################################
# export ODBCINI=/work/dev/odbc/envs/odbc.ini
export INFORMIXDIR=/work/dev/srv/sqldist.s
#################################################

export INFORMIXSERVER=ids0
export INFORMIXSQLHOSTS=/work/dev/srv/ids0/sqlhosts
export ONCONFIG=onconfig.ids0

export LD_LIBRARY_PATH=${INFORMIXDIR}/lib:${INFORMIXDIR}/lib/esql:${INFORMIXDIR}/lib/cli
export PATH=$INFORMIXDIR/bin:$PATH

export CLIENT_LOCALE=en_us.8859-1
export DB_LOCALE=en_us.8859-1
```

#### /work/dev/srv/ids0/sqlhosts
```
ids0     onsoctcp   127.0.0.1  5550
ids0_dr  drsoctcp   127.0.0.1  5560
```

#### ls -l |...
```
-rw-rw---- 1 informix informix   dbsp
-rw-rw-rw- 1 informix informix   log
-rw-r--r-- 1 informix informix   sqlhosts
drwxrwxr-x 2 informix informix   tmp
```

#### srv_clean.bsh 
```
# su informix
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

