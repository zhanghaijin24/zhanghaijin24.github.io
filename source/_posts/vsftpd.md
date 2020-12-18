---
title: vsftpd
---


#### centos7 安装vsftpd
```
yum install -y vsftpd

```

### 开机启动vsdtpd
```
systemctl enable vsftpd

```

### 配置selinux
vim /etc/selinux/config
```
配置SELINUX=enforcing

```

有用命令
getsebool -a | grep ftp
开启tftp_home_dir和ftpd_full_access 才能够访问ftp目录和传输文件
```
setsebool -P tftp_home_dir 1
setsebool -P ftpd_full_access 1
```

查看ftp是否启动，以及ftp开放端口
```
netstat -antup | grep ftp
```

### firewalld start/delete vsftpd port:21
```
firewall-cmd --list-ports
firewall-cmd --reload
firewall-cmd --zone=public --add-port=21/tcp --permanent
firewall-cmd --zone=public --add-port=40000-45000/tcp --permanent
firewall-cmd --zone=public --remove-port=21/tcp --permanent
```




#### ubuntu 18.04 安装vsftpd
```
apt update
apt install vsftpd
systemctl enable vsftpd
systemctl start vsftpd
netstat -antup | grep vsftpd

useradd david -m
passwd david

mkdir /ftp
chown -R david:david /ftp
```
#vim /etc/vsftpd.conf
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
#listen_ipv6=YES

local_root=/ftp
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=192.144.237.214 #请修改为您的 Linux 云服务器公网 IP
pasv_min_port=40000
pasv_max_port=45000
```

#vim /etc/vsftpd.chroot_list
```
david
```

```
systemctl restart vsftpd
```


