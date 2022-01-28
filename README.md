# ansible-service-deployment
we first add hostsfile which consists webservers ,snmpd , devhaproxy 
we should add config in the .ssh in the ubunut 
we should create ssh keys and place them in the webservers and change permissions for the keys with command chmod 600
config file should have bastion server and all the webservers and devhaproxy should have proxyjump to bastion server 
we should add keychecking authentication no so that while doing ssh it doesn't ask for password
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


now nginx.conf the default file has to be stored in the webservers after installing the nginx 
install php and php -fpm and place the config file in 
