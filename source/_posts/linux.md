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
### neovim 安装vim plug
```
mkdir -p ~/.config/nvim
cd ~/.config/nvim
git clone https://github.com/junegunn/vim-plug.git
mv vim-plug autoload
```
#nvim init.vim
```
call plug#begin('~/.config/nvim/plugged')

Plug 'vim-airline/vim-airline'
call plug#end()
```


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
