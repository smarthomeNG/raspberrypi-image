# [Samba](https://packages.debian.org/jessie/net/samba)
Purpose
--
Access your files from a different computer. Alternative to NFS and SFTP.

Configuration
--
Config-File: /etc/samba/smb.conf

Example:
~~~
[global]
    workgroup = WORKGROUP
    server string = SmartHome
    domain master = no
    syslog only = no
    syslog = 10
    panic action = /usr/share/samba/panic-action %d
    encrypt passwords = true
    passdb backend = tdbsam
    obey pam restrictions = yes
    unix password sync = yes
    unix extensions = no
    passwd program = /usr/bin/passwd %u
    passwd chat = *Enter\snew\s \*\spassword:* %n\n \*Retype\snew\s\*\spassword:\* %n\n \*password\supdated\ssuccessfully\* .
    pam password change = yes
    map to guest = bad user
    guest ok = no
    usershare allow guests = no
    load printers = no
    printing = bsd
    printcap name = /dev/null
    disable spoolss = yes
    bind interfaces only = yes
    log file = /var/log/samba-%m.log
    invalid users = root
[Logs]
    path = /var/log
    comment = Logfiles
    available = yes
    browseable = yes
    writable = yes
    force user = root
    force group = root
    create mask = 0755
    directory mask = 0775
[SmartHome.py]
    path = /usr/local/smarthome
    comment = SmartHome.py Directories
    available = yes
    browseable = yes
    writable = yes
    force user = smarthome
    force group = smarthome
    create mask = 0664
    directory mask = 0775
[www]
    path = /var/www/html
    comment = HTML Directories
    available = yes
    browseable = yes
    writable = yes
    force user = www-data
    force group = www-data
    create mask = 0775
    directory mask = 0775    *
[smartVISU]
    path = /var/www/html/smartVISU
    comment = smartVISU Directories
    available = yes
    browseable = yes
    writable = yes
    force user = www-data
    force group = www-data
    create mask = 0775
    directory mask = 0775    
~~~
    
Restart: **systemctl restart smbd**

Access
--
Mac OS X: Go / Connect to server *smb://IPADRESS* 
Windows: Type in address bar of Windows Explorer or Map Network drive *\\\IPADRESSE*

**use smarthome as user and password**

