---
layout: post
title: "Git status in bash prompt"
date: 2016-10-10
categories:
  - git
description: 
image: 
image-sm: 
---

Have you ever forgotten to add a particular file to your commit? Want to know your repository global status without doing a git status? You can configure your prompts to warn you, here's how.Have you ever forgotten to add a particular file to your commit? Want to know your repository global status without doing a git status? You can configure your prompts to warn you, here's how.

Go to your `.bashrc` configuration file. Locate the custom prompt variable definition (PS1), it looks like this: 

```
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\[\033[00m\]\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
```

Add the following definitions and include the __git_ps1 variable in PS1:

```
export GIT_PS1_SHOWDIRTYSTATE=true
export GIT_PS1_SHOWSTASHSTATE=true
export GIT_PS1_SHOWUNTRACKEDFILES=true
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\[\033[00m\]\[\033[01;34m\]\w\[\033[00m\]\$$(__git_ps1) '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$$(__git_ps1) '
fi
```

You're good to go now. Remember you'll have to restart the terminal to apply the changes. 
When you are in a git project, you should see the following: 

```
~$ cd Code/qt/gmot
~/Code/qt/gmot$ (master)
                ^^^^^^^ (current branch)
  
~/Code/qt/gmot$ (master) touch foo.txt
~/Code/qt/gmot$ (master %)
                       ^^^ (untracked content)
  
~/Code/qt/gmot$ (master %) git add foo.txt
~/Code/qt/gmot$ (master +)
                       ^^^ (staged content)
  
~/Code/qt/gmot$ (master +) git commit -m "added foo stuff"
[master 785374e] added foo stuff
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 foo.txt
 
~/Code/qt/gmot$ (master) 
                 ^^^^^^ (back to normal)
```   
