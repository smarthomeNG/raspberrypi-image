# [1-Wire](http://packages.debian.org/jessie/electronics/owserver)

Purpose
--
Server for 1-Wire System

Configuration
--
Config-File: /etc/owfs.conf
Change USB devices and ports accordingly.

Example:
~~~
server: server = 127.0.0.1:4304
server: usb = all
mountpoint = /mnt/1wire
allowother
http: port = 2121
ftp: port = 2120
server: port = 127.0.0.1:4304
~~~


Start and enable:
**systemctl enable owserver.service
systemctl enable owhttpd.service
systemctl restart owserver.service
systemctl restart owhttpd.service**

