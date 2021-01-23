---
title: hongji 4750G
---

# DELL Inspiron i5 5000 Series安装系统
***F2进行bios设置****
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

# DELL Inspiron i5 5000 Series安裝ubuntu18.04到固態硬盤
***1,按F2配置bios***
- ![92F84ACE-9872-4C1C-8004-3F1F4876A247.jpg](http://101.201.197.193/images/2021/01/20/92F84ACE-9872-4C1C-8004-3F1F4876A247.jpg)


- ![8A30C296-7373-4B62-9A4A-2D5B06DB6242.jpg](http://101.201.197.193/images/2021/01/20/8A30C296-7373-4B62-9A4A-2D5B06DB6242.jpg)
- ![E74D701B-C520-4131-9180-EFC415E509C0.jpg](http://101.201.197.193/images/2021/01/20/E74D701B-C520-4131-9180-EFC415E509C0.jpg)

***2,按F12進入usb***
- ![A38BD449-414F-43C8-9276-D3F47021AF7E.jpg](http://101.201.197.193/images/2021/01/20/A38BD449-414F-43C8-9276-D3F47021AF7E.jpg)


***ubuntu18.04 換源***
- sudo vim /etc/apt/sources.list
```
# 阿里源
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

```
- sudo apt update


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

***從github更新遠程倉庫到本地***
```
git fetch origin hexo:tmp
git diff tmp
git merge tmp
git branch -d tmp
```

# Rsync 簡單詳解
***遠程centos7同步到本地ubuntu18.04***
- rsync -avz -e 'ssh -p 10086' david@101.201.197.193:~/download/ ~/Downloads

# ubuntu18.04 B站看不了視頻
```
sudo add-apt-repository "deb http://archive.canonical.com/ $(lsb_release -sc) partner"
sudo apt update
sudo apt install adobe-flashplugin browser-plugin-freshplayer-pepperflash
```

# 安裝以及配置fzf
---
- git clone https://github.com/junegunn/fzf.git ~/.fzf
- ~/.fzf/install

***在github下載fd-musl_8.2.1_amd64.deb***
- sudo dpkg -i fd-musl_8.2.1_amd64.deb

***.zshrc配置fzf***
- nvim .zshrc
```
export FZF_DEFAULT_COMMAND="fd --hidden --exclude={.git,.idea,.sass-cache,      node_modules,build,.oh-my-zsh,.npm} --type f"                             
 
export FZF_DEFAULT_OPTS="--height 40% --layout=reverse --preview '(highlig      ht -O ansi {} || cat {}) 2> /dev/null | head -500'"
```

# ubuntu18.04 nvim 安裝系統剪貼板
---
- sudo apt install xclip
```
let mapleader=" "
map <leader>c "+y
map <leader>v "+gp  
```

# 安裝ubuntu18.04/MySQL
```
sudo apt install mysql-server -y
```

***配置mysql***
```
sudo mysql_secure_installation
```
配置圖片如下
[![707-3-mysql_secure_installation.png](http://101.201.197.193/images/2021/01/23/707-3-mysql_secure_installation.png)](http://101.201.197.193/image/X6Q)

*首先*，登陸數據庫：
```
sudo mysql
```
*其次*，輸入下面命令查看當前的認證方式
```
 mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
```
[![707-4-mysql-authentication-method.png](http://101.201.197.193/images/2021/01/23/707-4-mysql-authentication-method.png)](http://101.201.197.193/image/biv)

*再次*，依次輸入下面的命令修改用戶認證方式並更新設置：
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
mysql> FLUSH PRIVILEGES;

```

輸入下面命令退出MySQL登錄
```
mysql> \q
```
