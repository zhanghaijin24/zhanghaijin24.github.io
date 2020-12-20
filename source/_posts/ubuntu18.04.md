---
title: ubuntu 18.04
---

### Ubuntu 18.04 开启root登录

#sudo vim /etc/ssh/sshd_config
```
PermitRootLogin yes
```

```
sudo systemctl restart ssh
```
### 删除ubuntu用户
```
deluser ubuntu --remove-home
```


#### ubuntu 18.04 修改默认ssh端口
#vim /etc/ssh/sshd_config
```
Port 22
Port 10086
```
重启ssh
```
systemctl restart ssh
```
### ufw配置
```
ufw status verbose
ufw enable
ufw allow 22/tcp
ufw allow 10086/tcp
ufw status numbered
ufw delete 2
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

#vim /etc/vsftpd.chroot_list
```
david
```

```
systemctl restart vsftpd
```

### ubuntu 18.04安装hexo

##升级npm
```
sudo npm install -g npm
sudo npm install hexo-cli -g
cd /usr/bin
sudo ln -s /usr/local/node/bin/hexo hexo
hexo -v

sudo ufw allow 4000/tcp

```
