---
title: linux美化
---

### linux安装zsh、ohmyzsh
```
apt install -y zsh
chsh -s /bin/zsh
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
#vim .zshrc
```
plugins=(git
        zsh-autosuggestions
        zsh-syntax-highlighting
        )
```
#source .zshrc

### centos7 安装neovim
```
tar -vxf nvim-linux64.tar.gz -C /usr/local
cd /usr/local
mv nvim-linux64 nvim
cd /usr/bin
ln -s /usr/local/nvim/bin/nvim nvim
```
