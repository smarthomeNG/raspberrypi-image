# [Watchdog](https://packages.debian.org/jessie/admin/watchdog)

Purpose
--
Restart system automatically on overload.

Configuration
--
Config-File: /etc/watchdog.conf

Options: For details see [dundee.ac.uk](http://www.sat.dundee.ac.uk/psc/watchdog/watchdog-configure.html). For a standard setup the predefined example might be enough.

Example: 
~~~
watchdog-device = /dev/watchdog
max-load-1 = 35
max-load-5 = 20
file = /var/log/syslog
min-memory = 1
watchdog-timeout = 10
interval = 4
pidfile = /run/rsyslogd.pid
~~~

Config-File: /etc/default/watchdog

Options: Activate watchdog, keepalive and hardware watchdog or other modules.

Example:
~~~
runwatchdog=1
runwdkeepalive=0
watchdogmodule="bcm2835_wdt"
~~~

Restart:**systemctl restart watchdog**

Problem handling
--
If your computer constantly reboots, execute this command if deactivating the watchdog otherwise fails:
**mv /etc/watchdog.conf /etc/watchdog.bak**

Anschließend kann das Config-File angepasst und wieder umbenannt werden. Watchdog mittels **systemctl restart watchdog** neu starten.

If your Raspi reboots on poweroff you might want to change the line in */etc/modprobe.d/bcm2835wdt.conf* to: 
*options bcm2835wdt nowayout=0*
