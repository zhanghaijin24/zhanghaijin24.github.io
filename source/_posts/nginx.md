---
title: nginx
---

### 修改nginx默认端口80为81
```
vim /etc/nginx/nginx.conf
#修改listen 端口为81
systemctl restart nginx
firewall-cmd --zone=public --add-port=81/tcp --permanent
firewall-cmd --reload

#阿里云安全组规则开放81端口
```
