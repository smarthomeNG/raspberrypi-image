# [monit](https://packages.debian.org/jessie/monit)

Purpose
--
Monitor services, system processes, etc. and restart processes in case they exited. Additionally alerting the user via mail.

Configuration
--
Config-File: /etc/monit/monitrc

Options: [monit](https://mmonit.com/wiki/Monit/ConfigurationExamples) 

There are already some services pre-configured. This example shows how to monito smarthome based on pid file.

Example:
~~~
check process smarthome with pidfile /usr/smarthome/var/run/smarthome.pid
 start program "/bin/systemctl start smarthome"
 stop program "/bin/systemctl start smarthome"
 restart program "/bin/systemctl restart smarthome"
 if 20 restarts within 45 cycles then unmonitor
~~~

Restart **systemctl restart monit**
