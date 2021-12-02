This is 2204` new branch
MySql Manual Installation

Installing MySQL 5.5.51 on Ubuntu 16.04 and 18.04
Uninstall any existing version of MySQL
$ sudo rm /var/lib/mysql/ -R


Delete the MySQL profile
$ sudo rm /etc/mysql/ -R


Automatically uninstall mysql
$ sudo apt-get autoremove mysql* --purge
$ sudo apt-get remove apparmor


Download version 5.5.51 from MySQL site
$ wget https://dev.mysql.com/get/Downloads/MySQL-5.5/mysql-5.5.56-linux-glibc2.5-x86_64.tar.gz


Add mysql user group
$ sudo groupadd mysql


Add mysql (not the current user) to mysql user group
$ sudo useradd -g  mysql mysql


Extract mysql-5.5.51-linux2.6-x86_64.tar.gz to /usr/local
$ cd /usr/local
$ sudo tar -xvf mysql-5.5.49-linux2.6-x86_64.tar.gz


Create mysql folder in /usr/local
$ sudo mv mysql-5.5.49-linux2.6-x86_64 mysql


Set mysql directory owner and user group
$ cd mysql
$ sudo chown -R mysql:mysql *


Install the required lib package
$ sudo apt-get install libaio1 libaio-dev


Execute mysql installation script
$ sudo scripts/mysql_install_db --user=mysql


Set mysql directory owner from outside the mysql directory
$ sudo chown -R root /usr/local/mysql


Set data directory owner from inside mysql directory
$ sudo chown -R mysql data


Copy the mysql configuration file
$ sudo cp support-files/my-medium.cnf /etc/my.cnf 


Start mysql
$ sudo bin/mysqld_safe --user=mysql &
$ sudo cp support-files/mysql.server /etc/init.d/mysql.server


Initialize root user password
$ sudo bin/mysqladmin -u root password '111111'


Start mysql server
$ sudo /etc/init.d/mysql.server start


Stop mysql server
$ sudo /etc/init.d/mysql.server stop


Check status of mysql
$ sudo /etc/init.d/mysql.server status


Enable myql on startup
$ sudo update-rc.d -f mysql.server defaults 


Disable mysql on startup (Optional)
$ sudo update-rc.d -f mysql.server remove


Add mysql path to the system
$ sudo ln -s /usr/local/mysql/bin/mysql /usr/local/bin/mysql


Now directly use the command below to start mysql
$ mysql -u root -p 


I have implemented in Ubuntu18.04 machine.

Reference : https://askubuntu.com/questions/763240/is-it-possible-to-install-mysql-5-5-or-5-6-on-ubuntu-16-04
