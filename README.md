# assignment8_Database


The attempt to complete the whole assignment was not met, as for some technicality issues. 
The following procedure will describe the process to solve the assignment. The replicate was made, but not with the implementation of the classicmodel
An account in Digital Ocean was created. A droplet in Singapore (master) was established with the following info:
•  
mysql-s-1vcpu-1gb-sgp1-01
Add tags

Image
 Ubuntu MySQL on 18.04
Size
1 vCPUs
1GB / 25GB Disk
($5/mo)
Resize
Region
SGP1
IPv4
128.199.210.7 Copy
IPv6
Enable
Private IP
Enable

The next step:
The terminal used is Putty
apt-get update
Sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
Bind-address changed to 128.199.210.7
Uncomment the line server-id               = 1
Uncomment the line - log_bin                 = /var/log/mysql/mysql-bin.log
Mysql -u root -p
mysql> CREATE USER 'name'@'%' IDENTIFIED BY 'test';                             
CREATE USER 'name'@'%' IDENTIFIED BY 'test';
FLUSH PRIVILEGES;
create database classicmodels;

The main problem was to make the mysqldump of the classicmodels from the host to server.
From the command line
The mysqldump was straight forward
C:\User\... >mysqldump -u root -p classicmodels > data-dump.sql
Enter password: ****
An attempt to make a copy of the file to the server. 
C:\Users\yosuke>scp data-dump.sql name@128.199.210.7:~/data-dump.sql
name@128.199.210.7's password:
Permission denied, please try again.
This technical issue prevented to complete the rest.
The plan for the rest was as follow (if the classicmodel could be used):
Make the same slave setup in Frankfurt  
Sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
Bind-address changed to new ip(Frankfurt) 
Uncomment the line server-id               = 1
Uncomment the line - log_bin                 = /var/log/mysql/mysql-bin.log
Mysql -u root -p

The replication of the database from its master should allow users in Frankfurt to make analytical data retrieval from the main database. The overall concept to conclude from this distant setup is that (the slave cannot make changes/update), but understand the time difference in the update due to the transaction. 
   


