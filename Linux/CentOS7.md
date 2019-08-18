


### Basic
```bash
# Find CentOS version
rpm -q centos-release

# IP address
ifconfig -a
ip addr show
ip link show
```

### Update
```bash
yum -y update
yum -y upgrade

# if you get error: One of the configured repositories failed (Unknown)
# sudo dhclient

```


### Change Hostname
```bash

# How to Change Hostname (Computer Name) in Ubuntu 14.04
echo $HOSTNAME

# You need to edit the computer name in two files:
sudo vi /etc/hostname
and
sudo vi /etc/hosts


# Install and Configure sudo
# It will open the file /etc/sudoers for editing..
visudo

{
# User privilege specification
root	ALL=(ALL:ALL) ALL
-- -- -- -- --
-- -- -- -- --
# at the end add for the user, let us say lxblue
lxblue ALL=(ALL) NOPASSWD: ALL
}
```


### utilities
```bash
# wget
yum install wget

# Install 7-zip Utility
yum install p7zip

# Install Nmap to Monitor Open Ports
yum install nmap

# Install NTFS-3G Driver (to mount and access Windows NTFS file system)
yum install ntfs-3g

```


### Disable IPV6
```bash
# add the following in
sudo vi /etc/sysctl.conf

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

# on the terminal
sudo sysctl -p

# After that, if you run:
$ cat /proc/sys/net/ipv6/conf/all/disable_ipv6
# It will report:
1
# If you see 1, ipv6 has been successfully disabled
```


### FirewallD Configuration
```bash
# Firewalld removed iptables in CentOS 7
systemctl status firewalld
# OR
firewall-cmd --state


# Get a list of all the zones.
firewall-cmd --get-zones

# To get details on a zone before switching
# eg for work
firewall-cmd --zone=work --list-all

# To get default zone.
firewall-cmd --get-default-zone

# To switch to a different zone say ‘work‘.
firewall-cmd --set-default-zone=work


# To list all the services in the zone.
firewall-cmd --list-services

# To add a service say http, temporarily and reload firewalld
firewall-cmd  --add-service=http
firewall-cmd –reload

# To add a service say http, permanently and reload firewalld.
firewall-cmd --add-service=http --permanent
firewall-cmd --reload

# To remove a service say http, permanently.
firewall-cmd --zone=work --remove-service=http --permanent
firewall-cmd --reload

# To allow a port (say 331), temporarily.
firewall-cmd --add-port=331/tcp
firewall-cmd --reload

# To block/remove a port (say 331), permanently.
firewall-cmd --remove-port=331/tcp --permanent
firewall-cmd --reload

# To disable firewalld.
systemctl stop firewalld
systemctl disable firewalld
firewall-cmd --state

# To enable firewalld.
systemctl enable firewalld
systemctl start firewalld
firewall-cmd --state
```


### nmcli: Network Manager Command Line Interface
```bash
nmcli device
nmcli general
nmcli networking
nmcli connection
nmcli g permissions
nmcli d show
nmcli d
```

```bash
nmtui
```



### Setup Info

- [Install on Virtual Box](https://www.youtube.com/watch?v=A-VZwc-0Y1M)
- [Getting custom or maximum resolution from Virtualbox](https://www.youtube.com/watch?v=R7-poeD2rDA)
- [CentOS 7 Post Installation Settings](https://www.youtube.com/watch?v=ntg55uNCf8w)
- [30 Things to Do After Minimal RHEL/CentOS 7 Installation](https://www.tecmint.com/things-to-do-after-minimal-rhel-centos-7-installation/)
- [VirtualBox Networking (NAT & Port Forwarding, Bridged, Internal, Host-Only)](https://www.youtube.com/watch?v=cDF4X7RmV4Q)
- [Setting up Network on Red Hat / CentOS 7](https://www.youtube.com/watch?v=fXzGI_x-9UE)

### My VirtualBox networking setup list
The **enp0s3** is for **NAT** and **enp0s8** is for **Host only network** adapter, The **192.168.56.101** is the DHCP IP used in this
```bash
# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:03:fd:9a brd ff:ff:ff:ff:ff:ff
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:83:40:fc brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.101/24 brd 192.168.56.255 scope global noprefixroute dynamic enp0s8
       valid_lft 1144sec preferred_lft 1144sec
    inet6 fe80::c0de:df77:bb7e:fbb6/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
4: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 52:54:00:40:c1:b5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0
       valid_lft forever preferred_lft forever
5: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast master virbr0 state DOWN group default qlen 1000
    link/ether 52:54:00:40:c1:b5 brd ff:ff:ff:ff:ff:ff
```

