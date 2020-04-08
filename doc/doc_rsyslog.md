# [rsyslog](https://packages.debian.org/de/jessie/rsyslog)

Purpose
--
Logging of system events and messages

Configuration
--
Config-File: /etc/rsyslog.conf, /etc/rsyslog.d/*

Here you can change where specific messages should be saved.

Example:
~~~
*.*;mail.none;cron.none;auth,authpriv.none -/var/log/syslog
cron.* -/var/log/cron.log
mail.* -/var/log/mail.log
*.err;auth.notice -/dev/console
auth,authpriv.* -/var/log/auth.log
*.crit;*.err -/var/log/system_problems.log
~~~

Furthermore you can create own filters in the folder /etc/rsyslog.d/. There are already some files there like for mosquitto.

Restart: **systemctl restart rsyslogd**
