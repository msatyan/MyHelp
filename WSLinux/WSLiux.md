- [Windows 10 Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- [Blog-Windows 10 Installation Guide](https://blogs.msdn.microsoft.com/commandline/2017/10/11/whats-new-in-wsl-in-windows-10-fall-creators-update/)

- [OLD Windows 10 Installation Guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)

- [Frequently Asked Questions](https://msdn.microsoft.com/en-us/commandline/wsl/faq)

- [Fun with the Windows Subsystem for Linux](https://blogs.windows.com/buildingapps/2016/07/22/fun-with-the-windows-subsystem-for-linux/)

- [Python with Ubuntu on Windows](http://timmyreilly.azurewebsites.net/python-with-ubuntu-on-windows/)

- [Blogs](https://blogs.msdn.microsoft.com/wsl/)


### Resetting your WSL Environment
Open a command prompt from Winsows and run lxrun.exe:
```bash
C:> lxrun.exe /uninstall /full
C:> lxrun.exe /install

# See also :
ubuntu clean
```

### What is DrvFs
DrvFs is a filesystem plugin to WSL that was designed to support interop between WSL and the Windows filesystem. DrvFs enables WSL to mount drives with supported file systems under /mnt, such as /mnt/c, /mnt/d, etc. 


### Mount Removable Drives and Network Locations
```bash
# it is now possible to mount USB media (including formatted as FAT) and network shares with drvfs on Windows 10

# Mount removable media: (e.g. D:)
sudo mkdir /mnt/d
sudo mount -t drvfs D: /mnt/d
# To safely unmount
sudo umount /mnt/d

# You can also mount network shares without smbfs:
sudo mount -t drvfs '\\server\share' /mnt/share
```

### Mounting DrvFs
In order to mount a Windows drive using DrvFs, you can use the regular Linux mount command. For example, to mount a removable drive D: as /mnt/d directory, run the following commands:
```bash
sudo mkdir /mnt/d
sudo mount -t drvfs D: /mnt/d

# Now, you will be able to access the files of your D: drive under /mnt/d. When you wish to unmount the drive, for example so you can safely remove it, run the following command:
sudo umount /mnt/d
```

### Mounting network locations
When you wish to mount a network location, you can of course create a mapped network drive in Windows and mount that as indicated above. However, it's also possible to mount them directly using a UNC path:
```bash
sudo mount -t drvfs '\\server\share' /mnt/share
# FYI: WSL does not have any way to specify which credentials to use to connect to a network share. If you need to use different credentials to connect to the server, specify them in Windows by navigating to the share in File Explorer, using the Windows Credential Manager
```


### Run Linux Commands From Outside the Linux Shell
```bash
# eg: 
bash -c "vi"
```

### Run Windows Programs From Bash
```bash
# eg:
/mnt/c/Windows/system32/notepad.exe
```


### Basic Setup
```
bash
sudo apt-get update

lsb_release -a

sudo apt-get update
sudo apt-get upgrade

# Python
sudo apt-get install python
(Python 2.7 or Python 3.5)
sudo apt-get install python3

# Install Pip
sudo apt-get install python-pip
```

### Python Version
```
Check the python version and make it point to the version you prefer
python -V

ls -l /usr/bin/* | grep -i python
python -> python2.7
/usr/bin/python2 -> python2.7
/usr/bin/python3 -> python3.5

So you know ...
sudo rm    /usr/bin/python
sudo ln -s /usr/bin/python2.7 /usr/bin/python
sudo ln -s /usr/bin/python3.5 /usr/bin/python
```

### Extras
```
sudo apt-get install build-essential git libssl-dev
sudo apt-get install execstack
```

### Install Azure CLI 2.0 with one curl command.
```
curl -L https://aka.ms/InstallAzureCli | bash

FYI:
Install location: /work/azcli
az cli : /home/satyan/bin/az

### Uninstall
rm -r /work/azcli/lib/azure-cli
rm /work/azcli/bin/az

Delete the line /work/azcli/lib/azure-cli/az.completion 
from /work/azcli/.bash_profile

```

