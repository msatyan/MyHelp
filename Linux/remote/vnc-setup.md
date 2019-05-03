### VNC Host Searver Setup
We could configure a single VNC host server and start as many VNC sessions we want.
The we could redirect display from other UNIX host to these VNC sessions. 
In the given description my VNC host server is configured on mysystem.mydomain.com Linex system.
And then redirecting display from zelus (an AIX 64) to this VNC session. 


### Install VncServer
```bash
sudo yum groupinstall "GNOME Desktop"
sudo yum install tigervnc-server

https://www.tecmint.com/install-and-configure-vnc-server-in-centos-7/
```



### Very First Time launch (mysystem.mydomain.com)
```bash
vncserver :2 -geometry 1920x1200

# output
You will require a password to access your desktops.
Password:
Verify:
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/satyan/.Xauthority does not exist

New 'mysystem.mydomain.com:2 (satyan)' desktop is mysystem.mydomain.com:2

Creating default startup script /home/satyan/.vnc/xstartup
Creating default config /home/satyan/.vnc/config
Starting applications specified in /home/satyan/.vnc/xstartup
Log file is /home/satyan/.vnc/mysystem.mydomain.com:2.log

# copy paste problem can be solved with new 
# lxvm-comet: /home/pd/njgeib/software/tigervnc...
```



### Start VncServer
```bash
# My VNC Host server is installed on mysystem.mydomain.com
telnet mysystem.mydomain.com
vncserver :2

# To Kill VNC serve session use the option (-kill :display#)
vncserver -kill :2
or
kill `cat ~/.vnc/mysystem.mydomain.com:2.pid `
```


### Screen size
```bash
# Use -geometry option while starting the VNC session.
# 1900x1100 is a good fit for my monitor.

vncserver -geometry 1920x1200 
vncserver :2 -geometry 2000x1200     <<< Try using this on fyre-comet1
vncserver :2 -geometry 1920x1200

# New 'mysystem.mydomain.com:2 (satyan)' desktop is mysystem.mydomain.com:2
#
# Starting applications specified in /home/satyan/.vnc/xstartup
# Log file is /home/satyan/.vnc/mysystem.mydomain.com:2.log
```

# Vnc Session Password
```
vncpasswd
```

### Connecting to VncServer
```bash
# Optin VNC Viewer and give VNC session as shown bellow
mysystem.mydomain.com:2
```
