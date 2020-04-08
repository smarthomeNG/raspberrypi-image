# [KNX Daemon](https://github.com/knxd/knxd)

Purpose
--
Communicate with KNX Bus (via KNX Gateway/Router)


Configuration
--

**Version 0.12:**
Config-File: /etc/knxd.conf

Example config:
~~~
START_KNXD=YES
KNXD_OPTS="-e 1.1.245 -E 1.1.246:8 --no-tunnel-client-queuing -B single -b ipt:10.0.0.101 -c -DTRS"
~~~

**Version 0.14:**
Config-File: /etc/knxd.ini
You can create the content of the ini file by running the following command. Change everything after knxd_args to your own settings:
**/usr/lib/knxd_args -e1.1.65 -E1.1.66:8 -i -u -b ipt:10.0.0.101 -c**
There are also two additional files */etc/knxd_IPServer.ini* and */etc/knxd_Serial.ini*. Try these two first if you have problems.

Example config:
~~~
#KNXD_OPTS="-e1.1.65 -E1.1.66:8 -i -u -b ipt:10.0.0.101 -c"
[B.ipt]
driver = ipt
filters = C.pace
ip-address = 10.0.0.101
[C.pace]
delay = 50
filter = pace
[main]
addr = 1.1.65
client-addrs=1.1.66:8
cache = D.cache
connections = B.ipt
systemd = systemd
background = true
~~~

Please read [Wiki](https://github.com/knxd/knxd/wiki) for more information.

Using IP GATEWAY:
Change IP address (ipt:10.0.0.101) and physical address (1.1.61) in example ini. 

Using SERIAL INTERFACE:
**sudo udevadm info -a /dev/ttyAMA0 | grep KERNELS.\*uart**
If you don't get any result try:
**sudo udevadm info -a /dev/ttyAMA0 | grep KERNELS.\*serial**
Note KERNELS entry

**sudo udevadm info -a /dev/ttyAMA0 | grep \{id\}**
Note ATTRS{id}

**sudo nano /etc/udev/rules.d/70-knxd.rules**
*ACTION=="add", SUBSYSTEM=="tty", ATTRS{id}=="00241011", KERNELS=="3f201000.uart", SYMLINK+="ttyKNX1", OWNER="knxd"*
Replace ATTRS and KERNELS with your own values!

Change the knxd.ini for knxd.conf ile according to your needs. The interface is /dev/ttyKNX1 from now on!
To restart udev: **udevadm control --reload-rules && udevadm trigger**
See if /dev/ttyKNX1 is available and linking to /dev/ttyAMA0. If not, reboot and/or retry the steps above or just change the entry "ttyKNX1" to "ttyAMA0" accordingly. Actually it doesn't matter too much.

Restart knxd:
**systemctl stop knxd.socket
systemctl stop knxd.service
systemctl start knxd.socket
systemctl start knxd.service
**

Hardware | Config | Additional config
---------- | ---------- | ----------
[RTC-Onewire-TPUART Erweiterung für Raspberry Pi](http://shop.busware.de/product_info.php/products_id/83) | KNXD_OPTS="-e 1.1.254 -E 1.1.255:8 -DTRS -t 0xffc -f 9 -b tpuarts:/dev/ttyKNX1" | config.txt: dtoverlay=pi3-disable-bt<br>**systemctl disable hciuart.service**

You might change the phyical addresses -e and -E to your liking.

Upgrade/Downgrade
--
Up until image version 2.2 knxd 0.14 was installed. However, some IP gateways have problems with that version. In images 2.2 and newer version 0.12 is installed by default.

If you feel the urge to upgrade or downgrade follow one of these steps:
a) Upgrade to version 0.14 or downgrade to 0.12 again:
Run **/opt/setup/setup_knxd.sh** and choose to upgrade. 
b) Upgrade to newest version on github:
**sudo -i
git clone https://github.com/knxd/knxd.git (define a specific branch by -b BRANCHNAME)
cd /root/knxd
dpkg-buildpackage -b -uc
cd ..
sudo dpkg -i knxd_\*.deb knxd-tools_\*.deb
**
Use the ini file from now on and change the knxd.conf file accordingly!
