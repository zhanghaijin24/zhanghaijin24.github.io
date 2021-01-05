---
title: mac
---

# 安装fzf
---
- git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
- ~/.fzf/install

# Mac使用终端格式化U盘
---
- diskutil list
- sudo diskutil eraseDisk FAT32 MYUSB MBRFormat /dev/disk2

# 安装homebrew
---
- /bin/zsh -c "$(curl -fsSL https://gitee.com/jyotish/HomebrewCN/raw/master/Homebrew.sh)"
- git config --global http.postBuffer 924288000
- git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow
-  git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow
- export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"

- export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"

# 安装ohmyzsh
- brew install zsh
- cat /etc/shells
- chsh -s /bin/zsh
- reboot

- git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
- cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

- git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

- git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

=======
# 安装hexo以及nodejs
---
- brew install node
- sudo sudo npm install -g hexo-cli
- cd cd zhanghaijin24.github.io
- sudo npm install
- sudo npm install hexo-deployer-git
