# [nginx](https://packages.debian.org/stretch/nginx)
Purpose
--
nginx is like Apache2 in Image version <2.2 or lighttpd in Image version <1.5, a webserver. It's used to access smartVISU and other web pages like monitgraph, etc. PHP is also installed. For more info on PHP open IP-ADDRESS/phpinfo.php in your browser or see changelog on main page.

Configuration
--
Config-File: /etc/nginx/nginx.conf, /etc/nginx/sites-available/default

Options: Define servername, modules, locations, etc.

Access
--
It is recommended to use the reverse proxy function to access your webservices from outside securely (or VPN). Use **/opt/setup/setup_nginx.sh** to automatically configure all neccessary steps like creating a SSL certificate for your server and client certificates to secure your connection.

Most of the steps are based on this blog entry: [nginx als reverse proxy](https://www.smarthomeng.de/nginx-als-reverseproxy)
