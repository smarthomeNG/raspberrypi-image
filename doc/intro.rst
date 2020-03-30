SmarthomeNG Raspberry Pi Image
==============================

General
-------

**Base:** Raspbian lite Image. Version is depending on image version.
See changelog below.

German UTF-8 locale is activated by default. On English keyboards y is
z.

**Python:** Python 2.7 and Python 3.x (depending on image version)

**Compatibility** Hopefully all versions of Raspberry Pi from 1 to 4. When
using a monitor you might need to uncomment the line hdmi\_drive=2 in
/boot/config.txt

**Login** Standard user: smarthome Password: *none*

You can also login as user root with password root, although this is not
recommended.

**Security** Avoid direct access to your Pi from outside under any
curcumstances! Use the openVPN package that is already included in the
image to secure your connection. You can also setup a reverse proxy to
access VISU and more from outside securely on port 443.

By default root login for ssh and sftp is enabled for convenience
reasons. Consider disabling it for increased security. It's also
recommended to create SSH certificates to enable direct passwordless
access as smarthome or root user while providing the best possible
security layer. Certificates should be created automatically on first
boot, but you need to configure ssh manually.

**Liability Disclaimer** The providers of the software packages as well
as of this image file can not be hold responsible for any damage.

Python 3 Packages
-------------------

All dependencies for SmarthomeNG including plugins are installed plus
some additional packages like pymysql, awake, etc. List all installed
packages with **sudo pip3 list**

Install additional packages: **sudo pip3 install PACKAGENAME**

Smarthome NG
------------

Stable master version can be found in /usr/local/smarthome.

**Smarthome Backend** is accessible in your browser with
IP-ADRESS/backend Use *admin* and *xxxx* as login if asked. You can
change those credentials in the plugin.yaml file.

How to update (on Images >= 2.2): **system\_update**

SmartVISU
---------

Smartvisu 2.8 is installed in /var/www/html/smartVISU
Smartvisu 2.9 is installed in /var/www/html/smartVISU2.9
Configure it in the browser via IP-ADDRESS/smartVISU(2.9).

How to update (on Images >= 2.2): **system\_update**

Installation and configuration
------------------------------

1. "Burn" the image on a SD card using win32DiskImager, PiFiller,
   Etcher, etc. on a SD card with minimum 4GB. The larger the better.
2. It's recommended to run your system on a USB stick. Burn this image
   or copy your SD card on a stick. The procedure depends on your
   Raspberry Pi version:

-  Raspi <=2: On your SD card that still needs to be put in your Pi
   replace in *boot/cmdline.txt* the *root=..* entry with
   *root=/dev/sda2* If you have other USB sticks connected you need to
   use the PARTUUID.
-  Raspi 3: echo program\_usb\_boot\_mode=1 \| sudo tee -a
   /boot/config.txt && reboot
-  Raspi >=3+: just plug in your USB stick.

3. Run **setup\_all** to enable/disable/install or configure system preferences and services.
   BE AWARE: On English keyboards german y is z.
4. Update SmarthomeNG configuration with your own: *etc/plugin.yaml
   etc/logic.yaml etc/logging.yaml etc/smarthome.yaml logics/\*
   items/\** In the items directory you might create one file for each
   room or technology, etc. Also see `official smarthomeNG
   Site <http://smarthomeng.de/user/konfiguration/initiale_itemkonfiguration.html>`__
   You can transfer files to your Raspberry Pi using one of these
   methods:

a) SFTP, Port 22. Login: smarthome, Password: none. Using WinSCP,
   FileZilla, etc.
b) NFS: Enable the service on your Pi with **sudo systemctl enable
   nfs-server && sudo systemctl start nfs-server** To access your
   directories from a remote PC, see [NFS]
c) Samba: Connect to your Pi like you would connect to any other network
   drive. Username and password are smarthome
d) SSH: Connect to your Raspberry Pi with **ssh
   smarthome@SmarthomeNG.local** and use nano to edit files manually.
e) Copy via USB stick. **mkdir /mnt/usb && mount /dev/sda1 /mnt/usb**

6. Change the file */etc/knxd.ini* or */etc/knxd.conf* depending on your
   setup and knxd version. See also: `official knxd Wiki <https://github.com/knxd/knxd/wiki>`__
7. reboot

Debugging
---------

a) Type **sh.log** or **sh.error** in your command line to see the most
   recent SmarthomeNG log in realtime. The full log can be found in the
   directory */usr/local/smarthome/var/log*. You can change log levels
   based on plugins, etc. in the file
   */usr/local/smarthome/etc/logging.yaml*
b) To debug other services see their respective log file in /var/log or
   the global log /var/log/syslog. You can also use services like
   logcheck, monit, monitgraph, etc. to monitor your system. Just enable
   them. **systemctl status SERVICENAME** is also a good idea, as well
   as **journalctl -xe**
c) To debug knxd you can use **knxtool groupswrite ip:localhost 0/0/1
   0** Change the group address 0/0/1 respectively suiting your setup.

