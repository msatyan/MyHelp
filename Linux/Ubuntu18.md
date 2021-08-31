
### Basic setup after system install

#### Basics
```bash
# to get the shell
echo $0

# Find the Linux distribution information
lsb_release -a

# IP address
ifconfig -a
ip addr show

# echo $PS1
# vi $HOME/.bashrc
export PS1="[\u@\h:\w]$ "

## To make Black and White
export PS1="[\u@\h:\w]$ "

# To list directory with no color
alias ls='ls --color=none'


# How To Give a User Sudo Privileges
sudo usermod -aG sudo username
# or
sudo gpasswd -a username sudo
sudo gpasswd -a username wheel

# To check the listening ports
# Run any one of the following command:
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
sudo nmap -sTU -O IP-address-Here
```


#### Update the system
```bash
sudo apt update
sudo apt upgrade
```
#### Opt out of data collection in Ubuntu 18.04
```bash

disable it by going to System Settings ->
Privacy
and then
set the Problem Reporting to Manual.
```


#### Disable automatic suspend for laptops
```bash
Go to System Settings -> Power. Under Suspend & Power Button section,
either turn off the Automatic Suspend option or extend its time period
```

#### Screen resolution
```bash
Go to System Settings -> Device -> Display -> Resolution.
```

#### Change Terminal Font
```bash
Right Click inside open terminal area
Profile -> Profile Preferences
# Good for fixed width fond:
DejaVu Sans Mono
```


#### Install media codecs
```bash
sudo apt install ubuntu-restricted-extras
```


#### System cleaning
```bash
sudo apt autoremove
```

#### Install Node.js from the Ubuntu repository
```bash
sudo apt update
sudo apt install nodejs
node -v

sudo apt install npm

# To install a specif version
curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
sudo apt install nodejs
node -v
npm -v
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

### or get tar and ...
# wget https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.xz
# tar -xvf node-v8.9.4-linux-x64.tar.xz
```

#### Git
```bash
sudo apt install git-all
git --version
```

#### Build
```bash
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libgdbm-dev libc6-dev libbz2-dev  libsqlite3-dev tk-dev libssl-dev
```

#### Get any python tar
```
cd /work
wget https://www.python.org/ftp/python/2.7.10/Python-2.7.10.tgz
tar -zxvf  Python-2.7.10.tgz
```

#### FTP
```BASH
sudo apt-get update
sudo apt-get install vsftpd

sudo vi /etc/vsftpd.conf
write_enable=YES
local_umask=022
allow_writeable_chroot=YES
chroot_local_user=NO

# Add the following line at the end.
pasv_enable=Yes
pasv_min_port=40000
pasv_max_port=40100

# Restart vsftpd service using the below command
sudo service vsftpd restart

sudo /etc/init.d/vsftpd restart
```

#### Enable IP
**edit /etc/network/interfaces**. If you want one to be obtained automatically,
 add **eth0** to the auto line in the file,
and add a new line for it that reads **iface eth0 inet dhcp**.
You can then reboot or run sudo **ifup -a** to bring up the interface and obtain the IP address
```bash
sudo vi /etc/network/interfaces
#Then add the following two lines that are not commented

# interfaces(5) file used by ifup(8) and ifdown(8)
# auto lo
# iface lo inet loopback
auto eth0
iface eth0 inet dhcp
```

The eth0 has been renamed with the latest ubuntun, you may want to check the new name with the following command.
```bash
dmesg | grep -i eth
```


#### Enable SSH
```bash
# Check if SSH is currently running:
ps -aux | grep ssh

## Install
sudo apt-get install openssh-server -y

## Configure SSH
sudo vi /etc/ssh/sshd_config

#Then, find 'Port' and uncomment if it is commented
Port 22
# If you want custom port then
# Port 1337
# if so you may have to ssh by specifying port
# ssh username@ip -p1337

# restart SSH for the changes to take effect
sudo service ssh restart

# The system is ready to SSH
ssh username@ip
ssh user1@192.168.219.137

```


#### Change HostName, say to lxblue
```bash
How to Change Hostname (Computer Name) in Ubuntu 15.04
You need to edit the computer name in two files:
sudo vi /etc/hostname
and
sudo vi /etc/hosts
```


#### Disable IPV6
```bash
# Then add the following in
# sudo vi /etc/sysctl.conf

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# Ten on the terminal type this
sudo sysctl -p

### After that, if you run:
cat /proc/sys/net/ipv6/conf/all/disable_ipv6
# It will report:
# 1
# If you see 1, ipv6 has been successfully disabled
```


#### Python
Before local build of Python do this setup

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install build-essential python-dev python-setuptools python-pip python-smbus
sudo apt-get install libncursesw5-dev libgdbm-dev libc6-dev
sudo apt-get install zlib1g-dev libsqlite3-dev tk-dev
sudo apt-get install libssl-dev openssl
sudo apt-get install libffi-dev
```

#### Python3 local build
```bash
cd /work/dev
rm ./Python
sudo rm -rf ./Python-3.7.1

# Download the Python3 source
wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tgz
tar zxvf Python-3.7.1.tgz
ln -s  ./Python-3.7.1  ./Python
cd /work/dev/Python
sudo ./configure --enable-unicode=ucs4

# Fire the build 
sudo make
sudo make install

## Then Upgrade the tools, for example
sudo pip3 install setuptools --upgrade
sudo pip3 install wheel --upgrade
sudo pip3 install twine --upgrade
pip3 install --upgrade pip
```


#### PIP

```bash
sudo apt update
sudo apt install python-pip

pip --version

# Don't update system pip by pip
pip install --upgrade pip
pip install --upgrade --user pip

## Uninstall
python -m pip uninstall pip --user
# or
sudo apt remove python-pip

```

### Install PIP3
sudo apt update
sudo apt install python3-pip
pip3 --version


### PIP basics
pip search KEYWORD
to search for packages. Once you obtain the package name use pip to install it:
$ pip install PACKAGE_NAME
Lastly, to remove package enter:
$ pip uninstall PACKAGE_NAME



### Python install
sudo apt-get install python
# to uninstall
sudo apt purge python
or
 sudo apt-get remove python2.7-5
 then
sudo apt autoremove




##### To list
```bash
python3 -V

# To list all versions of installed python
apt list --installed | grep python

```

##### To install  latest version of python
```bash
# for 2.x
sudo apt-get install python

# for 3.x
sudo apt-get install python3
```


##### install python from source
```bash
# my setup, you may use any dir
cd /work/dev

rm ./Python
sudo rm -rf ./Python-2.7.14
# sudo rm -rf ./Python-3.6.4

wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
# wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz

tar zxvf Python-2.7.14.tgz
# tar zxvf Python-3.6.4.tgz

ln -s  ./Python-2.7.14  ./Python
# ln -s  ./Python-3.6.4  ./Python

cd /work/dev/Python
sudo ./configure --enable-unicode=ucs4


# Assuming you have already setup 'zlib1g-dev' on the system.
# sudo apt install zlib1g-dev

#Fire the Python build
sudo make

# if the build is success, to install
sudo make install

```


### Issues faced
- [Please enter password for encrypted keyring" when running Python script on Ubuntu](https://lnx.azurewebsites.net/please-enter-password-for-encrypted-keyring-when-running-python-script-on-ubuntu/)
Message pop up saying "Please enter password for encrypted keyring:"
```bash
# one of the way to solve this problem is to
# add the following content to keyringrc.cfg
# vi ~/.local/share/python_keyring/keyringrc.cfg

[backend]
default-keyring=keyrings.alt.file.PlaintextKeyring
```

