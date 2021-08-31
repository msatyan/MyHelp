
### Doc
- [OpenSSH Key Management](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement)
- [http://www.servermom.org/passwordless-ssh-login/](http://www.servermom.org/passwordless-ssh-login/)


### Create RSA key.
Let us create an RSA key for us to communicate with the the Cloud VM.
```bash
cd ~/.ssh

# ssh user1@mysystem.mydomain.com
# ssh-keygen -t rsa -b 4096 -C "user@domain.com"
ssh-keygen -t rsa -b 4096
# Enter file in which to save the key (/home/pd/user1/.ssh/id_rsa): user1_system1_tag1

# ls user1_system1_tag1*
# user1_system1_tag1
# user1_system1_tag1.pub

### Copy the public key to the cloud VM
ssh-copy-id -i ~/.ssh/user1_system1_tag1.pub user1@mysystem.mydomain.com
# user1@mysystem.mydomain.com's password:
# Number of key(s) added: 1

# FYI: if you don't have ssh-copy-id on your system then
# cat ~/.ssh/id_rsa.pub | ssh remote_username@server_ip_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
# cat ~/.ssh/user1_system1_tag1.pub | ssh user1@mysystem.mydomain.com "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Now we can login to the system with
ssh -i ~/.ssh/user1_system1_tag1 user1@mysystem.mydomain.com
```


### Edit ~/.ssh/config
```bash
Host comet1
     HostName mysystem.mydomain.com
     User user1
     IdentityFile ~/.ssh/user1_system1_tag1
```

### Set Permissions
```bash
# these file must be writable only by you

# Local System
chmod 600  ~/.ssh/config
chmod 600  ~/.ssh/user1_system1_tag1
chmod 600  ~/.ssh/user1_system1_tag1.pub

# Remote System
chmod 755 ~
chmod 755 ~/.ssh
chmod 640 ~/.ssh/authorized_keys
```

### Login
```bash
# Now we can login to the system by using
# ssh -i ~/.ssh/user1_system1_tag1 user1@mysystem.mydomain.com
ssh comet1
```




### FYI: SSH Config File
If you are connecting to multiple remote systems over SSH, then SSH Config File cold be very helpful. OpenSSH allows us to set up per-user configuration file where we can store different SSH options for each remote machine we connect to. The snapshot of SSH Config File Structure and Patterns may look like this.
```bash
Host hostname1
    SSH_OPTION value
    SSH_OPTION value

Host hostname2
    SSH_OPTION value

Host *
    SSH_OPTION value
```

