# ansible-service-deployment
we first add hostsfile which consists webservers ,snmpd , devhaproxy (check hosts)
we should add config in the .ssh in the ubunut 
we should create ssh keys and place them in the webservers and change permissions for the keys with command chmod 600
config file should have bastion server and all the webservers and devhaproxy should have proxyjump to bastion server 
we should add PasswordAuthentication no so that while doing ssh it doesn't ask for password
config file :


PasswordAuthentication no
StrictHostKeyChecking no

host BastionET2598
hostname 188.95.231.89
port 22
user ubuntu
IdentityFile /home/shiva/.ssh/id_rsa
PasswordAuthentication no

host devA
hostname 10.1.0.37
port 22
user ubuntu 
IdentityFile /home/shiva/.ssh/id_rsa
proxyjump BastionET2598

host devB
hostname 10.1.0.197
port 22
user ubuntu 
IdentityFile /home/shiva/.ssh/id_rsa
proxyjump BastionET2598

host devC
hostname 10.1.0.12
port 22
user ubuntu
IdentityFile /home/shiva/.ssh/id_rsa
proxyjump BastionET2598

host devhaproxy
hostname 188.95.226.61
port 22
user ubuntu
IdentityFile /home/shiva/.ssh/id_rsa
proxyjump BastionET2598


now nginx.conf the default file has to be stored in the webservers after installing the nginx (check nginx.conf)
install php and php -fpm and place the config file in var/www/html/index.php (check index.php)
install snmp and snmpd and change the agentaddress in snmpd.conf file to udp:161 so that it listens to all  the idp address(snmpdeamon)(check snmpd.conf)
In the devhaproxy webserver install haproxy and copy the files to the haproxy.conf and for the webservers in haproxy.conf file  write the for loop for getting the
ipaddress from gather_facts. devhaproxy will forward all tcp connections (check haproxy.conf)
In the devhaproxy install nginx and change default port listening to 1161 in /etc/nginx/sites-available/default for listening to the 1161 port (check nginx1.conf)
In the /etc/nginx/nginx.conf add webservers that needed for the udp.This udp webservers are added in the up stream webservers part in the nginx.conf file (check nginx2.conf)
Add the webservers from the gather_facts using forloop and make sure it listens to port 161
In the server part of nginx.conf file make sure it listens to port 1161
install snmp and run the snmpwalk test and haproxy text in devhaproxy(check site.yaml)
The haproxy uses round robin and least connected method to connent servers(to distribute the load)


