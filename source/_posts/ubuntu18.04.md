---
title: ubuntu 18.04
---

# Ubuntu 18.04 开启root登录
---
*#sudo vim /etc/ssh/sshd_config*
![ubuntu18.04/root](http://101.201.197.193/images/2020/12/25/-2020-12-25-10.48.16.png)
- sudo systemctl restart ssh

*删除ubuntu用户*
- deluser ubuntu --remove-home


# ubuntu 18.04 修改默认ssh端口
*#vim /etc/ssh/sshd_config*
[![ubuntu18.04 /port](http://101.201.197.193/images/2020/12/25/-2020-12-25-10.51.50.png)](http://101.201.197.193/image/GTS)

*重启ssh*
- systemctl restart ssh
*ufw配置*

- ufw status verbose
- ufw enable
- ufw allow 22/tcp
- ufw allow 10086/tcp
- ufw status numbered
- ufw delete 2
- ufw disable

# ubuntu 18.04 安装vsftpd

- apt update
- apt install vsftpd
- systemctl enable vsftpd
- systemctl start vsftpd
- netstat -antup | grep vsftpd

- useradd david -m
- passwd david

- mkdir /ftp
- chown -R david:david /ftp

*#vim /etc/vsftpd.conf*
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
listen=YES
#listen_ipv6=YES

local_root=/ftp
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=192.144.237.214 #请修改为您的 Linux 云服务器公网 IP
pasv_min_port=40000
pasv_max_port=45000
```

*#vim /etc/vsftpd.chroot_list*
```
david
```

- systemctl restart vsftpd


# ubuntu 18.04安装hexo

*升级npm*

- sudo npm install -g npm
- sudo npm install hexo-cli -g
- cd /usr/bin
- sudo ln -s /usr/local/node/bin/hexo hexo
- hexo -v

- sudo ufw allow 4000/tcp

# ubuntu18.04 安装owncloud
---
*installing Mysql*

- apt update

- apt install apache2 libapache2-mod-php7.2 openssl php-imagick php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-pgsql php-smbclient php-ssh2 php7.2-sqlite3 php7.2-xml php7.2-zip

*查看apache2 是否安装*
*#dpkg -l apache2*
![Alt text](http://101.201.197.193/images/2020/12/23/-2020-12-23-9.07.40.png)

*启动apache2 ，以及开机启动*

- systemctl start apache2
- systemctl enable apache2
*安装Mariadb*
- apt install mariadb-server
- mysql_secure_installation
	- CREATE DATABASE linuxidc_owdb;
	- GRANT ALL ON linuxidc_owdb.* TO 'linuxidc_owuser'@'localhost' IDENTIFIED BY'v';
	- FLUSH PRIVILEGES;
	- EXIT
- unzip owncloud-10.4.0.zip -d /var/www
*# vim /etc/apache2/conf-available/owncloud.conf*
```
Alias /owncloud "/var/www/owncloud"
  
<Directory /var/www/owncloud>
Options +FollowSymlinks
AllowOverride ALL

<IfModule mod_dav.c>
Dav off
</IfModule>

SetEnv HOME /var/www/owncloud
SetEnv HTTP_HOME /var/www/owncloud

</Directory>
```

- a2enconf owncloud
- a2enmod rewrite
- a2enmod headers
- a2enmod env
- a2enmod dir
- a2enmod mime

- systemctl restart apache2

- cd /var/www/owncloud
- mkdir data
- chown -R www-data:www-data data
- chown -R www-data:www-data config
- chown -R www-data:www-data apps

# 彻底卸载mysql
---
```
- dpkg --list | grep mariadb-server
- apt-get remove --purge mariadb-common
- apt-get remove --purge php7.2-mysql
```

# 安装Chevereto
---
- apt-get install mariadb-server mariadb-client
- systemctl start mysql
- systemctl enable mysql

- mysql_secure_installation
```
- CREATE DATABASE cheveretodb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
- GRANT ALL PRIVILEGES ON cheveretodb.* TO 'chevereto'@'localhost' IDENTIFIED BY 'password';
- FLUSH PRIVILEGES;
- \q
```

- tar -xvzf Chevereto-Free.tar.gz
- mv Chevereto-Free.tar.gz /var/www/html/chevereto
- cd /var/www/html/chevereto
- vim app/settings.php
```
<?php
$config['db_name'] = 'cheveretodb';
$config['db_user'] = 'chevereto';
$config['db_pass'] = 'password';
$config['admin_password'] = 'password';
```

- chown -R www-data:www-data /var/www/html/chevereto
- chmod -R 777 /var/www/html/chevereto

- vim /etc/apache2/sites-available/chevereto.conf
```
<VirtualHost *:80>
ServerAdmin admin@example.com
DocumentRoot /var/www/html/chevereto/
ServerName example.com
<Directory /var/www/html/chevereto/>
Options FollowSymLinks
DirectoryIndex index.php
AllowOverride All
Order allow,deny
allow from all
</Directory>
ErrorLog /var/log/apache2/chevereto-error_log
CustomLog /var/log/apache2/chevereto-access_log common
</VirtualHost>
```

- a2ensite chevereto
- systemctl restart apache2

***配置防火墙***
- ufw enable
- ufw allow 80
- ufw reload

# ubuntu18.04 安裝zsh
***1、手动修改ubuntu默认的shell***
- sudo vim /etc/passwd/
```
原来：li:x:1000:1000:li,,,:/home/li:/bin/bash
更改后：li:x:1000:1000:li,,,:/home/li:/usr/bin/zsh
```

