### Linux basics

#### Find the Linux distribution information
```
lsb_release -a
```

#### IP address
```
ifconfig -a
```

#### Root access
```bash
1) Log In As Root
$ ssh root@1.2.3.4

2) Use "su" to become 'root' or impersonation
$ su 
$ su user1

3) Use "sudo" to execute commands as 'root'
$ sudo ls -l
```
#### How To Give a User Sudo Privileges
```bash
sudo usermod -aG sudo username
# or
sudo gpasswd -a username sudo
sudo gpasswd -a username wheel

```
#### **sudo** command without entering password
```bash
# /etc/sudoers

# to edit the default editor used by visudo
$ sudo update-alternatives --config editor

# launch the sudoers
$ sudo visudo

# user1 to run all commands using sudo without a password.
user1 ALL=(ALL) NOPASSWD: ALL

# or specifi specific commands with no password 
user1 ALL=(ALL) NOPASSWD: /bin/kill, /bin/rm
```

#### apt-get
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install <package>
```

#### Change Hostname
```bash
# edit the computer name in two files:
sudo vi /etc/hostname 
# and
sudo vi /etc/hosts
```

#### Disable IPV6
```bash
# Then add the following in 
sudo vi /etc/sysctl.conf

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# on the terminal
sudo sysctl -p

# FYI:
# After that, if you run:
# $ cat /proc/sys/net/ipv6/conf/all/disable_ipv6
# It will report:
# 1
# If you see 1, ipv6 has been successfully disabled
```

#### To check the listening ports
```bash
# Run any one of the following command:
sudo lsof -i -P -n | grep LISTEN 
sudo netstat -tulpn | grep LISTEN
sudo nmap -sTU -O IP-address-Here
```

#### Add key to authentication agent
To avoid user manually typing passphrase, you may use authentication agent (ssh-add it asks for the passphrase from the user once). 
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```


#### Setup up public key authentication
```bash
# 1) Generate a SSH key 
cd ~/.ssh
ssh-keygen
# or specify parmas, say
ssh-keygen -t rsa -b 2048

# 2) Copy the Key to server (192.168.65.129)
ssh-copy-id -i ~/.ssh/id_rsa.pub blue@192.168.65.129

#3) Login to the server (no password wil be asked)
ssh blue@192.168.65.129

ssh -i ~/.ssh/id_rsa.pub blue@192.168.65.129
```


#### Copying your Public Key Using SSH
```bash
cat id_rsa.pub | ssh blue@192.168.65.129 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

#### Copying your Public Key Manually
```bash
# Copy id_rsa.pub to the server, then on the server 
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

#### Installation/FromUSBStick
- [Ubuntu Installation/FromUSBStick](https://help.ubuntu.com/community/Installation/FromUSBStick)
