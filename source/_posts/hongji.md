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

# 华硕ASUS U盘引导安装ubuntu18.04
---
首先开机按F2，进入系统BIOS，再按F8，选择U盘启动
***ubuntu 18.04分区***
**分区最先对/进行分区，主分区**
- 首先 挂载点：/：ext4日志文件系统，主分区，10G
- 其次 swap： 逻辑分区，电脑内存大学大小
- 最后 ：/home ：ext4日志文件系统，逻辑分区，剩余空间都是。
![E74BFD09-3BA7-448D-BF80-AB9EA231B9B8.jpg](http://101.201.197.193/images/2021/01/27/E74BFD09-3BA7-448D-BF80-AB9EA231B9B8.jpg)

![ACBBF6CA-FB97-4C6E-8EDE-32C17BD38709.jpg](http://101.201.197.193/images/2021/01/27/ACBBF6CA-FB97-4C6E-8EDE-32C17BD38709.jpg)
![F3BFD02F-A1B5-44D3-B7D2-E0B733DBF729.jpg](http://101.201.197.193/images/2021/01/27/F3BFD02F-A1B5-44D3-B7D2-E0B733DBF729.jpg)

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

# 安裝ubuntu18.04/apache2
---
```
sudo apt update && sudo apt install apache2 -y
```
***配置apache2***
```
sudo apachectl -S

```
輸出的結果如下圖：
![707-2-apachectl-S.png](http://101.201.197.193/images/2021/01/23/707-2-apachectl-S.png)

这条命令会打印出 **apache** 的所有配置等具体信息。其中最主要的就是 **VirtualHost configuration:** ，它给出了apache当前使用的配置文件，而 **apache** 的所有配置信息都是在这个文件里定义的。
　　这里需要注意的是配置文件的路径是：  **/etc/apache2/sites-enabled/000-default.conf** ，而实际上，真正的配置文件是   **/etc/apache2/sites-available/000-default.conf** .**/etc/apache2/sites-enabled** 文件夹下的文件只是 **/etc/apache2/sites-available/**  下面文件的软连接而已。所以要修改配置，请务必修改 **/etc/apache2/sites-available/**  下面的文件，修改完成之后，可以先使用  **sudo apache2ctl configtest**  来确认配置文件语法正确，然后需要执行下面两条命令来使配置生效。
```
sudo a2ensite ××××.conf
sudo systemctl restart apache2
```

# 安裝php7.2
```
sudo apt install  libapache2-mod-php7.2 openssl php-imagick php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-pgsql php-smbclient php-ssh2 php7.2-sqlite3 php7.2-xml php7.2-zip
```


# ubuntu18.04 安装Apache
- sudo apt install apache2
***禁用apache目录列表***
- sudo a2dismod autoindex
***开启额外模块***
- sudo a2enmod rewrite
- sudo a2enmod headers
- sudo a2enmod env
- sudo a2enmod dir
- sudo a2enmod mime
***重启apache***
- sudo systemctl restart apache2
***安装php***
现在owncloud只支持php7.1
- sudo apt-get install software-properties-common
- sudo add-apt-repository ppa:ondrej/php
- sudo apt update
- sudo apt install php7.1
接着安装php模块
- sudo apt-get install php7.1-cli php7.1-common php7.1-mbstring php7.1-gd php7.1-intl php7.1-xml php7.1-mysql php7.1-zip php7.1-curl php7.1-xmlrpc
安装完成后配置一下
- sudo nvim /etc/php/7.1/apache2/php.ini
```
file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_file_size = 100M

```
重启apache
- sudo systemctl restart apache2

# 安装chevereto
- tar -xvzf Chevereto-Free.tar.gz
- sudo mv Chevereto-Free /var/www/chevereto
- sudo chown -R www-data:www-data /var/www/chevereto
- sudo chmod -R 777 /var/www/chevereto 
***apache2/chevereto***
sudo nvim /etc/apache2/conf-available/owncloud.conf
```
Alias /chevereto "/var/www/chevereto"
  
<Directory /var/www/chevereto>
Options +FollowSymlinks
AllowOverride ALL

<IfModule mod_dav.c>
Dav off
</IfModule>

SetEnv HOME /var/www/chevereto
SetEnv HTTP_HOME /var/www/chevereto

</Directory>

```
***运行一下命令***

***禁用apache目录列表***
- sudo a2dismod autoindex
***开启额外模块***
- sudo a2enmod rewrite
- sudo a2enmod headers
- sudo a2enmod env
- sudo a2enmod dir
- sudo a2enmod mime
***重启apache***
- sudo systemctl restart apache2

一旦MariaDB得到保护，您将需要为Chevereto创建一个数据库和用户
- sudo mysql -u root -p
输入密码123456
- MariaDB [(none)]>CREATE DATABASE cheveretodb DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
- MariaDB [(none)]>GRANT ALL PRIVILEGES ON cheveretodb.* TO ‘chevereto’@’localhost’ IDENTIFIED BY ‘password’;
- MariaDB [(none)]>FLUSH PRIVILEGES;
- MariaDB [(none)]>\q

