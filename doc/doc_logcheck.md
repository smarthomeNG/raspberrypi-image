# [Logcheck](https://packages.debian.org/jessie/logcheck)

Purpose
--
Logcheck searches for problems in your logfiles and sends a summary to a specified mail address. You have to activate [exim4] for that.

Configuration
--
To enable logcheck uncomment all lines except first and last in the file */etc/cron.d/logcheck*. Adjust cron times to your likings, standard is once per hour.

Config-Files: 
/etc/logcheck/logcheck.logfiles
/etc/cron.d/logcheck  
/etc/logcheck/logcheck.conf

Options: 
logcheck.logfiles defines which logfiles to check
/etc/logcheck/logcheck.conf includes information about mail address, etc.

Example:
~~~
/var/log/messages
/var/log/auth.log
/var/log/cron.log
/var/log/dpkg.log
/var/log/syslog
/var/log/monit.log
/var/log/exim4/mainlog
/usr/local/smarthome/var/log/smarthome.log
~~~

Restart: Logcheck runs as cron job not as a service. If you want to trigger it manually run **sudo -u logcheck logcheck -t -d -m MAILADRESSE**

Configuration Logparser
--
In the /etc/logcheck/ignore.d.paranoid/ bzw. server you define log lines that are going to be ignored. 

Example:
~~~
^\[0-9\-\]{10}\[ :0-9\]{9}\[,0-9\]{0,4} INFO
^\[0-9\-\]{10}\[ :0-9\]{9}\[,0-9\]{0,4} WARNING\s(.\)problem reading cache
~~~

These exception would filter any warnings concerning the cache at SmarthomeNG start. Additionaly it ignores all INFO logfiles like:
*2016-08-27  23:34:46 INFO     nw           udpSend: LU.CO2Wert, 469.0*
