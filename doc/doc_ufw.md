# [UFW](https://packages.debian.org/stretch/ufw)

Purpose
--
Uncomplicated Firewall. Easy way to setup iptables firewall to restrict access to your Raspberry Pi.

Configuration
--
*/etc/ufw/user.rules*

Example:
Allows all traffic within LAN (10.0.0.\*) except for router (10.0.0.138) and port 80. Allows ports 443 (HTTPS) and 1194 (VPN) from anywhere.
~~~
### RULES ###

### tuple ### allow any any 0.0.0.0/0 any 10.0.0.0/24 in
-A ufw-user-input -s 10.0.0.0/24 -j ACCEPT

### tuple ### deny any any 0.0.0.0/0 any 10.0.0.138 in
-A ufw-user-input -s 10.0.0.138 -j DROP

### tuple ### allow any 443 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 443 -j ACCEPT
-A ufw-user-input -p udp --dport 443 -j ACCEPT

### tuple ### allow any 1194 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 1194 -j ACCEPT
-A ufw-user-input -p udp --dport 1194 -j ACCEPT

### tuple ### deny tcp 80 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 80 -j DROP

### END RULES ###
~~~
