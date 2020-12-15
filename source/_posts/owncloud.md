---
title: owncloud
---

#### centos7 owncloud

### 安装apache2 mariadb owncloud
```
yum install -y httpd
yum install -y mariadb mariadb-server
yum install -y unzip

systemctl start httpd
systemctl enable httpd

systemctl start mariadb
systemctl enable mariadb

unzip owncloud-10.4.0.zip -d /var/www/html/

chown -R apache:apache owncloud
```
touch /etc/httpd/conf.d/owncloud.conf
```
<VirtualHost 192.168.100.204:80>
ServerAdmin webmaster@yourdomain.com
DocumentRoot "/var/www/html/owncloud/"
ServerName yourdomain.com
ServerAlias www.yourdomain.com
ErrorLog "/var/log/httpd/yourdomain.com-error_log"
CustomLog "/var/log/httpd/yourdomain.com-access_log" combined
<Directory "/var/www/html/owncloud/">
DirectoryIndex index.html index.php
Options FollowSymLinks
AllowOverride All
Require all granted
</Directory>
</VirtualHost>
```
```
mkdir -p /owncloud/data
chown -R apache:apache /owncloud/data
systemctl restart php-fpm
systemctl restart httpd
systemctl restart httpd
systemctl enable httpd

```

### 彻底卸载php7.2
```
rpm -qa | grep php
rpm -e 
rpm -e --nodeps 
```
### 安装php7.2
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum clean all
yum -y update
yum install php72w php72w-mysql php72w-pecl-zip php72w-xml php72w-mbstring php72w-gd php72w-mcrypt php72w-pear php72w-pspell php72w-pdo php72w-xml php72w-intl php72w-zip php72w-zlib php72w-fpm php72w-cli php72w-common

php -i | grep -i php.ini
sed -i "s/post_max_size = 8M/post_max_size = 256M/" /etc/php.ini
sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 256M/" /etc/php.ini

systemctl start php-fpm

php -v
```
#vim /var/www/html/info.php
```
<?php
phpinfo();
?>
```
#find / -name php.ini
```
/etc/php.ini
```

#vim /etc/httpd/conf/httpd.conf
```
PHPIniDir /etc/php.ini
```

### 创建数据库
```
mysql_secure_installation
#创建密码123456

mysql -uroot -p123456
CREATE DATABASE owncloud;
GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost' IDENTIFIED BY '123456';
FLUSH PRIVILEGES;
exit
```

```
firewall-cmd --permanent --add-service=mysql
firewall-cmd --permanent --add-service=http  
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```