Services
--------

The following services are installed and running. You might want to update their
configuration files based on your preferences.

+---------------------------+-----------------------------------+-------------------------------------------------------------+
| Service                   | Description                       | Config File(s)                                              |
+===========================+===================================+=============================================================+
| timesyncd                 | Automatic time synchronisation    |                                                             |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [knxd]                    | KNX Bus Connection                | /etc/knxd.ini or /etc/knxd.conf                             |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [ssh]                     | Console access via Port 22        | /etc/ssh/sshd\_config                                       |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [rsyslog]                 | System Logging                    | /etc/rsyslog.conf                                           |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [Samba]                   | Access your files from anywhere   | /etc/samba/smb.conf                                         |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [apache2] (Image < 2.2)   | Webserver                         | /etc/apache2/apache2.conf                                   |
+---------------------------+-----------------------------------+-------------------------------------------------------------+
| [nginx] (Image >= 2.2)    | Webserver                         | /etc/nginx/nginx.conf, /etc/nginx/sites-available/default   |
+---------------------------+-----------------------------------+-------------------------------------------------------------+

The following services are installed but have to be activated and
started with **sudo systemctl enable SERVICE && sudo systemctl start
SERVICE** or via the **setup\_all** script

+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| Service              | Description                                                                                        | Config File(s)                                                                                   |
+======================+====================================================================================================+==================================================================================================+
| [NFS]                | Access your files from anywhere without login                                                      | /etc/exports                                                                                     |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [lircd]              | Use infrared capabilities                                                                          | /etc/lirc/lirc\_options.conf                                                                     |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [susvd]              | If you use an emergency battery system from `S.USV <http://www.s-usv.de/susv_pibasic_en.html>`__   | /opt/susvd                                                                                       |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [monit]              | Monitoring Service to restart failed services, etc.                                                | /etc/monit/monitrc                                                                               |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [logcheck]           | Monitoring Service that analyzes log files every hour                                              | /etc/logcheck/logcheck.logfiles                                                                  |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [exim4]              | Mail Server                                                                                        | dpkg-reconfigure exim4-config; /etc/email-addresses, /etc/aliases and /etc/exim4/passwd.client   |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [squeezelite]        | Headless Player for Logitech Squeezebox                                                            | /usr/local/bin/squeezelite.sh                                                                    |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [watchdog]           | Auto restart system on overload                                                                    | /etc/watchdog.conf                                                                               |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [freeradius]         | Network authentication service                                                                     | /etc/freeradius                                                                                  |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [openvpn]            | Connect to your Pi from outside securely                                                           | /etc/openvpn/server.conf, etc.                                                                   |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [1Wire]              | OneWire Server                                                                                     | /etc/owfs.conf                                                                                   |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [mysql]              | MySQL plus phpmyadmin                                                                              | mysql client, /etc/mysql/debian.cnf                                                              |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [mysql xtrabackup]   | MySQL Backup Tool from Percona                                                                     | /etc/cron.d/mysql\_backup                                                                        |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [mosquitto]          | MQTT Broker Service                                                                                | /etc/mosquitto/mosquitto.conf                                                                    |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
| [ufw]                | Uncomplicated Firewall                                                                             | /etc/ufw/user.rules                                                                              |
+----------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+

Starting with the moving of the Raspberry Pi image from sourceforge to the official
SmarthomeNG repository, the version numbering changed.

It now reflects the Raspbian and shng version much better. The first part of the
version number reflects the Debian version (e.g. 9: stretch, 10: buster). The
following 2-3 numbers show the SmarthomeNG master version (e.g. 1.5.1, 1.6).

Examples:

- 9.1.6: Debian Stretch, shng version 1.6
- 10.1.6: Debian Buster, shng version 1.6
- 10.1.6.1: Debian Buster, shng version 1.6.1


Changelog 10.1.6
----------------
New:
possibility to install node-red via setup_nodered.sh

Updated:
`Raspbian "Buster
   lite" <https://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2019-09-30/2019-09-26-raspbian-buster-lite.zip>`__

Changelog 9.1.6
---------------

New:

-  installed fail2ban to ban eval IP addresses trying to connect to the
   web server
-  Installed unattanded upgrades (inactive by default)
-  Additional package for eibd. Optional use of eibd instead of knxd
-  Installed additional packages: atop, snmp, python knx
-  Fixed logrotate for watchdog, openvpn and influxdb
-  Possibility to backup and restore the system configuration via
   setup\_all and setup\_backup.sh / setup\_restore.sh

Updated:

-  Updated system and python modules
-  Updated several packages and executables
-  Installed SmarthomeNG 1.6 (core and plugins)
-  Updated smartVISU 2.9
-  Disabled Swap file by default
-  Updated setup\_all to change hostname and swapfile size.
-  `Raspbian "stretch
   lite" <https://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2019-04-09/2019-04-08-raspbian-stretch-lite.zip>`__
   from April 2019

Changed/Fixed:

-  small tweaks
