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

