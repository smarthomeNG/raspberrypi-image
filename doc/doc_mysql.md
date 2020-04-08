# [mysql](https://packages.debian.org/stretch/mysql-server)

Purpose
--
MySQL database plus easy configuration via phpmyadmin. A smarthome database is already created.

Configuration
--

Access phpmyadmin in your browser with **http://IP-ADDRESS/phpmyadmin**

*Login as root: (access to all databases)*
Username: root
Password: smarthome

*Login as smarthome: (access to smarthome database only)*
Username: smarthome
Password: smarthome

Config-file: /etc/mysql/debian.cnf
Change user, password, etc. if necessary.

Config-file SmarthomeNG:
plugin.yaml:

~~~
database_mysql:
    plugin_name: database
    driver: pymysql
    connect:
      - host:localhost
      - user:smarthome
      - passwd:smarthome
      - db:smarthome
      - port:3306
~~~

Standard folder for mysql databases is */var/lib/mysql*

To setup users and database for smarthome manually, edit the mysqlinit file and run:
**mysql -uroot -proot mysql < /root/mysqlinit**

Backups
--
The script */etc/cron.hourly/mysqlbackup* forces the system to create one full backup of your mysql database at midnight and incremental backups every hour. 

If you want to disable backup or change the standard behaviour, edit the corresponding file. For more options see [mysql xtrabackup]

Standard folder for backups is */var/backups/mysql*
