
* [Initial System Setup]
* [Post OS Install Basic Setup]

## Initial System Setup
* [Raspberry Pi](https://www.raspberrypi.org/)

* [SD Memory Card Formatter](https://www.sdcard.org/downloads/formatter_4/)
Format SD card by using SD Memory Card Formatter

* [Download NOOBS](https://www.raspberrypi.org/downloads/)
Download NOOBS and extract content of the zip to root of the SD card. Then insert the SD to Pi and powr on.

## [Post OS Install Basic Setup](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)

### [User Management](https://www.raspberrypi.org/documentation/linux/usage/users.md)

#### Change passwd 
```bash
passwd 
or 
passwd  <usr id>
```

#### Create a new user
```bash
sudo adduser <user id>

#Delete a user (the -r flag to remove their home folder too)
sudo userdel -r <user id>
```

#### Change the default edito from Nano to vim
visudo command uses the default editor Nano, to use vim then
```
sudo update-alternatives --set editor /usr/bin/vim.tiny
```

visudo edits the sudoers file, which is used by the sudo command
```bash
sudo visudo 
#or 
sudo vi /etc/sudoers

<user id>   ALL = NOPASSWD: ALL
```

#### [Enable SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)
#### [Vnc Setup](https://www.raspberrypi.org/documentation/remote-access/vnc/README.md)
#### [IBM No-charge products, tools, and toolkits](https://www-01.ibm.com/marketing/iwm/tnd/nochargesearch.jsp?q=Informix)


### Update
```bash
sudo apt-get update
sudo apt-get upgrade
#sudo apt-get install git
```

### nodejs
#### Remove old nodejs installation if any
```bash
sudo apt-get remove nodered -y
sudo apt-get remove nodejs -y
sudo apt-get remove nodejs-legacy -y
sudo apt-get remove npm  -y
```

If the node doesn’t get removed then you have to do a bit of manual work
```bash 
# go to /etc/apt/sources.list.d and 
#remove any node list if you have; then do a
sudo apt-get update

# If you still see node, delete it from that location.
which node
```



#### Install 8x nodejs
```bash
# curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```


#### FYI Only: Alternative approach
```bash  
rm /work/nodejs
cd /work/dev

###### if ARM v7 (Raspberry Pi 3)
sudo wget https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-armv7l.tar.xz 
sudo tar -xvf node-v8.9.4-linux-armv7l.tar.xz
sudo ln -s  /work/dev/node-v8.9.4-linux-armv7l  /work/nodejs

export PATH=/work/nodejs/bin:$PATH
which node
node -v
```



### Install the required build-tools
```
sudo apt-get update
sudo apt-get install build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev
```

#### Build Python 2.7 from its source
``` bash
cd /work/dev
wget https://www.python.org/ftp/python/2.7.13/Python-2.7.13.tgz

tar zxvf Python-2.7.13.tgz
ln -s  ./Python-2.7.13  ./Python

cd /work/dev/Python
sudo ./configure --enable-unicode=ucs4
sudo make
#  sudo altinstall
```

#### Build Python 3.x from its source
```bash
cd /work/dev
wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tar.xz
tar xf Python-3.6.2.tar.xz
cd Python-3.6.2
./configure --enable-optimizations
make
# sudo make altinstall
```

#### Create a link for common usage
``` bash
cd /work/dev
rm ./Python
# ln -s  ./Python-2.7.13  ./Python
ln -s  ./Python-3.6.2   ./Python
export PATH=/work/dev/Python:$PATH
```
#### Informix easy access path
```bash
sudo rm /work/informix
# sudo ln -s /work/dev/srv/sqldist.s /work/informix
sudo ln -s /work/dev/srv/sqldist.c /work/informix
```



#### VS Code on pi
```
https://www.hanselman.com/blog/BuildingVisualStudioCodeOnARaspberryPi3.aspx
```

