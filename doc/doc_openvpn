# [OpenVPN](https://packages.debian.org/de/wheezy/openvpn)

Purpose
--
Access your SmarthomeNG Pi from outside your home network securely. This is the recommended way - don't configure your system that you can access via ssh or web browser from outside!

Configuration Server
--
Config-File: /etc/openvpn/server.conf
iptables Script: /usr/local/bin/iptables_openvpn.sh

Config-File: /etc/default/openvpn
Set general options like starting the server, etc.

Start and enable:
**systemctl enable openvpn@server.service
systemctl start openvpn@server.service**

Configuration Certificates
--
Config-File: /etc/ssl/easy-rsa/vars
Change information accordingly.

Certificates can be created interactively by running **/opt/setup/setup_openvpn.sh**

Otherwise feel free to do it manually using the following commands:
**cd /etc/ssl/easy-rsa/**
**sudo ./easyrsa init-pki**
**sudo ./easyrsa build-ca nopass**
**sudo ./easyrsa gen-crl**
**sudo ./easyrsa build-server-full server nopass**
**sudo ./easyrsa gen-dh**
**sudo ./easyrsa build-client-full $client $password** (replace client with the name of your remote device and password with your export pw)
**openvpn --genkey --secret /etc/openvpn/easy-rsa/keys/ta.key**
**openssl x509 -in clientname.crt -inform der -outform pem -out clientname.pem**
**openssl pkcs12 -export -out clientname.pfx -inkey clientname.key -in keys/certificate.crt -certfile keys/ca.crt**

Copy files ca.crt, clientname.\*, ta.key from server to client computer. For ios devices you might need Apple Configurator2.
Use the file */etc/openvpn/client.conf.template* as a starting point for the client configuration. 

Further information: https://wiki.debian.org/OpenVPN and https://openvpn.net/index.php/open-source/documentation/howto.html

Configuration Modem
--
Enable port forwarding for your openvpn port (standard 1194) to your Raspberry Pi. Disable firewall for that port.
