---
title: centos7
---

## selinux配置
- setenforce 0
- getenforce

# centos7 修改默认ssh端口/配置端口为10086
-----------------------

- sudo vim /etc/ssh/sshd_config
![centos7/sshd/port](http://101.201.197.193/images/2020/12/24/-2020-12-24-10.46.32.png)
- sudo yum -y install policycoreutils-python
- sudo semanage port -a -t ssh_port_t -p tcp 10086

- systemctl enable firewalld
- systemctl start firewalld

- sudo firewall-cmd --permanent --zone=public --add-port=10086/tcp
- sudo systemctl status firewalld
- sudo sudo firewall-cmd --reload

- sudo systemctl restart sshd.service

# centos7 安装vsftpd
----

- yum install -y vsftpd

*开机启动vsftpd*
- systemctl enable vsftpd
*配置selinux*
# vim /etc/selinux/config
![centos7/selinux](http://101.201.197.193/images/2020/12/24/-2020-12-24-11.03.28.png)

*查看ftp配置*
- getsebool -a | grep ftp
[![ftp](http://101.201.197.193/images/2020/12/24/-2020-12-24-11.22.56.png)](http://101.201.197.193/image/262)
*开启tftp_home_dir和ftpd_full_access 才能够访问ftp目录和传输文件*
- setsebool -P tftp_home_dir 1
- setsebool -P ftpd_full_access 1

*查看ftp是否启动，以及ftp开放端口*
- netstat -antup | grep ftp


*firewalld start/delete vsftpd port:21*
- firewall-cmd --list-ports
- firewall-cmd --reload
- firewall-cmd --zone=public --add-port=21/tcp --permanent
- firewall-cmd --zone=public --add-port=40000-45000/tcp --permanent
- firewall-cmd --zone=public --remove-port=21/tcp --permanent

# centos7 修改nginx默认端口80为81
---
- vim /etc/nginx/nginx.conf
[![centos7/nginx port](http://101.201.197.193/images/2020/12/24/-2020-12-24-11.31.46.png)](http://101.201.197.193/image/tLM)
**修改listen 端口为81**
- systemctl restart nginx
- firewall-cmd --zone=public --add-port=81/tcp --permanent
- firewall-cmd --reload

*阿里云安全组规则开放81端口*

# 阿里云配置hexo，克隆从github
---
- git clone -b hexo https://github.com/zhanghaijin24/zhanghaijin24.github.io.git
- sudo npm install -g hexo-cli
- sudo npm install
- sudo npm install hexo-deployer-git

# centos7 selinux阻止nginx，导致出现403 Forbidden
---
- chcon -R -t httpd_sys_rw_content_t zhanghaijin24.github.io

# centos7 owncloud
---
**安装apache2 mariadb owncloud**
- yum install -y httpd
- yum install -y mariadb mariadb-server
- yum install -y unzip

- systemctl start httpd
- systemctl enable httpd
- systemctl start mariadb
- systemctl enable mariadb

- unzip owncloud-10.4.0.zip -d /var/www/html/
- chown -R apache:apache owncloud

*#vim /etc/httpd/conf.d/owncloud.conf*
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

- mkdir -p /owncloud/data
- chown -R apache:apache /owncloud/data
- systemctl restart php-fpm
- systemctl restart httpd
- systemctl restart httpd
- systemctl enable httpd


# 彻底卸载php7.2
---
- rpm -qa | grep php
- rpm -e 
- rpm -e --nodeps 

# 安装php7.2
---
- rpm -Uvh https://mirror.webtatic.com/yum/el7/epel-release.rpm
- rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
- yum clean all
- yum -y update
- yum install php72w php72w-mysql php72w-pecl-zip php72w-xml php72w-mbstring php72w-gd php72w-mcrypt php72w-pear php72w-pspell php72w-pdo php72w-xml php72w-intl php72w-zip php72w-zlib php72w-fpm php72w-cli php72w-common

- php -i | grep -i php.ini
- sed -i "s/post_max_size = 8M/post_max_size = 256M/" /etc/php.ini
- sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 256M/" /etc/php.ini

- systemctl start php-fpm

- php -v

***#vim /var/www/html/info.php***
```
<?php
phpinfo();
?>
```
***#find / -name php.ini***
```
/etc/php.ini
```

***#vim /etc/httpd/conf/httpd.conf***
```
PHPIniDir /etc/php.ini
```

# 创建数据库
---
- mysql_secure_installation
**创建密码123456**

- mysql -uroot -p123456
- CREATE DATABASE owncloud;
- GRANT ALL PRIVILEGES ON owncloud.* TO 'owncloud'@'localhost' IDENTIFIED BY '123456';
- FLUSH PRIVILEGES;
- exit


- firewall-cmd --permanent --add-service=mysql
- firewall-cmd --permanent --add-service=http  
- firewall-cmd --zone=public --add-port=3306/tcp --permanent

# centos7 搭建Chevereto图床
*压缩Chevereto-Free文件*
- tar -zcvf /Users/zhanghaijin/Chevereto-Free.tar.gz Chevereto-Free
*解压Chevereto-Free.tar.gz*
- tar -vxf Chevereto-Free.tar.gz -C /var/www/html
- cd /var/www/html
- mv Chevereto-Free/ chevereto


*#vim /var/www/html/chevereto/app/settings.php*
```
<?php 
$config['db_name'] = 'cheveretodb'; 
$config['db_user'] = 'chevereto'; 
$config['db_pass'] = 'password'; 
$config['admin_password'] = 'password';
?php>
```

- chown -R apache:apache chevereto/
- chmod -R 777 /var/www/html/chevereto

*#vim /etc/httpd/conf.d/owncloud.conf*
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

- systemctl restart php-fpm
- systemctl restart httpd

