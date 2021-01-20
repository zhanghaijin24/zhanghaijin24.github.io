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

# DELL Inspiron i5 5000 Series安裝ubuntu18.04到固態硬盤
***1,按F2配置bios***
- ![92F84ACE-9872-4C1C-8004-3F1F4876A247.jpg](http://101.201.197.193/images/2021/01/20/92F84ACE-9872-4C1C-8004-3F1F4876A247.jpg)

- ![8A30C296-7373-4B62-9A4A-2D5B06DB6242.jpg](http://101.201.197.193/images/2021/01/20/8A30C296-7373-4B62-9A4A-2D5B06DB6242.jpg)
- ![E74D701B-C520-4131-9180-EFC415E509C0.jpg](http://101.201.197.193/images/2021/01/20/E74D701B-C520-4131-9180-EFC415E509C0.jpg)

***2,按F12進入usb***
- ![A38BD449-414F-43C8-9276-D3F47021AF7E.jpg](http://101.201.197.193/images/2021/01/20/A38BD449-414F-43C8-9276-D3F47021AF7E.jpg)


# Rsync 簡單詳解
***遠程centos7同步到本地ubuntu18.04***
- rsync -avz -e 'ssh -p 10086' david@101.201.197.193:~/download/ ~/Downloads
