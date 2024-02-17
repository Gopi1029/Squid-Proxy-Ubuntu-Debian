# Squid Proxy Installer

Auto install Squid 3 proxy on following linux OS.

* Ubuntu 14.04, 16.04, 18.04, 20.04, 22.04
* Debian 8, 9, 10, 11, 12
* CentOS 7, 8
* CentOS Steam 8, 9
* AlmaLinux 8, 9


## Install Squid

To install, run the script

```
wget https://raw.githubusercontent.com/Gopi1029/squid-proxy-installer/main/squid3-install.sh -O squid3-install.sh
sudo bash squid3-install.sh
```

# Create Proxy Users

To create users, run

```
squid-add-user
```

OR run following commands

```
sudo /usr/bin/htpasswd -b -c /etc/squid/passwd USERNAME_HERE PASSWORD_HERE
```

To update password for am existing user, run

```
sudo /usr/bin/htpasswd /etc/squid/passwd USERNAME_HERE
```

replace USERNAME_HERE and PASSWORD_HERE with your desired user name and password.

Reload squid proxy

```
sudo systemctl reload squid
```

# Configure Multiple IP Address

NOTE: This is only needed if you have more than one IP on your server.

Before you can configure squid to use muliple IP address, you need to add IP to your server and you should be able to connect to server using these IPs.

Once IP added to your server, you can configure it to use with squid proxy by running following command

```
wget https://raw.githubusercontent.com/Gopi1029/squid-proxy-installer/main/squid-conf-ip.sh
sudo bash squid-conf-ip.sh
```

# Change Squid Proxy Port

Default squid proxy port is 3128.


Squid proxy server runs on port 3128 by default. Changing squid proxy server port to a non-standard port is a good idea as it will protect your proxy server from abusers and hackers.

# Method 1

You can use the sed command to replace the port number


sudo sed -i 's/^http_port.*$/http_port NEW_PORT_HERE/g'  /etc/squid/squid.conf
In the above command, replace NEW_PORT_HERE with the port number you need.

For example, to run squid proxy on port 5555, run


sudo sed -i 's/^http_port.*$/http_port 5555/g'  /etc/squid/squid.conf
Now restart Squid Proxy server


sudo systemctl restart squid
If you have a firewall, you will need to open the port in the firewall.



# Method 2: Manual Configuration Change

Edit Squid configuration file with vi or nano editor.


sudo vi /etc/squid/squid.conf
In the file, find http_port, it should look like


http_port 3128
Change 3128 to whatever port number you like. Save and exit the editor.

Restart Squid Proxy server with the command


sudo systemctl restart squid
Open Port in firewall

# If you have a firewall, you need to open the port in the firewall.

CentOS/AlmaLinux/RHEL

If you are using firewalld, you can use the command


sudo firewall-cmd --permanent --zone=public --add-port=8000/tcp
sudo firewall-cmd --reload
Replace 8000 with your squid prox port.

Back to Squid Proxy Installer.
