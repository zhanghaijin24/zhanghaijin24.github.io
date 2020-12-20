---
title: git
---

### git fetch更新远程仓库
```
git fetch origin hexo:tmp
git diff tmp
git merge tmp
git branch -d tmp
```
### 如何上传博客工程到Github
```
git init 
git remote add origin https://github.com/zhanghaijin24/zhanghaijin24.github.io.git 
git checkout -b hexo 
git add . 
git commit -m "fix bug"
git push origin hexo 
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
