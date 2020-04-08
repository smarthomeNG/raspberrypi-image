# [exim4](https://packages.debian.org/jessie/exim4)
Purpose
--
exim4 allows you to send mails from your Raspberry Pi. This is useful for monit and logcheck and the [mail plugin](http://smarthomeng.de/user/plugins/mail/README.html) of SmarthomeNG.

Configuration
--
It's recommended to use the setup script **/opt/setup/setup_exim4.sh**

Otherwise follow these steps:
1. General
Option 1:
It's most likely sufficient to exchange the line in */etc/exim4/update-exim4.conf.conf*:
*dc_smarthost='*. If you want to use Yahoo server insert this: *dc_smarthost='smtp.mail.yahoo.com::587'*
Option 2:
**dpkg-reconfigure exim4-config** See [gargi.org](http://www.gargi.org/showthread.php?4502-Raspberry-Pi-Wheezy-E-Mails-via-Exim4-verschicken) (in german) for additional information.

2. /etc/exim4/passwd.client
The login to your mail server (like yahoo, etc.)

3. /etc/email-addresses and /etc/aliases
insert your recipient mail address for root, logcheck, monit, etc. depending on what you want

Restart: **sudo systemctl restart exim4**
Clear Queue (i.e. when there were problems sending mails): **cleanexim**
Debugging: **tail -f /var/log/exim4/mainlog**
