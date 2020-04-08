# [NFS Server](https://packages.debian.org/de/jessie/nfs-kernel-server)

Purpose
--
Access your files from a distant computer without needing credentials
Configuration
--
Config-File: /etc/exports

Options see [wiki.ubuntuusers.de](https://wiki.ubuntuusers.de/NFS/) 

Example:
~~~
/var/log 10.0.0.10/24(nosubtreecheck,rw,async,nowdelay,crossmnt,insecure,norootsquash,sec=sys,anonuid=1001,anongid=1001)
~~~

Restart: **sudo exportfs -ra**

Access
--
Raspberry Pi

1. **apt-get install nfs-client**
2. **makedir /mnt/smarthome**
3. **mount -t nfs IPADRESSE:/usr/smarthome /mnt/smarthome**

To mount automatically:
1. **nano /etc/fstab** *IPADRESS:/home   /home  nfs     defaults        0       0*
2. **apt-get install autofs**
3. Further steps see Mac OS X

OS X

1. **sudo -i**
2. **nano /etc/auto_master**
*/- autosmarthome -nobrowse,nosuid*
3. **nano /etc/auto_smarthome**
~~~
/../Volumes/SmartHome/Smarthome.py -fstype=nfs,noowners,nolockd,noresvport,hard,bg,int r,rw,tcp,nfc nfs://IPADRESS:/usr/smarthome
/../Volumes/SmartHome/Logs -fstype=nfs,noowners,nolockd,noresvport,hard,bg,int r,rw,tcp,nfc nfs://IPADRESS:/var/log
/../Volumes/SmartHome/www -fstype=nfs,noowners,nolockd,noresvport,hard,bg,int r,rw,tcp,nfc nfs://IPADRESS:/var/www
~~~
4. **sudo automount -vc**
5. Finder: Go/Go to Folder, type /Volumes. Drag and drop to the Favourites list on the upper left.

Windows

1. Turn Windows-Features on or off starten, activate Services for NFS
2. Windows Explorer address bar: *\\IPADRESSE*
3. For a permanent mounting (as drive H) run in a terminal window, **mount \\IPADRESSE\usr\smarthome H:**
