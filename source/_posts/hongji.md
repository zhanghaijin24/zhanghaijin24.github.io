---
---title: DELL Inspiron i5 5000 Series安装系统
---

# F2进行bios设置
***secureboot***
- Disabled
***General/Advanced Boot Options***
- Enable Legacy Option ROMs
***General/Boot Sequence***
- Legacy

# 按F12选择USB，进入PE，分区，安装系统

# 安装驱动精灵万能网卡版

# 宏基电脑ASPIRE 4750G开启无限功能 
- Fn+NumLK

# 下载ubuntu系统
- http://mirrors.aliyun.com/ubuntu-releases/

# 下载USBWriter

# ubuntu18.04安裝hexo
***安裝nodejs***
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
***安裝hexo***
```
sudo npm install -g npm
sudo npm install hexo-cli -g
cd /usr/bin
sudo ln -s /usr/local/node/bin/hexo hexo
hexo -v
```

***從github克隆hexo文件***
```
git clone -b hexo https://github.com/zhanghaijin24/zhanghaijin24.github.io.git
cd zhanghaijin24.github.io 
sudo npm install
udo npm install hexo-deployer-git
```
***推送到github基本操作***
```
git add .
git commit -m "hexo"
git push origin hexo
```
***git基本操作***
```
hexo clean
hexo g
hexo d
```

