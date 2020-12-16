---
title: vsftpd
---

### ubuntu 18.04 安装vsftpd
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
