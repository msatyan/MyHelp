
### Basic
```bash
db2stop
db2start

db2 create database MYDB1 using codeset UTF-8 territory US

db2 connect to MYDB1 user myuser1 using xxxxx
# db2 list applications
# db2 -tdf sample.sql
# db2 -td! -vf sample.sql
db2 disconnect all
```


### Creating a new schema
```bash
db2 CREATE SCHEMA <schema-name>

# to list schema users
db2 SELECT SCHEMANAME FROM syscat.schemata

# Grant privileges
GRANT ALL ON <schema-name>.<table-name> TO USER <user>
```

### List information about tables
```bash
#List all tables:
db2 list tables for all

#To list all tables in selected schema, use:
db2 list tables for schema <schema-name>

#To describe a table, type:
db2 describe table <table-schema.table-name>
```


### List information about databases
```bash
# Database uptime
db2pd -

# List databases:
db2 list database directory

# LIST ACTIVE DATABASES
db2 "LIST ACTIVE DATABASES"

# Activate a database:
db2 "ACTIVATE DATABASE dbname"

# Deactivating a database: (All connections must be removed first):
db2 "DEACTIVATE DATABASE dbname"

# Force off all connections to a database:
db2 "FORCE APPLICATION ALL"

# Force off specific connections to a database:
db2 "FORCE APPLICATION (pid)"
db2 "FORCE APPLICATION (pid, pid, pid)"

# Who is connected to the database?
db2 "LIST APPLICATIONS"

# How many connections are there to the database?
db2 "LIST ACTIVE DATABASES" | grep connected

db2 get dbm cfg
DB2 LIST DATABASE DIRECTORY
DB2 LIST NODE DIRECTORY
db2 list node directory show detail

###
db2set DB2_GRP_LOOKUP=LOCAL,TOKENLOCAL
db2 update dbm cfg using sysadm_group DB2ADMNS
db2stop
db2start
```




### Grant
```bash
# Grant the ability to connect to the database:
# for a user
db2 "GRANT CONNECT ON DATABASE TO USER (username)"

# For an OS group:
db2 "GRANT CONNECT ON DATABASE TO GROUP (groupname)"

# Grant authorization to do something to a table
# (Select from it, delete from it, etc):
db2 "GRANT <SELECT, INSERT, UPDATE, or DELETE> ON (SCHEMA).(TABLENAME) TO (USER or GROUP) (username or groupname)"
```


### optimizer plan
```bash
# Look at how optimizer runs SQL (Explain Plan):
db2expln -d -f -g -z \; -o ORIG_EXPLAIN.out
```


### Backup
```bash
# Backing up a database when it Offline: (No connections, Database Deactivated)
db2 "BACKUP DATABASE (dbname) TO (/directory) "

# Backing up a database (Online): (DB up and active with connections)
db2 "BACKUP DATABASE (dbname) ONLINE TO (/directory)"

# See details on a backup file: (Online or offline, how granular, compressed, log path, etc)
db2ckbkp -h
```


### DOS: Catalog template
```bat
@echo off
SET HOST_IP=my-computer1.mydns.com
SET SRV_PORT=5565
SET PHY_DB=dbla
SET NODE_NAME=mynode1

echo db2 uncatalog node %NODE_NAME%
echo db2 uncatalog db %PHY_DB%

echo db2 catalog tcpip node %NODE_NAME% remote %HOST_IP% server %SRV_PORT%
echo db2 catalog database %PHY_DB% at node %NODE_NAME%

echo db2 connect to %PHY_DB% user myuser1 using xxxxx
echo db2 disconnect all
```



### Uncatalog
```bash
db2 uncatalog node mynode1
db2 uncatalog db dbla

db2 catalog tcpip node mynode1  remote my-computer1.mydns.com  server 5565
db2 catalog database dbla at node mynode1

db2 connect to dbla user myuser1 using xxxxx
db2 disconnect all
```


### Catalog Inforix DB with DB2
```bash
# drop database ids0db1;
# CREATE DATABASE ids0db1 with LOG MODE ANSI;

# From DB2 command window catalog it as follow
db2 catalog tcpip node mynode1 remote my-computer1.mydns.com server 5565
db2 catalog database ids0db1 at node mynode1
db2 connect to ids0db1 user myuser1 using xxxxx
```


### Trace 
```bash
# To dump only the SQL statement
db2trc on -m "exit.*.42.73.*" -t
#db2trc on -m "entry.*.84.20.*" -t   (84 is for dotnet)
db2trc clear
db2trc dump dmp
db2trc off
db2trc fmt dmp    fmt.txt

# db2trc on -i 16m -m "*.*.*.*.*"
# db2trc on -i 16m -m  "*.*.42.*.*" -t

db2trc dump dmp
db2trc off
db2trc flw dmp flw.txt
db2trc fmt dmp fmt.txt
db2trc fmt -c dmp fmtc.txt
```

