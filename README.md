This is the Nginx configuration for hosting multiple Magento websites with php-fpm in a Centos Server.

Steps to install Nginx PHP-FPM on Centos7 Server

`````````````````````````````````````````````````````````````````````````````````````````````````````````````
 Nginx Installation:
 
 yum update
 yum install epel-release
 yum install nginx
 systemctl enable nginx
 systemctl start nginx
`````````````````````````````````````````````````````````````````````````````````````````````````````````````

 yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
 yum install yum-utils
 yum-config-manager --enable remi-php71
 yum install php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo  php-bcmath  php-dom php-intl php- mbstring  php-soap

yum install http://www.percona.com/downloads/percona-release/redhat/0.1-4/percona-release-0.1-4.noarch.rpm
yum install Percona-Server-server-57
systemctl enable mysql

grep -i  "temporary password" /var/log/mysqld.log
 systemctl enable php-fpm
 systemctl restart php-fpm
