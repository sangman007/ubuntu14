#!/bin/bash

# go to root
cd

# Install Pritunl
#!/bin/bash
echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" > /etc/apt/sources.list.d/mongodb-org-3.2.list
echo "deb http://repo.pritunl.com/stable/apt trusty main" > /etc/apt/sources.list.d/pritunl.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 42F3E95A2C4F08279C4960ADD68FA50FEA312927
apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 7568D9BB55FF9E5287D586017AE645C0CF8E292A
apt-get --assume-yes update
apt-get --assume-yes install pritunl mongodb-org
service pritunl start

# Install Client
echo "deb http://repo.pritunl.com/stable/apt trusty main" > /etc/apt/sources.list.d/pritunl.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 7568D9BB55FF9E5287D586017AE645C0CF8E292A
apt-get update
apt-get install pritunl-client -y
clear

# Install Squid
apt-get -y install squid3
cp /etc/squid3/squid.conf /etc/squid3/squid.conf.orig
wget -O /etc/squid3/squid.conf "https://raw.githubusercontent.com/dathai/pritunl-ubuntu14.04/master/API/squid.conf" 
MYIP=`ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0' | grep -v '192.168'`;
sed -i s/xxxxxxxxx/$MYIP/g /etc/squid3/squid.conf;
service squid3 restart
clear

# Enable Firewall
sudo ufw allow 22,80,81,222,443,3128,8080/tcp
sudo ufw allow 22,80,81,222,443,3128,8080/udp
sudo yes | ufw enable

#FIGlet In Linux
sudo apt-get install figlet
yum install figlet

# About
clear
figlet "THAI-VPN"
echo "Script by dathai :-"
echo "-Pritunl"
echo "-MongoDB"
echo "-Squid Proxy Port 8080,3128"
echo "Pritunl    :  https://$MYIP"
echo "Login pritunl?"
echo "copy key"
pritunl setup-key
