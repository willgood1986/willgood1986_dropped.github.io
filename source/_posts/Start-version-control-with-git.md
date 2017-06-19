---
title: Start version control with git
date: 2017-02-22 06:21:40
tags: [git, tools, user-guide]
categories: Git
---

>Git is a very useful tool for version control.

<!--more-->

### Common concepts in git

* Git works with changes
* There are three states for changes: unstaged, staged, committed
* Only staged changes can be committed

### git init

> To initialize a git repository

### git add
> To mark changes as staged state

### git checkout -- file
> To discard unstaged changes

### git commit
> To commit changes marked with staged

### git log [--pretty=oneline]
> To show repository history

### git reflog
> To show historical commands

### git reset HEAD file
> To mark staged changes as unstaged

### git diff HEAD -- file
> To see difference of the file between in working directory and in the latest respository

### ssh-keygen -t rsa -C "youremail"
> To generate a ssh key

### ssh -T git@github.com
> To test ssh key

### git remote add origin git@gitserver:username/repository.git
> Connect local repository to remote repository

### git push -u origin master
> The first time to push the master branch 

### git push origin master
> To push master branch

### git clone git@gitserver:path/repository.git [localdirectory]
> Clone remote repository to local, if localdirectory is not specified, a folder named with repository directory

### git checkout -b branch-name
> Create and switch to a new branch, the switch -b means to create a new branch

### git branch
> To display current branch

### git branch branch-name
> To create a new branch

### git checkout branch-name
> Switch to a branch

### git merge branch-name
> To merge the specified branch to current branch

### git branch -d a-branch
> To delete a specified branch

### git merge -no-ff -m "new comment" branch-name
> To merge a branch and create a comment

### add a new ssh key into git
```
1. ssh-keygen -t rsa -C "email address"
2. Hit Enter key 3 times to save data by default
3. Open /root/.ssh/id_rsa.pub, copy all contents
4. Add a ssh key on git, and paste the contents in the text box, save and close
5. Test by ssh -T git@github.com
```

### Global config
```bash
 git config --global user.name "user.name"
 git config --global user.email "user email"
``` 
