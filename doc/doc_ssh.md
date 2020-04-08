# [SSHD](https://packages.debian.org/jessie/ssh)
Purpose
--
Service to remotely connect to your Pi from a different computer.

Configuration
--
Config-File: /etc/ssh/sshd_config

For information on all the options see [debian.org](https://manpages.debian.org/jessie/openssh-server/sshd_config.5.en.html). 

As soon as you can successfully connect with certificates, change the following options:
*Port \[arbitrary number\]
PubkeyAuthentication yes
PermitEmptyPasswords no
PasswordAuthentication no 
*
Restart: **systemctl restart sshd**

Access
--
Access your Pi from any other computer using the terminal or one of these clients:
- [vssh](http://www.velestar.com/Pages/VSSHIOSPage.aspx) (ios and Mac OSX) 
- [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
- [mobaxterm](http://mobaxterm.mobatek.net/) (recommended for Windows)

Login: smarthome
Password: *none*

At first boot new ssh keys are generated. Make sure this happened in */var/log/firstboot.log*
You can create new keys by running **/opt/setup/setup_ssh.sh**
Copy the file /home/smarthome/smarthomeng.private to your client, define it as your private key and login as root or smarthome user without password. Connect via **ssh -i   ~/.ssh/servername.private -p port loginname@ipaddress**

Certificates
--
If you want to generate your own new certificate files manually (why would you?) follow these steps:
**sudo ssh-keygen -t rsa -N "" -f /etc/ssh/ssh_host_rsa_key**
**sudo ln -s /etc/ssh/ssh_host_rsa_key.pub /root/.ssh/authorized_keys**


For more information read: [linux.die.net](http://linux.die.net/man/1/ssh-keygen)
