---
title: centos7 vsftpd
---

### 安装vsftpd
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



