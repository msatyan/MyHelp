


### Network setup
Please refer the actual documentation for full set of information, here is a snapshot for the most commonly used scenario. If the VM need to access internet and the Host system need to access the VM with IP then likely you may need NAT and Host-only networking. You may also explore port forwarding if you are dealing with only selected port(s). In this scenario I am using Windows 10 Host and Ubuntu18 Guest VM.

[Youtube: NAT & Port Forwarding, Bridged, Internal, Host-Only](https://www.youtube.com/watch?v=cDF4X7RmV4Q)


### network map
```bash
+-----------+-------------+-------------+----------------+----------------+
|           | VM <-> Host | VM1 <-> VM2 | VM -> Internet | VM <- Internet |
+-----------+-------------+-------------+----------------+----------------+
| HostOnly  |     Yes     |     Yes     |      No        |       No       |
| Internal  |     No      |     Yes     |      No        |       No       |
| Bridged   |     Yes     |     Yes     |      Yes       |       Yes      |
| NAT       |     No      |     No      |      Yes       |  Port forward  |
| NATNet    |     No      |     Yes     |      Yes       |       No       |
+-----------+-------------+-------------+----------------+----------------+
```


```bash
route -n
ifconfig -a
cat /etc/network/interfaces
```

##### Network Address Translation (NAT) :
If guest os need to access internet.

##### Host-only networking :
Create a network containing the host and a set of guest virtual machines.

##### Internal networking
This can be used to create a different kind of software-based network which is visible to selected virtual machines

##### See also:
- Bridged networking
- NAT Network
- Generic networking


### Enable Host-only networking
- By using Virtualbox Create a Host-only networking adapter on your host (if it is not already exist then only).
- On your VM setup select the Host-only networking also.
##### Create a Host-only networking
- [pdf: Host-only network setting image](./VirtualBox-HostOnlyNetwork-img.pdf)
```bash
# 1) From the host File Menu of the host select
- Host Network Manager
- Click on the Create button (this will create an network adapter on your computer)
  Please note the IP address assigned, this will be the gateway address for your VM

# 2) Select the VM you would like to enable Host-Only Network
- Then click on the Setting
- Select the Network tab
- Select Adapter2
- Checkmark "Enable Network adaptor"
- From the Attach to sist box select Host-Only Adaptor
- From the Name list box, select the network adaptor that you have created in the Option#1.

FYI: if you would like to set static IP for the VM see the "Set the static IP" setting given bellow
```


### Setting static IP on the VM with Host-only networking
- https://www.tecmint.com/network-between-guest-vm-and-host-virtualbox/  
- https://www.youtube.com/watch?v=9vtSvPnCBwo  
- https://www.youtube.com/watch?v=YkbShiPaE_0  
- https://codewithintent.com/how-to-configure-static-ip-address-on-ubuntu-16-04-lts-using-virtualbox/
Let us say (on your host) Host-only network adaptor has the following property
```bash
IP of the adapter 192.168.56.1
Subnet mask :  255.255.255.0
```

On your guest system you may update the IP information (/etc/network/interfaces).


```bash
ip add

# The output may look like this
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:8c:25 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86368sec preferred_lft 86368sec
    inet6 fe80::6178:99d8:74f7:7061/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8f:55:5b brd ff:ff:ff:ff:ff:ff
    inet6 fe80::895c:291c:be4d:2bd6/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

- lo – loopback interface

- enp0s3 (Adapter 1) – In this enp0s3 is being used for NAT (only good for Internet access. By default DHCP (IP now is 10.0.2.15)).

- enp0s8 (Adapter 2) – is for host-only communication we will set a static IP on this adapter.



```bash
# FYI only
 dmesg | grep -i eth

# output may:
[    1.738984] e1000 0000:00:03.0 eth0: (PCI:33MHz:32-bit) 08:00:27:e9:8c:25
[    1.738990] e1000 0000:00:03.0 eth0: Intel(R) PRO/1000 Network Connection
[    2.133489] e1000 0000:00:08.0 eth1: (PCI:33MHz:32-bit) 08:00:27:8f:55:5b
[    2.133491] e1000 0000:00:08.0 eth1: Intel(R) PRO/1000 Network Connection
[    2.134466] e1000 0000:00:08.0 enp0s8: renamed from eth1
[    2.148946] e1000 0000:00:03.0 enp0s3: renamed from eth0
```



##### Configure NAT and Host Only Network
- [How To Configure Static IP address on Ubuntu 16.04 LTS using VirtualBox](https://www.youtube.com/watch?v=YkbShiPaE_0)
- NAT  (DHCP)
- Host Only Network (static)

Add the following in  
sudo vi /etc/network/interfaces

```bash
auto lo
iface lo inet loopback

# nat
auto enp0s3
iface enp0s3 inet dhcp

# Host Only Static
auto  enp0s8
iface enp0s8 inet static
address  192.168.56.5
network  192.168.56.0

#netmask  255.255.255.0
#gateway  192.168.56.1
#dns-nameservers  8.8.8.8  192.168.56.1
```
Then Restart system or networking
```bash
# Try restarting network, if not then restart the guest OS
sudo systemctl restart networking
```


### Test the IP on the gust VM
```bash
ip add
# output
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:8c:25 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85786sec preferred_lft 85786sec
    inet6 fe80::6178:99d8:74f7:7061/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8f:55:5b brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.5/24 brd 192.168.56.255 scope global enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::895c:291c:be4d:2bd6/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

The IP address 192.168.56.5 has been assigned and it should be accessible from the Host OS. If you get problem while accessing the VM from host OS then reboot the VM once and check your firewall settings.


---

### Copy Past problem.
- https://websiteforstudents.com/installing-virtualbox-guest-additions-on-ubuntu-18-04-beta/
- Enable Bidirectional for Clipboad and Drag'n Drop
- Install VirtualBox Guest Additions
```bash
# navigation info
General -> Advance
Shared Clipboad : Bidirectional
Drag'n Drop : Bidirectional
```

```bash
# Install VirtualBox Guest Additions
Start the Ubuntu
From the VirtualBox menu (on the top) select Devices
Insert Guest Addition CD image
Run
```



### cat  /etc/network/interfaces
- https://www.youtube.com/watch?v=YkbShiPaE_0  
It is from my home computer 
```bash
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback

# nat
auto enp0s3
iface enp0s3 inet dhcp


# Host Only Static
auto  enp0s8
iface enp0s8 inet static
address  192.168.56.5
network  192.168.56.0

# netmask  255.255.255.0
# gateway  192.168.56.1
#dns-nameservers  8.8.8.8  192.168.56.1
```


