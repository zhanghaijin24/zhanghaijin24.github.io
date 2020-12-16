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
