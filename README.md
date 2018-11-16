This is the Nginx configuration for hosting multiple Magento websites with php-fpm in a Centos Server. Only the basisc installation steps are mentioned here.

Steps to install Nginx, PHP-FPM, MySQL and PHPMyAdmin on Centos7 Server

Pre Install:

 Disable Selinux
 ```
 sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config && cat /etc/selinux/config && reboot
 ```
 Update packages and install Extra packages
 ```
 yum update
 yum install epel-release
```

`````````````````````````````````````````````````````````````````````````````````````````````````````````````
 Nginx Installation:

 yum install nginx
 systemctl enable nginx
 systemctl start nginx
`````````````````````````````````````````````````````````````````````````````````````````````````````````````
nginx.conf in kept unmodifed. 

default.d directory contains the phpmyadmin vhost config. 

conf.d directory contains the vhost for the websites hosted on the server. Each website is running under a seperate user. Here I have create a user named "live" changed its home_directory to "/usr/share/nginx/html/live/". The group and ownership of the document root should be "live".

`````````````````````````````````````````````````````````````````````````````````````````````````````````````
PHP and php-fpm Installation:

 yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
 yum install yum-utils
 yum-config-manager --enable remi-php71
 yum install php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo  php-bcmath  php-dom php-intl php- mbstring  php-soap
 systemctl enable php-fpm
 systemctl restart php-fpm
`````````````````````````````````````````````````````````````````````````````````````````````````````````````
Seperate php-fpm pools are created for each user in the directory "/etc/php-fpm.d" (here live.conf).

`````````````````````````````````````````````````````````````````````````````````````````````````````````````
MySQL Installation:

yum install http://www.percona.com/downloads/percona-release/redhat/0.1-4/percona-release-0.1-4.noarch.rpm
yum install Percona-Server-server-57
systemctl enable mysql
grep -i  "temporary password" /var/log/mysqld.log
mysql_secure_installation

`````````````````````````````````````````````````````````````````````````````````````````````````````````````
After installation of MySQL, the root password needs to be found from the mysqld.log.This will be required mysql initialisation.
