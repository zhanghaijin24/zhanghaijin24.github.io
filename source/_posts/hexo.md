---
title: hexo
---

### 安装nodejs
```
tar -vxf node-v12.16.1-linux-x64.tar.xz -C /usr/local
cd /usr/local
mv node-v12.16.1-linux-x64/ node
cd /usr/bin
ln -s /usr/local/node/bin/node node
ln -s /usr/local/node/bin/npm npm
node -v
npm -v
```

### 阿里云配置hexo，克隆从github
```
git clone -b hexo https://github.com/zhanghaijin24/zhanghaijin24.github.io.git
sudo npm install -g hexo-cli
sudo npm install
sudo npm install hexo-deployer-git
```

### 修改，同步
```
git add .
git commit -m "hexo"
git push origin hexo
```

### 从github拉取数据
```
git pull
```

### selinux阻止nginx，导致出现403 Forbidden
```
chcon -R -t httpd_sys_rw_content_t zhanghaijin24.github.io
```
