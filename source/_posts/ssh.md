---
title: 修改默认ssh端口
---
#### centos7 修改默认ssh端口

```
git config --global user.name "zhanghaijin24"
git config --global user.email "1171892570@qq.com"
ssh-keygen -t rsa -C "1171892570@qq.com"
```

```
sudo vi /etc/ssh/sshd_config
sudo yum -y install policycoreutils-python
sudo semanage port -a -t ssh_port_t -p tcp 10086

systemctl enable firewalld
systemctl start firewalld

sudo firewall-cmd --permanent --zone=public --add-port=10086/tcp

sudo systemctl status firewalld

sudo sudo firewall-cmd --reload

sudo systemctl restart sshd.service
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
