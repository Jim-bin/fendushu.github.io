---
title: Hexo多终端同步
date: 2020-06-06 01:36:58
tags: 教程
---

多终端写作
<!--more-->

### 在github.io或者终端新建hexo分支，并设为默认分支，_config.yml配置推送为master

```bash
# 新建新分支
git checkout -b hexo

# 切换分支
git checkout hexo

# 查看分支
git branch
```

### 推送到github

```bash
git add .
git commit -m "新建分支"
git remote add origin https://github.com/jim-bin/jim-bin.github.io.git
git push -u origin hexo # -f 强制推送
```

### 其他电脑首次开始写作

```bash
git clone https://github.com/jim-bin/jim-bin.github.io.git
npm install hexo-cli -g
npm i hexo --save
npm install hexo-deployer-git --save
```

### 写作之后

```bash
# 在本地查看示例(localhost:4000)
hexo g
hexo s

# 部署
hexo new post "title"
hexo d -g
```

### 同步文件

```bash
git add .
git commmit -m "some"
git push origin hexo
```

### 下次写作

```bash
git pull # 或者 git pull origin hexo
git add .
git commmit -m "some"
git push origin hexo
```

### 第一台电脑继续

```bash
git pull # 或者 git pull origin hexo
git add .
git commmit -m "some"
git push origin hexo
```