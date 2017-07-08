---
title: Start blog journey with hexo
date: 2017-02-17 18:19:25
tags: 
 - hexo
 - blog
categories: Hexo
---

> We can use github pages to setup a static blog easily and freely.
> The hexo is very handy to make blog management easy and fun.
> This post is about the very first step to hexo.   

<!--more-->

### Install Nodejs

1. **Download source code**
```bash
   $ wget https://nodejs.org/dist/v7.5.0/node-v7.5.0-linux-x64.tar.xz
   $ tar -xvJf node-v7.5.0-linux-x64.tar.xz
```
2. **Create soft link and use taobao mirror to accelerate**
```bash 
   $ cd node-v7.5.0-linux-x64/bin
   $ ln -s -f node /usr/local/bin/node
   $ ln -s -f npm  /usr/local/bin/npm
   $ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### Write Blog with hexo
1. **Create a directory to store blog content**
```bash
   $ sudo mkdir myblog && cd myblog
```
2. **Install Hexo and init a hexo project and install required packages**
```bash
  $ npm install -g hexo
  $ hexo init
  $ hexo install
```
3. **Deploy on local and browse the local url to check the blog**
```bash
  $ hexo s -g
```

### Deploy blog on github pages
1. **Create a repository with the format 'username.github.io'**

2. **Generate SSH keys with default settings and add them on github**
```bash
   $ ssh-keygen -t rsa -C "user.email"
```
3. **Test ssh on local**
```bash
   $ ssh -T git@github.com
```
4. **Configure deploy method**
 - Open the file vim ./myblog/_config.yml
 - Add a section like following:
  deploy:
    type: git
    repository: git@github.com:username/username.github.io.git
    branch: master

5. **Deploy the blog to githubpages(hexo-deployer-git is optional)**
```bash
   $cnpm install hexo-deployer-git --save
   $hexo d -g
```

6. **Check the blog in the browser**
```bash
   https://username.github.io
```

### Use custom domain to navigate to blog
1. Add two records into the parser settings:
- record type: CNAME
  Host name: @
  value:username.github.io
- record type: CNAME
  Host name: www
  value: username.github.io

2. Add a CNAME file in the blog
- Go to source directory
  ```bash
    $ cd ./myblog/source
  ```
- Add a file named CNAME, add the custom domain into the file

3. Deploy the blog again, it works by custom domain after about 10 minutes
```bash
   $ hexo d -g
```

### Source Code management
> Hexo just pushes static files into git in the master branch.While source codes
  remains in the myblog directory. We can push them into verson control by git

1. Add source codes into local respository
```bash
   $ cd ./myblog
   $ git init
   $ git add .
   $ git commit -m "the init blog source codes"
```
2. Add remote repository
```bash
   $ git remote add origin git@github.com:username/username.github.io.git
```
3. Create branch to maintain source codes as blog contents are reserved in the master branch
```bash
   $ git checkout -b hexo
   $ git push origin hexo
   $ git branch -d master
```

### Write blogs anywhere
>By now, we have put all source codes under version control. We can write blogs anywhere.
As hexo can regenerate blog content with source codes at any time.

- Checkout the source codes into a custom folder
```bash
   $git clone git@github.com.com:username/username.github.io.git ./yourfolder
   $cd yourfolder
   $git checkout -b hexo origin/hexo
   $git branch -d master
```
- Install required modules if there is 'local hexo not found' issue. As modules are not under version control.
```bash
   $ cd ./yourfolder
   $ cnpm install
```
- Write articles and deploy again
```bash
   $ hexo d -g
```
- Update git
```bash
   $ git add .
   $ git commit -m "your comment ..."
```

### Custom Theme
>By default, the theme is Landscape. It is rather tough. We can use the following steps to custom theme settting. We can take the 
popular theme Next for example.

1. Drop themes folder
```bash
   rm -r themes
```
2. Fork the hexo-theme-next on github

3. Add submodule
```bash
   git summodule add https://github.com/yourname/hexo-theme-next themes/next
```
4. Sync with source
```bash
   git remote add upstream https://github.com/iissnan/hexo-theme-next.git 
```
5. Mergee
```
  cd themes/next
  git fetch upstream
  git merge upstream/master

6. Update site configuration file

Edit ./_config.yml, replace Landscape with Next for the threshold theme



[My Github](https://github.com/willgood1986/willgood1986.github.io)
[Send Email](mailto:willgood1986@outlook.com)
