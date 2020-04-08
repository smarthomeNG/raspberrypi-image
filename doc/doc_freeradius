# [freeradius Server](https://packages.debian.org/stretch/freeradius)

Purpose
--
Use WPA2 enterprise security for your WiFi.

Configuration
--
Config-File: /etc/freeradius/3.0/mods-enabled/eap/freeradius_eap.conf

Options: Change the password for the certificate files! Everything else can be left as it is. You have to copy your certificate files into the folder /etc/freeradius/3.0/certs and name them as stated in the config file.

Config-File: /etc/freeradius/3.0/clients.conf

Options: Define your Access Points and routers by providing the IP address and your RADIUS password.

Example:
~~~
client NAME {
        ipaddr = IP
        proto = *
        secret = secret_password
        require_message_authenticator = no
        limit {
                max_connections = 16
                lifetime = 0
                idle_timeout = 30
        }
}
~~~

More information on the [official freeradius site](http://wiki.freeradius.org/config/Configuration-files).
Restart: **systemctl restart freeradius**
