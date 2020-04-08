# [lirc](https://packages.debian.org/stretch/lirc)

Purpose
--
Use Infrared diodes to send and/or receive IR commands.

Configuration
--
Config-File: /etc/lirc/lirc_options.conf

Options: Usually you can leave this file as it is.

Config-File: /etc/lirc/lircd.conf.d/devinput.lircd.conf

Options: Here you have to define all your IR commands. Have a look at the official lirc Wiki for aupport.

Example:
~~~
begin remote
  name  Sony CD-Player
  flags RAW_CODES|CONST_LENGTH
  eps            30
  aeps          100
  gap          44917
      begin raw_codes
          name Play
             2410     575     597     575    1194     597
              597     597     618     575    1194     597
             1194     597     597     575    1194     597
              575     597     575     597     575     597
             1173
          name Pause
             2389     597    1194     597     575     597
              597     575    1194     597    1173     597
             1194     597     597     575    1194     597
              597     575     597     597     575     597
             1173
      end raw_codes
end remote
~~~


Restart **systemctl restart lircd**

If the service fails with *input line too long in /etc/lirc/lirc_options.conf* use **nano /etc/lirc/lirc_options.conf** and erase the empty line at the end of the file.
